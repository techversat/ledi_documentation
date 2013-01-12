:title: 0x03 Operating LEDI
:id: 1405
:type: page
:parent_id: 1022


0x03 Operating LEDI
===================

In this document, we will discuss various features LEDI. We will explain how to
set it up and operate it. From here on, we will assume you have
a completely assembled LEDI. We also assume you have an Android phone that
can be used to communicate with LEDI.

When it's first powered up, LEDI will go into a clock mode. The clock starts
at "00:00", since LEDI does not keep track of time when it's powered off.
Once powered on, however, it will constantly keep accurate time across various
operating modes. Also in addition to HH:MM clock digits, you will see the binary
indicator ticking every second. 


Power Switches
--------------
There are 2 slide switches on the board. With the barrel jack faced down, the 
slide switch left of it is "on/off" switch. The slide switch to the right of the
barrel jack is the "3v/5v" toggle switch. Slide the power switch up to turn the
power on and supply regulated 5 volts to the circuit.


Tactile Buttons
---------------
There are 4 buttons on the board.

* 1st button resets the device
* 2nd button puts LEDI into Conway's Game-of-Life display mode
* 3rd button allows you to set the time
  - short press for incrementing one minute at a time
  - long press for fast-forwarding time
* 4th button (located near Bluetooth module) resets the bluetooth module.


Bluetooth Pairing
-----------------
Everytime LEDI's power is reset, the bluetooth module will go into discoverable mode.
Other bluetooth devices can easily scan and pair with LEDI. 

Let's first "bond" with LEDI using an Android phone. Go to::

  Settings -> Wireless Settings -> Bluetooth Settings

Hit **scan** for devices. Your device should show up and it will be called either 

* linvor
* HC-06

Select the device and you will get a bluetooth pairing request.
Use the passcode **1234** to establish the pairing.


LEDIManager Android App
-----------------------

|icon1|

We have written an Android app specifically designed to work with LEDI. This app is the
main controller for LEDI which allows it to communicate with the "world".

LEDIManager sends various notifications from your Android phone to LEDI. It maintains
stable connection to LEDI and allows user to interact with LEDI wirelessly.

The current list of LEDIManager features:

#. Gmail, sms, call, alarm notifications supported
#. Remotely set current time
#. Send arbitrary message from your Android phone
#. Virtual interface that allows you to "draw" on LEDI wirelessly

When you start the app
~~~~~~~~~~~~~~~~~~~~~~
Your app will look like this:

|screen_off|


Other Android Apps
------------------
We are currently working on making a customized Android app for LEDI. In the meantime,
there are slew of available Android Apps that just works with LEDI. Almost all of them are
free. For example, I've tested:

* SENA_ BTerm Bluetooth Terminal 
* BlueTerm_

LEDI uses Bluetooth module that understands SPP (Serial Port Profile). What this
basically means is that it's compatible with lots of bluetooth-enabled software out there.

We have interesting set of features planned for our Android App:

* Virtual LEDI face that will give you the ability to light up individual led
* Notification forwarding (email, sms, text msg, etc..)
* Automatic clock time setting

We also welcome open source contributions! If you have ideas and would like to help writing
the Android app, please `contact us <http://techversat.com/about-us/contact-us/>`_!


Talk to It
----------

Let's try downloading BlueTerm_ from the App store on your phone. I found it to be the 
simplest one to use when I was testing LEDI.

#. Open the App
#. Hit settings button on your phone
#. Tap "Connect device"
#. Tap "Scan for devices"
#. Your LEDI will show up as one of the devices as "linvor" or "LEDI_XXX"
#. It will say "Connected to <your_device>"
#. Type something on the terminal
#. Hit "enter" on your virtual keyboard

Hopefully, you will see the message you just typed scroll across LEDI.


Power Supply
------------

The power circuit gives you options. Sometimes options are good, but sometimes they can be confusing.
Hopefully the DC power circuit in LEDI can prove to be the prior. We've taken the power schematics 
from Sparkfun_'s breadboard power supply.

This power circuit provides clean 5v or 3.3v DC. You can source power from an external battery through
the connector shown in the picture:

.. insert pic here

Or you can supply regulated power to other circuits through these pins on the PCB:

.. insert pic here


For example, I am powering the Arduino via the power output pins:

.. another power here


.. _Sena: https://play.google.com/store/apps/details?id=com.sena.bterm&feature=search_result#?t=W251bGwsMSwxLDEsImNvbS5zZW5hLmJ0ZXJtIl0.
.. _BlueTerm: https://play.google.com/store/apps/details?id=es.pymasde.blueterm&feature=search_result#?t=W251bGwsMSwxLDEsImVzLnB5bWFzZGUuYmx1ZXRlcm0iXQ..
.. _Sparkfun: https://www.sparkfun.com/products/114


.. |icon1| image:: /nas/docs/techversat/web/img/android_ledi_96x96.png
   :uploaded: http://techversat.com/wp-content/uploads/ledi/android_ledi_96x96.png
.. |screen_on| image:: /nas/docs/techversat/web/img/screenshot_onex_on.png
   :uploaded-scale50: http://techversat.com/wp-content/uploads/ledi/screenshot_onex_on-scale50.png
   :uploaded: http://techversat.com/wp-content/uploads/ledi/screenshot_onex_on.png
   :scale: 50
   :width: 300
.. |screen_off| image:: /nas/docs/techversat/web/img/screenshot_onex_off.png
   :uploaded-scale50: http://techversat.com/wp-content/uploads/ledi/screenshot_onex_off-scale50.png
   :uploaded: http://techversat.com/wp-content/uploads/ledi/screenshot_onex_off.png
   :scale: 50
   :width: 300
.. |screen_search| image:: /nas/docs/techversat/web/img/screenshot_onex_search.png
   :uploaded-scale50: http://techversat.com/wp-content/uploads/ledi/screenshot_onex_search-scale50.png
   :uploaded: http://techversat.com/wp-content/uploads/ledi/screenshot_onex_search.png
   :scale: 50
   :width: 300
.. |screen_select| image:: /nas/docs/techversat/web/img/screenshot_onex_search2.png
   :uploaded-scale50: http://techversat.com/wp-content/uploads/ledi/screenshot_onex_search2-scale50.png
   :uploaded: http://techversat.com/wp-content/uploads/ledi/screenshot_onex_search2.png
   :scale: 50
   :width: 300
.. |screen_vledi1| image:: /nas/docs/techversat/web/img/screenshot_onex_vledi1.png
   :uploaded-scale50: http://techversat.com/wp-content/uploads/ledi/screenshot_onex_vledi1-scale50.png
   :uploaded: http://techversat.com/wp-content/uploads/ledi/screenshot_onex_vledi1.png
   :scale: 50
   :width: 600
.. |screen_vledi2| image:: /nas/docs/techversat/web/img/screenshot_onex_vledi2.png
   :uploaded-scale50: http://techversat.com/wp-content/uploads/ledi/screenshot_onex_vledi2-scale50.png
   :uploaded: http://techversat.com/wp-content/uploads/ledi/screenshot_onex_vledi2.png
   :scale: 50
   :width: 600
