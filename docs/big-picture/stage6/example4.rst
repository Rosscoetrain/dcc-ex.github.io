.. include:: /include/include.rst
.. include:: /include/include-l2.rst
|EX-BP-LOGO|

****************************************************************************
Example - ROUTEs with servo based turnouts/signals on a PCA9685 servo module
****************************************************************************

|tinkerer| |engineer|

.. code-block:: 

  // myAutomation.h for simple ROUTEs with servo based turnouts and signals.

  ALIAS(TRN1, 100)
  ALIAS(TRN2, 101)
  ALIAS(SIG1_TRN1_APP, 102)
  ALIAS(SIG2_TRN2_GO, 103)
  ALIAS(SIG3_STN_EX, 104)

  // Start up with turnouts closed and signals red
  CLOSE(TRN1)
  CLOSE(TRN2)
  RED(SIG1_TRN1_APP)
  RED(SIG2_TRN2_GO)
  RED(SIG3_STN_EX)
  
  SERVO_TURNOUT(TRN1, 100, 400, 100, Slow, "Station entry")
  SERVO_TURNOUT(TRN2, 101, 400, 100, Slow, "Station exit")
  SERVO_SIGNAL(SIG1_TRN1_APP, 400, 250, 100)
  SERVO_SIGNAL(SIG2_TRN2_GO, 400, 250, 100)
  SERVO_SIGNAL(SIG3_STN_EX, 400, 250, 100)

  // We need DONE to tell EX-RAIL not to automatically proceed beyond definitions above
  DONE

  // Define our ROUTEs:
  ROUTE(1, "Main track")        // Select this route to just use the main track
    RED(SIG3_STN_EX)            // Set signal 3 red as it is not safe to exit the station siding
    IFTHROWN(TRN1)              // If turnout 1 is thrown, do these:
      AMBER(SIG1_TRN1_APP)      // Set signal 1 amber for 2 seconds to warn of the change
      DELAY(2000)
      RED(SIG1_TRN1_APP)        // Set signal 1 red while we close turnout 1
      CLOSE(TRN1)               // Close turnout 1
      DELAY(2000)               // Wait 2 seconds for the turnout to close
    ENDIF
    IFTHROWN(TRN2)              // If turnout 2 is thrown, do these:
      AMBER(SIG2_TRN2_GO)       // Set signal 2 amber for 2 seconds to warn of the change
      DELAY(2000)
      RED(SIG2_TRN2_GO)         // Set signal 2 red while we close turnout 2
      CLOSE(TRN2)               // Close turnout 2
      DELAY(2000)               // Wait 2 seconds for the turnout to close
    ENDIF
    GREEN(SIG1_TRN1_APP)        // Set signal 1 green because we're safe to proceed
    GREEN(SIG2_TRN2_GO)         // Set signal 2 green because we're safe to proceed
  DONE

  ROUTE(2, "Station siding")    // Select this route to use the station siding
    RED(SIG2_TRN2_GO)           // Set signal 2 red as it is not safe to proceed beyond turnout 2 on the main track
    IFCLOSED(TRN1)              // If turnout 1 is closed, do these:
      AMBER(SIG1_TRN1_APP)      // Set signal 1 amber for 2 seconds to warn of the change
      DELAY(2000)
      RED(SIG1_TRN1_APP)        // Set signal 1 red while we throw turnout 1
      THROW(TRN1)               // Throw turnout 1
      DELAY(2000)               // Wait 2 seconds for the turnout to throw
    ENDIF
    IFCLOSED(TRN2)              // If turnout 2 is closed, do these:
      AMBER(SIG3_STN_EX)       // Set signal 2 amber for 2 seconds to warn of the change
      DELAY(2000)
      RED(SIG3_STN_EX)         // Set signal 2 red while we throw turnout 2
      THROW(TRN2)               // Throw turnout 2
      DELAY(2000)               // Wait 2 seconds for the turnout to throw
    ENDIF
    GREEN(SIG1_TRN1_APP)        // Set signal 1 green because we're safe to proceed
    GREEN(SIG3_STN_EX)          // Set signal 2 green because we're safe to proceed
  DONE
