# 💻 Software – Smart Table Fan (ESP32-C3)

## Overview
The software is built on the **ESP32 Arduino framework**, combining:

- PWM motor control
- HTTP web server
- NTP time synchronization
- Task scheduling
- Non-blocking system design

It is designed to be:
- Responsive
- Reliable
- Expandable

---

## System Architecture

The firmware is structured into key modules:

- **PWM Control** → Handles fan speed
- **Ramp Engine** → Smooth acceleration (soft start)
- **Scheduler** → Time-based automation
- **Night Mode** → Speed cycling logic
- **Sleep Timer** → Auto shutdown
- **WiFi Manager** → Connection + AP fallback
- **Web Server** → HTTP API + UI
- **Storage** → Persistent state (Preferences)

---

## Core Features

### PWM Fan Control
- Uses ESP32 LEDC PWM
- 0–100% logical speed
- Mapped to physical minimum duty

Key concept:
- Low PWM does not spin motor → handled via mapping

---

### Soft Start (Non-blocking)
Fan does not jump instantly to speed.

Instead:
- Uses **3-phase ramp system**
- Fully asynchronous (no delay)

Phases:
1. Ramp up (smooth curve)
2. Kickstart (if needed)
3. Hold and transition

Benefits:
- Prevents current spike
- Reduces mechanical stress
- Improves reliability

---

### Kickstart Logic
Some motors cannot start at low speed.

Solution:
- Boost to higher speed briefly
- Then drop to target speed

---

### Scheduler (NTP-Based)
- Uses real-time clock via NTP
- Executes tasks at specific time (hour + minute)

Supported actions:
- Turn OFF
- Turn ON
- Set speed

---

### Night Mode
Automated speed cycling:

- Alternates between:
  - Low speed
  - High speed

Based on:
- Time window
- Duration per phase

---

### Sleep Timer
- Turns off fan after X minutes
- Uses overflow-safe timing:
  - Stores start time + duration
  - Avoids millis() overflow issues

---

### Button Control (State Machine)

Handles:
- Single click → Cycle speeds
- Double click → Toggle WiFi
- Long press → Toggle fan ON/OFF

Uses proper **state machine**:
- Reliable detection
- No false triggers

---

### WiFi System

Behavior:
1. Try saved WiFi
2. If fail → start AP mode
3. User config via web UI

Features:
- WiFi toggle (via button)
- Auto reconnect
- NTP re-sync after reconnect

---

### Web Server (HTTP API)

Runs on:
- Port 80

Supports:
- JSON requests/responses
- CORS (for external devices)

Main endpoints:
- `/api/status`
- `/api/fan`
- `/api/schedules`
- `/api/nightmode`
- `/api/sleep`
- `/api/wifi`

---

### State Persistence

Uses:
- ESP32 **Preferences (flash storage)**

Saves:
- Power state
- Speed
- WiFi settings
- Schedules
- Night mode config

Ensures:
- System resumes after reboot

---

## Design Principles

- **Non-blocking code** (no delay-based logic)
- **Failsafe operation**
- **Offline usability (button control)**
- **Modular structure**
- **Expandable architecture**

---

## Limitations

- No sensor feedback (open-loop control)
- No PID or closed-loop speed control
- Depends on stable WiFi for remote control

---

## Future Improvements

- Temperature-based automation
- External display controller (ESP32 CYD)
- MQTT / cloud integration (optional)
- RPM feedback system