SAVIOR — Smart Autonomous Vehicle for Incident Observation and Response
Smart India Hackathon 2026 — Problem Statement SIH26177
Organization: Qualcomm Inc. | Category: Hardware | Theme: Robotics and Drones

🚁 Overview
SAVIOR is an autonomous, single-drone search-and-rescue (SAR) platform built to detect, decide, and report entirely on-device — with zero cloud dependency and full offline resilience. It is designed to operate in GPS-denied, communication-limited disaster zones where conventional cloud-reliant drones fail.

The platform senses its environment through RGB and thermal cameras, fuses that data on-device using an onboard Raspberry Pi 5, classifies hazards and detects survivors in real time, and reports geo-tagged findings back to a ground control station — continuing its mission autonomously even if the communication link is lost.

Designed as a single-airframe platform that can also be transitioned into a coordinated swarm of drones in future iterations.

🧩 Problem Statement
Disaster-hit and rubble-covered environments (earthquakes, building collapses, floods) are often inaccessible or unsafe for human first responders. Existing drone-based solutions typically depend on stable connectivity and cloud inference, making them unreliable in GPS-denied or network-cut-off disaster zones — exactly where SAR support is needed most.

Expected Solution (per SIH26177):

Autonomous Navigation (GPS-enabled + GPS-denied via AI/SLAM/obstacle avoidance)
On-Device AI Inference
Multi-Sensor Fusion (RGB, thermal, IMU, GPS)
Hazard Classification
Geo-Tagged Mapping
Emergency Alerting
Offline Resilience
Command Center Dashboard
💡 Our Solution
SAVIOR tackles the above with a low-cost, off-the-shelf hardware stack that is easily replicable and scalable for disaster-response agencies across India.

Key innovations:

On-device RGB + thermal fusion, powered by the onboard Raspberry Pi 5, detects survivors and classifies hazards — zero cloud dependency.
Detects survivors even through smoke, darkness, or partial debris cover — where single-sensor drones fail.
Low-cost, off-the-shelf hardware — easily replicable and scalable for disaster-response agencies.
Mission continues autonomously (RTH/LAND failsafe) even if the ground control station link is lost.
🛠️ Hardware Architecture
Component	Role
STM32 Flight Controller	Low-level flight stabilization & control
Raspberry Pi 5 (heatsink + fan + vented shroud)	Onboard AI inference, sensor fusion, flight computer
Raspberry Pi Camera Module 3	RGB imaging
MLX90640 Thermal Camera	Thermal imaging for survivor/hazard detection
OpenMV Cam	Real-time obstacle avoidance
GPS + Compass Module (mast-mounted)	Positioning & heading
ESP32-S3 + EBYTE E22-900T22D-V2 (SX1262 LoRa, 865–867MHz)	Long-range telemetry/command link
5.8GHz Video Transmitter (VTX)	Live video downlink
30A ESCs + 1400KV Brushless Motors	Propulsion
3D-printed lattice frame	Lightweight airframe
3S LiPo Battery	Power
Video path: Raspberry Pi (HDMI) → VTX → 5.8GHz → VRX → Capture Card → GCS Dashboard
Failsafe: Autonomous Return-to-Home / Land triggered via link-loss timer
