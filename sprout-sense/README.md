# Sprout Sense — Smart Plant Monitoring System

**Senior Design Capstone Project**

## Overview

Sprout Sense is a plant health monitoring device developed as a senior design capstone, combining embedded hardware, IoT connectivity, and a live web dashboard. The product tracks real-time plant health metrics light, air temperature, humidity, and soil moisture and surfaces them through a subscription-free dashboard, so plant owners can understand and act on their plant's needs without guesswork.

The project was developed end-to-end as a five-person, cross-functional team covering engineering, market validation, and business planning, and was presented at Design Day.

**Team:** Sammy Van Geffen (CEO), Kyle Strickland (CDO), Dylan Beetcher (CFO), Grace Scully (CMO), Khushi Chaturvedi (COO)

## My Role

Full-stack technical contributor — designed and built both the embedded firmware running on the device and the web dashboard used to visualize live and historical sensor data.

## Problem

Market research found that a large share of plant owners struggle to keep their plants alive simply because they lack accessible, specific guidance:

- Surveyed 47 and interviewed 25 prospective customers
- 83% of respondents care for a houseplant
- 63.8% of respondents reported struggling to properly care for it
- Broader research indicated this pain point affects a large share of the ~600 million plant-owning households worldwide

## Solution

A compact, sensor-equipped device that clips into a plant's soil and continuously reports on the conditions that actually determine plant health, paired with a dashboard that translates raw sensor data into clear, actionable status — no ongoing subscription required.

## System Architecture

| Layer | Implementation |
|---|---|
| **Microcontroller** | DFRobot Beetle ESP32-C6 |
| **Sensors** | BH1750 digital light sensor (I2C), Adafruit SHTC3 air temperature/humidity sensor (I2C), analog capacitive/resistive soil moisture sensor |
| **Power** | Solar-powered battery system |
| **Connectivity** | Wi-Fi via `WiFiManager` (captive-portal onboarding, no hardcoded credentials, auto-reconnect logic) |
| **On-device API** | Onboard `WebServer` exposing REST-style endpoints (`/data`, `/status`, `/control`) for live sensor reads and remote start/pause control |
| **Cloud logging** | Sensor data streamed to ThingSpeak for historical logging, with TalkBack-based remote command support |
| **Reliability** | Hardware watchdog timer (`esp_task_wdt`) to auto-recover from firmware hangs; serial command interface (`start`, `pause`, `status`, `wifi`, `read`, `resetwifi`, `help`) for on-bench debugging |
| **Dashboard** | Standalone HTML/CSS/JavaScript single-page dashboard using Chart.js for live and 24-hour historical trend visualization across all four metrics |

## Engineering Highlights

- **Sensor fusion firmware** — integrated multiple I2C and analog sensors into a single stable read/report loop on a resource-constrained MCU, with calibrated soil-moisture mapping (raw ADC → 0–100% scale).
- **Resilient connectivity** — implemented Wi-Fi reconnection handling and a watchdog timer so the device recovers automatically from dropped networks or firmware faults without manual intervention, which matters for a device meant to run unattended in someone's home.
- **Dual data paths** — device data is both queryable live (on-device REST API for the local dashboard) and logged to the cloud (ThingSpeak) for historical trends, giving the system both real-time and longitudinal visibility.
- **End-user-facing dashboard** — built a responsive Chart.js dashboard (light, temperature, humidity, soil moisture trends plus a combined 24-hour view) designed for a non-technical plant owner, not just an engineer debugging the device.
- **Remote control loop** — dashboard and cloud commands (start/pause/ping) close the loop back to the device, so the system isn't just one-way telemetry.

## Market Validation & Business Case

Beyond the engineering build, the team developed a full go-to-market case validated through direct customer research:

- Target price point: $60/unit at a $32.73/unit production cost
- Planned production capacity: 320,000 units/year
- Financial projections modeled through Year 3, with an estimated 38.2% IRR and 7–9 month payback period
- Funding ask: $500K for 20% equity at a $2.5M valuation

## Skills Demonstrated

`Embedded C++ (Arduino/ESP32)` · `I2C Sensor Integration` · `Wi-Fi/IoT Connectivity` · `REST API Design (embedded)` · `Cloud IoT Logging (ThingSpeak)` · `JavaScript` · `Chart.js Data Visualization` · `Responsive Web Design` · `Product Development` · `Market Research & Validation` · `Cross-functional Team Collaboration`

## Result

Delivered a fully working hardware-to-dashboard prototype including live sensor readings, cloud data logging, and remote control — presented at Design Day alongside a validated business case built from direct customer research.
