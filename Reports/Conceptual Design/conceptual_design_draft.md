# Conceptual Design
**Capstone I – Team 8**  
**Triage Drone**  

Ryan Lee  
Allison Wolden  
Weston LaRue  
Brandon Price  
Sidney Delgado  

---

## Table of Contents
* [I. Introduction](#i-introduction)
* [II. Background](#ii-background)
    * [A. Defining Triage](#a-defining-triage)
    * [B. Benefits of a Triage Drone](#b-benefits-of-a-triage-drone)
    * [C. Sensors, Peripherals, and their Functional Roles](#c-sensors-peripherals-and-their-functional-roles)
    * [D. Previous Designs and Iterative Evolution](#d-previous-designs-and-iterative-evolution)
* [III. Fully Formulated Problem](#iii-fully-formulated-problem)
* [IV. Comparative Analysis of Potential Solutions](#iv-comparative-analysis-of-potential-solutions)
    * [A. Control Systems](#a-control-systems)
    * [B. Radar Systems](#b-radar-systems)
    * [C. Human Locating Systems](#c-human-locating-systems)
    * [D. Communication Systems](#d-communication-systems)
        * [1. Data Transfer](#1-data-transfer)
        * [2. Human Communication](#2-human-communication---sidney)
* [V. High-Level Solution](#v-high-level-solution)
    * [A. Hardware Block Diagram](#a-hardware-block-diagram)
    * [B. Operational Flow Chart](#b-operational-flow-chart)
* [VI. Atomic Subsystem Specifications](#vi-atomic-subsystem-specifications)
    * [A. Drone Subsystem](#a-drone-subsystem)
    * [B. Power & Circuitry Design Subsystem](#b-power--circuitry-design-subsystem)
    * [C. Signal Processing Subsystem](#c-signal-processing-subsystem)
    * [D. Interfacing Subsystem](#d-interfacing-subsystem)
    * [E. Human Detection Subsystem](#e-human-detection-subsystem---sidney)
    * [F. Vital Sensing Subsystem](#f-vital-sensing-subsystem)
    * [G. Human Communication Subsystem](#g-human-communication-subsystem---sidney)
* [VII. Ethical, Professional, and Standards Considerations](#vii-ethical-professional-and-standards-considerations)
* [VIII. Resources](#viii-resources)
    * [A. Budget](#a-budget)
    * [B. Division of Labor](#b-division-of-labor)
    * [C. Timeline](#c-timeline)
* [IX. References](#ix-references)
* [X. Statement of Contributions](#x-statement-of-contributions)

---

## I. Introduction
Emergency response efforts in hazardous environments often face a critical bottleneck in the rapid response of identifying and triaging casualties without risking additional human life. While aviation drones excel at visual reconnaissance, terrain mapping, and search and rescue surveillance, standard platforms are unable to evaluate physical trauma or autonomously assess casualties and victim priority. Drones with such capabilities would be vital tools in saving the valuable time and resources of responders, saving more lives in the process. While some drones do possess some of the capabilities required to autonomously categorize victims, they lack the ability to triage victims in the same conditions and at the same speed as a human. This obstacle has become a concern of the Defense Advanced Research Projects Agency (DARPA), who has formulated a challenge to address this problem.

In search and rescue operations, this drone system would enable rapid initial canvassing of disaster, relaying casualty locations and health metrics directly to ground and air medical teams to optimize aid and rescue. The following conceptual design will outline the background information, design constraints, system specifications, and technical framework of this project to meet this objective. Additionally, it will provide a comparative analysis of contemporary technologies and previous solutions to highlight how the proposed design most effectively addresses the problem.

---

## II. Background

### A. Defining Triage 
Triage is the process of rapidly assessing and prioritizing victims in emergency situations based on their physical condition and severity of injuries. The goal of triage is to direct immediate care to those who need it most, optimizing the amount of time and medical resources spent to maximize the number of lives saved.

### B. Benefits of a Triage Drone
Traditional ground-based triage approaches rely on human responders physically reaching each victim on foot. This process is inherently constrained by dangerous environments, available methods of travel, and finite personnel. Developing a semi-autonomous triage drone addresses several critical operational challenges:

* **Eliminating the "Golden Hour" Delay:** In severe trauma cases, victim survival heavily depends on the initial treatment window, often referred to as the "golden hour." Aerial platforms are perfect for this application since they can cross impassable terrain or infrastructure in shorter paths and in less time to begin physiological evaluation long before ground crews.
* **Data-Driven Decision Making:** High-stress disaster scenarios may cause human assessment to be subject to panic, environmental distraction, or cognitive overload. Drones equipped with automated sensing would deliver objective, standardized vital sign measurements directly to control stations, ensuring data and decision making is less dependent on human error.
* **Efficient Monitoring Without Resource Strain:** Standard triage protocol carries limitations on victim monitoring. A drone enables periodic re-examination of stationary victims to provide live updates, informing medical teams of critical changes in real time.
* **Separation of Search and Treatment:** A triage drone can transfer the initial detection and vital-sign screening tasks to a semi-autonomous system that does not necessarily require trained medical personnel for operation. This means that medical personnel can maintain focus on the treatment of high-priority victims whilst drone operation is placed upon individuals without extensive medical training.

### C. Sensors, Peripherals, and their Functional Roles
To execute non-contact assessment and remote navigation, the triage drone integrates a suite of specialized sensors and peripherals:

* **Single-Board Computer (SBC)**
    * **Function:** Serves as the onboard CPU responsible for controlling connected sensors and processing sensor data.
    * **Role:** Manages sensor filtering, local data processing, and coordinates the transmission of sensor data via the Communications Module. The SBC also orchestrates control of the Telescoping Arm.
* **Communications Module**
    * **Function:** Transmits operational data such as video feeds, two-way audio, and processed vital sign metrics gathered by the SBC back to the remote command center.
    * **Role:** The module will handle the bandwidth required to stream quality sensor and media data for remote triage.
* **Telescoping Arm**
    * **Function:** An extension mechanism designed in coordination with a mechanical engineering senior design team.
    * **Role:** Extends the physical reach of the drone's sensor payload to enhance the Radar Module's operational distance, overcome the drone's acoustic noise for the Acoustic Array, and provide enhanced video footage.
* **Radar Module**
    * **Function:** Operates as a non-contact vital sign monitor from a specified standoff distance.
    * **Role:** Serves as the primary physiological assessment tool, capable of obtaining vital signs through degraded visual conditions such as smoke, dust, or partial physical obstruction.
* **Acoustic Array**
    * **Function:** A filtered microphone and speaker array to converse with victims.
    * **Role:** Establishes two-way voice interaction between the victim and remote operator, allowing responders to gather verbal feedback such as name, reported pain, injury details, and victim responsiveness.
* **Optical Cameras**
    * **Function:** Captures live environmental video feeds.
    * **Role:** Provides visual feedback to remote human operators for manual navigation and targeting. Also serves as a secondary assessment tool to analyze the facial expressions and physical condition of a victim.
* **LiDAR Sensor**
    * **Function:** Emits pulsed lasers to gauge distances to surrounding surfaces and map terrain.
    * **Role:** Integrated into the drone and supports baseline distance measurement and spatial awareness, even in degraded conditions.
* **GPS Navigation Module**
    * **Function:** Receives satellite signals for positional tracking and stability.
    * **Role:** Integrated into the drone and provides basic geographic coordinate tracking during operator-guided flights to communicate victim location.

These sensors, including what specific models were selected and their precise functionality, will be expanded in later sections of this design. Note that future iterations of this design will likely include automated object detection (such as machine learning vision models) and fully autonomous path planning. These functions have been considered and are intentionally omitted from the current design scope and will be deferred to a future team.

### D. Previous Designs and Iterative Evolution
The current Triage Drone project builds upon three consecutive capstone design iterations that progressively evolved from an original DARPA challenge framework into an integrated flight platform:

1. **Foundational DARPA Challenge Sensing Prototype (Spring 2023 Team):** The earliest iteration strictly focused on tackling the DARPA Triage Challenge (DTC) by designing a standalone, non-contact vital sign and cognition testing system. Because of time and resource constraints, this team established and operated on a benchtop model that was modeled after a DJI Matrice 300 RTK weight budget of $2.7\text{ kg}$ (about $6\text{ pounds}$) to prove the viability of a Doppler radar for heart/respiratory rates and voice activity detection under the START triage model, leaving physical drone iterations for future groups [29].
2. **Initial Drone Adaptation & Baseline Architecture (Fall 2024 Team):** Building on the sensing concepts built by the previous team, the Fall 2024 team established preliminary specifications using the Parrot ANAFI Ai within a theoretical design scope. Like the previous group, their work centered on component studies and baseline processing rather than physical flight integration [30].
3. **Modular Refinement & Airframe Selection (Fall 2025 Team):** The subsequent iteration shifted the design focus toward a high-payload, open-source platform, specifically selecting and designing around the Aurelia X4 Standard airframe. While they established the architecture and conducted simulation for a radar module, acoustic array, LiDAR system, and payload weight limits, physical flight integration and testing remained uncompleted due to time and resource constraints [31].

The table below briefly compares the different subsystem approaches from each team:

| Design Aspect | Spring 2023 | Fall 2024 | Fall 2025 |
| :--- | :--- | :--- | :--- |
| **Airframe Status** | Theoretical weight budget (Matrice 300 RTK Model, 6 pounds, no drone) | Evaluated Parrot ANAFI Ai (Design only) | Selected Aurelia X4 Standard (Design and component sizing only) |
| **Computing** | Raspberry Pi | Raspberry Pi 4 Model B, NVIDIA Jetson Nano | NVIDIA Jetson Nano Single-Board Computer |
| **Sensing Suite** | 24 GHz Doppler radar, SparkFun MEMS microphones and general speakers | 24 GHz Doppler radar, SparkFun MEMS microphones and general speakers | Added mmWave radar (60-64 GHz) and a LiDAR module |
| **Mechanical Peripherals** | Benchtop housing only | Benchtop housing only | Benchtop housing only |
| **Project Scope Focus** | Direct response to DARPA Triage Challenge requirements | Proof-of-concept vital sign extraction and drone integration | Enhanced sensor calibration and drone integration via simulation |

The current team is now in possession of the Aurelia X4 Standard and will be integrating their solution around its design. 

---

## III. Fully Formulated Problem
Capstone Team 8 has been assigned the Triage drone project. The project's customer and advisor is Doctor W. Dale Blair of Georgia Tech, whose professional background includes radar systems, systems engineering and target tracking. Doctor Christopher "Storm" Johnson of Tennessee Tech serves as the faculty advisor and project manager. The team has been tasked with modifying and adapting the Aurelia X4 standard drone so that it can respond to disaster areas where human rescuers have limited access or would be placed at risk. The modified drone must locate victims, perform a preliminary non-contact assessment of their condition, and relay the information to a remote command center. All of this must be accomplished within the regulatory, technical, and ethical constraints described within this document.

### Objective and Scope
The objective of the project is to deliver a semi-autonomous triage drone built on the Aurelia X4 Standard platform that can:
* Navigate a predefined search area using GPS waypoints while avoiding obstacles with Lidar. 
* Detect and locate potential victims, including victims who are partially obscured.
* Measure heart rate and respiration rate without contact using radar. Classify predefined facial expressions using onboard cameras. 
* Provide two-way audio communication between a victim and the command center.
* Operate with/in moderate wind, low visibility, and moisture exposure. 
* Complete a minimum 15-minute mission on the shared flight battery. 
* Protect victim data from unauthorized access and avoid storing health information.

**In Scope:** Integration of The Jetson Nano, radar module, 3 IMX 219 cameras, re-speaker microphone array and speaker, mm wave radar, GPS, Wi-Fi adapter and PETG mounts onto the X4 onboard signal and image processing the data linked to the command center, Power Distribution and system level testing.

**Out of Scope:** Mechanical design and modeling of the extendable arm and the 3D printed mounting components which are the responsibility of the Mechanical Engineers senior design team. 

### Customer Objective
Dr. Blair's desired outcome is a drone that rapidly canvasses a disaster area and relays casualty locations and health metrics to medical teams, reducing the time and risk borne by human responders. The performance requirements below (S1–S7) define what that outcome means in measurable terms, and the customer guidance also governs design trade-offs such as the power consumption of the communication system. Because Dr. Blair's background is radar and target tracking [13], radar-based vital sensing and reliable victim localization are central to meeting his expectations.

### Performance Specifications
* **(S1)** The system SHALL detect and locate potential victims within a 6-foot radius.
    * *Measure of success:* The system shall correctly detect and locate a test subject in at least 80% of trials involving partial visual obstruction or other specified interference.
    * *Origin:* Customer requirement and project goal.
* **(S2)** The system SHALL attempt to measure the heart rate and respiration rate using selected sensors.
    * *Measure of success:* The system shall be compared against reference instruments, and the system shall meet an 80% accuracy tolerance for each sensor before testing.
    * *Origin:* Customer requirement and project goal (search and detection). Vital signs are the primary basis for prioritizing victims, and the requirement reflects the customer's radar expertise.
* **(S3)** The system SHALL attempt to identify predefined facial expressions when the victim's face is sufficiently visible.
    * *Measure of success:* The system shall correctly classify predefined expressions in at least 80% of labeled test cases under the specified lighting and visibility conditions.
    * *Origin:* Customer requirement and project goal. Facial expression supplements vital signs as an indicator of the victim's visual condition and awareness.
* **(S4)** The system SHALL support two-way audio communication between the victim and the remote command center.
    * *Measure of success:* The system shall successfully transmit and receive at least 80% of predefined test messages under specified operating conditions.
    * *Origin:* Customer Requirement and project goal. Audio allows responders to check a victim's awareness, identity and reported injuries.
* **(S5)** The system SHALL maintain its required functions under specified environmental conditions.
    * *Measure of success:* The system shall complete a controlled test under a defined wind speed and visibility level, remain functional, and pass a defined moisture-exposure test.
    * *Origin:* Project goal and environmental challenges identified in the proposal. Disaster areas involve smoke, wind, rain, and low visibility potentials.
* **(S6)** The drone SHALL supply sufficient power to the system without exceeding limits.
    * *Measure of success:* The fully equipped system shall complete a test flight lasting at least the minimum mission duration of 15 minutes with sufficient battery reserve to land safely.
    * *Origin:* Customer requirement and flight duration/battery challenge. All added components draw from the same battery that powers the motors, so every added load shortens flight time. Potential idea of external battery to be discussed.
* **(S7)** The system SHALL restrict access to victims’ information and health data to unauthorized users.
    * *Measure of success:* Testing shall verify that unauthorized users cannot access protected data.
    * *Origin:* Ethical concern and broader implication concern. Recorded data about victims is sensitive and must be kept private.

### Constraints
* **(C1)** The drone SHALL remain under $400\text{ ft}$ above ground level.
    * *Origin:* Federal regulation (FAA 14 CFR part 107). Keeps drone separated from manned aircraft.
* **(C2)** The drone SHALL not exceed $100\text{ mph}$.
    * *Origin:* Federal Regulation (FAA, 14 CFR Part 107).
* **(C3)** The drone SHALL be equipped with anti-collision lighting.
    * *Origin:* Federal Regulation (Part 107). Lighting is required for night operations.
* **(C4)** The drone SHALL weigh under $55\text{ lbs}$.
    * *Origin:* Federal Regulation (FAA Part 107 Small unmanned aircraft Limit). In practice, the binding limit is the X4's $3.3\text{ lb}$ payload capacity, which is far stricter.
* **(C5)** The drone SHALL utilize encrypted wireless communication conforming to IEEE 802.11 standards for control and data transmission.
    * *Origin:* Industry standard (IEEE 802.11) and ethical concern. Encryption protects victim data in transit and supports S7.
* **(C6)** The EMI test setup SHALL maintain all measurement tolerances within the limits specified by MIL-STD-461G § 4.3.
    * *Origin:* Military standard (MIL-STD-461G). Addresses frequency interference challenge: motor and converter noise can corrupt radar and audio signals.
* **(C7)** The system SHALL operate at an autonomy level functionally equivalent to SAE J3016 Level 3, where the drone can perform mission tasks under limited conditions while maintaining continuous human oversight.
    * *Origin:* Industry standard (SAE J3016) adapted from on-road vehicles combined with the semi-autonomous flight goal and ethical requirement to keep a human in loop.
* **(C8)** The drone SHALL not store health information or associate such data with any individuals.
    * *Origin:* Legal and ethical concern, HIPAA, privacy, and broader implication concern. Not storing data also makes it harder to repurpose the system for surveillance.

---

## IV. Comparative Analysis of Potential Solutions
In this section, various potential solutions are hypothesized, design considerations are discussed, and factors influencing the selection of a solution are outlined. The chosen solution is then identified with justifications for its selection. 

### A. Control Systems
While designing the control system, the team decided between using the default transmitter, a mobile device, and a PC system. The control system will be used to communicate between the drone and command center as well as transmitting data gathered from our sensors. 

#### Default Transmitter – Radiomaster TX16S
This 16-channel transmitter is included with the Aurelia X4 standard drone; therefore, it is a low-cost solution. This transmitter can be programmed from a PC using OpenTX Companion and is best suited for control over flight. There are 2 UART ports included that can be used for GPS, Bluetooth, and other serial devices, allowing live GPS updates from the drone as well as supporting Bluetooth connections for the Jetson Nano. 
* **Pros:** Easy to use, cost-friendly, best option for in-flight control.
* **Cons:** Does not support camera and microphone feeds.

#### Mobile Device
Handheld device used to program flight paths, set waypoints, and view live telemetry. Is not suitable for flying the drone (this has to be done through the transmitter).  
* **Pros:** Compact, easily transportable.
* **Cons:** Program to change drone settings is not intended for mobile devices; analyzing sensor data is not ideal through a mobile device.

#### PC System
Personal laptop to program flight controls, view live telemetry, and set waypoints. All collected data can be wirelessly transmitted to the laptop and processed. 
* **Pros:** Easy to program, software designed for PC interface, cost-friendly.
* **Cons:** Not compact, implementation may be more complicated.

#### Control System Solution
The ideal solution is a combination of the PC and transmitter system. The PC will be used to determine flight path, radio settings, and analyze sensor data. The transmitter will only be used for flying the drone and will not receive or transmit any data from aftermarket components.

### B. Radar Systems 
The Radar systems usable for heart rate monitoring are very limited. The options for types of radar signals are pulse, pulse doppler, Continuous Wave (CW) doppler, and frequency-modulated continuous wave (FMCW). For measuring heart rate and respiratory signals, CW waveforms are the best option for reliable data. 

#### Infineon Demo BGT60UTR11AIP radar sensor
The Infineon Demo BGT60UTR11AIP radar sensor is a $60\text{ GHz}$ Frequency Modulated Continuous Wave (FMCW) radar; however, it also possesses the capability to operate in Continuous Wave (CW) mode. The sensor is attached to an Infineon Radar Baseboard MCU7 Plus which is roughly 3 inches by 1 inch and weighs less than a gram. It can be operated via board pins or micro-USB. Infineon provides an extensive SDK and GUI.
* **Pros:** Uses $60\text{ GHz}$ Continuous Waves for reliable readings; capable of both FMCW and CW doppler waveforms.
* **Cons:** Limited on range and resolution.

#### Texas Instruments AWR1843 radar sensor
The Texas Instruments AWR1843 radar is an integrated single-chip FMCW radar sensor capable of operation in the $76\text{ to }81\text{ GHz}$ band. It is built on TI’s low-power 45nm RFCMOS process, enabling a monolithic implementation of a 3TX, 4RX system with built-in PLL and ADC converters. Includes a BIST processor subsystem for radio configuration, control, and calibration.
* **Pros:** Higher frequency range of FMCW waveforms that penetrate skin less and relay more information; built-in processing creates a cleaner signal.
* **Cons:** Costliest option; requires more power than other options.

#### Radar System Solution 
The best option is the Infineon Demo BGT60UTR11AIP radar sensor because of its lower power consumption, smaller form factor, and affordability. The $60\text{ GHz}$ range of the radar makes it fully viable for its purpose.

### C. Human Locating Systems
The location system helps visually locate the victim and establish contact. Candidates include the Yahboom IMX219 camera, Waveshare IMX219-83 Stereo Camera, and Arducam IMX477 HQ Camera.

#### Yahboom IMX219 Camera (Default)
The NVIDIA Jetson IMX219 camera measures $24\text{ mm} \times 25\text{ mm}$. It features a $160^\circ$ field of view, 8MP resolution, Sony IMX219 chip, and CSI interface for real-time image recognition.
* **Pros:** Compatible with Jetson Nano, $160^\circ$ field of view, 1080p resolution with 8MP, supports real-time human detection, connects directly via ribbon cable.
* **Cons:** Processing delays possible due to limited resources; wide-angle distortion can reduce detection.

#### Waveshare IMX219-83 Stereo Camera
Uses a dual-camera system to estimate depth and width. Each camera has a $3280 \times 2464$ resolution (8MP). Features $<1\%$ lens distortion, a $73^\circ$ field of view, and a $60\text{ mm}$ stereo baseline. Compatible with Jetson Nano B01.
* **Pros:** Compatible with Jetson Nano, dual cameras estimate distance accurately, built-in motion sensing, $<1\%$ distortion, dual Sony IMX219 chips.
* **Cons:** Environmental conditions affect depth accuracy; requires more image processing; smaller FOV ($73^\circ$).

#### Arducam IMX477 HQ Camera
Compatible with Jetson Nano, supporting interchangeable lenses with a $65^\circ$ FOV and 12.3MP resolution. Improves image detail for identifying individuals.
* **Pros:** Compatible with Jetson Nano, high resolution, improves visual tracking/human detection, interchangeable lenses.
* **Cons:** Does not measure distance; narrow horizontal FOV ($65^\circ$ standard); additional lenses needed for wide FOV; high resolution increases processing demand.

#### Human Locating System Solution
The chosen sensor for human locating is the Yahboom IMX219 $160^\circ$ camera. It lacks depth perception but offers broader scene coverage and lower processing demands, minimizing lag.

### D. Communication Systems
Two communication systems are implemented: data transfer between the Jetson Nano and PC laptop, and human communication (speaker/microphone with victim).

#### 1. Data Transfer 
To transmit data from the Jetson Nano to a personal laptop, options across Wi-Fi/Bluetooth, cellular, ethernet, and LoRa were evaluated:

* **EDIMAX N150:**
    * Supports Wi-Fi/Bluetooth on Jetson Nano at speeds up to 150Mbps. Range: 10–30 meters. Transmits radar, camera, and microphone data. Built-in network security.
    * *Pros:* Jetson Nano compatible, no bulky attachments, lightweight.
    * *Cons:* Short range.
* **Intel AC8265 Wireless NIC:**
    * Supports Wi-Fi/Bluetooth on Jetson Nano at 300Mbps (2.3GHz). Range: 30–50 meters. Transmits radar, video, and audio with integrated network security.
    * *Pros:* Jetson Nano compatible, lightweight.
    * *Cons:* Short range.
* **GNSS Expansion Board Module:**
    * Supports 4G cellular communication up to 5000 meters. Transmits video, audio, and radar data over long distances.
    * *Pros:* Long range.
    * *Cons:* Difficult to integrate, heavier payload impact.
* **LoRa (Long Range Radio):**
    * Supports long-range radio communication for image clusters up to 300 meters. Lowest cost long-range option. Video is greyscale/image-based.
    * *Pros:* Long range, low cost, lightweight.
    * *Cons:* Lower quality video, susceptible to external noise interference.

##### Data Transfer System Solution
The primary solution is the Intel AC8265 Wireless NIC Wi-Fi adapter for high-quality real-time feeds. In rural environments, LoRa will be equipped as a backup to transmit low-quality image clusters and telemetry.

#### 2. Human Communication
Five hardware options were evaluated (3 microphones, 2 speakers):

* **ReSpeaker 4-Mic Array (UAC 1.0 - Default):** Low-power USB microphone array with embedded audio processing, voice capture, sound direction detection, and noise suppression.
    * *Pros:* 4 mics for directional capture, USB connection, noise suppression, low power.
    * *Cons:* Filtering may not fully eliminate drone rotor noise; requires external speaker for 2-way comms.
* **ReSpeaker USB 4-Mic Array XVF3800:** Updated array featuring $360^\circ$ voice pickup up to $5\text{ m}$, echo cancellation, and noise suppression.
    * *Pros:* $360^\circ$ sound pickup, source localization, echo cancellation.
    * *Cons:* Expensive, does not completely eliminate drone noise, potential Jetson driver/feature limitations.
* **RØDE VideoMic Go II:** Lightweight directional microphone with USB-C/3.5mm outputs.
    * *Pros:* Highly directional pickup pattern, lightweight, includes windshield.
    * *Cons:* Expensive, proximity to drone still picks up rotor noise, must be aimed directly at victim.
* **2831/3128 Mini Full-Range Cavity Speaker:** Compact output speaker for tight spaces.
    * *Pros:* Compact, lightweight, low power, ideal for voice instructions.
    * *Cons:* May require an external amplifier to overcome drone noise.
* **Yahboom USB Sound Card & Speaker:** Designed for Raspberry Pi/Jetson series boards.
    * *Pros:* Native Jetson compatibility, budget-friendly, all-in-one setup.
    * *Cons:* Less field-tested, dual-system design adds weight.

##### Human Communication System Solution
The ReSpeaker 4-Mic Array was selected for its minimal processing impact on the Jetson Nano. Custom notch filtering will be implemented in software to handle rotor noise. The Mini Full-Range Cavity Speaker was chosen as the output unit due to higher reliability and lower weight; dual speakers can be deployed if amplification is required.

---

## V. High-Level Solution
The Triage Drone integrates a sensing and processing payload onto the Aurelia X4 standard. The X4 Pixhawk flight controller running ArduPilot handles stabilized and semi-autonomous flights. A Jetson Nano serves as the onboard computer controlling the sensors, camera, microphone, and speaker. It runs victim detection and vital sign processing on board so that only live results rather than raw recordings are sent to the command center.

| Subsystem | Selected Solutions | Purpose | Requirements Addressed |
| :--- | :--- | :--- | :--- |
| **Drone Platform** | Aurelia X4 Standard with Pixhawk flight controller and ArduPilot | Carries and powers payload, provides stabilized flight, GPS navigation, and return-to-home. | S5, S6, C1–C4, C7 |
| **Pathfinding & Obstacle Detection** | GPS waypoint navigation via ArduPilot; LiDAR obstacle avoidance | Semi-autonomous flight through predefined search areas, including low visibility. | S5, C7 |
| **Human Detection** | Two IMX219 cameras on Jetson Nano cross-checked with radar | Detects and locates victims | S1, S3 |
| **Vital Sensing** | Infineon BGT60UTR11AIP $60\text{ GHz}$ radar | Non-contact heart and respiration rate tracking in $0.1\text{--}3\text{ Hz}$ band | S2 |
| **Signal Processing & Inferencing** | Onboard processing via Jetson Nano | Filters radar/audio/image data and packages results for transmission | S1–S4, S7 |
| **Human Communication** | ReSpeaker 4-Mic Array v2.0 + Cavity Speaker ($80\text{--}225\text{ Hz}$ filtered) | Two-way audio between victim and command center | S4 |
| **Data Transfer** | Encrypted IEEE 802.11 Wi-Fi link (Intel AC8265) / Backup LoRa | Carries live video, audio, vitals, and GPS to command center | S4, S7, C5 |
| **Control Systems** | Command center PC + Radiomaster TX16S Transmitter | Operator interface for monitoring, flight control, verification, and intervention | C7, S7 |
| **Power & Circuitry** | Shared flight battery or external payload battery with regulated supply | Powers payload electronics without compromising flight duration or signal quality | S6, C6 |
| **Mounts & Arm** | PETG 3D-printed mounts and extendable arm (ME Team) | Holds payload, damps vibration, resists moisture/UV | S1, S2, S5 |

### Maximizing Stakeholder Goal Attainment 
Each customer objective maps directly to a subsystem. Radar-based vital sensing reflects Dr. Blair's expertise in non-contact measurements. Combining camera YOLO detection with radar verification improves detection confidence during visual degradation [16]. Two-way audio allows responders to assess victim consciousness. Onboard processing ensures the command center receives real-time metrics without network latency.

### Adherence to Constraints 
The design stays within FAA Part 107 limits for altitude, speed, weight, and lighting [12][14]. The $3.3\text{ lb}$ payload limit of the X4 is tracked via a strict mass budget. Data transmission utilizes encrypted IEEE 802.11 [18]. System EMI is verified under MIL-STD-461G [19]. Autonomy is capped at SAE J3016 Level 3 equivalence for continuous human oversight [20]. Data is streamed live without onboard persistence, satisfying C8.

### Risk Minimization 
| Risk | Mitigation in Design |
| :--- | :--- |
| **Payload exceeds 3.3 lb limit** | Strict mass budget maintained for every component, mount, wire, and fastener. |
| **Flight time below 15 mins** | Component power budget enforced; Jetson power modes optimized; hover energy budgeted. |
| **Jetson resets during motor current spikes** | Regulated buck supply sized to ride through takeoff/gust transients. |
| **Motor noise corrupts radar/audio** | Shielded power wiring, software FIR notch filtering, and MIL-STD-461G testing. |
| **Camera degraded by smoke/fog** | Radar and LiDAR provide non-visual detection and obstacle avoidance [17]. |
| **Lost link or low battery** | Automatic Return-to-Home (RTH) triggered with safe battery reserve. |
| **False "no vital signs" reading** | Readings displayed with confidence levels; operator verification mandatory. |
| **Unauthorized data access** | Encrypted link, command PC access control, and zero local data storage. |

### Resource Utilization 
Major hardware assets (Aurelia X4, Jetson Nano, ReSpeaker array, LiDAR, GPS) are already owned by the team. The projected purchase cost is $54 for two additional IMX219 cameras and PETG filament. The design builds upon prior capstone iterations [8][9] using COTS modular components for cheap and fast replacement.

---

### A. Hardware Block Diagram
*(Hardware block diagrams created in Canva center on the drone and computer subsystems, outlining primary communications, power paths, and digital conversion loops.)*

### B. Operational Flow Chart
*(High-level flowchart depicting pre-flight initialization, GPS navigation, target acquisition, vital reading execution, data transmission, and return-to-home protocols.)*

---

## VI. Atomic Subsystem Specifications

### A. Drone Subsystem
* **Overview:** Housing, transport, and flight stability for all sensors and computing payloads. Consists of the Aurelia X4 Standard multi-rotor platform with a Pixhawk flight controller running ArduPilot.
* **Operation:** Pre-flight checks verify GPS, battery, and rotor health. Executes semi-autonomous navigation via GPS waypoints to hover over target areas, holding the payload stably while maintaining operational limits.
* **Interfacing:**
    * *Flight Controller $\leftrightarrow$ Control System:* MAVLink / Internal Bus (Bidirectional)
    * *Radio Telemetry $\leftrightarrow$ Interfacing:* Proprietary RF (Bidirectional)
    * *Power Distribution $\leftrightarrow$ Power & Circuitry:* Battery Bus (Input)
* **Specifications:**
    1. The drone SHALL remain under $400\text{ ft}$ AGL per 14 CFR §107.51.
    2. The drone SHALL not exceed $87\text{ knots}$ ($100\text{ mph}$) ground speed per 14 CFR §107.51.
    3. The drone SHALL be equipped with anti-collision lighting visible for $3\text{ statute miles}$ for night operations per 14 CFR §107.29.
    4. The drone SHALL weigh under $55\text{ lbs}$ at takeoff per 14 CFR §107.3.
    5. The drone SHALL remain within visual line of sight per 14 CFR §107.31.
    6. The drone SHALL comply with Remote ID requirements per 14 CFR Part 89.
    7. The drone SHALL meet Part 107 Subpart D requirements for operations over people (propeller guards/ducted fans).
    8. Controlled flight testing SHALL obtain FAA airspace authorization per 14 CFR §107.41.
    9. UAS critical components SHALL not be on the FCC Covered List [27].
    10. The fully equipped system SHALL achieve $\ge 15\text{ minutes}$ flight duration with safe landing reserve.
* **Applicable Standards:** FAA Part 107, Remote ID Part 89, ANSI/UL 3030.

---

### B. Power & Circuitry Design Subsystem
* **Overview:** Supplies regulated power to payload components. Evaluating Configuration A (Shared Flight Battery via TI TPS56637 buck converter) vs Configuration B (Dedicated Payload Battery).
* **Interfacing:**
    * *Power Output $\rightarrow$ Drone / SBC / Sensor Suite / Arm:* DC Power Bus
* **Specifications:**
    1. The power subsystem SHALL include low-battery triggers and protocols.
    2. Onboard electronics SHALL meet unintentional radiator limits of 47 CFR Part 15 Subpart B.
    3. The EMI setup SHALL conform to MIL-STD-461G § 4.3.1 limits.
    4. Lithium batteries SHALL comply with IEC 62133-2 / UL 2054 and UN 38.3.
    5. Electrical architecture SHALL follow ANSI/UL 3030 standards.
    6. Moisture protection SHALL be rated and tested per IEC 60529.
    7. System components SHALL not violate FCC Covered List mandates.
    8. The system SHALL support at least $15\text{ minutes}$ of operational payload power.
    9. System power draws SHALL respect Aurelia X4 payload limits.
* **Applicable Standards:** ANSI/UL 3030, IEC 62133-2, UL 2054, MIL-STD-461G, IEC 60529, FCC Part 15.

---

### C. Signal Processing Subsystem
* **Overview:** Internal digital signal processing pipeline on the Jetson Nano to extract heart rate, respiration, and filtered audio from raw sensor streams.
* **Operation:** Applies an FIR low-pass filter ($< 5\text{ Hz}$) to radar data, downsamples to $10\text{--}20\text{ Hz}$, then uses FIR band-pass filters ($0.8\text{--}3.0\text{ Hz}$ for heart rate; $0.13\text{--}1.0\text{ Hz}$ for respiration). Applies FFT-based notch filtering to acoustic data to attenuate propeller frequencies.
* **Interfacing:**
    * *Radar $\rightarrow$ SBC:* USB (Input)
    * *Microphone $\rightarrow$ SBC:* I2S/USB (Input)
    * *Speaker $\leftarrow$ SBC:* I2S/USB (Output)
    * *Camera $\rightarrow$ SBC:* MIPI CSI-2 (Input)
* **Specifications:**
    1. DSP SHALL extract respiration rates ($0.13\text{--}1.0\text{ Hz}$) and heart rates ($0.8\text{--}3.0\text{ Hz}$).
    2. Vitals SHALL be extracted from a standoff distance of at least $1\text{ meter}$.
    3. DSP updates SHALL process within $\le 500\text{ ms}$ per cycle.
    4. The subsystem SHALL operate on sampling rates between $100\text{--}200\text{ Hz}$.
    5. All signal processing SHALL be computed locally onboard.
* **Applicable Standards:** HIPAA (data privacy & zero persistence).

---

### D. Interfacing Subsystem
* **Overview:** Routes sensor feeds through the Jetson Nano to the ground command PC via wireless communication.
* **Interfacing:**
    * *SBC $\leftrightarrow$ Wireless Transceiver:* NGFF M.2 / USB
    * *Wireless Link $\leftrightarrow$ Ground PC:* IEEE 802.11ac Wi-Fi / LoRa
* **Specifications:**
    1. SHALL display signal processing output live on ground control hardware.
    2. SHALL utilize onboard Wi-Fi / LoRa links for data transport.
    3. SHALL run ground control software interface for operator monitoring.
* **Applicable Standards:** IEEE 802.11ac ($5\text{ GHz}$ operational band).

---

### E. Human Detection Subsystem
* **Overview:** Uses Yahboom IMX219 $160^\circ$ camera feeds and image processing to identify human presence and classify facial expressions.
* **Specifications:**
    1. The system SHALL detect human forms.
    2. The system SHALL classify basic facial expressions.
    3. Camera operation SHALL remain clear under environmental test limits.
    4. Continuous visual feed access SHALL be provided during flight.
    5. Mass and power SHALL conform to system budgets.
* **Applicable Standards:** HIPAA, IEEE 802.11, FAA Part 107, NSPE/IEEE Ethics.

---

### F. Vital Sensing Subsystem
* **Overview:** Non-contact extraction of physiological signals using a $60\text{ GHz}$ Continuous Wave (CW) Doppler radar.
* **Specifications:**
    1. Standoff range SHALL be $\ge 1\text{ meter}$.
    2. RF exposure SHALL pose no biological threat to subjects.
    3. Heartbeat frequency tracking range SHALL cover $0.45\text{--}3.33\text{ Hz}$ ($27\text{--}200\text{ BPM}$).
    4. Respiration rate tracking range SHALL cover $0.1\text{--}1.0\text{ Hz}$ ($6\text{--}60\text{ RPM}$).
* **Applicable Standards:** FDA Cardiac Monitor Guidance, ANSI/AAMI EC13, IEEE C95.1 (EMF Exposure), FCC Part 15.255.

---

### G. Human Communication Subsystem
* **Overview:** Enables two-way voice interaction between victim and operator using a ReSpeaker 4-Mic Array and Cavity Speaker.
* **Specifications:**
    1. System SHALL establish full two-way voice communication.
    2. Audio quality SHALL undergo noise distortion testing during active flight.
    3. Audio capture and broadcast feeds SHALL link reliably to the command center.
* **Applicable Standards:** FAA Part 107, IEEE 802.11, HIPAA, NSPE Code of Ethics.

---

## VII. Ethical, Professional, and Standards Considerations

### Public Safety
Flight safety risks are managed via built-in Return-to-Home (RTH) protocols on low battery or signal loss (Power Spec 9), PETG physical enclosures for crash protection (S5), documented environmental limits, and short-circuit/overheat electrical protection.

### Public Health and Privacy
To address surveillance and privacy concerns under HIPAA:
* Onboard real-time processing streams metrics live; **no raw video or vital data is saved to storage** (C8).
* Transmissions are encrypted over IEEE 802.11 links (C5, S7).
* Victim identifiers are strictly separated from telemetry data.

### Society, Culture, and Trust
To mitigate false positive/negative risks in triage (target accuracy $\approx 80\%$), autonomy is locked to **SAE J3016 Level 3**, keeping a human operator in the loop at all times. The system acts as a decision-support tool rather than an autonomous medical judge.

### Environment & Economy
LiPo batteries will be charged, discharged, and recycled per UN 38.3 standards. Commercial off-the-shelf (COTS) components and modular mounting reduce repair e-waste and maintain a total purchase budget under $330.

### Summary Standards Matrix
| Standard / Regulation | Requirement Summary | Design Response |
| :--- | :--- | :--- |
| **FAA 14 CFR Part 107** | $<400\text{ ft}$ AGL, $<100\text{ mph}$, $<55\text{ lbs}$, anti-collision lights | Constraints C1–C4 enforced |
| **IEEE 802.11** | Encrypted wireless LAN transmission | Encrypted Wi-Fi data link (C5) |
| **MIL-STD-461G § 4.3** | Electromagnetic interference limits | Shielded power routing (C6) |
| **SAE J3016 Level 3** | Driving/flight automation taxonomies | Human-in-the-loop oversight (C7) |
| **HHS / HIPAA** | Health data privacy protection | Zero local data storage (C8) |
| **IEEE C95.1 / FCC Part 15** | Human RF exposure & bandwidth compliance | Low-power $60\text{ GHz}$ radar limits |

---

## VIII. Resources

### A. Budget

#### Radar & Data Communication Subsystem
| Item | Cost | Quantity | Subtotal |
| :--- | :--- | :--- | :--- |
| 433MHz SX1278 LoRa Module | $4.47 | 3 | $13.41 |
| Intel AC8265 Wireless NIC | $26.87 | 2 | $53.74 |
| Infineon Demo BGT60UTR11AIP | $156.86 | 1 | $156.86 |
| **Subtotal** | | | **$224.01** |

#### Human Communication & Vision Subsystem
| Item | Cost | Quantity | Subtotal |
| :--- | :--- | :--- | :--- |
| Yahboom IMX219 Camera | $26.99 | 2 | $53.98 |
| **Subtotal** | | | **$53.98** |

#### Power Subsystem
| Item | Cost | Quantity | Subtotal |
| :--- | :--- | :--- | :--- |
| 5V External Power Supply | $37.99 | 1 | $37.99 |
| AA Batteries (20 pack) | $9.99 | 1 | $9.99 |
| **Subtotal** | | | **$47.98** |

#### Complete Project Budget
| Total Estimated Cost | $325.97 |
| :--- | :--- |

---

### B. Division of Labor
* **Allison Wolden:** Wireless communication systems, data transfer interfaces, budget management, embedded coding (C/C++), system testing.
* **Ryan Lee:** Power distribution, circuitry design subsystem, hardware block diagrams, microcomputer/SBC integration.
* **Brandon Price:** Power management budgets, regulatory standards, problem formulation, risk/ethical considerations.
* **Weston LaRue:** Vital sensing algorithms, digital signal processing (FIR/FFT filtering), mmWave radar configuration.
* **Sidney Delgado:** Human detection vision models, two-way audio integration, camera/microphone hardware selection.

---

### C. Timeline
*(Gantt chart and task tracking schedule spanning Capstone I conceptual design through Capstone II flight integration and field testing.)*

---

## IX. References
1. Aurelia Aerospace, *Aurelia X4 User Manual*, Rev. 5, 2026.
2. Infineon Technologies, "BGT60UTR11AIP 60 GHz Radar Sensor Product Page."
3. Infineon Technologies, *BGT60UTR11AIP Datasheet*.
4. Infineon Developer Community, *FAQs for XENSIV BGT60UTR11AIP Radar Sensor*, 2026.
5. Seeed Studio, *reComputer J1020 v2 (Jetson Nano) Product Specification*.
6. NVIDIA, *Jetson Nano Power Modes Configuration Guide*.
7. Texas Instruments, *TPS56637 Synchronous Buck Converter Datasheet*.
8. Fall 2025 Capstone Team 8, *Project Documentation & Engineering Reports*.
9. Fall 2024 Capstone Team 5, *Project Repository & Parts List*.
10. Dr. W. Dale Blair, Customer Consultation Notes, Sept. 16, 2026.
11. *Power and Payload Design Specifications*, Aurelia X4 Triage Drone, Fall 2026.
12. Federal Aviation Administration, *Small Unmanned Aircraft Systems (sUAS) Regulations*.
13. IEEE AESS, "W. Dale Blair Professional Profile," 2026.
14. Electronic Code of Federal Regulations, *14 CFR §107.51 Operating Limitations for Small Unmanned Aircraft*.
15. MatterHackers, "The Best 3D Printing Filament for Outdoor Use," 2026.
16. F. Ciccone and A. Ceruti, "Real-Time Search and Rescue with Drones: A Deep Learning Approach for Small-Object Detection Based on YOLO," *Drones*, vol. 9, no. 8, p. 514, 2025.
17. P. Tang, J. Li, and H. Sun, "A Review of Electric UAV Visual Detection and Navigation Technologies for Emergency Rescue Missions," *Sustainability*, vol. 16, no. 5, p. 2105, 2024.
18. IEEE, *IEEE Standard for Information Technology—IEEE Std 802.11ax-2021*.
19. U.S. Department of Defense, *MIL-STD-461G: Requirements for the Control of Electromagnetic Interference Characteristics of Subsystems and Equipment*, 2015.
20. SAE International, *J3016: Taxonomy and Definitions for Terms Related to Driving Automation Systems*, 2021.
21. C. Bradley and A. Chiou, *Examining the Ethical Considerations of Humanitarian Drones*, 2024.
22. R. Hoek Spaans et al., "Ethical considerations related to drone use for environment and health research," *PLOS ONE*, 2024.
23. R. Hoek Spaans et al., "Ethical considerations related to drone use for environment and health research: a scoping review," *Royal Society Open Science*, 2026.
24. National Society of Professional Engineers, *NSPE Code of Ethics for Engineers*.
25. IEEE, *IEEE Code of Ethics*, Section 7.8.
26. *Health Insurance Portability and Accountability Act of 1996 (HIPAA)*, Pub. L. 104-191.
27. Federal Communications Commission, *FCC Covered List Requirements*.
28. G. Paterniani et al., "Radar-based monitoring of vital signs: A tutorial overview," *Proc. IEEE*, vol. 111, no. 3, pp. 277–317, 2023.
29. M. West et al., *Conceptual Design and Planning for Drone Triage Project*, Spring 2023.
30. C. Bucher et al., *Conceptual Design Final Report*, Fall 2024.
31. K. Dyess et al., *Conceptual Design Report*, Fall 2025.
32. U.S. FDA, *Cardiac Monitor Guidance (including Cardiotachometer and Rate Alarm)*, Doc. No. 2233, 1998.
33. ANSI/AAMI EC13:2002/(R)2007, *Cardiac Monitors, Heart Rate Meters, and Alarms*.
34. IEEE, *IEEE Std C95.1-2019: Safety Levels with Respect to Human Exposure to Electric, Magnetic, and Electromagnetic Fields*.
35. Federal Communications Commission, *FCC Report and Order 23-35 (57-71 GHz Radar Band)*, 2023.
36. G. Vinci et al., "Six-Port Radar Sensor for Remote Respiration Rate and Heartbeat Vital-Sign Monitoring," *IEEE TMTT*, vol. 61, no. 5, pp. 2093–2100, 2013.
37. M. Alizadeh et al., "Remote Monitoring of Human Vital Signs Using mm-Wave FMCW Radar," *IEEE Access*, vol. 7, pp. 54958–54968, 2019.
38. International Electrotechnical Commission, *IEC 60529: Degrees of Protection Provided by Enclosures (IP Code)*.
39. FCC, *Secure Networks Act Covered Equipment List*, 2021.
40. United Nations, *Manual of Tests and Criteria*, Part III, Section 38.3 (Lithium Batteries).

---

## X. Statement of Contributions
* **Introduction:** Ryan Lee
* **Background:** Ryan Lee
* **Fully Formulated Problem:** Brandon Price
* **Comparative Analysis of Potential Solutions:**
    * **Control Systems:** Allison Wolden
    * **Radar Systems:** Weston LaRue
    * **Human Locating Systems:** Sidney Delgado
    * **Communication System (Data Transfer):** Allison Wolden
    * **Communication System (Human Communication):** Sidney Delgado
* **High-Level Solution:** Brandon Price
* **Hardware Block Diagram:** Ryan Lee
* **Operational Flow Chart:** Brandon Price
* **Atomic Subsystem Specifications:**
    * **Drone Subsystem:** Ryan Lee
    * **Power & Circuitry Design Subsystem:** Brandon Price, Ryan Lee
    * **Signal Processing Subsystem:** Weston LaRue
    * **Interfacing Subsystem:** Allison Wolden
    * **Human Detection Subsystem:** Sidney Delgado
    * **Vital Sensing Subsystem:** Weston LaRue
    * **Human Communication Subsystem:** Sidney Delgado, Ryan Lee
* **Ethical, Professional, and Standards Considerations:** Brandon Price
* **Resources:**
    * **Budget:** Allison Wolden
    * **Division of Labor:** Allison Wolden
    * **Timeline:** Weston LaRue
* **Editing:** Allison Wolden, Ryan Lee