# 🌬️ Smart Table Fan – ESP32-C3 IoT Prototype

## Overview
Smart Table Fan is a **DIY IoT prototype project** where a standard table fan is modified and enhanced using an **ESP32-C3 Super Mini**.  
The system enables **PWM-based speed control, web-based operation, and time-based automation**, while integrating safety and usability features such as soft start and manual override.

This project demonstrates the integration of **hardware modification, embedded systems, and networking** in a practical everyday appliance.

> ⚠️ This is a prototype and involves **overdriving a fan motor**, which may affect safety and lifespan.

---

## Features
- **PWM fan control:** Adjustable speed from 0–100% using ESP32  
- **Web-based control:** Control fan via HTTP interface (ON/OFF + speed slider)  
- **NTP scheduling:** Time-based automation (no date required)  
- **Soft start:** Gradual ramp-up to prevent current spikes and hardware stress  
- **Minimum start threshold:** Ensures motor spins reliably at low speeds  
- **Failsafe system:** Safe fallback if ESP crashes or loses connection  
- **Manual override button:** Physical control independent of WiFi  
- **State persistence:** Saves power state, speed, and schedule in flash memory  
- **WiFi management:** Auto-connect or fallback to AP mode for setup  
- **Expandable design:** Ready for future features like temperature-based control  

---

## Prototype Setup

### Hardware
- **Controller:** ESP32-C3 Super Mini  
- **Fan:** Modified table fan (overdriven for extended control range)  
- **Control circuit:** PWM driver (MOSFET or equivalent switching circuit)  
- **Input:** Single push button for manual override  
- **Power:** 5V2A External power supply (must handle increased load due to overdrive)  
- **Boost:** 12V Boost converter + 470uf Capacitor

### Software
- **Firmware:** ESP32-based control system (PWM + HTTP server)  
- **Web Interface:** Hosted directly on ESP32 for local control  
- **Time Sync:** NTP for accurate scheduling  
- **Storage:** Flash memory for saving user settings and schedules  
- **Control Protocol:** HTTP endpoints for both UI and external controllers  

---

## Workflow
1. ESP32 boots and attempts to connect to saved WiFi  
2. If connection fails, it starts **Access Point (AP mode)** for setup  
3. User accesses web UI to control fan or configure settings  
4. PWM signal controls fan speed based on user input or automation  
5. Scheduler triggers actions (ON/OFF or speed change) at set times  
6. Manual button can override system at any time  
7. System state is saved and restored after reboot  

> This allows both automated and manual control without relying fully on network connectivity.

---

## Challenges & Learning
- **Motor control behavior:** Managing PWM with real fan motors (dead zones, startup issues)  
- **Electrical safety:** Handling increased load from overdriving the fan  
- **Soft start implementation:** Preventing sudden current spikes during startup  
- **Reliable networking:** Designing fallback AP mode when WiFi fails  
- **User experience:** Ensuring system remains usable without WiFi (manual button)  
- **Embedded design:** Combining real-time control, scheduling, and web server on ESP32  
- **Limitations:** No closed-loop feedback (no RPM sensing or temperature input yet)  

---

## Potential Applications
- Smart home fan automation  
- Energy-saving airflow control based on schedule  
- Low-cost IoT appliance modification projects  
- Foundation for environmental control systems (future temp-based control)  

---

## Media
*(Add screenshots of web UI, wiring diagram, or demo videos here)*

---

## Notes
This is a **prototype project** meant to demonstrate skills in:  
- Embedded systems programming (ESP32)  
- PWM motor control and hardware interfacing  
- Building HTTP-based control systems  
- Designing resilient IoT systems (failsafe + offline control)  
- Creating expandable and modular system architecture  

It is **not a commercial or safety-certified product**.