:title: 0x07 LEDI Android App Dev
:id: 1418
:type: page
:parent_id: 1022

0x07 LEDI Android App Dev
=========================

Most Android phones are capable of Bluetooth 2.0 SPP (Serial Port Profile). Your LEDI can
talk SPP, which gives various interface options. You can connect to it from your PC, an
Android phone, or even from another microcontroller! Here, we describe the inner guts of 
our Android app. It's heavily borrowed from an already existing app that does something
similar: `MetaWatch Manager <https://github.com/MetaWatchOpenProjects/MWM-for-Android>`_


A Bit About Android
-------------------
Back to Android. It takes a bit of education to understand Android. Android development
is different from traditional software development, where you implement all the functionality
from scratch. A simple program typically involves defining overall structure and writing specific
functions, then calling them to carry out specific set of tasks.

In contrast, Android app is more about implementing customized pieces of a larger body of complex
system. You don't need to know much about how the machine works - but you need to know 
when the machine will invoke your functions. Android is a framework, and the Android App is
a piece of software that just "melts" into this framework. You often don't invoke critical pieces
of code directly. You anticipate what your App needs to do in various situations and implement 
your specific logic for predefined interfaces. Thus, the paradigm of Android program can be
summed up in this sentence: "Don't call us, we will call you".

While there is an abundance of resources for Android
(`google android dev <http://developer.android.com/training/index.html>`_),
I found `this book <http://www.amazon.com/Programming-Android-Zigurd-Mednieks/dp/1449389694>`_
very useful when I was learning Android programming. 


Overall Structure
-----------------
There's **Activity** and **Service** within the LEDI Manager App. The **Service** component
is the core of the App. It starts a background thread that:

#. subscribes from other services (like gmail, sms) and monitors their **Intent** broadcasts 
#. handles messages to be sent to LEDI asynchronously

The service component allows other apps to interact with the LEDI Manager. You can write 
a completely different App which can use LEDI Manager to trigger alerts and messages.

Once the service is started, it does the following:

#. Starts up monitors : registers content observers for email, sms, calls, etc..
#. checks the connection status with LEDI and establishes bluetooth connection


Implementation
--------------
The source code is organized as follows:

====================  ===============  =================================================================
Name                  Derived From     Description
====================  ===============  =================================================================
LEDI.java             Activity         Main activity - entry point
LEDIService.java      Service          Implementation of service that runs in the background.
                                       Contains handle to bluetooth input, output streams.
Protocol.java         Standalone       Composes msgs and queues it up to send it over bluetooth
Notification.java     Standalone       Calls functions within Protocol to send specific notifications
====================  ===============  =================================================================

