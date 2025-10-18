**\[Preview\] Ultrasound acoustic tools (+ source code which measures echos of numerous transducers to produce volumetric pointclouds of surfaces)**

\[[This post](./Ultrasound_Pointclouds.md) is [released through *Creative Commons Attributions 2* (which allows all uses)](https://creativecommons.org/licenses/by/2.0/). Version of this post is [SusuPosts@`preview`](https://github.com/SwuduSusuwu/SusuPosts/commit/preview).\]

# Table of Contents
- [Discussion](#discussion)
  - [*Solar-Pro-2*'s answer](#solar-pro-2s-answer)
  - [**Q** #2](#q-2) (speculative 100m near-ultrasound sonar)
    - [*Solar-Pro-2*'s answer #2](#solar-pro-2s-answer-2)
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

# **Q** #2
Notice: will replace this section (with a future `# Discusion #2` for 10m point clouds), since the attributes of 100m ultrasound are not suitablle for use around humans.

**Q**: "This is for autonomous tools to use to transport or manufacture, so objects within 100m should show (with sufficient resolution to know what the object is, such as inanimate objects versus humans) in those pointclouds.
Wish that you produce the sonar transmitter/receiver attributes + source code."
- [Discussion #2](https://poe.com/s/wLjMViG23L6dUW3NtRh7)

## *Solar-Pro-2*'s answer #2
> For autonomous systems operating at ranges up to **100 meters** in air, standard ultrasound (20 kHz–1 MHz) faces significant limitations due to **attenuation** (e.g., 1 MHz ultrasound attenuates ~10 dB/m in air). To detect and classify objects (humans vs. inanimate) at this range, you’d need either:
> 1. **LIDAR** (optical) for high resolution, or
> 2. A **hybrid system** combining low-frequency acoustics (for long range) with machine learning for classification.
>
> However, if strictly using **acoustics**, here’s a practical approach:
>
> ---
>
> ### **1. Sonar Transmitter/Receiver Attributes for 100m Range**
> #### **Transmitter:**
> - **Frequency**: **10–40 kHz** (trade-off between attenuation and resolution).
>   - 10 kHz: λ = 3.4 cm (poorer resolution but longer range).
>   - 40 kHz: λ = 0.86 cm (better resolution but ~30 dB more attenuation at 100m).
> - **Power**: **≥180 dB SPL (peak)** to overcome air absorption.
>   - Use piezoelectric or capacitive ultrasonic transducers with high excitation voltage (e.g., 100–200 Vpp).
> - **Pulse Shape**: **Chirp signal** (linear FM, 5–40 kHz) for pulse compression and improved SNR.
> - **Beamwidth**: **Narrow beam** (e.g., <30°) using a **large aperture** (e.g., 15 cm diameter) or **acoustic lens**.
>
> #### **Receiver:**
> - **Sensitivity**: **≥40 dB re 1V/Pa** (high-gain preamplifier needed).
> - **Array Design**: **Phased array** (e.g., 8×8 elements) for beamforming and directionality.
> - **Sampling Rate**: **≥100 kHz** (Nyquist for 40 kHz).
> - **Dynamic Range**: **≥90 dB** to handle near/far targets.
>
> #### **Signal Processing:**
> - **Pulse Compression**: Matched filter for chirp signals to improve axial resolution.
> - **Beamforming**: Delay-and-sum for spatial filtering.
> - **Clutter Rejection**: Moving Target Indication (MTI) or Doppler filtering to distinguish humans (motion) from static objects.
> - **Classification**: Machine learning (CNN/LSTM) on time-of-flight/amplitude patterns.
>
> ---
>
> ### **2. Example Source Code (Python + MATLAB-style Pseudocode)**
> #### **Transmitter Signal Generation (Python):**
> ```python
> import numpy as np
> import sounddevice as sd
>
> # Chirp parameters
> start_freq = 5e3  # 5 kHz
> end_freq = 40e3   # 40 kHz
> duration = 1e-3   # 1 ms pulse
> fs = 100e3        # Sampling rate
>
> t = np.linspace(0, duration, int(fs * duration), endpoint=False)
> chirp = np.sin(2 * np.pi * (start_freq * t + (end_freq - start_freq) / (2 * duration) * t**2))
>
> # Transmit (requires ultrasonic amplifier and transducer)
> sd.play(chirp, samplerate=fs, blocking=True)
> ```
>
> #### **Receiver Signal Processing (MATLAB/Python):**
> ```python
> import numpy as np
> from scipy.signal import correlate
>
> # Simulated received signal (with attenuation and noise)
> received = np.convolve(chirp, np.exp(-t/0.1)) + 0.1 * np.random.randn(len(chirp)*2)
>
> # Matched filter for pulse compression
> matched = correlate(received, chirp, mode='same')
>
> # Peak detection for ToF
> peaks = find_peaks(matched, height=0.5)
> tof = peaks['peak_hrs'][0] / fs  # Time of flight in seconds
> distance = (tof * 343) / 2  # Round-trip distance in meters
>
> print(f"Detected object at {distance:.2f} meters")
> ```
>
> #### **Classification (Simplified Example):**
> ```python
> from sklearn.svm import SVC
>
> # Features: [distance, max_amplitude, duration, Doppler_shift]
> features = np.array([[15, 0.8, 0.5e-3, 2],  # Human (motion)
>                       [30, 1.2, 0.3e-3, 0],  # Static object
>                       ...])
>
> ```
>
> ### **3. Full Source Code (Python + Pseudocode)**
> #### **A. Hardware Setup (Simulated)**
> ```python
> import numpy as np
> import sounddevice as sd  # For audio I/O (ultrasonic transducers need external amp)
> from scipy.signal import chirp, correlate, find_peaks
>
> # Transmitter parameters
> fs = 200e3       # Sampling rate (Nyquist for 100 kHz)
> duration = 2e-3  # 2 ms chirp
> f0 = 10e3        # Start frequency (10 kHz)
> f1 = 40e3        # End frequency (40 kHz)
>
> # Generate linear FM chirp
> t = np.linspace(0, duration, int(fs * duration), endpoint=False)
> tx_signal = chirp(t, f0=f0, f1=f1, t1=duration, method='linear')
>
> # Transmit (requires ultrasonic amplifier and transducer)
> sd.play(tx_signal, samplerate=fs, blocking=True)
> ```
>
> #### **B. Receiver Signal Processing**
> ```python
> # Simulate received signal (with attenuation, noise, and multipath)
> def simulate_received_signal(tx_signal, fs, target_range, snr_db=20):
>     speed_of_sound = 343  # m/s
>     tof = 2 * target_range / speed_of_sound  # Round-trip time
>     delay_samples = int(tof * fs)
>
>     # Attenuation model (approximate for air at 1 atm)
>     attenuation = 0.85 ** (target_range / 10)  # ~15 dB/km at 40 kHz
>
>     # Add multipath (e.g., ground reflection)
>     multipath_delay = int(5e-3 * fs)  # 5 ms delay
>     multipath = 0.3 * np.roll(tx_signal, multipath_delay)
>
>     # Noise
>     noise_power = np.var(tx_signal) / (10**(snr_db / 10))
>     noise = np.random.normal(0, np.sqrt(noise_power), len(tx_signal) + len(tx_signal))
>
>     rx_signal = np.convolve(tx_signal, np.exp(-np.linspace(0, 1, len(tx_signal)) * 0.01))  # Simplified impulse response
>     rx_signal = np.roll(rx_signal, delay_samples) * attenuation + multipath + noise
>     return rx_signal[:2*len(tx_signal)]  # Trim to expected length
>
> # Example: Detect object at 50 meters
> rx_signal = simulate_received_signal(tx_signal, fs, 50.0)
> ```
>
> #### **C. Pulse Compression & Target Detection**
> ```python
> # Matched filter for pulse compression
> matched_filter = correlate(rx_signal, tx_signal, mode='same')
> matched_filter /= np.max(np.abs(matched_filter))  # Normalize
>
> # Peak detection for ToF
> peaks, _ = find_peaks(matched_filter, height=0.3, distance=50)
> detected_ranges = []
> for peak in peaks:
>     tof = peak / fs
>     distance = (tof * 343) / 2  # Convert to meters
>     detected_ranges.append(distance)
>
> print(f"Detected objects at: {detected_ranges} meters")
> ```
>
> #### **D. Doppler Processing (Human vs. Static Object)**
> ```python
> from scipy.fft import fft, fftshift
>
> # Short-time Fourier transform for Doppler
> window_size = 1024
> overlap = 512
> frequencies = fftshift(fft.rfftfreq(window_size, d=1/fs))
>
> # Extract Doppler-shifted peaks
> doppler_peaks = []
> for i in range(0, len(rx_signal) - window_size, window_size - overlap):
>     window = rx_signal[i:i+window_size]
>     fft_window = fftshift(fft(window))
>     doppler_peaks.append(np.argmax(np.abs(fft_window)))
>
> # Example: Detect motion (human)
> if any(abs(frequencies[peak]) > 100 for peak in doppler_peaks):
>     print("Motion detected (likely human).")
> else:
>     print("Static object.")
> ```
>
> ### **F. Feature Extraction & Classification**
> Here’s the **continued and completed source code** for the sonar-based object classification system, including the machine learning pipeline for distinguishing humans from inanimate objects.
> ```python
> from sklearn.ensemble import RandomForestClassifier
> from sklearn.preprocessing import StandardScaler
> from sklearn.pipeline import make_pipeline
>
> # Simulated dataset: [distance, max_amp, pulse_width, doppler_freq, num_peaks]
> # 1 = human, 0 = inanimate
> X_train = np.array([
>     [15.2, 0.75, 0.45e-3, 120, 2],  # Human
>     [28.0, 1.10, 0.30e-3, 0, 1],    # Static object
>     [42.5, 0.65, 0.50e-3, 80, 3],   # Human
>     [60.0, 1.30, 0.25e-3, 0, 1],    # Static object
>     # Add more samples as needed
> ])
> y_train = np.array([1, 0, 1, 0])
>
> # Train classifier
> clf = make_pipeline(StandardScaler(), RandomForestClassifier(n_estimators=100))
> clf.fit(X_train, y_train)
>
> # Example prediction from detected object
> if detected_ranges:
>     # Extract features from matched_filter and Doppler
>     peak_amp = np.max(matched_filter)
>     pulse_width = np.mean(np.diff(peaks))
>     doppler_freq = np.max(np.abs(frequencies[doppler_peaks]))
>     num_peaks = len(peaks)
>
>     # Feature vector for classification
>     features = np.array([[detected_ranges[0], peak_amp, pulse_width, doppler_freq, num_peaks]])
>     prediction = clf.predict(features)
>
>     print(f"Object classified as: {'Human' if prediction[0] else 'Inanimate'}")
> ```
>
> ---
>
> ### **4. Hardware Implementation Notes**
> - **Transducer Selection**:
>   Use **high-power piezoelectric transducers** (e.g., **40 kHz Murata MA40S4S**) with a **matching network** for air coupling.
>   - **Transmitter**: Drive with a **high-voltage amplifier** (e.g., 200 Vpp).
>   - **Receiver**: Use a **low-noise preamplifier** (e.g., LMV723 op-amp) with **variable gain** (40–60 dB).
>
> - **Array Design**:
>   For **beamforming**, arrange transducers in a **2D grid** (e.g., 8×8) with **digital beamforming** via an **FPGA** or **microcontroller** (e.g., Teensy 4.1).
>
> - **Power Considerations**:
>   - **Peak power** for 100m range: **≥170 dB SPL** (requires **class D amplifier** and high-voltage supply).
>   - **Duty cycle**: Keep **<1%** to avoid overheating.
>
> ---
>
> ### **5. Limitations & Improvements**
> - **Attenuation**: Air absorbs ultrasound strongly. Consider **hybrid systems** (LIDAR + sonar) for robustness.
> - **Resolution**: Ultrasound struggles to resolve small objects at 100m. Use **multiple frequencies** (e.g., 10 kHz for range, 40 kHz for detail).
> - **Classification**: Improve with **deep learning** (e.g., **1D CNN** on raw time-series data).
>
> ---
>
> ### **6. Example Deep Learning Model (Optional)**
> ```python
> import tensorflow as tf
> from tensorflow.keras import layers
>
> # Simplified 1D CNN for raw signal classification
> model = tf.keras.Sequential([
>     layers.Conv1D(32, 5, activation='relu', input_shape=(None, 1)),
>     layers.MaxPooling1D(2),
>     layers.Conv1D(64, 5, activation='relu'),
>     layers.GlobalAveragePooling1D(),
>     layers.Dense(1, activation='sigmoid')
> ])
>
> model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
> ```
>
> Let me know if you’d like help with:
> - **FPGA beamforming code**,
> - **Hardware schematics**,
> - **Dataset generation** for training.

## Errata
* The decibels are not suitable for use around humans (unless this is inaudible ultrasound).
* This source code not seem to use servos to scan the transducer around (which is required to produce volumetric point clouds).

******************************************

# Synopsis
This was produced for use with [*Arduino* / *Elegoo* tools](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/ArduinoElegooTools.md).
* That post has [a section for how to produce optical point clouds](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/ArduinoElegooTools.md#howto-produce-point-clouds).
