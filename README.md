# 🦾 RoboFlex-ROS2: 6-DOF Robotic Arm with ESP32, Micro-ROS, and MoveIt

🚀 **RoboFlex-ROS2** is an open-source robotic arm powered by **ESP32**, **Micro-ROS**, and **ROS 2**, designed for precise motion planning using **MoveIt**. This project aims to provide a modular, easy-to-use framework for robotic manipulation with real-time control.

---

## 📜 Table of Contents
- [🛠 Features](#-features)
- [📦 Hardware Requirements](#-hardware-requirements)
- [🖥️ Software Stack](#️-software-stack)
- [🚀 Installation Guide](#-installation-guide)
- [🤖 ROS 2 Integration](#-ros-2-integration)
- [🎯 Motion Planning with MoveIt](#-motion-planning-with-moveit)
- [📂 Repository Structure](#-repository-structure)
- [🚀 Running the Robotic Arm](#-running-the-robotic-arm)
- [📸 Demos & Visualization](#-demos--visualization)
- [🤝 Contributing](#-contributing)
- [📜 License](#-license)
- [📞 Contact](#-contact)

---

## 🛠 Features
- ✅ **5 Degrees of Freedom (DOF)**
- ✅ **ESP32 + Micro-ROS** for real-time control
- ✅ **ROS 2 & MoveIt** for advanced motion planning
- ✅ **Supports RViz & Gazebo Simulation**
- ✅ **Low-cost and DIY-friendly**
- ✅ **Modular architecture for easy customization**

---

## 📦 Hardware Requirements
| Component           | Specification                    |
| ------------------- | -------------------------------- |
| **Microcontroller** | ESP32 with Micro-ROS             |
| **Servos/Motors**   | MG996R / MG90S (customizable)    |
| **Power Supply**    | 6V–12V (depending on motor type) |
| **Communication**   | WiFi, UART                       |
| **Frame Material**  | Aluminum / 3D Printed Parts      |

---

## 🖥️ Software Stack
- **Operating System:** Ubuntu 24.04 (Recommended)
- **Robot Middleware:** ROS 2 (Jazzy)
- **Motion Planning:** MoveIt 2
- **Simulation:** Gazebo / RViz
- **Microcontroller Firmware:** Micro-ROS on ESP32
- **Programming Languages:** C++, Python

---

## 🚀 Installation Guide
### 1️⃣ Install ROS 2
Follow the official ROS 2 installation guide:  
🔗 [https://docs.ros.org/en/jazzy/Installation.html](https://docs.ros.org/en/humble/Installation.html)

### 2️⃣ Install Micro-ROS on ESP32

Refer to this documentation for setup

```sh
https://github.com/munn33b/esp32-microROS/blob/main/README.md
```

(Refer to official Micro-ROS documentation for configuration)

### 3️⃣ Clone This Repository

```bash
git clone https://github.com/BrainSwarmRobotics/RoboFlexv2.0
```

### 4️⃣ Install Dependencies

```bash
sudo apt install ros-jazzy-ros2-control ros-jazzy-ros2-controllers ros-jazzy-ros-gz ros-humble-gz-ros2-control ros-humble-ros-gz-sim
```

### 4️⃣ Configure Packages

Go to `brainswarm_ws/src/roboflex_description/launch`. Modify **Line 45** and **Line 48** with appropriate Paths.

### 4️⃣ Build Workspace

```bash
cd brainswarm_ws
```

 Run the following command

```bash
colcon build
```

### 4️⃣ Running the System

#### Running the Simulation

In terminal, run the following command to start the simulation

```bash
ros2 launch roboflex_description simulation.launch.py
```

#### Starting Interface for Real Hardware Integration

```bash
ros2 launch roboflex_description real_hardware.launch.py
```

For starting controllers, you need to run following script, inside the root of your `ROS2 Workspace` run following command

```
./src/roboflex_description/start_controllers
```

It will start all controllers

To run the complete robotic Arm system, make sure you have `micro_ros_agent` running. In the `Firmware/six_motors_microROS_udp4_millis_and_map_servo_driver/six_motors_microROS_udp4_millis_and_map_servo_driver.ino` file, modify line 81 with appropriate values.

After that, run the Micro ROS Agent on terminal

```bash
ros2 run micro_ros_agent micro_ros_agent udp4 --port 8888
```

After running above command, switch on / power on the Robotic Arm.

**Note:** The sequence is important, make sure the `micro_ros_agent` is running before powering on the robotic arm. After that, proceed with further steps.

#### Starting the Motion Planner

```
ros2 launch brainswarm_robotic_arm_moveit_config move_group.launch.py
```

#### Setting SIM Time Parameter

```
ros2 param set /move_group use_sim_time True
```

#### Running RViz

```
ros2 run rviz2 rviz2
```

### 4️⃣ Topics and Actions

| Topic Name                                              | Description                                                  |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| /joint_states                                           | Feedback of Joint Values from Simulation                     |
| /real_robot/joint_states                                | Feedback of Joint States from Real Robot                     |
| /arm_controller/follow_joint_trajectory                 | Action Server that accepts Goal Joint Trajectory Commands for Simulation |
| /real_robot/real_arm_controller/follow_joint_trajectory | Action Server that accepts Goal Joint Trajectory Commands for Real Hardware |
| /motor_commands                                         | Topic that is configured in Hardware Interface to send Joint Angles to Real Hardware |
