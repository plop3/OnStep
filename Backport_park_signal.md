Intégration Pin Park dans OnStep

Config.h
#define PARK_SIGNAL                  HIGH

Pins.xxx
#define PARK_SIGNAL_PIN      PA2     // SCL Pin ordre de park

OnStep.ino (after     // SAFETY CHECKS in loop2)
// SCL
#if PARK_SIGNAL != OFF
  // Support for park mount with pin
  byte park_1st = digitalRead(PARK_SIGNAL_PIN);
  if (park_1st == PARK_SIGNAL) {
    delayMicroseconds(50);
    byte park_2nd = digitalRead(PARK_SIGNAL_PIN);
    if (park_2nd == PARK_SIGNAL) {
      // Park the telescope
      park();
    }
  }
#endif

Initialize.ino (after   // limit switch sense)
  // SCL Park sense
#if PARK_SIGNAL != OFF
  pinMode(PARK_SIGNAL_PIN, INPUT);
#endif
