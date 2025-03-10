.. include:: /include/include.rst
.. include:: /include/include-l1.rst
  
*****************************************
*Under Development:* DCC-EX Track Manager
*****************************************

|tinkerer| |engineer| |githublink-ex-commandstation-button2|

|NOT-IN-PROD-VERSION|

.. sidebar::

   .. contents:: On this page
      :depth: 2
      :local:

Welcome to DCC-EX Track Manager
===============================

A first for the DCC & DC model railroading world.  A dual digital (DCC) and analogue (DC) command and control station.

With just a single |EX-CS| and a |DCC-EX| compatible throttle you can simultaneously run both your DCC Locos and analogue DC Locos (or Cabs) as throttle addresses from 1 to 10239 to control and drive them on multiple separate insulated tracks/districts.

Throttle Compatibility

  * WiFi Throttles
  * The DCC-EX  browser based EX-WebThrottle
  * Other wired throttles to operate your DCC layout and your DC layout, either separately or a simultaneous combination of the two modes

|EX-CS| with Track Manager includes the following features:

  * DCC track modes of MAIN, PROG, and OFF
  * DC track modes of DC, DCX (DC Reversed Polarity), and OFF

|EX-CS| development version v.4.2.30+ supports both DCC (PWM) and DC (PWM) Pulse Width Modulation modes as an embedded standard feature.
Track Manager allows you to set up and operate up to eight separate dual insulated sections of track/districts in either DCC (PWM) and or DC (PWM) as tracks A - H.

An Arduino Mega (with or without WiFi) and Standard L298P Motor Shield |EX-CS| has two ready to run Tracks (A & B) which can be configured as:

  * DCC (PWM) modes MAIN for mainline tracks and PROG for a programming track
  * DC (PWM) modes for DC or DCX (opposite polarity)
  * Each track/district can also be OFF

No additional external DCC decoders are required for DC (PWM) track assignments, and a single |EX-CS| is the only hardware needed for full functionality.

One key difference to note in comparing DCC vs. DC is that in DCC mode, forward/reverse is determined by the DCC decoder, not the track, whereas in DC mode the direction is dependent upon the track polarity.

Before you begin
----------------

**This is not your father's DC railway which used DC transformers for cab control.**

Turn off, unplug the AC power cord, and disconnect your current DC transformer(s) / power supply(s) from the DC layout track to place in a box for safe keeping.

You will instead be using a regulated DC (Laptop) 12-18 Vdc 3-5Amp power supply to your motor board to run all your DCC Locos and analogue DC cabs on all your individual tracks/districts/blocks.

You will be using DC (Pulse Width Modulation PWM) to drive the DC engines, Not DC Direct Current (-0 +16v).

.. image:: /_static/images/track_manager/DCCpwm_DCCpwm_AC_DC.png
  :alt: Waveform Comparison
  :scale: 50%

.. note:: 

  These modes, (PWM) vs analogue DC are totally incompatible with one another and if crossed will result in magic smoke and a burned out motor shield and or USB connector. 

 * DCC(PWM) is detected on a multimeter as an AC signal but in a square wave form, not as a sine wave
 * DC(PWM) is detected on a multimeter as a DC signal in a square wave form, not as a direct current wave

The DC(PWM) track is Power supply dependent and needs a varying amount of 0 zero to maximum Vdc passed to the track of 12 or 16 or 18vdc, depending on whether they're N, HO or G scale engines.

Note; The signal is detected as DC on this track, from 0Vdc to max +xxVdc depending on the Motor Shield DC power supply output. The DCC-EX 122.55Hz PWM DC motor signal allows for better functioning and better running than most competing systems.

Track Manager DCC vs. DC wave forms
===================================

A simplified representation of what the dual (PWM) signals might look like through the track:

.. image:: /_static/images/track_manager/dcc-and-dc-on-track.png
  :alt: DCC PWM signal
  :scale: 50%

.. note:: Note on PWM frequency

  Different microcontrollers utilise different PWM frequencies, and at present, these default frequencies are in use rather than using software to define them.

  The side effect of these differing frequencies is that you may notice humming or sometimes squealing noises from older DC motors.

  The known PWM frequencies are:

    * Mega2560 - 122.55Hz
    * ESP32      - variable
    * STM32 Nucleo - typically 1000Hz

Replacing or Integrating Into Your Current Layout
=================================================

Existing analogue DC layouts which have standard DC transformers on two or more separate DC tracks/districts/blocks and/or also have a second separate proprietary DCC command station would have in place a section of dead rail, an electric relay, or a DPDT centre-off switch between the two types of controller powered stations. These should not be using a common ground rail, and only use dual insulated tracks.

You will be replacing this kind of legacy analogue DC and proprietary DCC installation described above with a single |EX-CS| which will have a software switching implementation, allowing you to easily and quickly swap between the two DCC (PWM) and DC (PWM) modes on any of the A thru H dual insulated tracks/districts in real time.

This allows for replacing the physical hardware DPDT switch also.

This is all done through a single |EX-CS|.

.. note:: 
  
  When specifying a DC or DCX cab ID, do not use one of your existing locomotive DCC addresses or road number IDs, otherwise a command sent to control a Cab on that DC or DCX track will also operate your DCC Loco with the same address.

Hardware Requirements and Technical Notes
=========================================

.. note:: 

  These requirements are only for operating DC locomotives. There is nothing to do in a pure DCC environment where no DC or analogue locomotives are run.

In order for Track Manager to operate in DC mode, the motor shield must have a brake pin with this defined in your “config.h” motor shield definition.

Non-standard motor shields must be validated for compatibility and require a fourth brake pin to be configured to run in DC (PWM) mode. A list of current supported motor drivers can be found in :ref:`ex-commandstation/advanced-setup/supported-motorboards/index:supported motor drivers`.

Do not attempt to connect two insulated tracks together and drive a DCC engine back and forth until someone bolder than you tries it first (or you've tested it).

.. warning:: 

  Never drive a loco from an |EX-CS| controlled track or district to any other DCC or DC System.

Some suggested precautions are to add 4 fuses on wires (-b +b, -a +a) to the |EX-CS| connections. Use 2A fuses for the standard L298P motor shield or 5A fuses for the larger motor boards.

How do you run a EX-CommandStation in DC (PWM) mode?
====================================================

Using Track Manager with simple easy commands from a throttle or from a serial monitor we can change any insulated track A-H from DCC (PWM) to DC (PWM) and back in real time.

  * Valid DCC modes are MAIN, PROG, and OFF
  * Valid DC modes are DC, DCX, and OFF
  * DCX is DC with an opposite polarity like NMRA modular layout track B which is wired left rail positive (+) and right rail negative (-)
  * This allows a throttle on track B set to DCX to operate in forward and reverse correctly for west bound engines

So, you can take a standard DC motor only engines CAB number on the side of the engine and assign it to one or more of up to 8 tracks/districts/blocks labeled A thru H then enter that same number into a throttle and control that Loco Cab # on each and every one of the assigned tracks.

  * Valid Cab addresses are 1 to 10239.
  * Invalid Cab address is 0 zero.

.. warning:: 

  We do not support 0 zero stretch address function, found on Digitrax and Lenz command Stations on purpose. The constant dual DCC electrical signal may damage certain types of older DC motors if left on for a long time.

Unlike Digitrax and Lenz 0 Zero stretch DCC (PWM) signal which leaves the engine lit up and humming loudly with the throttle and engine at 0 speed, because it is receiving a Dual DCC(PWM) aka AC signal, while the |EX-CS| Track Manager is dead quiet and at rest at 0 speed.

Place any analogue DC Cab on our EX-CommandStation with a Track Manager DC assigned track and it sits there dead quiet with lights off Until the throttle speed is increased in either direction and then lights up and begins to move.

DCC Loco with DC enabled CV decoder also sits quietly and when the throttle increases the Sound will turn on first then as you throttle up more it will begin moving.  You can throttle back until it stops but leave a little throttle speed on say 5% and the Sound will continue to play while it is stopped.

Throttle speed response for DC Cabs.
Because the DCdistrict track is operating from 0Vdc to 16+Vdc ~PWM waveform signal, CAB's operating on a DCdistrict with either WiFi Throttles and |EX-R| Automation scripts with |Engine Driver| handoff run different DC motors at different speeds.

So a script for FWD(50) speed will run at completely different speeds for two different DC motors depending on their resistance and efficiency.  One crawls at 50 while the other one runs like a bat out of hell.

You can also run a DCC Locos with DC Conversion CV enabled On and run on the DCdistrict, without having to change the decoder DCC address.
They will all run on that section of track.

DCC Sound Decoder locos with DC conversion enabled may be silent until the track reaches between 2v to 6Vdc then the Sound will start up, and between 3v to 8Vdc the motor will begin to respond and move depending on the manufacturer's decoder.

Controlling & Managing DCC-EX Track Manager modes
-------------------------------------------------

You can Assign Tracks/Districts to DCC and DC mode in four ways

  1. Command Line via PC with Arduino IDE Serial Monitor or JMRI serial Traffic Monitor and it is sent through your USB connected cable.
  2. Create a |EX-R| myAutomation.h file Scripts for Track Manager assigned commands and have them automatically appear in Engine Driver as GUI Automation (Handoff) and Route (Set) buttons
  3. Enhanced |Engine Driver| WiFi Throttle Android app v2.34.163 features;

    * Track Manager set mode screen by touching a track mode entering an address
    * Command Cmd Line Serial Monitor and enter them like in example (1) above but via WiFi Native mode

  4. New |EX-TB| WiFi Android app features;
  
    * Track/District Manager set mode screen by touching a track mode, entering an address
    * Command Cmd Line Serial Monitor and enter them like in example (1) above but via WiFi Native mode

New Engine Driver DCC-EX Native mode features now available today via Google Play Store:

  * `Engine Driver <https://play.google.com/store/apps/details?id=jmri.enginedriver>`_
  * `EX-Toolbox <https://play.google.com/store/apps/details?id=dcc_ex.ex_toolbox>`_

Track Manager Commands
======================

Sending commands from the Arduino IDE Serial Monitor or JMRI Send Command Line.

To display the current Track Manager configuration, use the command ``<= ...>`` an equal sign looks like a track.

To change or configure the current track modes use the new command ``<= trackletter mode [address]>`` which has been added for Track Manager, where:

  * ``trackletter`` is A through H
  * ``mode`` is one of MAIN, PROG, DC, DCX, or OFF (DCX is DC with opposite polarity)
  * ``address`` is the cab ID is only required when specifying DC or DCX
  * Note that the "address" parameter is only required for DC or DCX modes

.. code-block::

  <= A MAIN>     // Set track A to MAIN DCC mode
  <= B PROG>     // Set track B to PROG DCC mode
  <= A DC 1234>  // Set track A to DC mode with address 1234
  <= B DCX 4321> // Set track B to DC mode Opposite Polarity address 4321
                // or any number you assign from 1 to 10239
  <= B OFF>      // Set track B OFF, like a staging yard when it gets too noisy.

.. note:: 

  You would then enter your Engine address on the throttle of 1234 and 4321 and drive them on the layout.

Create EX-RAIL Scripts to Change Track modes
--------------------------------------------
Using |EX-R| functions inside myAutomation.h file to run Automation scripts to change track modes from DCC to DC and back.
my.Automation.h file

.. code-block:: 

  //SET_TRACK(id,mode)
    SET_TRACK(A, MAIN)
    SET_TRACK(B, DCX)
    SET_TRACK(C, DC)

Create EX-RAIL list of Track Manager Functions for Engine Driver Automatically Assign (Handoff) buttons
-------------------------------------------------------------------------------------------------------

In a |EX-R| Automation script we could assign a track mode to DC and wait for a Engine Driver throttle to Assign the Current Selected Active Engine Address and drive Manually through the district on the layout.

.. code-block:: 

 AUTOMATION(500, "Districts A MAIN _ B PROG Default")// Reset Default back to DCC Main & PROG
  SET_TRACK(A,MAIN) PRINT("Default Districts Tracks MAIN A & PROG B")
  SET_TRACK(B,PROG)
  DONE
 AUTOMATION(501, "District A MAIN")   // Alternate DCC Main track A
  SET_TRACK(A,MAIN) PRINT("District A MAIN")
  DONE
 AUTOMATION(502, "District A PROG")   // Alternate DCC PROG track A
  SET_TRACK(A,PROG) PRINT("District A PROG")
  DONE
 AUTOMATION(503, "District A DC")     // Alternate DC track A
  SET_TRACK(A,DC) PRINT("District A DC")
  DONE
 AUTOMATION(504, "District A DCX")    // Alternate DCX track A Changed to Opposite Polarity 
  SET_TRACK(A,DCX) PRINT("District A DCX Opposite Polarity") // Track A Opposite Polarity DC    
  DONE
 AUTOMATION(505, "District A OFF")    // A Track OFF
  SET_TRACK(A, OFF) PRINT ("District A OFF")
  DONE
 Copy and repeat AUTOMATION(506-510, District B  mode)

Create EX-RAIL Track Manager Functions for Engine Driver Throttle Automation (Handoff) buttons
----------------------------------------------------------------------------------------------

In a |EX-R| Automation script we could a Set a Loco Address to a specific track in DC mode and have it run on Automation through the layout.

.. code-block::

 AUTOMATION(1225,"Roundhouse to Turntable Back & Forth")
   SETLOCO(1225)
   SET_TRACK(B,DC)
   Run a your Roundhouse script blow whistle, run Forward delay wait and run Reverse        
   DELAYRANDOM(msec, msec) // randomize the run time between runs    
   DONE

Create EX-RAIL Track Manager Functions for Engine Driver Throttle Route (Set) buttons
-------------------------------------------------------------------------------------

In a |EX-R| Automation script we could Set a Loco Address to a specific track in DC mode and Manually run a preassigned address on the layout.

.. code-block:: 

 ROUTE(1225,"Set track B to DC 1225")
   SETLOCO(1225)    // Assign Loco 1225
   SET_TRACK(B,DC)  // Set Track B to DC with address 1225
   CLOSE(1)         // Close Turnout 1
   THROW(2)         // Throw Turnout 2
   DONE

Then manually drive the Cab# around the layout

All done through DCC-EX Track Manager with a simple push of a GUI button of Either or Both  Engine Driver (Handoff) to Acquire the last Throttle Engine# used and run it on the mode of the track  [i.e. DC engine 1225], Or Engine Driver (Set) button to set a block to a specific mode.

TrackMagic uses the Cab number of a DC Engine in a throttle to run it on a assigned track/district/block, mimicking the look of DCC Engines.
No DPDT Switches are required, all waveform mode switching is done by Track Manager Software instructions.


DCC-EX Command Station with EX-RAIL & Track Manager
---------------------------------------------------

Cool thing is the new |EX-R| the Automation(n) & Routes(n) work the same with DCC engines on MAIN tracks and the DC engines on DC or DCX tracks, and with the Sensors, Servos /Turnouts, Signals & MP3 Sound DFPlayer triggers with little or no script changes other than maybe the FWD(n) & REV (n) Speeds.

With the new DCC-EX direct WiFi Discovered Server you can connect Engine Driver & other WiThrottle app based throttles directly and have |EX-R| (Handoff) & (Set) buttons to run |EX-R| scripts from the throttles.

These are DCC-EX Major feature/benefit because with other systems you’ll have to use a PC computer or Pi processor & JMRI for a WiThrottle Server throttle access and you have to write two different JMRI Jython.py Scripts for DCC and for DC automation & routes.

Modular Layouts
---------------

DCC-EX Track Manager 4.2.30+ is perfect for NMRA DCC Standards Modular Layouts which have two MAIN tracks/districts,
Track A and Track B with sidings;

* Track A (east bound) wired rails L-  R+
* Track B (westbound) which also have all the siding and spurs, wired rails L+  R-

You can set each district separately as mode

* DCC for MAIN, PROG or OFF
* analogue for DC, DCX or OFF

DCX is Opposite Polarity and is what you set Block B to when you want it in DC mode because it is wired to NMRA Modular DCC Standards L+, R-.

Using the New Track Manager Function commands you can run the whole layout as
------------------------------------------------------------------------------

.. code-block::

 Track A & Track B
   MAIN & PROG
   MAIN & MAIN
   PROG & MAIN
   MAIN & DC
   PROG & DC
     DC & MAIN
     DC & PROG
     DC & DC
     DC & DCX
   MAIN & DCX
   PROG & DCX  (Use JOIN on A Programming track to make a MagicTrack) 
 or any combination with up to 8 separate dual insulated tracts/disteicts from A - H.

All done through the free |DCC-EX| Track Manager commands.

How Do I Get On Board with DCC-EX Track Manager ?
==================================================

To use TrackManger, you will need the current development version of |EX-CS| which you can obtain by following the directions in our :ref:`download/ex-commandstation:latest ex-commandstation unreleased development version` section.

We highly encourage you to join our Discord server to keep up to date on developments. Refer to :ref:`support/contact-us:contact us` for details on how to join.

Example of User defined |EX-R| Scripts running on Engine Driver Throttle App (Android):

.. figure:: /_static/images/track_manager/trackmanager_engine_driver_1.png
  :alt: Track Manager ED 1
  :scale: 50%

  |Engine Driver| controlling Two Locos:
  
  - DCC PE 1225 on track A address 1225 with a Sound Decoder
  - DC NH  667 on Track B address 667 with IPLS Virtual Sound Decoder

.. figure:: /_static/images/track_manager/trackmanager_engine_driver_2.png
  :alt: Track Manager
  :scale: 50%
 
  DCC-EX Commands, scroll-able

.. figure:: /_static/images/track_manager/trackmanager_engine_driver_3.png
  :alt: Track Manager handoff
  :scale: 50%
 
  DCC-EX Track Manager "Handoff" & "Set" buttons

  - Scroll through & select track modes
  - Takes the current selected Active Throttle Engine and assigns that Address to the DC or DCX track

.. figure:: /_static/images/track_manager/trackmanager_engine_driver_4.png
  :alt: Track Manager DCC-EX native mode
  :scale: 50%

  Engine Driver DCC-EX Native mode
  
  - Track Manager MAIN & PROG
  - With DCC-EX Cmd Line & Serial monitor

.. figure:: /_static/images/track_manager/trackmanager_engine_driver_5.png
  :alt: Track Manager A/B
  :scale: 50%

  Engine Driver DCC-EX Native mode

  - Track Manager Track A  DCC 1225
  - Track B   DC  667

.. figure:: /_static/images/track_manager/trackmanager_engine_driver_6.png
  :alt: Track Manager handoff
  :scale: 50%

  Engine Driver |EX-R| automation (Handoff) and special effects buttons
  
.. figure:: /_static/images/track_manager/trackmanager_engine_driver_7.png
  :alt: Track Manager handoff/set
  :scale: 50%
  
  Special Effects (Set) continued and route (Set) buttons

.. warning:: 

  This feature is under active development, meaning commands, features, and behaviour may change without notice. While we endeavour to keep these features functional, our development releases are updated regularly and we cannot guarantee there are no bugs that will have unexpected results.

  If using our development release and, especially, the Track Manager feature, we highly recommend keeping in touch with conversations and developments via our `Discord server <https://discord.gg/PuPnNMp8Qf>`_.

  You can also use our new GitHub issue templates to report a bug: |githublink-ex-commandstation-button2|

