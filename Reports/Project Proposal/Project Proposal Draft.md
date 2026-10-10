# Project Proposal
## Capstone I – Team 8: Triage Drone

**Team Members:**
* Ryan Lee
* Allison Wolden
* Weston LaRue
* Brandon Price
* Sidney Delgado

---

## Table of Contents
* [I. Introduction](#i-introduction)
* [II. Challenges and Obstacles](#ii-challenges-and-obstacles)
* [III. Goals](#iii-goals)
* [IV. Specifications & Measures of Success](#iv-specifications--measures-of-success)
* [V. Constraints](#v-constraints)
* [VI. Survey of Existing Solutions & Relevant Literature](#vi-survey-of-existing-solutions--relevant-literature)
  * [A. Radar - Weston LaRue](#a-radar)
  * [B. Image Processing – Sidney Delgado](#b-image-processing)
  * [C. Deep Learning for Object Detection - Ryan Lee](#c-deep-learning-for-object-detection)
  * [D. UAV Path Planning – Ryan Lee](#d-uav-path-planning)
  * [E. Power & Payload - Brandon Price](#e-power--payload)
  * [F. Communications – Allison Wolden](#f-communications)
* [VII. Timeline & Budget](#vii-timeline--budget)
* [VIII. Personnel](#viii-personnel)
* [IX. Broader Implications, Ethics, and Responsibility as Engineers](#ix-broader-implications-ethics-and-responsibility-as-engineers)
* [X. References](#x-references)
* [XI. Statement of Contributions](#xi-statement-of-contributions)

---

## I. Introduction
Emergency response efforts in hazardous environments often face a critical bottleneck in the rapid response of identifying and triaging casualties without risking additional human life. While aviation drones excel at visual reconnaissance, terrain mapping, and search and rescue surveillance, standard platforms are unable to evaluate physical trauma or autonomously assess casualties and victim priority. Drones with such capabilities would be vital tools in saving the valuable time and resources of responders, saving more lives in the process. While some drones do possess some of the capabilities required to autonomously categorize victims, they lack the ability to triage victims in the same conditions and at the same speed as a human. This obstacle has become a concern of the Defense Advanced Research Projects Agency (DARPA), who has formulated a challenge to address this problem.

In search and rescue operations, this drone system would enable rapid initial canvassing of disaster, relaying casualty locations and health metrics directly to ground and air medical teams to optimize aid and rescue. The following proposal will outline the design constraints, system specifications, and technical framework of this project to meet this objective. Additionally, it will provide a comparative analysis of contemporary technologies and highlight how the proposed design most effectively addresses the problem.

---

## II. Challenges and Obstacles
* **Weight:** Adding necessary peripherals, such as the sensors and arm.
* **Flight Duration & Battery:** Ensuring the added power loads do not excessively reduce flight time.
* **Range:** Reducing the impact of weather, weight, and battery life on flight distance.
* **Pathfinding:** Sensing methods that allow for semi-autonomous flight.
* **Victim Location:** Sensors may need to detect victims who are obscured.
* **GPS Denial:** Some structures may interfere with GPS signals, meaning the drone may need to take alternate paths for optimal performance.
* **Vital Sensing:** Sensors must accurately communicate a victim’s vitals and visual condition.
* **Weather & Environmental Conditions:** Weather, temperature, and ruined infrastructure may affect the operation of the drone and its subsystems.
* **Frequency Interference:** Audible and operational noise can interfere with the drone’s subsystems.
* **Privacy:** Recorded data is sensitive information and must be kept private.

The drone will retain many aspects from the research of previous teams, but our design must focus on the functionality of the external devices in tandem with the drone. This will require more precise filtering, power management, and general controls.

---

## III. Goals 

### Semi-autonomous Flight
* **Objective:** Drone is capable of semi-autonomous flight through GPS waypoint navigation and object detection using Lidar. The drone should be able to generate and follow its own flight paths with little to no human input. 
* **Success Measurement:** The drone is capable of independently navigating a predefined area with predetermined waypoints and avoiding obstacles while maintaining a stable flight with minimal human input.

### Search & Detection Capabilities 
* **Objective:** Integrated sensing and processing methods that allow the drone to detect and locate victims within a $6\text{ ft}$ radius of the drone. Including their heart rate, respiration rate, and facial expression. This will work in obstructed or harsh conditions. 
* **Success Measurement:** The drone will successfully identify victims under partial interference conditions in $80\%$ of the test trials. 

### Voice Based User Interaction
* **Objective:** Implement a two-way communication system to complete a preliminary assessment used to determine a victim's status and identity directly through the drone. Including stating their injuries, stating their name, receiving feedback from the command center, etc.
* **Success Measurement:** The drone will successfully be able to transmit $80\%$ of the communication in an emergency triage situation.

### Environmental Durability
* **Objective:** All modifications and electronic components can sustain exposure to hazardous environment conditions. Including but not limited to smoke, wind, rain, and low visibility conditions. 
* **Success Measurement:** The drone can maintain flight stability and sensor function in a controlled test with moderate wind speed and low visibility. The 3D printed enclosure for the electronics will keep them dry. 

---

## IV. Specifications & Measures of Success
1. The system shall detect and locate potential victims within a $6$-foot radius.
   * **Measure of success:** The system shall correctly detect and locate a test subject in at least $80\%$ of trials involving partial visual obstruction or other specified interference.
2. The system shall attempt to measure heart rate and respiration rate using selected sensors.
   * **Measure of success:** The system shall be compared against reference instruments, and the system shall meet an $80\%$ accuracy tolerance for each sensor before testing. 
3. The system shall attempt to identify predefined facial expressions when the victim's face is sufficiently visible.
   * **Measure of success:** The system shall correctly classify predefined expressions in at least $80\%$ of labeled test cases under the specified lighting and visibility conditions.
4. The system shall support two-way audio communication between the victim and the remote command center.
   * **Measure of success:** The system shall successfully transmit and receive at least $80\%$ of predefined test messages under specified operating conditions.
5. **Flight Duration:**
   * **Measure of success:** The fully equipped system shall complete a test flight lasting at least the minimum mission duration of $15\text{ minutes}$ with sufficient battery reserve to land safely.
6. Environmental Resilience:
   * **Measure of success:** The system shall complete a controlled test under a defined wind speed and visibility level, remain functional, and pass a defined moisture-exposure test.
7. Data Security:
   * **Measure of success:** Testing shall verify that unauthorized users cannot access protected data.

---

## V. Constraints
The design for the Triage Drone must fall within the constraints set by governing bodies such as the FAA, IEEE, HHS, etc. The constraints are as follows:

* The drone **SHALL** remain under $400\text{ ft}$ above ground level [12][14].
* The drone **SHALL** not exceed $100\text{ mph}$ [12][14].
* The drone **SHALL** be equipped with anti-collision lighting [12][14].
* The drone **SHALL** weigh under $55\text{ lbs}$ [12][14].
* The drone **SHALL** utilize encrypted wireless communication conforming to IEEE 802.11 standards for control and data transmission [18].
* The EMI test setup **SHALL** maintain all measurement tolerances within the limits specified by MIL-STD-461G § 4.3.1 [19].
* The system **SHALL** operate at an autonomy level functionally equivalent to SAE J3016 Level 3, where the drone can perform mission tasks under limited conditions while maintaining continuous human oversight [20].
* The drone **SHALL** not store health information or associate such data with any individuals (HIPAA compliance).

---

## VI. Survey of Existing Solutions & Relevant Literature

### A. Radar

#### General Overview
Non-contact vital sign monitoring with radar has gained substantial attention due to the availability of both low-cost radar devices and computationally efficient algorithms for processing their measurements. The importance of this measurement for a triage drone will be prioritizing victims during emergency searches based on vital readings. Non-contact measurements are necessary when dealing with emergency reconnaissance and the well-being of the victims.

#### Key Considerations
Radar-based non-contact vital sign monitoring comes with many different considerations to consider with this application:
* Fine-tuning radar signals to avoid interference from drone vibrations or external motion.
* Differentiating between heart rate and breathing rate, both of which fall within the $0.1\text{–}3\text{ Hz}$ frequency range.
* Designing for minimal power consumption without sacrificing signal fidelity.
* Implementing onboard processing to reduce latency and improve real-time responsiveness.
* Proper data handling to follow HIPAA regulations and information privacy laws.

### B. Image Processing

#### General Overview 
The image processing system needs to improve the images captured by the drone. Reliable images are important for helping the search team identify victims during emergency situations. To achieve this, the camera needs to capture clear, high-quality images and video. When weather or lighting conditions affect image quality, image enhancement may be used to improve visibility. The system must also process images promptly so the search team can receive information while emergencies are taking place. The image processing system needs to be compatible with the rest of the components in the system. Weather and other environmental conditions can limit the ability to capture clear images and identify victims accurately. 

#### Key Considerations
* The image processing system must reliably identify people in aerial images.
* The cameras must capture images with sufficient resolution and clarity. 
* Image enhancement may be needed due to low lighting or shadows. 
* Processed images should be compatible with the other components in the system. 
* Environmental restraints such as dust, rain, and physical obstructions can reduce image quality and disrupt image enhancement. 
* Images must be processed quickly enough to provide useful information during search-and-rescue operations.

### C. Deep Learning for Object Detection

#### General Overview
To perform effective search and rescue (SAR) operations without high-bandwidth video surveillance, autonomous systems use onboard deep learning models such as YOLO (You Only Look Once) to identify potential victims that may be obscured by surrounding objects. Incorporating such a model on computing platforms like the Jetson Nano enables precision diagnostic capabilities that are critical for time-sensitive operations [16].

#### Key Considerations
* Managing power and memory constraints when deployed on hardware such as the Jetson Nano.
* Selecting the correct model architecture to balance speed and accuracy.
* Integrating cross-modal sensor data (e.g., camera and radar) to improve detection in low-visibility environments.
* Training models on specialized SAR datasets to improve victim detection under heavy visual clutter.

#### Example: YOLO Architecture on Jetson Nano for Victim Detection
In [16], a lightweight YOLO model deployed on an embedded Jetson module demonstrated real-time human detection in rubble. By coupling a vision module with onboard radars and acoustic arrays, researchers were able to overcome visual noise to reliably improve detection.

* **Benefits:**
  * Real-time detection of small, partially obscured targets with minimal processing latency [16].
  * Autonomous operation independent of ground stations, further decreasing latency.
  * Scalable across diverse environments with specialized datasets.
* **Drawbacks:**
  * Accuracy still drops in fog, smoke, low-light, or similarly cluttered conditions.
  * Deep learning models require extensive SAR training data to lower the rate of false positives.
  * Opaque decision-making present in such learning models can make decisions hard to interpret.

#### Key Takeaways
1. Optimize model deployment on the Jetson Nano to maintain operation under thermal and power constraints [6]. 
2. Train and fine-tune YOLO using SAR datasets to improve small target recognition in complex environments.
3. Establish hierarchical trigger systems to flag candidate coordinates using visual detection, radar, and acoustic verification to improve detection confidence [16].

Additional model comparisons and sensor fusion strategies will be explored in future iterations of the system design.

### D. UAV Path Planning

#### General Overview
To achieve autonomous navigation with minimal operator input, SAR drones require robust path-planning architecture that can adapt to dynamic environments [16]. This process comes with an array of possible approaches and challenges that have been reviewed in [17]. For this system to be effective, it must reach potential victims quickly and safely regardless of difficult terrain.

#### Key Considerations
* Path optimization must be balanced with energy consumption to extend operational search time and radius.
* Algorithmic selection is important; while reinforcement learning offers fast local reaction times, hybrid approaches avoid heavy memory footprint and transfer errors [17].
* Visual sensors must be assisted by onboard navigation radar to handle visual degradation.
* Victim detection should trigger an immediate path-override routine that maintains spatial stability [16][17].

#### Example: Hybrid Framework for Electric UAV Emergency Rescue
Tang et al. [17] evaluated contemporary navigation and detection integration strategies tailored specifically for emergency rescue drones with limited carrying capacities, computational performance, and battery life. Their study analyzed how electric UAVs combine visual detection and navigation technologies to reduce path-planning complexity.

* **Benefits:**
  * Smooth trajectory planning minimizes computational load and extends total flight time [17].
  * Hybrid sensor design ensures reliable obstacle avoidance when cameras are blinded by visual clutter.
  * Enables real-time collision avoidance without ground station latency [17].
* **Drawbacks:**
  * Large datasets are required for diverse victim and environment appearance [17].
  * Inconsistent lighting and shading of urban rubble may cause targets to blend into backgrounds or become obscured.
  * Stationary hovering for target verification places a heavy draw on battery life, reducing total search range [17].

#### Key Takeaways
1. Battery consumption must be directly factored into path selection algorithms [17].
2. Utilize active radar and acoustic sensors to maintain navigation integrity in low-visibility environments [17].
3. Incorporate identification and pathfinding techniques that consider environmental lighting and visual angles.

Additional path-planning models will be explored in future iterations of the system design.

### E. Power & Payload
*(Content pending)*

### F. Communications
* Communications between Jetson Nano and sensors, and communication between Jetson Nano and PC.
* Go through the drone or 3rd party option (data link Jetson Nano).

---

## VII. Timeline & Budget

*(Gantt Chart representation based on project schedule)*

| Item | Predicted Quantity | Predicted Total Cost | Justification |
| :--- | :---: | :---: | :--- |
| **Yahboom IMX219 Camera Module** | 1 | $30 | Used as a secondary method to identify victims and aid in situational awareness. Attached at the front and rear of the drone so $360^\circ$ around the drone will be visible. |
| **Respeaker Microphone Array V2.0** | 1 | $10 | Provides communication allowing responders to check the victim for awareness. Can be filtered to the $80\text{–}225\text{ Hz}$ band. Recordings will not be stored to comply with HIPAA regulations regarding two-party consent. |
| **Lidar Sensor** | 1 | $350 | Used for obstacle detection and semi-autonomous flight path planning, ideal for low-visibility conditions. Solution for pathfinding and degraded sensing challenges to align with UAV path-planning requirements. |
| **PETG 3D Printing Filament ELEG∞** | 2 | $24 | Used to create custom mounts for all electronic components because it is resistant to moisture and UV. Although ASA would be better for sun/heat, PETG is significantly cheaper and less hazardous [15]. Reduces noise caused by drone vibrations. Supports robust sensing accuracy while in motion. |
| **GPS** | 1 | $30 | Used to geotag victim positions and support operator situational awareness. Supports triage reporting and near real-time display, as well as return-to-home and lost-link functions. |
| **Jetson Nano** | 1 | $200 | Used to control sensors, cameras, microphone, and speaker. Single-Board Computer (SBC) recommended by drone manufacturer for processing power, object detection, and speech processing. |
| **Total Cost** | | **$674** | |

---

## VIII. Personnel

The Triage Drone team is composed of the following five electrical engineering students:  

* **Weston LaRue:** Experience in Digital Signal Processing, Microcontroller Programming, Software Coding, Networking, and Circuit Design. With a background in network communications and audio processing, he has experience in live signal processing and data transfer.
* **Allison Wolden:** Experience in Project Management, Technical Documentation, circuit design, programming sensors and servos, and soldering through SAE Aero Design as president and member of the Avionics and Propulsion team. Managed completion of the Golden Eagle 3 aircraft, designed test stand circuitry for current, voltage, thrust, and RPM, and installed avionics systems.
* **Brandon Price:** Experience in Power Management, Power Distribution, and Budget Management through his position as a Paid Research Assistant at Tennessee Technological University. Diagnosed and optimized a low-cost LoRa water-level module reader for automated year-round operation.
* **Ryan Lee:** Experience in Circuit Design, Software Programming, Microcontroller Programming, Power Management, and Data Acquisition from interning with data acquisition experts at NASA. Built a portable data acquisition system using proprietary NASA software, calibrated sensors, budgeted, and optimized systems for harsh rocket engine testing environments.
* **Sidney Delgado:** Experience in programming, data analysis, and robotics. Analyzed network data and installed communication devices at Nashville Electric Service. Worked on robotic arm integration using servo motors, sensors, microcontrollers, and digital logic circuits.

### Interdisciplinary Collaboration & Advisory
* **Mechanical Engineering Team:** We are collaborating with a Senior Design team from Mechanical Engineering responsible for designing and modeling the extendable arm in SolidWorks, as well as 3D printing mounting components.
* **Customer & Advisor:** Dr. Dale Blair from Georgia Tech serves as customer and advisor. His background in radar systems, systems engineering, and target tracking [13] provides vital technical guidance.
* **Faculty Advisor & Project Manager:** Dr. Christopher (Storm) Johnson from Tennessee Tech oversees and guides the assembly, testing, and evaluation of the drone through weekly progress meetings.

---

## IX. Broader Implications, Ethics, and Responsibility as Engineers

### Safety
The primary purpose of the triage drone is to reduce risk to human responders in search and rescue missions, particularly in environments with limited access or extreme danger. However, technical failures or malfunctions could cause operational delays and pose risks to responders or victims. Enclosures and robust sub-system protection must be designed to mitigate structural or environmental damage to the drone.

### Privacy
Drones capturing video and sensor data present privacy concerns. Data captured along flight paths must be secured, particularly as video footage could inadvertently capture private property or sensitive human information. HIPAA guidelines must be enforced so no identifiable health metrics are stored or linked to individual identities.

### Human-Drone Relationship
Building trust between human emergency responders and autonomous systems is critical. Operational transparency and reliable reporting are required before responders will rely on automated triage data in high-stakes scenarios.

### Regulation
Drone regulation varies widely across regions and states. Compliance with local regulations and federal guidelines (FAA Part 107) is necessary during design and deployment.

---

## X. References
1. Aurelia Aerospace, *Aurelia X4 User Manual*, Rev. 5, 2026.
2. Infineon Technologies, *BGT60UTR11AIP 60 GHz Radar Sensor*, Product Page. https://www.infineon.com/cms/en/product/sensor/radar-sensors/radar-sensors-for-iot/60ghz-radar/bgt60utr11aip/
3. Infineon Technologies, *BGT60UTR11AIP Datasheet*.
4. Infineon Developer Community, *FAQs for XENSIV BGT60UTR11AIP Radar Sensor*, 2026.
5. Seeed Studio, *reComputer J1020 v2 (Jetson Nano)* product listing.
6. NVIDIA, *Jetson Nano power modes (5 W and 10 W)*.
7. Texas Instruments, *TPS56637 Synchronous Buck Converter Datasheet*.
8. Fall 2025 Capstone Team 8, project documents (*Power and Safety, Sensors, Communication, Drone Operator, Drone to PC Link, Conceptual Design*).
9. Fall 2024 Capstone Team 5, project repository and parts list.
10. Customer meeting notes with Dr. Blair, September 16, 2026.
11. Power and Payload Design, Aurelia X4 Triage Drone, Fall 2026, September 20, 2026.
12. Federal Aviation Administration. Small Unmanned Aircraft System (sUAS).
13. “W. Dale Blair | IEEE AESS,” Ieee-aess.org, Sept. 10, 2026. https://ieee-aess.org/contact/w-dale-blair (accessed Oct. 02, 2026).
14. Electronic Code of Federal Regulations, "14 CFR §107.51 Operating limitations for small unmanned aircraft."
15. MatterHackers, “The best 3D printing filament for outdoor use,” 2026. https://www.matterhackers.com/articles/the-best-3d-printing-filament-for-outdoor-use (accessed Oct. 03, 2026).
16. F. Ciccone and A. Ceruti, “Real-Time Search and Rescue with Drones: A Deep Learning Approach for Small-Object Detection Based on YOLO,” *Drones*, vol. 9, no. 8, pp. 514–514, July 2025, doi: 10.3390/drones9080514 (accessed Oct. 8, 2026).
17. P. Tang, J. Li, and H. Sun, “A Review of Electric UAV Visual Detection and Navigation Technologies for Emergency Rescue Missions,” *Sustainability*, vol. 16, no. 5, pp. 2105–2105, Mar. 2024, doi: 10.3390/su16052105 (accessed Oct 8, 2026).
18. IEEE, *IEEE Standard for Information Technology—Amendment 1: Enhancements for High-Efficiency WLAN*, IEEE Std 802.11ax-2021, May 2021.
19. U.S. Department of Defense, *MIL-STD-461G: Requirements for the Control of Electromagnetic Interference Characteristics of Subsystems and Equipment*, Washington, D.C., 2015.
20. SAE International, *J3016: Taxonomy and Definitions for Terms Related to Driving Automation Systems for On-Road Motor Vehicles*, Warrendale, PA, 2021.

---

## XI. Statement of Contributions

This proposal was worked on as a team through multiple revisions.

* **Introduction:** Ryan Lee
* **Challenges and Obstacles:** Ryan Lee
* **Specifications:** Sidney Delgado
* **Constraints:** Weston LaRue
* **Set Goals:** Allison Wolden
* **Relevant Literature:** Weston LaRue, Sidney Delgado, Ryan Lee, Brandon Price, Allison Wolden
* **Timeline, Resources, and Budget:** Allison Wolden
* **Personnel:** Allison Wolden, Brandon Price, Ryan Lee, Weston LaRue, Sidney Delgado
* **Implications, Ethics, Responsibility as Engineers:** Brandon Price
* **Editing:** Allison Wolden
