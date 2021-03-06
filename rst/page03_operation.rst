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

Most features of LEDI can be controlled via Android App, LEDI Manager.
It gives you the ability to interact with it without much fuss, and gives you
intuitive control over electronics circuit you've assembled.

First download the App from Google Play:

  LEDIManager_

.. _LEDIManager: https://play.google.com/store/apps/details?id=com.techversat.ledimanager&feature=search_result#?t=W251bGwsMSwxLDEsImNvbS50ZWNodmVyc2F0LmxlZGltYW5hZ2VyIl0.

|ledimanager_screenshot|


Power up LEDI
-------------
Simply turn the power switch to the "on" position. Also, make sure the power supply
voltage switch is set to "5v".

When it's first powered up, LEDI will go into a clock mode. The clock starts
at "00:00", since LEDI does not keep track of time when it's powered off.
Once powered on, however, it will constantly keep accurate time across various
operating modes. Also in addition to HH:MM clock digits, you will see the binary
indicator ticking every second. 


Bluetooth Pairing
-----------------
First, make sure Bluetooth radio is turned on in `Settings`.

Everytime LEDI's power is reset, the bluetooth module will go into discoverable mode.
Other bluetooth devices can easily scan and pair with LEDI. You will first need to
pair LEDI with your Android device.

Let's first "bond" with LEDI using an Android phone. Go to::

  Settings -> Wireless Settings -> Bluetooth Settings

Hit **scan** for devices. Your device should show up and it will be called either 

* linvor
* HC-05

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

First search for your LEDI and bond with it, by pressing the "Search" button on the App.
If you haven't already paired against it, it will prompt you for the passcode for pairing.
(Remember **1234** to pair)

|screen_search|

Once the search is done, select your LEDI. After your device is selected, it will bring 
you back to the main screen.

|screen_select|


Establish connection
~~~~~~~~~~~~~~~~~~~~
Press the large button on top that says "service off". It's a toggle button that will 
turn green when the connection is properly established. If successful, your screen will
look like this, and LEDI will greet you with a chime.

|screen_on|


Send Commands
~~~~~~~~~~~~~
You can send simple messages to LEDI from a text box on the bottom of the screen, and
then hitting "Send". This will scroll your text across LEDI.


Test Virtual LEDI
~~~~~~~~~~~~~~~~~
You'll notice that there's a button called vLEDI. This interface allows you to "draw" on
LEDI from your Android. You can trace your finger across the virtual LEDI screen and see
the same dots lit up on your LEDI!

|screen_vledi1|

|screen_vledi2|


Other Android Apps
------------------
There are slew of available Android Apps that just works with LEDI.
Almost all of them are free. For example, I've tested:

* Sena_ BTerm Bluetooth Terminal 
* BlueTerm_

LEDI uses Bluetooth module that understands SPP (Serial Port Profile). What this
basically means is that it's compatible with lots of bluetooth-enabled software out there.


Talk to it
~~~~~~~~~~
Try downloading BlueTerm_ from the App store on your phone. I found it to be the 
simplest one to use when I was testing LEDI.

#. Open the App
#. Hit settings button on your phone
#. Tap "Connect device"
#. Tap "Scan for devices"
#. Your LEDI will show up as one of the devices as "linvor" or "LEDI_XXX"
#. It will say "Connected to <your_device>"
#. Type something on the terminal
#. Hit "enter" on your virtual keyboard

If everything went right, you will see the message you just typed scroll across LEDI.


Power Switches
--------------
There are 2 slide switches on the board. With the barrel jack faced down, the
slide switch left of it is "on/off" switch. The slide switch to the right of the
barrel jack is the "3v/5v" toggle switch. Slide the power switch up to turn the
power on and supply regulated 5 volts to the circuit.


Tactile Buttons
---------------
There are 4 buttons on the board.

====================  =========================================================
Button Name           Description
====================  =========================================================
Reset                 Located at the top, resets the microcontroller
Programmable Btn1     Currently puts LEDI into Conway's game-of-life display
Programmable Btn2     Allows you to manually adjust time (short, long presses)
Bluetooth Reset       Located near bluetooth module, resets the module
====================  =========================================================

The behavior of both programmable buttons can be changed in the firmware.


Power Supply
------------

The power circuit supplies either 5v or 3.3v of clean DC. There are access headers
to either

1. source power from other external voltage source (upto 9VDC)
2. supply power to other circuits (5 or 3.3v)

We've taken the power schematics from Sparkfun_'s breadboard power supply.

You can source power from an external battery through the connector shown in the picture:

.. insert pic here

Or you can supply regulated power to other circuits through these pins on the PCB:

.. insert pic here


For example, I am powering the Arduino via the power output pins:

.. another power here


.. _Sena: https://play.google.com/store/apps/details?id=com.sena.bterm&feature=search_result#?t=W251bGwsMSwxLDEsImNvbS5zZW5hLmJ0ZXJtIl0.
.. _BlueTerm: https://play.google.com/store/apps/details?id=es.pymasde.blueterm&feature=search_result#?t=W251bGwsMSwxLDEsImVzLnB5bWFzZGUuYmx1ZXRlcm0iXQ..
.. _Sparkfun: https://www.sparkfun.com/products/114


.. |icon1| image:: /nas/docs/techversat/web/icons/96x96_00.png
   :uploaded: http://techversat.com/wp-content/uploads/96x96_00.png

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
.. |ledimanager_screenshot| image:: /nas/docs/techversat/web/img/ledimanager_googleplay2.png
   :uploaded: http://techversat.com/wp-content/uploads/ledimanager_googleplay2.png

