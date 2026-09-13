# SAVIOR
### Smart Autonomous Vehicle for Incident Observation and Response

[![SIH 2026](https://img.shields.io/badge/Smart%20India%20Hackathon-2026-blue)](https://sih.gov.in)
[![Problem Statement](https://img.shields.io/badge/PS-SIH26177-orange)]()
[![Theme](https://img.shields.io/badge/Theme-Robotics%20%26%20Drones-green)]()
[![License](https://img.shields.io/badge/License-MIT-lightgrey)]()

**Organization:** Qualcomm Inc. &nbsp;|&nbsp; **Category:** Hardware &nbsp;|&nbsp; **Theme:** Robotics and Drones

An autonomous, single-drone search-and-rescue platform that senses, decides, and reports **entirely on-device** — with zero cloud dependency and full offline resilience in GPS-denied disaster zones.

---

## Table of Contents

- [Problem Statement](#problem-statement)
- [Our Solution](#our-solution)
- [Key Differentiators](#key-differentiators)
- [System Architecture](#system-architecture)
- [Hardware Stack](#hardware-stack)
- [Data & Communication Flow](#data--communication-flow)
- [Repository Structure](#repository-structure)
- [Roadmap](#roadmap)
- [Team](#team)
- [License](#license)

---

## Problem Statement

Disaster-hit and rubble-covered environments — collapsed buildings, earthquake zones, flood-hit regions — are often too dangerous or inaccessible for human first responders to search quickly. Most existing drone-based SAR solutions depend on stable connectivity and cloud-based inference, which makes them unreliable exactly where they're needed most: GPS-denied, network-cut-off disaster sites.

**SIH26177 expects a solution covering:**

| Capability | Description |
|---|---|
| Autonomous Navigation | GPS-enabled and GPS-denied (AI/SLAM-based obstacle avoidance) |
| On-Device AI Inference | No dependency on cloud or external compute |
| Multi-Sensor Fusion | RGB, thermal, IMU, GPS |
| Hazard Classification | Real-time identification of survivors and hazards |
| Geo-Tagged Mapping | Location-tagged incident reporting |
| Emergency Alerting | Immediate notification to command center |
| Offline Resilience | Full functionality without network connectivity |
| Command Center Dashboard | Centralized monitoring and control interface |

---

## Our Solution

SAVIOR is built on a low-cost, off-the-shelf hardware stack — engineered to be easily replicable and scalable for disaster-response agencies across India, without compromising on autonomy or reliability.

- Fuses **RGB + thermal imaging on-device** via an onboard Raspberry Pi 5 to detect survivors and classify hazards in real time
- Operates with **zero cloud dependency** — all inference happens locally on the drone
- Continues its mission autonomously (return-to-home / land failsafe) even if the ground control link is lost
- Designed as a **single-airframe platform today**, architected to transition into a coordinated swarm in future iterations

---

## Key Differentiators

| Traditional Drone-Based SAR | SAVIOR |
|---|---|
| Relies on stable cloud connectivity for inference | Fully on-device inference — no cloud, no network dependency |
| Fails in GPS-denied or communication-dark zones | Purpose-built for GPS-denied, offline environments |
| Single-sensor detection (RGB only) | RGB + thermal fusion — detects survivors through smoke, darkness, and partial debris cover |
| High-cost, proprietary hardware | Low-cost, off-the-shelf components — easily replicable at scale |
| Mission halts if link is lost | Autonomous failsafe keeps the mission running without ground control |

---

## System Architecture

```
                     ┌───────────────────────┐
                     │   Ground Control       │
                     │   Station (Dashboard)  │
                     └───────────▲────────────┘
                                 │  LoRa Telemetry / VTX Video
                     ┌───────────┴────────────┐
                     │   ESP32-S3 + LoRa       │
                     │   (Command & Telemetry) │
                     └───────────▲────────────┘
                                 │
   ┌──────────────┐     ┌───────┴────────┐     ┌──────────────┐
   │ RGB Camera    │────▶│                │◀────│ Thermal Cam  │
   │ (Pi Camera 3) │     │  Raspberry Pi 5 │     │ (MLX90640)   │
   └──────────────┘     │  On-Device AI    │     └──────────────┘
   ┌──────────────┐     │  Fusion & Infer. │     ┌──────────────┐
   │ OpenMV Cam    │────▶│                 │◀────│ GPS + Compass│
   │ (Obstacle Av.)│     └───────┬────────┘     │ (Mast-mount) │
   └──────────────┘             │              └──────────────┘
                                 │ Flight Commands
                     ┌───────────┴────────────┐
                     │   STM32 Flight          │
                     │   Controller            │
                     └───────────┬────────────┘
                                 │
                     ┌───────────┴────────────┐
                     │  ESCs + Brushless Motors│
                     └────────────────────────┘
```

---

## Hardware Stack

| Component | Role |
|---|---|
| STM32 Flight Controller | Low-level flight stabilization and control |
| Raspberry Pi 5 (heatsink + fan + vented shroud) | Onboard AI inference, sensor fusion, flight computer |
| Raspberry Pi Camera Module 3 | RGB imaging |
| MLX90640 Thermal Camera | Thermal imaging for survivor and hazard detection |
| OpenMV Cam | Real-time obstacle avoidance |
| GPS + Compass Module (mast-mounted) | Positioning and heading |
| ESP32-S3 + EBYTE E22-900T22D-V2 (SX1262 LoRa, 865–867 MHz) | Long-range telemetry and command link |
| 5.8 GHz Video Transmitter (VTX) | Live video downlink |
| 30A ESCs + 1400KV Brushless Motors | Propulsion |
| 3D-Printed Lattice Frame | Lightweight, low-cost airframe |
| 3S LiPo Battery | Power supply |

---

## Data & Communication Flow

**Video path:**
`Raspberry Pi (HDMI) → VTX → 5.8 GHz Link → VRX → Capture Card → GCS Dashboard`

**Failsafe behavior:**
`Link-loss timer triggers → Autonomous Return-to-Home / Land`

---

## Repository Structure

```
savior-sih26177/
├── README.md            Project overview, problem statement, architecture
├── firmware/             STM32 flight controller code
├── companion-ai/         Raspberry Pi 5 code (RGB + thermal fusion, inference)
├── docs/                 Discussion summaries, architecture diagrams
├── hardware/             BOM, wiring diagrams, CAD / 3D-print files
└── deck/                 SIH presentation slides and assets
```

---

## Roadmap

| Milestone | Status |
|---|---|
| Single-drone hardware integration | In Progress |
| On-device RGB + thermal fusion pipeline | In Progress |
| Priority Rescue & Safe-Route Recommendation Engine | Planned |
| Swarm coordination (multi-drone transition) | Planned |
| Field testing in simulated disaster environment | Planned |

---

## Team

| Name | Role |
|---|---|
| Pankaj Kute | Team Lead — Project Administration & Coordination, Flight Computer Logic |
| Jaideep Khare | Flight Controller Engineer — STM32 & Flight Hardware |
| Rudra Kanojiya | Communications & GCS Lead — Communication Architecture, GCS Dashboard, Project Co-Coordination |
| Shivam Pandey | Perception & ML Engineer — Camera Systems (OpenMV, RGB, Thermal), ML Pipeline & Flight Computer |
| Partth Bhardwaj | Aeromechanics & Design Lead — Frame Design, Aeromechanics, Build Planning |
| Tanisha Giri | Documentation & Presentation Lead — Technical Documentation, SIH Deck & Reporting |

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
