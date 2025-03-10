.. include:: /include/include-ex-cs.rst
.. meta::
   :keywords: EX-CommandStation Command Station purchasing

.. include:: /include/include.rst
.. include:: /include/include-l2.rst
|EX-CS-LOGO|

****************
Purchasing Parts
****************

|conductor| 

.. sidebar::

  .. contents:: On this page
    :depth: 2
    :local:

This page explains what you will need to acquire to build a |EX-CS| using the recommended parts for a |conductor-text|.  

Some of the parts (like track and some wire) you will likely already have on hand.

.. rst-class:: clearer

What you need to Acquire
========================

.. sidebar::  Optional configuration
    
  |conductor| |BR| |EX-CS| can be configured in an additional 'Conductor friendly', without wifi, but it requires that |JMRI| installed on a computer.

  |tinkerer| |engineer| |BR| |EX-CS| is also supported on a variety of different hardware that you might also consider

  - Supported :doc:`Arduino boards </reference/hardware/microcontroller-boards>`
  - Supported :doc:`motor shields </reference/hardware/motor-boards>`
  - Supported :doc:`ESP8266 WiFi shield </reference/hardware/wifi-boards>`
  - Supported :doc:`Ethernet shield </reference/hardware/ethernet-boards>`

Hardware
--------

You will need to find or purchase:

#. a supported **Arduino board** |BR| We recommend the `Elegoo Mega 2560 <https://www.amazon.com/ELEGOO-ATmega2560-ATMEGA16U2-Projects-Compliant/dp/B01H4ZLZLQ/>`_ |BR| |BR|
#. a supported **Motor Driver**  |BR| We recommend the `Arduino Motor Shield Rev3 <https://store.arduino.cc/collections/shields/products/arduino-motor-shield-rev3>`_ |BR| |BR|
#. a supported **WiFi shield** |BR| We recommend the `Makerfabs ESP8266 WiFi Shield <https://www.makerfabs.com/esp8266-wifi-shield.html>`_ |BR| |BR|
#. Two (2) Male to Female **Jumpers leads** |BR| |BR|
#. a 9-14v DC :doc:`power supply </reference/hardware/power-supplies>` for the motor shield |BR| We recommend `12V 5Amp Power Supply for the Track <https://www.amazon.com/LEDMO-Power-Supply-Transformers-Adapter/dp/B01461MOGQ/>`_ |BR| |BR|
#. a 2.5mm x 5.5mm Female DC Plug to **Screw Terminal (optional, but recommended)** to connect the motor shield power supply |BR| |BR|
#. a **7-9v DC power supply** |BR| for the Arduino - be sure it is **tip positive** such as `this one on amazon <https://www.amazon.com/Adapter-Arduino-Schwinn-Elliptical-Recumbent/dp/B06Y1LF8T5/ref=sr_1_2_sspa>`_ (while it is connected to the PC, this is not needed) |BR| |BR|
#. any **computer** running Windows, macOS, or Linux (only needed for the initial install of the software) |BR| |BR|
#. a **USB Cable** from the computer to the Arduino |BR| |BR|
#. a **piece of track** to run trains or program on |BR| |BR|
#. some **wire** (18 to 16 AWG twisted pair recommended [#wire]_.) |BR| |BR|
#. a 'known' working **DCC-equipped locomotive**

.. note:: 

  You can also find more detailed hardware information in the :doc:`/reference/hardware/index` section.

Software
--------

Our |EX-I| app is recommended for most users as it automatically downloads and installs the required software. 

13. See the :doc:`Command Station download page </download/ex-commandstation>` to download a copy to your computer.

A Throttle (Controller)
-----------------------


14. You'll also need something to control your trains. |BR| There are several options. We will discuss these following the system setup, but the introductory configuration covered in the following pages lends itself to using a smart phone (Android or Apple iOS).

Next Steps
==========

Click the "next" button to see how to assemble your |EX-CS|.

----

.. [#wire] **Wire Gauge** - The recommended Arduino |Motor Driver| can only provide about 1.5 Amps of power (despite being rated for 2A), so 18 AWG wire is ample. If you use a different |Motor Driver| and deliver more current to your track, you may need thicker wire (lower number gauge).
