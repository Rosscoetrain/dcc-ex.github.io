.. include:: /include/include.rst
.. include:: /include/include-l2.rst
|EX-AN-LOGO|

******************************************
EX-CommandStation 4.1.2 Release [Oct 2022]
******************************************

29 October 2022

The DCC-EX Team is pleased to release CommandStation-EX v4.1.2 as a Production Release for the general public.
This release is a Minor release with many significant EX-RAIL enhancements and new automation features in addition to some bug fixes.
The team continues improving the architecture of DCC++EX to make it more flexible and optimizing the code to get more performance from the Arduino (and other) microprocessors. This release includes all of the Point Releases from v4.0.1 to v4.1.2.

**New Command Station & EX-RAIL Features**

* ACK defaults are now set to LIMIT 50mA, MIN 2000uS, MAX 20000uS for more compatibility with non NMRA compliant decoders
* Automatically detect and run a myFilter add-on (no need to call setFilter)
* New Commands for the Arduino IDE Serial Monitor and JMRI DCC++ Traffic Monitor

    * </RED signal_id> to turn a individual LED Signal On & Off
    * </AMBER signal_id> "
    * </GREEN signal_id> "
    * </KILL ALL> command to stop all tasks, and Diagnostic messages when KILL is used
    * < t cab> command to obtain current throttle setting

* Allow WRITE CV on PROG
* Updated CV read command . Equivalent to <V cv 0>. Uses the verify callback.
* Allow WRITE CV on PROG <W CV VALUE)
* Change callback parameters are now optional on PROG
* New JA, JR, JT commands availabe for Throttle Developers to obtain Route, Roster and Turnout descriptions for communications
* New EX-RAIL Functions to use in Automation(n), ROUTE(N) & SEQUENCE(N) Scripts

    * ATGTE & ATLT wait for analog value, (At Greater Than or Equal and At Less Than a * certain value)
    * FADE command now works for LEDs connected on PCA9685 Servo/Signal board Output vpins
    * FORGET Forgets the current loco in DCC reminder tables saving memory and wasted packets sent to the track
    * "IF" signal detection with IFRED(signal_id), IFAMBER(signal_id), IFGREEN(signal_id)
    * KILLALL command to stop all tasks, and Diagnostic messages when KILL is used
    * PARSE <> commands in EXRAIL allows sending of DCC-EX commands from EX-RAIL
    * SERVO_SIGNAL Servo signals assigned to a specific servo turnout
    * SIGNALH High-On signal pins (Arduino normally handles active LOW signals. This allows for active HIGH)
    * HIDDEN turnouts (hide a REAL turnout and create a VIRTUAL turnout to handle actions that happen BEFORE a turnout is thrown)
    * VIRTUAL_TURNOUT definition

**EX-RAIL Updates**

* EXRAIL BROADCAST("msg") sends any message to all throttles/JMRI via serial and WiFi
* EXRAIL POWERON turns on power to both tracks from EX-RAIL (the equivalent of sending the <1> command)

**Other Enhancements**

* UNO Progmem is optimize to allow for small EXRAIL Automation scipts to run within the limited space for testing purposes.
* PCA9685 Servo Signal board supports 'Nopoweroffleds', servo pins stay powered on after position reached, otherwise the new FADE would always turn off.
* Position servo can use spare servo pin as a GPIO pin.

**4.1.2 Bug Fixes**

* Fixed Ethernet shield W5100 support since it does not report HW or link level like the W5200 and W5500 chips.

**4.1.1 Bug Fixes**

* Preserve the turnout format
* Parse multiple commands in one buffer string currectly
* Fix </> command signal status in EX-RAIL
* Read long loco addresses in EX-RAIL
* FIX negative route IDs in WIthrottle

See the version.h file for notes about which of the 4.1.2 features were added/changed by point release.

**Known Issues**

* Wi-Fi - Requires sending <AT> commands from a serial monitor if you want to switch between AP mode and STA station mode after initial setup
* Pololu Motor Shield - is supported with this release, but the user may have to adjust timings to enable programming mode due to limitations in its current sensing circuitry

| Contact info:
| Name: Fred Decker
| Organization: DCC-EX
| Address: 113 Main Street #767, Holly Springs, NC 27540
| Phone: +1 919-285-1576
