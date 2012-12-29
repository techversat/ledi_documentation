:title: 0x05 LEDI Development
:id: 1411
:type: page
:parent_id: 1022

0x05 LEDI Development
=====================

There are various ways you can modify and tune LEDI. The development involving
our device spans, largely, 3 distinct programming areas:

* microcontroller firmware
* host PC interface software
* Android interface software

You can tackle any of these areas to hack LEDI. Within the confines of LEDI
hardware, your imagination is the only limit on how you choose to extend
LEDI's functionality.


Obtaining the Source Code
-------------------------

At the core, LEDI uses the same microcontroller that powers the Arduino Duemilanove.
This microcontroller, Atmega328p, is a wildly popular device. It's often used
in many hobbist projects because of its 1) opensource toolchain 2) powerful
features, and 3) expansive AVR community their myriad of projects.

The firmware is written in C. It does not rely on any of the Arduino libraries,
and conscious effort has been made to keep the firmware as lean as possible.
First, download the source from github::

  cd $HOME
  mkdir git
  git clone git@github.com:jbremnant/project_ledi.git


Under ``project_ledi`` directory, you will see these directories:

* `doc`  contains documentation materials, including this tutorial
* `fw`   contains firmware source code
* `hw`   contains design files for the PCB  
* `sw`   contains PC interface source, Android interface source


This directory contains the source code for the firmware of LEDI project.
Compiled using avr-gcc 4.7.0 under Ubuntu linux.

Here's the list of sources and brief description of each:

* main.c
  Main entry point, implements interaction logic with LEDI.

* font.h
  Contains 5x7 sized font. Supports meta characters.

* calibration.c/calibration.h
  Internal RC clock calibration routines. It uses the 32.678kHz watch crystal.

* ht1632.c/ht1632.h
  Library to communicate with led matrix.

* uart.c/uart.h
  Interrupt based UART library, based on Peter Fluery's uartlib.

* uartsync.c/uartsync.h
  Synchronous UART lib that uses hardware UART. (unused by default)

* term.c/term.h
  Library to retrieve strings from UART.

* utils.c/utils.h
  Small collection of utility functions.


Internal Guts
=============


Calibration of Internal RC Clock
--------------------------------

By default, Atmega328p comes preconfigured with internal clock running at 2MHz.
The factory calibration for the clock is done to within ~20% accuracy, which is
rather imprecise for doing time critical operations such as UART. The datasheet
claims you can calibrate your clock to within 1% accuracy. When you
want to run the microcontroller at higher frequency, you will want to calibrate
the clock.


UART Considerations
-------------------
Very good post about uart overflow and the timing of reading bytes
from a serial connection. It's especially important when the our
LEDI board receives a lot of data when connected to the PC:

  http://binglongx.wordpress.com/2011/10/26/arduino-serial-port-communication/

You can either 1) throttle the data transmission from the PC software so that
it doesn't overload atmega328p with inundated msgs, or 2) atmega only accepts
messages in certain length, and estimate the time it will take until the next
read from the ring buffer.

  number of clock cycles to overflow = 3     x 10     x      F    /  B
                                      [FIFO]  [10bit data]  [clk]    [baud]

"To prevent HardwareSerial buffer overflow, the user code, often in loop(),
should check Serial.available() and call Serial.read() without too long intervals.
Assuming 128-byte buffer and 9600 baud, in 133 milliseconds the buffer may overflow.
With 115200 baud, the buffer may overflow in 11.1 milliseconds if you do
not fetch the characters."

With 9600 baud rate, it may take 1.04 msec per character.
With 38400, it will take 0.26msec. Assuming the buffer is 128 bytes, the processor
should not wait more than 33.28 msec to start reading from the ring buffer.

