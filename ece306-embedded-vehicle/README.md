# Autonomous Embedded Vehicle System - ECE 306: Introduction to Embedded Systems

**North Carolina State University · Department of Electrical and Computer Engineering**

## Overview

This project is a cumulative, semester-long embedded systems build in which I designed, programmed, and physically assembled an autonomous microcontroller-based vehicle from the ground up  progressing from bare power-delivery and I/O fundamentals to a fully autonomous robot capable of line-following navigation, wireless telemetry, and closed-course completion. Each of the ten project milestones built directly on the previous one, so the final system reflects an integrated stack spanning power electronics, embedded C/assembly, real-time firmware, motor control, sensor fusion, and IoT connectivity.

The course modeled the constraints and workflow of real embedded systems engineering: fixed hardware resources, hard timing requirements, individual accountability for every line of code (even within a collaborative team structure), and live technical demonstrations in place of most written submissions.

## System Architecture

| Layer | Implementation |
|---|---|
| **Microcontroller** | Texas Instruments MSP430FR2355 (MSP-EXP430FR2355 LaunchPad) — FRAM-based ultra-low-power MCU |
| **Languages** | C and MSP430 Assembly |
| **Toolchain** | IAR Embedded Workbench |
| **RTOS** | Thread-based real-time program design for concurrent sensor, motor, and communication tasks |
| **Connectivity** | ESP32-WROOM-32E module for IoT/wireless telemetry and serial communication |
| **Power System** | Independently regulated battery power stage, current-verified via digital multimeter |
| **Sensing** | Reflectance/line-detection sensor array for track navigation |
| **Actuation** | Dual DC motor drive with forward and forward/reverse control |
| **Test & Measurement** | Digilent Analog Discovery (mixed-signal oscilloscope/logic analyzer) for signal verification and debugging |

## Development Milestones

The vehicle was built incrementally across ten cumulative project stages, each independently designed, soldered, coded, and demonstrated:

1. **Power System** — Designed and validated the regulated power delivery stage for the vehicle platform.
2. **LCD Interface** — Implemented a memory-mapped display driver for on-board status/debug output.
3. **Vehicle Assembly** — Mechanically assembled and soldered the chassis and drivetrain; verified powered mobility.
4. **Motor Control (Forward)** — Implemented PWM-based single-direction motor control.
5. **Motor Control (Forward/Reverse)** — Extended motor drivers to support bidirectional control and speed regulation.
6. **Black Line Detection** — Integrated an optical sensor array and signal-conditioning logic to detect a track boundary in real time.
7. **Black Line Navigation** — Built closed-loop control logic to autonomously follow a line using sensor feedback.
8. **Serial Port Communication** — Implemented UART-based serial communication for host-vehicle data exchange and debugging.
9. **IoT Integration** — Interfaced the MSP430 with an ESP32-WROOM-32E module for wireless data transmission.
10. **Autonomous Course Navigation** — Integrated all prior subsystems into a fully autonomous run of a complete competition-style course, demonstrated live in class.

## Engineering Highlights

- **Bare-metal firmware development** on a resource-constrained FRAM microcontroller, with direct register-level configuration of peripherals (timers, ADC, UART, GPIO).
- **Real-time, multi-threaded task design** to manage simultaneous sensor polling, motor PWM generation, and communication without blocking.
- **Mixed hardware/software debugging** — used an Analog Discovery to trace and correct timing and signal-integrity issues at the electrical level, not just in code.
- **End-to-end system integration** — every subsystem (power, sensing, actuation, communication) had to interoperate reliably under real-time constraints for the final autonomous run.
- **Individual technical ownership** — while teams collaborated on strategy, all code was individually authored and defended live in TA/instructor Q&A, reflecting professional-level accountability for one's own implementation.

## Skills Demonstrated

`Embedded C` · `Assembly (MSP430)` · `Real-Time/Threaded Firmware Design` · `PWM Motor Control` · `Sensor Interfacing & Signal Conditioning` · `UART Serial Communication` · `IoT / Wireless Module Integration (ESP32)` · `Hardware Debugging (Oscilloscope/Logic Analyzer)` · `PCB-Level Soldering & Hardware Assembly` · `Power System Design`

## Result

Successfully completed the full circuit and vehicle build within the given project timeframe, meeting every milestone deadline across the semester. Each of the ten cumulative stages from initial power system design through final autonomous course navigation was designed, soldered, coded, and demonstrated on schedule, resulting in a fully functional autonomous vehicle by the end of the term.
