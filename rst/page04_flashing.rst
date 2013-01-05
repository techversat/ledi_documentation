:title: 0x04 LEDI Firmware Flashing
:id: 1408
:type: page
:parent_id: 1022

0x04 LEDI Firmware Flashing
===========================

If you wish you update LEDI with the latest firmware, you've come to the 
right place. To take advantage of the latest LEDI development, it is advisable
that you acquire the tools and the know-how to flash LEDI's firmware.

You will need 3 things in order to upgrade the firmware on your LEDI.

===============================  ==========================================
What You Need                    What It Is
===============================  ==========================================
1  latest firmware               file with extension .hex
2  ISP_ (In-System Programmer)   "burns" the .hex file onto the chip
3  avrdude_                      sends the firmware file to ISP for upload
===============================  ==========================================

.. _ISP: http://en.wikipedia.org/wiki/In-system_programming
.. _avrdude: http://www.nongnu.org/avrdude/

**Disclaimer**: We are not affiliated with any of the companies that
make any of the programmers mentioned in this tutorial. 


Obtaining the Firmware
----------------------
All the latest code is in git repository:

  https://github.com/techversat/ledi_firmware

The latest firmware will be placed under

  https://github.com/techversat/ledi_firmware/tree/master/bin

You can also easily pull the entire project from git::

  git clone https://github.com/techversat/ledi_firmware.git	
  # or
  git clone git@github.com:techversat/ledi_firmware.git

If you are new to git, we suggest reading this page first:

  https://help.github.com/articles/set-up-git


Choosing the Programmer
-----------------------
Atmel's microcontrollers are quite popular with the hobbyist community. As such,
there are variety of hardware choices available. We've listed some of the programmers
we've personally tested.

=================  ===================  =======================================
Programmer         Synopsis             Comments
=================  ===================  =======================================
avrisp mkII_       you like brands      Official programmer by Atmel. Can't go
                                        wrong, but pricey in comparison
avrisp clone_      personal fav         Cheap, yet reliable. Powers the target
littlewire_        multi-purpose        Relatively cheap, can be used for other
                                        purposes besides programming.
USBTiny_           easy to follow       Great resources online from adafruit.com
=================  ===================  =======================================

.. _mkII: http://www.digikey.com/product-detail/en/ATAVRISP2/ATAVRISP2-ND/898891
.. _clone: http://fun4diy.com/AVRISP_mkII.htm
.. _littlewire: http://littlewire.cc/
.. _USBTiny: http://www.adafruit.com/products/46

.. |clone_img| image:: http://fun4diy.com/photos/AVRISP-mkII.jpg
   :uploaded: http://techversat.com/wp-content/uploads//AVRISP-mkII.jpg

No matter which programmer device you choose, you will use a single software
to communicate against it: avrdude_


Setting up the FlashingSoftwre
------------------------------
avrdude_ is a command line utility which works for Windows, Mac OS X, and Linux.
It can flash most Atmel produced microcontrollers, and also can modify configuration
"fuses" on these chips.

For Linux
~~~~~~~~~
Simply run::

  sudo apt-get install avrdude
  which avrdude

You then need to give proper system permissions for ISP device.
Create a file called `/etc/udev/rules.d/99-avrisp.rules` with this content::

  # AVRISP mkII
  SUBSYSTEM=="usb",ATTRS{idVendor}=="03eb",ATTRS{idProduct}=="2104",GROUP="plugdev",MODE="0666"
  SUBSYSTEM=="usb",ATTRS{idVendor}=="03eb",ATTRS{idProduct}=="2104",GROUP="users",MODE="0666"
  SUBSYSTEM=="usb", SYSFS{idVendor}=="1781", SYSFS{idProduct}=="0c9f", GROUP="plugdev", MODE="0666"

The run::
 
  sudo service udev restart 

For more detailed instructions, please refer to:

http://www.ladyada.net/make/usbtinyisp/avrdude.html
http://www.ladyada.net/learn/avr/setup-unix.html

For Mac OS X
~~~~~~~~~~~~
There is an excellent all-in-one package called CrossPack-AVR on OS X.

http://www.obdev.at/products/crosspack/index.html

This package is one-stop-shop. It gives the development environment
as well as the avrdude_. Very neat.

For Windows
~~~~~~~~~~~
There's an excellent tutorial by adafruit:

* installation: http://www.ladyada.net/learn/avr/setup-win.html
* usage: http://www.ladyada.net/make/usbtinyisp/avrdude.html 
* download from: http://sourceforge.net/projects/winavr/files/?source=navbar


Connect Programmer to LEDI
--------------------------
On the bottom right side of LEDI (next to the microcontroller), you will see
2x3 header. That's where the ISP connector goes. The top right pin is
annotated with a small triangle. That's where the red strip on the ribbon
cable will align::

  /-----------\
  | o   o   o | <- first pin    
  | o   o   o |
  \-----------/


Flash with New Firmware
-----------------------

If you have downloaded the ledi_firmware repository, you can also simply do::

  cd ledi_firmware/src
  make upload
  make tinyisp

If you only downloaded the firmware file, run the following commands for
the programmer you own. It assumes your firmware file is named `main.hex` and
exists in current working directory.

**avrisp mkII or avrisp clone**::

  avrdude -V -F -P usb -c avrispmkII -p m328p -U flash:w:main.hex

**litlewire or usbtiny**::

  avrdude -V -F -c usbtiny -p m328p -U flash:w:main.hex


