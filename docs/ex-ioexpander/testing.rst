.. meta::
  :keywords: EX-CommandStation Command Station EX-IOExpander

.. include:: /include/include.rst
.. include:: /include/include-l1.rst
|EX-IO-LOGO|

*********************
Testing EX-IOExpander
*********************

|tinkerer| |githublink-ex-ioexpander-button2|

.. sidebar:: 
  
  .. contents:: On this page
    :depth: 2
    :local:

Additional diagnostic and testing commands have been added to allow testing your |EX-IO| device independently of your |EX-CS|.

These commands will validate the various I/O pins operate as expected as digital inputs (with/without pullups), digital outputs, and analogue inputs.

Diagnostic commands
===================

``<D>`` - Issue this command to toggle the diagnostic display on and off. When enabled, a display of the configuration and state of every digital and analogue pin will be displayed in the serial console, which will be updated every 5 seconds by default. The display delay is configurable.

``<D delay>`` - Issue this command to adjust the diagnostic display delay, where "delay" is a number in seconds eg. ``<D 1>`` will display the diagnostic data every second. This will override the "DIAG_CONFIG_DELAY" specified in "myConfig.h". If diagnostics are not enabled, this command will also enable them.

Testing commands
================

``<A>`` - Issue this command to toggle analogue input testing on and off. When enabled, all defined analogue input pins are enabled as analogue inputs, with their values displayed via the diagnostic output in the serial console. Enabling this will also enable diagnostic output.

``<I>`` - Issue this command to toggle digital input testing (with pullups disabled) on and off. When enabled, all defined digital input pins are enabled as digital inputs (including analogue pins capable of digital input), with their values displayed via the diagnostic output in the serial console. Enabling this will also enable diagnostic output.

``<O>`` - Issue this command to toggle digital output testing on and off. When enabled, all defined digital output pins are enabled as outputs (including analogue pins capable of digital output). All output pins will cycle between high and low output at half second intervals, allowing a device such as an LED to be connected to validate the output is correct (don't forget a current limiting resistor). Enabling this will also enable diagnostic output.

``<P>`` - Issue this command to toggle digital input testing with pullups enabled on and off. When enabled, all defined digital input pins are enabled as digital inputs with pullups (including analogue pins capable of digital input), with their values displayed via the diagnostic output in the serial console. Enabling this will also enable diagnostic output.

``<T>`` - Issue this command to to display which test mode is in progress.