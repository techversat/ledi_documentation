:title: 0x04 LEDI Firmware Flashing
:id: 1408
:type: page
:parent_id: 1022

0x04 LEDI Firmware Flashing
===========================

Updating LEDI with the latest firmware is easy. You can use various devices
to do this. Disclaimer: We are not affiliated with any of the companies that
make any of the programmers mentioned in this tutorial. 

You will need 3 things in order to upgrade the firmware on your LEDI.

* latest firmware file with extension .hex
* 


Choosing the Programmer
-----------------------

Atmel's microcontrollers are quite popolar with the hobbyist community. There are
tons of great resources online on how to flash the chips. We've listed here some 
of the programmers we've personally tested and verified.

* avrisp clone (cheap)
  http://fun4diy.com/AVRISP_mkII.htm
* avrisp mk II (official)


Download the Flashing Software
------------------------------

A command line program called **avrdude** can flash most Atmel
microcontrollers via one of the programmer device listed above.

For Linux
~~~~~~~~~
Simply run::

  sudo apt-get install avrdude


For Mac OS X
~~~~~~~~~~~~
There is an excellent all-in-one package called CrossPack-AVR on OS X.

http://www.obdev.at/products/crosspack/index.html

