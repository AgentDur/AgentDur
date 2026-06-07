# AQUABRAIN

**Autonomous lightweight marine monitoring platform**

AQUABRAIN is an experimental autonomous surface vehicle project designed for environmental monitoring of small water bodies.

The platform is focused on low-cost deployment, modular hardware, LoRa safety communication and future cloud-connected telemetry.

---

## Project status

**Early prototype / MVP safety layer**

Current milestone:

* LoRa operator node validated
* LoRa bridge validated
* heartbeat-based link monitoring implemented
* selective ACK system implemented
* Arduino motion controller failsafe prepared
* hardware communication test completed

---

## Core idea

AQUABRAIN is designed as a compact autonomous boat for:

* environmental monitoring
* small lake and pond inspection
* water quality data collection
* telemetry experiments
* autonomous navigation research

The goal is to create an accessible alternative to large and expensive hydrographic platforms.

---

## System architecture

```text
Operator / Ground Station
        |
        | LoRa command + heartbeat
        v
Heltec LoRa Operator Node
        |
        | 866 MHz LoRa
        v
Heltec LoRa Bridge
        |
        | Serial command forwarding
        v
Arduino Motion Controller
        |
        | PWM
        v
Dual ESC + Differential Propulsion
```

---

## Communication protocol

### Movement command

```text
M leftPWM rightPWM
```

Example:

```text
M 1550 1550
```

### Stop command

```text
S
```

### Heartbeat packet

```text
H <seq>
```

Example:

```text
H 271
```

Heartbeat packets are sent automatically every 500 ms by the operator node.

They are used to confirm that the communication link is still alive.

---

## Safety layer

AQUABRAIN uses a heartbeat-based failsafe system.

If the boat-side controller does not receive heartbeat packets within the timeout window, it automatically stops the motors.

Current timeout:

```text
LINK_TIMEOUT_MS = 2500
```

This prevents the boat from continuing movement after communication loss.

---

## Firmware modules

| File                              | Device                    | Status               |
| --------------------------------- | ------------------------- | -------------------- |
| `aquabrain_operator_node.ino`     | Heltec LoRa operator node | Validated            |
| `aquabrain_lora_bridge.ino`       | Heltec LoRa bridge        | Validated            |
| `aquabrain_motion_controller.ino` | Arduino motion controller | Ready for bench test |

---

## Validated features

* Non-blocking heartbeat scheduler
* LoRa TX/RX switching
* Bridge command forwarding
* Selective ACK system
* RSSI / SNR diagnostics
* Legacy command mapping
* Heartbeat end-to-end test

---

## Hardware used

* Heltec ESP32 LoRa V3
* Arduino-compatible motion controller
* Dual ESC propulsion system
* Brushed DC motors
* Li-Ion / Li-Po battery system
* Raspberry Pi 5 planned for future onboard computing

---

## Roadmap

### Stage 1 — Embedded safety

* Heartbeat scheduler
* Link timeout failsafe
* Emergency stop
* Selective ACK

### Stage 2 — Motion validation

* Arduino bench test
* ESC signal validation
* Motor failsafe test
* Dry hardware test before water trials

### Stage 3 — Telemetry

* Battery voltage
* Temperature
* GPS position
* RSSI / SNR
* Packet loss counter

### Stage 4 — Operator interface

* Tablet dashboard
* Manual control interface
* Link status indicator
* Telemetry visualization

### Stage 5 — Autonomy

* GPS waypoint navigation
* ROS2 integration
* Obstacle avoidance
* Autonomous mission planning

### Stage 6 — Cloud layer

* Raspberry Pi 5 + 4G
* Cloud telemetry backend
* Web dashboard
* Data storage and analytics

---

## Project philosophy

AQUABRAIN is built around several principles:

* safety first
* modular architecture
* low-cost components
* open experimentation
* field-ready engineering
* gradual transition from manual control to autonomy

---

## Current mission

Prevent heartbeat-induced self-destruction of the vessel.

---

## Author

**Vasilii Sokolov**

Marine robotics, embedded systems and autonomous surface vehicle development.
