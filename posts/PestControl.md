# PestControl — small autonomous robots for stinging‑insect mitigation

This post collects schematics, blueprints, and implementation notes for small autonomous robots intended to mitigate populations of disease-carrying stinging insects (e.g., mosquitoes, wasps, hornets) in controlled settings. The material reuses tools and patterns from existing posts in this repository (Arduino/Elegoo microcontroller toolchain, ultrasound and laser point-cloud sensing, IMU-based collision handling, and point-cloud routing). All original code and text is released under the same permissive terms used in the referenced posts.

WARNING / ETHICS / LEGAL
- This document targets non-prohibited, humane pest-control in lawful contexts (private property, permitted public deployments). Before building or deploying any system that actively captures or kills animals, verify local laws, wildlife regulations, and safety requirements.
- Take steps to avoid harming non-target species (pets, pollinators such as honeybees and butterflies) and to avoid exposing people to dangerous components (laser diodes, exposed blades, high voltage).
- Provide fail-safes to stop motion and disable capture mechanisms on human presence detection. Do not deploy in densely populated public spaces without explicit review and permits.

Overview
- Goal: small mobile robots (wheeled or compact limbed devices) that locate and assist in neutralizing disease-carrying stinging insects in defined areas (e.g., backyard, greenhouse, near standing water).
- Approach: combine lightweight on-board sensing (camera + optical flow or monocular depth, ultrasonic range-finders, inexpensive LIDAR/laser distance modules), IMU for kinematic safety, and a safe capture/neutralization mechanism (examples: suction + containment, adhesive capture pads, mechanical trapping; avoid explosive or otherwise unsafe methods).
- Software stack: simple microcontroller-level control (Arduino/Elegoo family) for low-level actuation and sensor sampling; optional on-board Raspberry Pi or companion computer for heavier vision / point-cloud processing; ROS optional for multi-robot coordination.

Safety-first design principles
- Low-voltage actuators and power-limited capture actuators to minimize risk.
- Physical guards around moving parts; enclosed intake for suction-based capture.
- Visual and proximity interlocks: stop capture and motion if humans or pets are detected.
- Logging and manual override controls.
- Clear, visible labeling on deployed units and documentation for owners/operators.

Hardware components (example)
- MCU: Arduino Uno / Elegoo UNO R3 or an MCU with sufficient I/O for sensors + actuators.
- Companion compute (optional): Raspberry Pi Zero/4 for machine vision and point-cloud processing.
- Locomotion: two-wheel differential drive with encoders (small DC motors + H-bridge) or micro continuous-track modules.
- Power: LiPo battery with proper charging & overcurrent protection; fuse + cutoff.
- Sensors:
  - IMU (e.g., MPU6050 / LSM6DS3) for collision detection & pose stabilization.
  - Ultrasonic distance sensors (HC-SR04) for short-range obstacle detection.
  - Time-of-flight / laser distance sensors or low-cost LIDAR for point-cloud / obstacle mapping.
  - Camera (Pi Camera, USB camera, or small M12 module) for insect detection and visual confirmation.
- Capture mechanism options (choose one based on safety/regulatory compliance):
  - Low-power suction with a small fan and capture container (easy to empty); include one-way valve and protective grille.
  - Retractable adhesive pad on a small arm to pick up insects (use caution: sticky pads attract non-target insects too).
  - Small mechanical trap (chamber that closes after insect detection) — ensure safety interlocks to prevent accidental trapping of larger animals.
- Misc: micro servos for actuator arms, MOSFETs or motor drivers, voltage regulators, connectors, enclosure.

Sensor fusion & perception
- Short-range detection: ultrasonic sensors detect presence and range in a narrow band; useful for obstacle avoidance and close-range engagement.
- Medium-range mapping: laser distance sensors or low-cost LIDAR produce sparse point clouds for obstacle mapping and path planning.
- Vision-based detection: use lightweight object-detection or motion-based heuristics to identify flying insects:
  - Motion detection (frame differencing / optical flow) to detect small, fast-moving objects.
  - Small neural models (Tiny-YOLO, MobileNet-SSD) can classify larger targets (wasps/hornets) if trained appropriately; these require a companion computer.
  - For many mosquito-sized targets, optical detection is difficult; combining motion + acoustic signatures (microphone with bandpass tuned to wingbeat frequency) can help detection.
- Combine sensors in a simple finite-state logic: detect → approach → engage-capture → confirm containment → log & release/neutralize.

Point-cloud mapping and routing (high-level)
- Use laser/time-of-flight modules to build local 2D/2.5D occupancy maps.
- Fuse camera detections into the local map with coarse depth estimates (monocular depth model or motion parallax / optical-flow derived depth).
- Path planning: simple A* or DWA (Dynamic Window Approach) on the small occupancy grid; replan frequently to handle moving obstacles (people/pets).
- For multi-robot systems, consider a minimal decentralized task allocation: broadcast short route/intent messages and avoid route collisions.

Collision detection, IMU safety & kinematic checks
- Use IMU to detect unexpected accelerations or rotations indicating collision or tipping — on such events, stop motors and actuators and retract capture mechanisms.
- Implement periodic calibration and expected-motion lookups per joint/actuator to detect deviations (see IMU-based kinematic detection patterns in the Arduino tooling post).

Behavior/state machine (pseudocode)
- Idle: patrol route or remain stationary scanning.
- DetectCandidate: motion / vision / acoustic detection implies insect in region.
- Approach: plan short safe approach; slow-speed mode; enable fine sensors.
- EngageCapture: activate capture mechanism; continue monitoring for human presence.
- Confirm: verify capture (camera or sensor confirmation) and contain insect.
- PostProcess: log event, optionally neutralize if required and permitted, or store for operator inspection.
- EmergencyStop: human/pet detected or collision; retract and disable capture.

Example high-level pseudocode
```
state = IDLE
while true:
  readSensors()
  if humanDetected():
    state = EMERGENCY_STOP
  if state == IDLE:
    patrol()
    if candidate = detectInsect():
      state = APPROACH
  elif state == APPROACH:
    planApproach(candidate)
    if closeEnough():
      state = ENGAGE
  elif state == ENGAGE:
    activateCapture()
    if captureConfirmed():
      state = CONFIRM
    if timeout or humanDetected():
      deactivateCapture(); state = IDLE
  elif state == CONFIRM:
    storeLog(); state = IDLE
  elif state == EMERGENCY_STOP:
    stopAll(); retractCapture(); waitForManualReset()
```

Minimal Arduino example (locomotion + ultrasonic obstacle avoidance)
- Use the wheeled Arduino patterns and encoder loops already present in the Arduino/Elegoo tooling post. Integrate an ultrasonic check before motion and IMU checks in loop to stop on anomalies. Keep the MCU code focused on safe actuation and rely on a companion computer for heavier perception.

Deployment and operation checklist
- Test indoors with harmless targets (paper insects, small foam objects) to validate approach and capture logic before any field deployment.
- Add clear visible warnings on devices; include a hardware kill switch accessible to a human operator.
- Provide a manual companion app or physical control to retrieve captured material and disable device.
- Maintain logs and timestamps of captures and encounters for auditing.

Limitations & further research
- Detecting and capturing extremely small insects (e.g., mosquitoes) reliably in the wild is a challenging research problem — consider controlled traps (standing water treatment) alongside mobile agents.
- Vision-based classifiers require labeled datasets and careful balancing to avoid misclassification of beneficial insects.
- Acoustic detection (wingbeat frequency) is an emerging, promising area; combining modalities improves precision.

References
- See posts: ArduinoElegooTools.md (microcontroller and IMU patterns), Ultrasound_Pointclouds.md (ultrasonic sensing and short-range mapping), Laser_Pointclouds.md (laser/LIDAR mapping and point-cloud routing). Reuse their schematics, safety notes, and code snippets where relevant.
