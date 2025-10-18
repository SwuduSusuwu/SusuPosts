**Ultrasound acoustic tools (+ source code which measures echos of numerous transducers to produce volumetric pointclouds of surfaces)**

\[[This post](./Ultrasound_Pointclouds.md) is [released through *Creative Commons Attributions 2* (which allows all uses)](https://creativecommons.org/licenses/by/2.0/). Version of this post is [SusuPosts@`preview`](https://github.com/SwuduSusuwu/SusuPosts/commit/preview).\]

# Table of Contents
- [Discussion](#discussion)
  - [*Solar-Pro-2*'s answer](#solar-pro-2s-answer)
- [Discussion #2](#discussion-2) (10m distance, 2mm resolution point clouds)
  - [*Solar-Pro-2*'s answer](#solar-pro-2s-answer-dis-2) (source code suitable to use)
- [Synopsis](#synopsis)

******************************************

# Discussion
From [this discussion](https://poe.com/s/6GA3u84bb2aBBQqr7u4Y) with [*Solar-Pro-2*](https://poe.com/Solar-Pro-2) of how to produce pointclouds [for autonomous tools to use](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/ArduinoElegooTools.md#howto-use-point-clouds-to-route):

**Q**: "At standard atmospheric pressure: which attributes of ultrasound modules allow to best produce point clouds? Guess that the atmosphere is not conducive to match LIDAR's resolution (a simple apparatus which scans a laser+receiver across the visual field should have resolution equal to the laser resolution, which is an improvement versus what visible photons can do): wish to know the best sound resolution."

## *Solar-Pro-2*'s answer
> To produce high-resolution **point clouds** using ultrasound at standard atmospheric pressure, the following attributes of ultrasound modules are critical for maximizing acoustic resolution:
>
> ### 1. **Frequency (Wavelength)**
> - **Higher frequencies (e.g., 40 kHz to a few MHz)** provide better spatial resolution because the wavelength (λ = c/f, where c is the speed of sound in air ~343 m/s) is smaller.
>   - *Example*: A 40 kHz ultrasound has a wavelength of ~8.6 mm, while a 400 kHz transducer has λ ~0.86 mm, enabling finer detail.
> - **Trade-off**: Higher frequencies attenuate faster in air, limiting range. For short-range applications (e.g., <1 m), higher frequencies are optimal.
>
> ### 2. **Beamwidth (Directivity)**
> - **Narrow beamwidth** (controlled by transducer aperture size and focusing optics) improves lateral resolution.
>   - A **large aperture** and **focused beam** reduce divergence, allowing sharper point localization.
> - *Example*: A phased-array transducer can steer and focus beams electronically for dynamic resolution.
>
> ### 3. **Pulse Duration & Bandwidth**
> - **Short pulses** (broad bandwidth) improve axial resolution (Δz ≈ c·τ/2, where τ is pulse duration).
>   - *Example*: A 1 µs pulse gives ~17 cm axial resolution, but a 0.1 µs pulse improves this to ~1.7 cm.
> - **Chirped signals (FMCW or pulse compression)** can achieve high resolution with longer ranges by exploiting frequency-modulated pulses.
>
> ### 4. **Receiver Sensitivity & Signal Processing**
> - **High signal-to-noise ratio (SNR)** from sensitive receivers (e.g., piezoelectric or MEMS microphones) and noise filtering (e.g., matched filtering) enhances detection of weak echoes.
> - **Time-of-flight (ToF) precision**: Sub-nanosecond timing resolution is needed for mm-scale accuracy.
>
> ### 5. **Transducer Array Design**
> - **Multi-element arrays** (e.g., 1D/2D phased arrays) enable synthetic aperture techniques, beamforming, and speckle reduction.
>   - *Example*: A 128-element linear array can electronically scan and focus for 3D point clouds.
>
> ### 6. **Atmospheric Considerations**
> - Air is a poor acoustic medium (compared to water/solids) due to:
>   - High attenuation (~dB/cm·MHz at standard pressure).
>   - Temperature/humidity gradients causing refraction.
> - **Optimization**: Use frequencies below 1 MHz for longer ranges, or operate in controlled environments (e.g., humidity >50% reduces attenuation).
>
> ### **Limitations vs. LIDAR**
> - LIDAR’s optical wavelengths (~µm) inherently offer micrometer-scale resolution, while ultrasound is limited to mm–cm scales in air.
> - Ultrasound’s diffraction limit (λ/2) is ~0.4 mm at 400 kHz, but practical systems rarely achieve this due to air’s properties.
>
> ### **Best Sound Resolution Scenario**
> For a balance of resolution and range:
> - **Frequency**: 200–500 kHz (λ ~0.7–1.7 mm).
> - **Transducer**: Focused, large-aperture array with matched filtering.
> - **Range**: <1 m (due to attenuation).
> - **Resolution**: ~1–5 mm (axial/lateral) under ideal conditions.
>
> In summary, while ultrasound cannot match LIDAR’s optical resolution in air, optimizing frequency, beamforming, and signal processing can yield the best possible acoustic point clouds for short-range applications.

******************************************

# Discussion 2
From [this discussion](https://poe.com/s/jcZk6J2pciEFEFqzfuG6) with *Solar-Pro-2*:

**Q**: "Wish that you produce source code which uses acoustic transducers to produce point clouds. Those transducers should use low (just a few hertz above notice to humans) ultrasound.

The point clouds are for autonomous tools to use to manufacture (not for cars on roads), so a distance of 10m is sufficient for this use. Guess resolution of around 2mm will give sufficient info of  structures (or of humans)."

## *Solar-Pro-2*'s answer dis. #2

> Creating a system that uses low-frequency ultrasound transducers (just above human hearing range, ~20Hz–25kHz) to generate 3D point clouds for industrial manufacturing automation is an ambitious but feasible concept. Below is a breakdown of the approach and sample code for prototyping, though note that the actual hardware implementation would require careful engineering.
>
> ---
>
> ### **System Overview**
> 1. **Transducers**: Use phased arrays of low-frequency ultrasonic transducers (25kHz–50kHz) to emit directional sound waves.
> 2. **Time-of-Flight (ToF) Sensing**: Measure the time taken for echoes to return to calculate distances.
> 3. **Phased Array Beamforming**: Steer beams electronically to scan the environment.
> 4. **Point Cloud Generation**: Aggregate distance measurements to reconstruct 3D structures.
> 5. **Resolution**: With 2mm resolution and 10m range, the system needs sub-microsecond timing precision.
>
> ---
>
> ### **Key Components**
> - **Hardware**:
>   - Ultrasonic Transducers (e.g., Murata MA40S4S or custom arrays).
>   - Microcontroller with high-speed timers (e.g., Teensy 4.1, STM32H7).
>   - ADC/DAC for signal processing (optional for advanced modulation).
>   - Beamforming control circuitry (FPGA or DSP for real-time steering).
>
> - **Software**:
>   - Pulse generation and timing.
>   - Echo detection (thresholding, cross-correlation).
>   - Beamforming algorithms (delay-and-sum).
>   - Point cloud fusion (e.g., with PCL or Open3D).
>
> ---
>
> ### **Sample Code (Microcontroller + Beamforming)**
> This example uses a simplified beamforming approach with an array of 4 transducers. For a real system, you’d need more transducers and advanced signal processing.

\<snip\>

> Apologies for the cut-off. Let's continue the beamforming and point cloud generation logic. Here's the refined version of the code to compute 3D coordinates from the ultrasonic measurements:
>
> ```cpp
> #include <Arduino.h>
> #include <vector>
> #include <cmath>
> #include <pcl/point_types.h>  // If using PCL for point cloud output
>
> // Constants
> #define NUM_TRANS 4
> #define SOUND_SPEED 343.0    // m/s at 20°C
> #define FREQ 40000           // 40kHz (adjust based on transducer)
> #define TRANS_SPACING 0.03   // 3cm spacing between transducers (adjust as needed)
>
> // Pins for transducer triggers and echo inputs
> const int trigPins[NUM_TRANS] = {2, 3, 4, 5};
> const int echoPins[NUM_TRANS] = {6, 7, 8, 9};
>
> // Structure for 3D point
> struct Point3D {
> 		float x, y, z;
> };
>
> // Function to measure distance with one transducer
> float measureDistance(int trigPin, int echoPin) {
> 	digitalWrite(trigPin, LOW);
> 	delayMicroseconds(2);
> 	digitalWrite(trigPin, HIGH);
> 	delayMicroseconds(10);  // 10µs pulse
> 	digitalWrite(trigPin, LOW);
>
> 	long duration = pulseIn(echoPin, HIGH, 5000);  // 5ms timeout (~7m max range)
> 	if (duration == 0) return -1.0;               // No echo
> 	return (duration * SOUND_SPEED) / (2.0 * 1e6); // Distance in meters
> }
>
> // Simplified beamforming (steer to angle theta)
> void steerBeam(float theta_deg, float phi_deg, std::vector<Point3D>& pointCloud) {
> 	float theta = radians(theta_deg);  // Azimuth angle (horizontal)
> 	float phi = radians(phi_deg);      // Elevation angle (vertical)
>
> 	// Calculate delays for beamforming (2D steering)
> 	float delay[NUM_TRANS];
> 	for (int i = 0; i < NUM_TRANS; i++) {
> 		// Assuming linear array along x-axis; for 2D arrays, add y-axis terms
> 		delay[i] = (i * TRANS_SPACING * sin(theta) * cos(phi)) / SOUND_SPEED;
> 	}
>
> 	// Simulate phased transmission (in real hardware, use FPGA/DAC for precise timing)
> 	for (int i = 0; i < NUM_TRANS; i++) {
> 		digitalWrite(trigPins[i], LOW);
> 		delayMicroseconds((unsigned long)(delay[i] * 1e6) + 1);  // Add 1µs safety margin
> 		digitalWrite(trigPins[i], HIGH);
> 		delayMicroseconds(10);
> 		digitalWrite(trigPins[i], LOW);
> 	}
>
> 	// Receive echoes and compute 3D points
> 	for (int i = 0; i < NUM_TRANS; i++) {
> 		float dist = measureDistance(trigPins[i], echoPins[i]);
> 		if (dist > 0 && dist < 10.0) {  // Ignore outliers >10m
> 			Point3D pt;
> 			pt.x = dist * cos(theta) * cos(phi);  // Spherical to Cartesian
> 			pt.y = dist * sin(theta) * cos(phi);
> 			pt.z = dist * sin(phi);
> 			pointCloud.push_back(pt);
> 		}
> 	}
> }
>
> // Example usage: Scan a volume
> void scanVolume(std::vector<Point3D>& fullCloud) {
> 	for (int theta_deg = -45; theta_deg <= 45; theta_deg += 5) {  // Azimuth sweep
> 		for (int phi_deg = -15; phi_deg <= 15; phi_deg += 5) {   // Elevation sweep
> 			steerBeam(theta_deg, phi_deg, fullCloud);
> 			delay(50);  // Cooldown between measurements
> 		}
> 	}
> }
>
> void setup() {
> 	Serial.begin(115200);
> 	for (int i = 0; i < NUM_TRANS; i++) {
> 		pinMode(trigPins[i], OUTPUT);
> 		pinMode(echoPins[i], INPUT);
> 	}
> }
>
> // Here's the completed `loop()` function that outputs the point cloud in **PCL (Point Cloud Library) format** (`.pcd`), a widely used standard in robotics and 3D sensing. For simplicity, the code outputs ASCII PCD here (binary would be more efficient but harder to debug).
> void loop() {
> 	std::vector<Point3D> pointCloud;
> 	scanVolume(pointCloud);
>
> 	// Convert to PCL point cloud format
> 	pcl::PointCloud<pcl::PointXYZ> pclCloud;
> 	for (const auto& pt : pointCloud) {
> 		pcl::PointXYZ pclPt;
> 		pclPt.x = pt.x;
> 		pclPt.y = pt.y;
> 		pclPt.z = pt.z;
> 		pclCloud.width = pclCloud.points.size() + 1;
> 		pclCloud.height = 1;
> 		pclCloud.is_dense = false;
> 		pclCloud.points.push_back(pclPt);
> 	}
>
> 	// Output as ASCII PCD
> 	Serial.println("# .PCD v.7 - Point Cloud Data file format");
> 	Serial.print("VERSION .7\n");
> 	Serial.print("FIELDS x y z\n");
> 	Serial.print("SIZE 4 4 4\n");
> 	Serial.print("TYPE F F F\n");
> 	Serial.print("COUNT 1 1 1\n");
> 	Serial.print("WIDTH ");
> 	Serial.print(pclCloud.width);
> 	Serial.print("\n");
> 	Serial.print("HEIGHT 1\n");
> 	Serial.print("VIEWPOINT 0 0 0 1 0 0 0\n");
> 	Serial.print("POINTS ");
> 	Serial.print(pclCloud.width);
> 	Serial.print("\n");
> 	Serial.print("DATA ascii\n");
>
> 	for (const auto& pt : pclCloud.points) {
> 		Serial.print(pt.x, 3); Serial.print(" ");
> 		Serial.print(pt.y, 3); Serial.print(" ");
> 		Serial.print(pt.z, 3); Serial.print("\n");
> 	}
> 	Serial.println("END");
>
> 	// Delay between scans (adjust based on hardware speed)
> 	delay(1000);
> }
> ```
>
> ---
>
> ### **Key Notes for Implementation**
> 1. **Hardware Limitations**:
>    - The Arduino `pulseIn()` function has ~5µs resolution, limiting sub-millimeter precision. For 2mm resolution, consider:
>      - FPGA-based timing for nanosecond precision.
>      - Cross-correlation of received waveforms (requires ADC).
>
> 2. **Beamforming Improvements**:
>    - The code uses a simple delay-and-sum method. For better resolution:
>      - Use a 2D transducer array.
>      - Implement MIMO (Multiple-Input Multiple-Output) ultrasound.
>
> 3. **Signal Processing**:
>    - Add filtering (bandpass around 40kHz) to reject noise.
>    - Use matched filters for echo detection.
>
> 4. **Real-World Calibration**:
>    - Account for temperature (sound speed varies with temperature).
>    - Calibrate transducer positions and timing offsets.
>
> 5. **PCD Output**:
>    - For binary PCD (more compact), use `DATA binary` and write raw bytes.
>    - For large datasets, store to SD card instead of Serial.
>
> ---
>
> ### **Example PCD Output Snippet**
> ```
> # .PCD v.7 - Point Cloud Data file format
> VERSION .7
> FIELDS x y z
> SIZE 4 4 4
> TYPE F F F
> COUNT 1 1 1
> WIDTH 12
> HEIGHT 1
> VIEWPOINT 0 0 0 1 0 0 0
> POINTS 12
> DATA ascii
> 0.123 0.456 0.789
> 0.234 0.567 0.890
> ...
> END
> ```
>
> This can be loaded into tools like **CloudCompare** or **PCL** for visualization/processing. For industrial use, pair this with a more powerful microcontroller (e.g., Teensy 4.1, Raspberry Pi Pico) or an FPGA for real-time beamforming.

******************************************

# Synopsis
This was produced for use with [*Arduino* / *Elegoo* tools](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/ArduinoElegooTools.md).
* That post has [a section for how to produce optical point clouds](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/ArduinoElegooTools.md#howto-produce-point-clouds).

## Speculative
The famous question "How is it to live as a bat?" is somewhat answered with this source code: in addition to normal sounds, bats have "echolocation experiences" similar to "synesthesia" (sound signals crossover into visuals) in humans: signals from echos are replaced with (interpolated, smoothed) point-cloud visuals.
* More difficult to answer is "How is it to live as a computer or Kuratas?", which [this discussion with *Solar-Pro-2*](https://github.com/SwuduSusuwu/SusuJava/blob/pos2/posts/ConcernsOfExistenceMonism.md#what-if-carbon-chauvinism-is-disproven) somewhat answers.

