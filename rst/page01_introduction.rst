:id: 1394
:title: 0x01 Introduction to LEDI
:type: page
:parent_id: 1022


0x01 Introduction to LEDI
=========================

LEDI, short for **LED I** nterface, is your own personal display device that you can
build, control, and modify. It can receive messages from bluetooth devices or
from host PC and display it to the LED matrix board.

|ledi1|

LEDI was designed to be simple, fun to build, and customizable by DIY-ers and
non-DIYers alike. We wanted the kit to not only be useful, but a good introduction
for people to take interest in the Do-It-Yourself electronics scene.
We also love open source, and for that reason, all aspects of this kit is open source.
You are welcome to modify or reuse any parts of LEDI in any way you like.

LEDI is immediately hackable, and you will find that it's possible to extend its
usage to countless electronic projects. 


Highlights
----------

There's lots of features built into LEDI:

* 32 x 8 LED matrix, a total of 256 individual LEDs (comes in green or red)
* Uses the versatile Atmega328p, the same microcontroller that powers the popular
  `Arduino <http://www.arduino.cc>`_
* Bluetooth enabled! It can pair with your Android phone and even with your PC
* Downloadable Android app to "talk" to your LEDI
* Keeps accurate time keeping
* Through-hole components for easy construction
* Customizable firmware, complete hack-ability
* You can design your own custom enclosures! Check out our `homemade cases <http://techversat.com/projects/ledi/ledi-gallery/>`_
* Completely opensource!

We are excited to see how the community will utilize this kit.

|ledi1_back|


Technical Features
------------------

For those who are interested in looking under the hood and getting more out of the kit:

* 32.678kHz crystal for accurate time keeping
* Supports chaining 2 LED displays
  - The kit comes with 1 LED display
* ISP programming header for flashing the chip
* UART breakout pins for both bluetooth module and microcontroller
* 8 additional GPIO pins from Atmega328p are accessible via breakout header
* Piezo buzzer
* 3.3v or 5v switcheable power supply
  - Regulated power can be supplied to other circuits
  - Accepts external DC power
* Bluetooth module can be controlled isolated from microcontroller

As you can see, these features allow LEDI to be integrated into variety of projects.
We hope you find these features useful for your next project!



How It All Started
------------------

This project simply started out of my wife.s rather nonchalant question::

  can you do something useful with your electronics hobby?

I made `this clock <http://hackaday.com/2010/09/22/matrix-clock-is-a-breadboarding-win/>`_
mostly to impress my wife and justify my purchases of electronic parts and devkits,
lots of devkits... After our son turned one, I wanted to teach him the alphabets.
So the clock went on to becoming a `bluetooth enabled display <http://jbremnant.wordpress.com/2011/12/09/led-display-over-bluetooth-with-android/>`_.
I would send letters to the clock from my Android phone, and attempt to 
grab a toddler's attention on reading the scrolling letters. Good luck to that, right?

|ledi2|

And then my wife thought it would be great to have this on my desk at work. 
Why? So that she can grab my attention by sending messages to it remotely. Yikes! 
At first I didn't like the idea of my wife creating uncomfortable situations at 
work, but... I caved in. And that was the birth of LEDI.  :-)

* LED clock originally created without bluetooth:

  http://jbremnant.wordpress.com/2010/11/18/my-first-complete-avr-project/

* And then upgraded with HC-06 bluetooth module, which enables sending text message
  and time update via bluetooth from Android phone or from PC.

  http://jbremnant.wordpress.com/2011/12/09/led-display-over-bluetooth-with-android/

* Now a proper product with its own PCB and enhanced firmware, called LEDI.

  http://techversat.com

LEDI was born out of our desire to learn and have fun at the same time.
As such, we hope that you find both educational and recreational value in LEDI!


.. |ledi1| image:: /nas/docs/techversat/web/product_img/ledi_general3.JPG
   :uploaded: http://techversat.com/wp-content/uploads/ledi/ledi_general3.jpg
.. |ledi2| image:: /nas/docs/techversat/web/product_img/ledi_generalColor-800x450.JPG
   :uploaded: http://techversat.com/wp-content/uploads/ledi/ledi_generalColor-800x450.jpg
.. |ledi1_back| image:: /nas/docs/techversat/web/product_img/ledi_back1.JPG
   :uploaded: http://techversat.com/wp-content/uploads/ledi/ledi_back1.jpg

.. LEESA put image of something here

