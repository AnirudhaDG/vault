**Anirudha Duttagupta**
4th Year BTech Information Technology, Vellore Institute of Technology, Vellore
- *[Portfolio](https://anirudhadg.notion.site/Anirudha-DG-1a2cbeb8409f80e7a3b0cc8d90f16978)*
- *[LinkedIn](https://www.linkedin.com/in/anirudhaduttagupta/)*
- *[CV](https://drive.google.com/drive/folders/1gQA6ygqFTGsE6B2covnSltJueJ74G9Hx)*
- *[Github](https://github.com/AnirudhaDG)*
Application for internship at RIL @ IISc, Bangalore


## <u>Design and modeling of a Quadruped legged robot for Navigation and Control in Disaster Mitigation Operations</u>
- [[#Objective]]
- [[#Summary]]
	- Novelty
	- Methodology 
	- Figures/schematics
	- Deliverables
## Objective 
The primary objective is to design, simulate, and make a  quadruped robot capable of navigating through unstable, and hazardous environments, regardless of their terrain, and carry out disaster mitigation operations. The robot should demonstrate mobility, stability, and adaptive control in terrains where wheeled or tracked robots fail, enabling safe exploration, victim detection, and assistance delivery.
## Summary 
### Novelty
- Unlike conventional wheeled disaster robots, this system employs **bio-inspired quadruped locomotion**, enabling adaptability to rubble, stairs, slopes, and uneven terrain. 
- Integration of **adaptive gait control with real-time environment feedback** (via sensors like IMU, LiDAR, and depth cameras) for robust navigation.
- Energy-efficient gait planning using **dynamic modeling and inverse kinematics** to ensure longer operational times.
- Modular leg design with compliance (possibly through **Series Elastic Actuators (SEA)** or passive springs) to absorb shocks during unstable terrain traversal.
- Potential integration with **teleoperation + semi-autonomous control modes** for effective human-robot collaboration in disaster scenarios.
### Methodology
It is most helpful for us to break this down into several components:
#### 1. System Architecture and Design
- **Hardware Subsystems**
    - **Mechanical Structure**: Lightweight quadruped frame with 3–4 DOF per leg.
    - **Actuation**: High-torque servo/BLDC motors.
    - **Sensing**:
        - Inertial Measurement Unit (IMU) for body orientation.
        - Joint encoders for proprioception.
        - Force/pressure sensors in feet for ground contact detection.
        - Depth camera/LiDAR for terrain mapping and obstacle detection.  
        - Microphones/thermal sensors for victim detection.
    - **Computation**:
        - **Onboard SBC** (e.g., Jetson Orin Nano) for high-level ROS2 processing (SLAM, navigation, AI-based perception).
        - **MCU** for real-time motor control and sensor data acquisition.
- **Software Subsystems**
    - **Low-Level Control Layer (MCU Firmware)**:
        - Implements motor drivers, joint PID loops, sensor interfacing over I2C/SPI/CAN.
        - Real-time control of leg trajectories at kHz frequency.
    - **Middleware (ROS2)**:
        - ROS2 nodes for gait planning, navigation, sensor fusion, and communication.
        - DDS (Data Distribution Service) for real-time communication between nodes.
    - **High-Level Autonomy Layer**:
        - SLAM for environment mapping.
        - Global/local path planning algorithms (A*, RRT*, DWA).
        - Disaster-specific behaviors (victim detection, kit delivery).
#### 2. Control Systems Architecture
- **Kinematic Modeling**
    - Forward Kinematics: Determines foot position from joint angles.
    - Inverse Kinematics: Solves required joint angles for target foot trajectory.
- **Dynamic Modeling**
    - Zero Moment Point (ZMP) and Center of Pressure (CoP) used for balance.
- **Gait Generation**
    - Predefined gaits: crawl (stable, slow), trot (balanced speed), bound (fast, for flat terrain).
    - Adaptive gait switching based on terrain classification from sensors.
    - Reflexive behaviors (e.g., stumble recovery).
- **Control Architecture**
    - High-level gait planner in ROS2. 
    - Low-level motor control loop on MCU.
    - Continuous feedback between both layers.
#### 3. Disaster Navigation and Autonomy Layer
At the highest layer, the quadruped integrates perception and decision-making to function as a **rescue robot**.
- **Mapping and Localization**
    - Visual SLAM or LiDAR-SLAM for 3D reconstruction of collapsed buildings. 
    - Loop closure detection for accurate maps in GPS-denied zones. 
- **Path Planning**
    - Global Planner: A* or RRT* generates overall route. 
    - Local Planner: Dynamic Window Approach (DWA) for reactive obstacle avoidance.
- **Survivor Detection and Human-Robot Interaction**
    - Thermal camera + microphone identify possible survivors.
    - Communication relay established via Wi-Fi/mesh networking.
    - Semi-autonomous control: rescuers can teleoperate specific tasks.
#### 4. Swarm and Cooperative Operation
**1. Pair-Based Cooperation**
When deployed in pairs, quadruped robots can:
- **Divide and Conquer Mapping**: Each robot scans different sections of a collapsed structure, merging their SLAM maps into a shared 3D reconstruction of the disaster zone.
- **Redundancy for Safety**: If one robot becomes immobilized, its partner can relay data, provide light payload assistance, or act as a communication repeater until human rescuers retrieve it.
- **Collaborative Victim Assistance**: Two robots can cooperatively carry a small stretcher module, water container, or emergency medical kit to trapped survivors.
- **Sensor Complementarity**: One robot can prioritize thermal/victim detection while the other focuses on navigation and mapping, reducing energy and processing load.

**2. Swarm Deployment**
In a full swarm setup, multiple quadrupeds can coordinate for large-scale disaster site coverage:
- **Distributed Mapping**
    - Robots spread across the rubble field, sharing partial maps in real-time via a mesh network.
    - Data fusion algorithms integrate maps into a unified global 3D model. 
- **Task Allocation**
    - A task allocation algorithm (e.g., market-based allocation or multi-agent reinforcement learning) distributes missions like “map area A,” “scan for victims in area B,” “deliver supplies to zone C.” 
- **Communication Relay Chain**
    - Robots form a **dynamic mesh communication backbone**, extending wireless connectivity deep into collapsed zones where human radio cannot reach.
- **Swarm Intelligence Behaviors**
    - Adaptive formation control: robots maintain safe distances to avoid collisions.  
    - Self-healing networks: if one robot fails, others reconfigure roles to maintain mission continuity.

### Deliverables
- **Embedded Control Firmware**
    - Low-level C/C++ firmware for STM32 (or equivalent MCU) handling:
        - Motor control (joint PID, torque/velocity modes). 
        - Sensor interfacing (IMU, encoders, force sensors, thermal camera modules). 
        - Real-time gait execution at sub-millisecond cycle times. 
    - Communication stacks:
        - CAN bus for motor drivers.  
        - I2C/SPI/UART for peripheral sensors.   
        - Ethernet/USB for high-level SBC communication.  
    - RTOS-based scheduling for deterministic performance and safety watchdogs. 
- **ROS2-Based Control and Navigation Stack**
    - URDF/Xacro model of the quadruped with full joint definitions.
    - ROS2 nodes for:
        - **Leg kinematics and inverse kinematics solver.**  
        - **Gait planner node** (crawl, trot, bound, adaptive terrain gaits). 
        - **State estimation node** integrating IMU + odometry + vision. 
        - **Mapping & SLAM node** (LiDAR/Depth camera-based). 
        - **Path planning node** using A*, RRT*, or DWA for dynamic terrain.  
    - Multi-robot framework with namespace isolation and distributed SLAM support for swarm operation.
- **Simulation Framework**
    - Gazebo/ROS2 simulation of the quadruped with physics-based locomotion.
    - Disaster environment maps (collapsed building, tunnel, rubble field).
    - Sensor plugins (LiDAR, IMU, thermal camera, microphones).
    - Validation of gait stability, obstacle traversal, and victim detection strategies.
- **Middleware and Communication Interface**
    - Protocol bridge between **embedded firmware (MCU)** and **ROS2 SBC**.
    - Message definitions (ROS2 custom msgs) for:
        - Joint commands.  
        - Sensor feedback.    
        - Fault/error reporting.  
    - Logging and telemetry pipeline for mission replay and debugging.
- **Autonomy and Disaster-Specific Software Modules**
    - Victim detection node (thermal signature + audio processing). 
    - Payload delivery coordination module (semi-autonomous drop-off).
    - Swarm coordination module for pair/multi-robot deployment:
        - Map sharing and merging. 
        - Task allocation strategies. 
        - Mesh networking support. 
- **Performance Reports and Testing Metrics**
    - Firmware latency benchmarks (control loop execution times, communication delays). 
    - Simulation vs. real-world comparison of gait stability.
    - SLAM accuracy and coverage metrics in complex environments. 
    - Swarm deployment results (map merging efficiency, communication reliability).