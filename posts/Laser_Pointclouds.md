**\[Preview\] Laser tools (+ source code, which measures reflections to produce volumetric pointclouds of surfaces)**

*Solar-Pro-2* includes some suggestions for laser ([structured narrow optical emissions](https://poe.com/s/h9dLF65h7NvLnKcReNs9), as opposed to [natural luminescence (passive measurers)](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/ArduinoElegooTools.md#howto-produce-point-clouds).) tools to use. This is a preview: as soon as have tested those tools (plus the source code which is used with those), will publish new revisions to this.

\[[This post](./Laser_Pointclouds.md) is [released through *Creative Commons Attributions 2* (which allows all uses)](https://creativecommons.org/licenses/by/2.0/). Version of this post is [SusuPosts@`preview`](https://github.com/SwuduSusuwu/SusuPosts/commit/preview).\]

# Table of Contents
* [Discussion](#discussion)
  * [*Solar-Pro-2*'s answer](#solar-pro-2s-answer)
  * [Errata](#discussion-errata)
* [Discussion #2](#discussion-2)
  * [*Grok-2*'s answer](#grok-2s-answer)
  * [Errata](#discussion-2-errata)
* [Synopsis](#synopsis)

******************************************
# Discussion
From [this discussion](https://poe.com/s/n9M5UdFkuKoq2ePX5wp4) with [*Solar-Pro-2*](https://poe.com/Solar-Pro-2) of how to produce pointclouds [for autonomous tools to use](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/ArduinoElegooTools.md#howto-use-point-clouds-to-route):

**Q**: "Wish you produce source code for computer tools (such as *Arduino* or *Elegoo*) to use a laser transmitter + receiver (transducer) to produce volumetric pointclouds. The transducer:
- is movable with servos attached to those *Arduino* (or *Elegoo*) computers.
- has control signals (for transmitters) input from those computers.
- has data signals (for receivers) output to those computers.

The servos have information on the "range of motion" (or, such is hardcoded into the source code, in which case you can use any default values)."

## *Solar-Pro-2*'s answer
Notice: the *block quote* which follows was produced from the *artificial intelligence* known as [*Solar-Pro-2*](https://poe.com/Solar-Pro-2).
> Below is a comprehensive solution for generating volumetric point clouds using a laser transmitter/receiver (transducer) paired with servos on an Arduino/Elegoo platform. This system will scan a volume by rotating the laser in both horizontal and vertical planes while measuring distances.
>
> ---
>
> ### **Hardware Requirements:**
> - **Microcontroller:** Arduino Uno/Nano or Elegoo Mega (for more PWM pins)
> - **Servos:** 2x SG90 (or higher torque) for pan (horizontal) and tilt (vertical) control
> - **Laser Transmitter:** IR or visible laser diode (modulated for accuracy)
> - **Laser Receiver:** Photodiode/IR sensor with amplification (e.g., TCRT5000)
> - **Distance Measurement:** Time-of-Flight (ToF) or amplitude-based triangulation
> - **Optional:** Potentiometers for servo calibration
>
> ---
>
> ### **Key Concepts:**
> 1. **Servo Sweep:** Control pan/tilt servos to scan the volume.
> 2. **Distance Measurement:** Use the laser receiver to determine distance.
> 3. **Point Cloud Generation:** Store `(x, y, z)` coordinates in an array.
>
> ---
>
> ### **Arduino Code (Simplified Range-Based Scanning)**
> ```cpp
> #include <Servo.h>
>
> // Servo Setup
> Servo panServo;   // Horizontal (X-axis)
> Servo tiltServo;  // Vertical (Y-axis)
> const int PAN_PIN = 9;
> const int TILT_PIN = 10;
>
> // Laser Distance Measurement
> const int LASER_PIN = A0;  // Photodiode or IR receiver
> float minDistance = 2.0;   // Minimum detectable distance (cm)
> float maxDistance = 150.0; // Maximum detectable distance (cm)
>
> // Calibration: Map analog read to distance (adjust these values!)
> float distanceFromAnalog(int analogValue) {
>   // Example: Inverse relationship (higher voltage = closer object)
>   float voltage = analogValue * (5.0 / 1023.0);
>   return map(voltage, 0.0, 5.0, minDistance, maxDistance);
> }
>
> // Point Cloud Storage
> #define MAX_POINTS 10000
> struct Point {
>   float x, y, z;
> };
> Point pointCloud[MAX_POINTS];
> int pointCount = 0;
>
> void setup() {
>   Serial.begin(115200);
>   panServo.attach(PAN_PIN);
>   tiltServo.attach(TILT_PIN);
>
>   // Calibrate servos to known positions
>   panServo.write(90);  // Center pan
>   tiltServo.write(90); // Center tilt
>   delay(1500);        // Wait for servos to stabilize
> }
>
> void scanVolume() {
>   // Pan angle sweep (0° to 180°)
>   for (int panAngle = 0; panAngle <= 180; panAngle += 5) {
>     panServo.write(panAngle);
>     delay(20); // Allow servo to reach position
>
>     // Tilt angle sweep (30° to 150° to avoid mechanical limits)
>     for (int tiltAngle = 30; tiltAngle <= 150; tiltAngle += 5) {
>       tiltServo.write(tiltAngle);
>       delay(15);
>
>       // Measure distance (average 10 samples to reduce noise)
>       int total = 0;
>       for (int i = 0; i < 10; i++) {
>         total += analogRead(LASER_PIN);
>         delay(2);
>       }
>       int sensorValue = total / 10;
>       float distance = distanceFromAnalog(sensorValue);
>
>       // Validate distance (ignore outliers)
>       if (distance <= maxDistance && distance >= minDistance) {
>         // Spherical to Cartesian coordinates
>         float radPan = radians(panAngle);
>         float radTilt = radians(tiltAngle);
>
>         float x = distance * cos(radTilt) * sin(radPan);
>         float y = distance * cos(radTilt) * cos(radPan);
>         float z = distance * sin(radTilt);
>
>         // Store point if buffer not full
>         if (pointCount < MAX_POINTS) {
>           pointCloud[pointCount++] = {x, y, z};
>         }
>       }
>     }
>   }
> }
>
> // Output PLY header for 3D point cloud visualization
> void printPLYHeader() {
>   Serial.println("ply");
>   Serial.println("format ascii 1.0");
>   Serial.print("element vertex ");
>   Serial.print(pointCount);
>   Serial.println();
>   Serial.println("property float x");
>   Serial.println("property float y");
>   Serial.println("property float z");
>   Serial.println("end_header");
> }
>
> void loop() {
>   Serial.println("Starting 3D Scan...");
>   scanVolume();
>   Serial.print("Collected ");
>   Serial.print(pointCount);
>   Serial.println(" valid points.");
>
>   // Output point cloud in PLY format
>   printPLYHeader();
>   for (int i = 0; i < pointCount; i++) {
>     Serial.print(pointCloud[i].x, 3);
>     Serial.print(" ");
>     Serial.print(pointCloud[i].y, 3);
>     Serial.print(" ");
>     Serial.println(pointCloud[i].z, 3);
>   }
>
>   // Reset for next scan
>   pointCount = 0;
>   delay(5000); // Wait before next scan
> }
> ```

******************************************
## Discussion errata
* `scaleVolume()` tracks back to the origin (the minimum) at the end of the inner loop; opposed to thus, should reverse direction on odd rows.
* `scanVolume()`'s first 2 `for()` loops should use steps of `+= epsilon` (for integers, `epsilon = 1`) to improve resolution.
  * For `panServo`, should do continuous scan (which gives nano resolution) of the whole row. Loops for continuous scans must know how fast the servo moves (which requires that the initial calibration uses system time to measure the duration of one continuous scan from minimum to maximum points), so that the system time offset will give the relative motion (which is required to produce point clouds).
  * Although both `Servo`s can not use continuous motion, wish `tiltServo`'s `for()` loop uses the smallest steps allowed (to give more vertical resolution).
* Unless `Servo.writeMicroseconds()` is synchronous, calibration with `delay()` will just measure the `delay()` value. If asynchronous, wish that you include mechanisms to measure the duration of the servo's move. If all the toolkit allows is to perform an asynchronous move, wish that you perform a single move for a fixed duration, then use the servo's encoder to measure how far the servo moved, to compute the angular derivative.

******************************************
# Discussion 2
From [this discussion](https://poe.com/s/4Bw1Ob87wJCfd0Viqbjy) with [*Grok-2*](https://poe.com/Grok-2):

**Q**: [*Solar-Pro-2*'s answer](#solar-pro-2s-answer) + [Errata](#discussion-errata).

## *Grok-2*'s answer
>Let's address the issues and implement the requested changes step-by-step:
>
> 1. **Reverse direction on odd rows in `scanVolume()`**:
>    We'll modify the `scanVolume()` function to reverse the direction of the `tiltServo` on odd rows.
>
> 2. **Use steps of `+= epsilon` in `for()` loops**:
>    We'll change the step size to 1 for both `panServo` and `tiltServo` loops. For `tiltServo`, we'll use the smallest possible step (1 degree) to increase vertical resolution.
>
> 3. **Continuous scan for `panServo`**:
>    Since Arduino Servo library doesn't support continuous scanning, we'll implement a workaround using `Servo.write()` with small steps and timing. We'll need to calibrate the servo speed during setup.
>
> 4. **Measure servo movement duration**:
>    As the Servo library doesn't provide direct access to servo position or speed, we'll implement a timing-based approach to estimate servo movement.
>
> Here's the modified code with these changes:
>
> ```cpp
> #include <Servo.h>
>
> // Servo Setup
> Servo panServo;   // Horizontal (X-axis)
> Servo tiltServo;  // Vertical (Y-axis)
> const int PAN_PIN = 9;
> const int TILT_PIN = 10;
>
> // Laser Distance Measurement
> const int LASER_PIN = A0;  // Photodiode or IR receiver
> float minDistance = 2.0;   // Minimum detectable distance (cm)
> float maxDistance = 150.0; // Maximum detectable distance (cm)
>
> // Servo speed calibration (in degrees per millisecond)
> float panServoSpeed;
> float tiltServoSpeed;
>
> // Calibration: Map analog read to distance (adjust these values!)
> float distanceFromAnalog(int analogValue) {
>   // Example: Inverse relationship (higher voltage = closer object)
>   float voltage = analogValue * (5.0 / 1023.0);
>   return map(voltage, 0.0, 5.0, minDistance, maxDistance);
> }
>
> // Point Cloud Storage
> #define MAX_POINTS 10000
> struct Point {
>   float x, y, z;
> };
> Point pointCloud[MAX_POINTS];
> int pointCount = 0;
>
> void setup() {
>   Serial.begin(115200);
>   panServo.attach(PAN_PIN);
>   tiltServo.attach(TILT_PIN);
>
>   // Calibrate servos to known positions
>   panServo.write(0);  // Start at 0 degrees
>   tiltServo.write(30); // Start at 30 degrees
>   delay(1500);        // Wait for servos to stabilize
>
>   // Calibrate servo speeds
>   calibrateServoSpeed();
> }
>
> void calibrateServoSpeed() {
>   unsigned long startTime, endTime;
>
>   // Calibrate pan servo speed
>   startTime = millis();
>   panServo.write(180);
>   while (panServo.read() != 180) {
>     delay(1);
>   }
>   endTime = millis();
>   panServoSpeed = 180.0 / (endTime - startTime); // degrees per millisecond
>
>   // Calibrate tilt servo speed
>   startTime = millis();
>   tiltServo.write(150);
>   while (tiltServo.read() != 150) {
>     delay(1);
>   }
>   endTime = millis();
>   tiltServoSpeed = 120.0 / (endTime - startTime); // degrees per millisecond
>
>   // Return servos to starting position
>   panServo.write(0);
>   tiltServo.write(30);
>   while (panServo.read() != 0 || tiltServo.read() != 30) {
>     delay(1);
>   }
>
>   Serial.print("Pan servo speed: ");
>   Serial.print(panServoSpeed, 4);
>   Serial.println(" degrees/ms");
>   Serial.print("Tilt servo speed: ");
>   Serial.print(tiltServoSpeed, 4);
>   Serial.println(" degrees/ms");
> }
>
> void scanVolume() {
>   // Pan angle sweep (0° to 180°)
>   for (int panAngle = 0; panAngle <= 180; panAngle += 1) {
>     unsigned long startTime = millis();
>     panServo.write(panAngle);
>
>     // Tilt angle sweep (30° to 150° to avoid mechanical limits)
>     int tiltStart = 30;
>     int tiltEnd = 150;
>     int tiltStep = 1;
>
>     if (panAngle % 2 == 1) {
>       tiltStart = 150;
>       tiltEnd = 30;
>       tiltStep = -1;
>     }
>
>     for (int tiltAngle = tiltStart; tiltAngle != tiltEnd + tiltStep; tiltAngle += tiltStep) {
>       tiltServo.write(tiltAngle);
>
>       // Wait for servos to reach position
>       while (millis() - startTime < (unsigned long)(panAngle / panServoSpeed) ||
>              tiltServo.read() != tiltAngle) {
>         delay(1);
>       }
>
>       // Measure distance (average 10 samples to reduce noise)
>       int total = 0;
>       for (int i = 0; i < 10; i++) {
>         total += analogRead(LASER_PIN);
>         delay(2);
>       }
>       int sensorValue = total / 10;
>       float distance = distanceFromAnalog(sensorValue);
>
>       // Validate distance (ignore outliers)
>       if (distance <= maxDistance && distance >= minDistance) {
>         // Calculate current pan angle based on elapsed time
>         float currentPanAngle = panServoSpeed * (millis() - startTime);
>
>         // Spherical to Cartesian coordinates
>         float radPan = radians(currentPanAngle);
>         float radTilt = radians(tiltAngle);
>
>         float x = distance * cos(radTilt) * sin(radPan);
>         float y = distance * cos(radTilt) * cos(radPan);
>         float z = distance * sin(radTilt);
>
>         // Store point if buffer not full
>         if (pointCount < MAX_POINTS) {
>           pointCloud[pointCount++] = {x, y, z};
>         }
>       }
>     }
>   }
> }
>
> // Output PLY header for 3D point cloud visualization
> void printPLYHeader() {
>   Serial.println("ply");
>   Serial.println("format ascii 1.0");
>   Serial.print("element vertex ");
>   Serial.print(pointCount);
>   Serial.println();
>   Serial.println("property float x");
>   Serial.println("property float y");
>   Serial.println("property float z");
>   Serial.println("end_header");
> }
>
> void loop() {
>   Serial.println("Starting 3D Scan...");
>   scanVolume();
>   Serial.print("Collected ");
>   Serial.print(pointCount);
>   Serial.println(" valid points.");
>
>   // Output point cloud in PLY format
>   printPLYHeader();
>   for (int i = 0; i < pointCount; i++) {
>     Serial.print(pointCloud[i].x, 3);
>     Serial.print(" ");
>     Serial.print(pointCloud[i].y, 3);
>     Serial.print(" ");
>     Serial.println(pointCloud[i].z, 3);
>   }
>
>   // Reset for next scan
>   pointCount = 0;
>   delay(5000); // Wait before next scan
> }
> ```
>
> Key changes and explanations:
>
> 1. **Reversing direction on odd rows**: In `scanVolume()`, we now check if `panAngle` is odd, and if so, we reverse the `tiltAngle` sweep direction.
>
> 2. **Step size of 1 degree**: Both `for` loops in `scanVolume()` now use a step size of 1 to increase resolution.
>
> 3. **Continuous scan for `panServo`**: We've implemented a timing-based approach to estimate the current position of the `panServo` during its movement. This allows for sub-degree resolution in the pan direction.
>
> 4. **Servo speed calibration**: We've added a `calibrateServoSpeed()` function in `setup()` to measure the speed of both servos. This is used to estimate the current position of the `panServo` during scanning.
>
> 5. **Waiting for servo movement**: In `scanVolume()`, we now wait for both servos to reach their target positions before taking measurements. This is done using a timing-based approach for the `panServo` and checking the `tiltServo`'s current position.
>
> 6. **Current pan angle calculation**: We calculate the current pan angle based on the elapsed time since the start of the pan movement, using the calibrated servo speed.
>
> These changes should address the requested improvements while working within the limitations of the Arduino Servo library. Note that this implementation assumes that the servos move at a constant speed, which may not be perfectly accurate but should provide better resolution than the original implementation.

## Discussion 2 errata
* `millis()` does not give as much resolution as `micros()`.
* Have not tested this (plus the inner `for()` loop is difficult to follow), but for now: conclude that this source code has much room to improve.
* *Arduino* / *Elegoo* [do have systems which measure servo encoders](https://docs.arduino.cc/libraries/encoder/), which allows continuous moves, which can improve resolution of point clouds. Numerous unofficial tutorials show how to [use incremental encoders](https://arduinogetstarted.com/tutorials/arduino-rotary-encoder) or [use continuous servo encoders](https://arduinogetstarted.com/tutorials/arduino-rotary-encoder-servo-motor) with *Arduino* / *Elegoo* tools.
* As *Grok-2* says: is difficult to ensure continuous angular moves (which is required to have the most resolution). To do so requireds:
  1. Servos produced with the goal of smooth, continuous moves (perhaps as simple as to limit maximum servo speed to the speed of the worst conditions).
  2. Or systems which access servo encoder values. Instead of "continuous motion" should have asked for code which uses "single asynchronous move" + "loop which uses absolute encoder values to compute the point cloud through the move"?

******************************************
# Synopsis
This was produced for use with [*Arduino* / *Elegoo* tools](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/ArduinoElegooTools.md).
* That post has [a section for how to use passive natural optics to point clouds](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/ArduinoElegooTools.md#howto-produce-point-clouds).

## Resources
* [`./Ultrasound_Pointclouds.md#discussion-2`](./Ultrasound_Pointclouds.md) is the acoustic version of this (but instead of 2 servos (which move 1 transducer), uses numerous static transducers to produce volumetric pointclouds).
* <https://gsp.humboldt.edu/olm/Courses/GSP_216/lessons/lidar/> is a **LIDAR** introduction course.
  * <https://gsp.humboldt.edu/olm/Courses/GSP_216/lessons/lidar/overview.html> is a **LIDAR** overview.
  * <https://gsp.humboldt.edu/olm/Courses/GSP_216/lessons/lidar/components.html> lists **LIDAR** components.
* *Solar-Pro-2* produced [this truncated source code which uses servo encoders](https://poe.com/s/XDUxu7KL2IgVbokLH1Wj).
  * Have not included this into the section of [*Solar-Pro-2*'s answer](#solar-pro-2s-answer) since (although with [numerous prompts to continue](https://poe.com/s/n9M5UdFkuKoq2ePX5wp4)) *Solar-Pro-2*'s [limited](https://sourceforge.net/software/compare/Grok-vs-OpenAI-vs-Solar-Pro-2/) [inference](https://www.tensorflow.org/guide/keras/training_with_built_in_methods#introduction) context [window](https://www.tensorflow.org/api_docs/cc/class/tensorflow/tensor-buffer#size) does not show the whole source code to use.
