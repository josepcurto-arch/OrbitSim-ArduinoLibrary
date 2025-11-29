  OrbitSim Library Documentation

  OrbitSim is a lightweight Arduino library to simulate satellite orbits around the Earth.
  It calculates the position of a satellite in either inertial or Earth-centered, Earth-fixed (ECEF) coordinates in real time.

  ------------------------------------------------
  Features:
  ------------------------------------------------
  - Simulates circular satellite orbits at a fixed altitude.
  - Supports orbital inclination.
  - Provides positions in both inertial and ECEF coordinates.
  - Handles timed updates automatically.
  - Easy to integrate with Arduino projects.

  ------------------------------------------------
  Installation:
  ------------------------------------------------
  1. Copy OrbitSim.h and OrbitSim.cpp into your Arduino project folder.
  2. Include the library in your sketch:
     #include "OrbitSim.h"

  ------------------------------------------------
  Usage:
  ------------------------------------------------

  1. Initialize the library in setup():
```
void setup() {
  Serial.begin(9600);
  orbitSetup();  // Initializes the simulation
}
```

  2. Get satellite position automatically in loop():
```
void loop() {
  double* pos = orbitLoop();  // Returns [x, y, z] in meters

  Serial.print("X: "); Serial.print(pos[0]);
  Serial.print(" Y: "); Serial.print(pos[1]);
  Serial.print(" Z: "); Serial.println(pos[2]);
}
```
     - orbitLoop() automatically updates the satellite position based on MILLIS_BETWEEN_UPDATES.
     - Returns a static array [x, y, z] representing coordinates relative to Earth's center.

  3. Manual simulation with inclination or ECEF coordinates:
```
unsigned long t = millis();           // current time in ms
double inclination = PI / 6;          // 30° inclination in radians
int ecef = 1;                         // 1 = ECEF coordinates, 0 = inertial

double* pos = simulate_orbit(t, inclination, ecef);

Serial.print("X: "); Serial.print(pos[0]);
Serial.print(" Y: "); Serial.print(pos[1]);
Serial.print(" Z: "); Serial.println(pos[2]);
```
     - inclination controls the tilt of the orbit.
     - ecef = 1 converts coordinates to Earth-centered, Earth-fixed frame.

  ------------------------------------------------
  Constants:
  ------------------------------------------------
  ```
  G                    = 6.67430e-11  // Universal gravitational constant
  M                    = 5.97219e24  // Earth mass (kg)
  R_EARTH              = 6371000      // Earth radius (meters)
  ALTITUDE             = 400000       // Default satellite altitude (meters)
  EARTH_ROTATION_RATE  = 7.2921159e-5 // Earth's rotation rate (rad/s)
  MILLIS_BETWEEN_UPDATES = 1000       // Time between simulation updates (ms)
  TIME_COMPRESSION     = 90.0         // Factor to speed up simulation time
```

  ------------------------------------------------
  Notes:
  ------------------------------------------------
  - The returned array [x, y, z] is static; calling orbitLoop() or simulate_orbit() again overwrites it.
  - Orbits are assumed circular.
  - Positions are relative to Earth's center.
  - Inclination is in radians.

  ------------------------------------------------
  Example Sketch:
  ------------------------------------------------
  ```
     #include "OrbitSim.h"

     void setup() {
         Serial.begin(9600);
         orbitSetup();
     }

     void loop() {
         double* pos = orbitLoop();  // Automatic update every second
         Serial.print("X: "); Serial.print(pos[0]);
         Serial.print(" Y: "); Serial.print(pos[1]);
         Serial.print(" Z: "); Serial.println(pos[2]);
         delay(500);
     }
```
  ------------------------------------------------
  License:
  ------------------------------------------------
  This project is open-source and free to use.
