:title: 0x05 LEDI Development
:id: 1411
:type: page
:parent_id: 1022

0x05 LEDI Development
=====================

There are various ways you can modify and tune LEDI. Largely, there are 3 distinct
development areas with LEDI:

#. Microcontroller firmware development
#. Android app development
#. Host PC interface development

You can tackle any of these areas to hack LEDI. Within the confines of LEDI
hardware, your imagination is the only limit on how you choose to extend
LEDI's functionality.

In this document, we will discuss the firmware. We will also briefly mention
other projects associated with LEDI.


Obtaining the Source Code
-------------------------

At the core, LEDI uses the same microcontroller that powers the Arduino Duemilanove.
This microcontroller, **Atmega328p**, is a wildly popular device. It's often used
in many hobbist projects because of its 1) opensource toolchain 2) powerful
features, and 3) expansive AVR community their myriad of projects.

LEDI communicates with the bluetooth module via UART_.
The same UART lines can be used to interface LEDI from a PC, using USB to serial
bridge.

.. _UART: http://en.wikipedia.org/wiki/Universal_asynchronous_receiver/transmitter

The firmware is written in C. Android app is all in Java. Hardware schematics are
created in Cadsoft Eagle. All the source code, documentation, and schematics are
available online. The source code and documentation files are provided as-is,
completely open source and no strings attached.

====================  ==============================================================
Name                  Git Project Page
====================  ==============================================================
Firmware source       https://github.com/techversat/ledi_firmware 
Android App source    https://github.com/techversat/ledi_android
Hardware Schematics   https://github.com/techversat/ledi_hardware
Documentation (RST)   https://github.com/techversat/ledi_documentation
====================  ==============================================================

Source code for each these projects can be simply downloaded via git::

  git clone git@github.com:techversat/ledi_firmware.git
  git clone git@github.com:techversat/ledi_android.git
  git clone git@github.com:techversat/ledi_hardware.git
  git clone git@github.com:techversat/ledi_documentation.git


Firmware Source Files
---------------------
The firmware source code does not rely on any of the Arduino libraries. 
Conscious effort has been made to keep the firmware as lean as possible,
and we've tried to avoid inclusion of bulky libraries.

Here's the list of files and brief description of each:

===============  =====================================================================
Filename         Synopsis
===============  =====================================================================
main.c           main entry point, implements interaction logic with LEDI
font.h           contains 5.7 sized font in hex, support all ascii characters
calibration.h    header file for calibrating the 32.678kHz watch crystal
calibration.c    implementation of calibrating the crystal
ht1632.h         defines configuration constants for LED driver chip ht1632
ht1632.c         implements various functions to drive the LED matrix
uart.h           header for asynchronous, hardware register-driven UART
uart.c           implements the UART lib
term.h           simple header file for term.c
term.c           convenience wrapper around uart.c 
utils.h          simple header file for utils.c
utils.c          small collection of utility functions
===============  =====================================================================

The main logic is contained within `main.c`. It is this file that keeps track of
time, reads data received from UART (bluetooth), and switches LEDI into different
operating modes.


Internal Guts
=============

We highlight important aspects of the firmware to make development easier.

Calibration of Internal RC Clock
--------------------------------
By default, Atmega328p comes preconfigured with internal clock (RC oscillator)
running at 2MHz. Without calibration, the internal clock is rather imprecise - it can
be wrong 20% of the time. This poses issues for time critical operations such as UART.
The UART protocol relies on preset baud rate, and the clock on both the sender and receiver
need to be accurate. With ~20% accuracy, using the microcontroller as-is with 
factory calibration poses a problem.

Furthermore, the Atmega328p microcontroller on LEDI runs at 8MHz. The necessity
of clock calibration becomes even more apparent. The datasheet claims you can
calibrate the clock to within 1% accuracy. Fortunately, the internal RC oscillator
can be calibrated during runtime using various techniques. LEDI board is equipped
with an accurate external watch crystal. We use this crystal to calibrate the 
internal RC oscillator of Atmega328p.

This internal clock calibration is done automatically when LEDI starts up.
It only takes fraction of a second. The implementation is borrowed from Atmel's
reference doc: http://www.atmel.com/Images/doc8002.pdf


Timers
------
To keep track of time, asynchronous timer is used on TIMER2 peripheral. 


HT1632 Shawdow Ram
------------------
It's a simple output buffer. For efficient communication between the microcontroller
and the LED matrix, a bulk command is preferred as supposed to an individual one.



UART Considerations
-------------------
There's a very good post about UART overflow and the timing of reading bytes
from a serial connection. It's especially important when the our
LEDI board receives a lot of data when connected to the PC:

  http://binglongx.wordpress.com/2011/10/26/arduino-serial-port-communication/

You can either 1) throttle the data transmission from the PC software so that
it doesn't overload atmega328p with inundated msgs, or 2) atmega only accepts
messages in certain length, and estimate the time it will take until the next
read from the ring buffer::

  number of clock cycles to overflow = 3     x 10     x      F    /  B
                                      [FIFO]  [10bit data]  [clk]    [baud]

Here's an useful blurp from the blog post:

  "To prevent HardwareSerial buffer overflow, the user code, often in loop(),
  should check Serial.available() and call Serial.read() without too long intervals.
  Assuming 128-byte buffer and 9600 baud, in 133 milliseconds the buffer may overflow.
  With 115200 baud, the buffer may overflow in 11.1 milliseconds if you do
  not fetch the characters."

With 9600 baud rate, it may take 1.04 msec per character.
With 38400, it will take 0.26msec. Assuming the buffer is 128 bytes, the processor
should not wait more than 33.28 msec to start reading from the ring buffer.

The HC-05, HC-06 both come with factory preset baud rate of 9600.
The LEDI firmware operates on 9600 baud rate. However, it is possible to change
to higher baud rates.


