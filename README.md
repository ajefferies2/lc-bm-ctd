# OpenCTD-like Bristlemouth-Compatible Sensor Node

A modular, cost-effective CTD (Conductivity, Temperature, Depth) sensor node designed to transmit real-time data over a Bristlemouth-style CAN bus. This system is intended for scalable academic deployments using I2C-only digital sensors and STM32 microcontrollers. It avoids legacy analog and 1-Wire protocols for simplicity and future compatibility with lab-grade sensors. 

**NOTE: This project will NOT be plug and play with bristlemouth infrastructure unless we use their hardware dev kit (unavailible) or other 2-wire power/data soln.**

## Goals

- Replace microSD logging with real-time CAN / "bristlemouth lite" broadcast
- Use only I2C sensors for reduced wiring and modularity
- Maintain low cost while ensuring reliability
- Design for compatibility with Bristlemouth bus architecture (TX-only)
- Future-proof for lab-grade sensor drop-in replacements and additional sensors

## System Overview

### Microcontroller
- STM32F103C8T6 ("Blue Pill")
- ST-Link V2 for flashing/debugging
- SN65HVD230 CAN transceiver (standard CAN 2.0B)

### Sensors (I2C only) (similar suite to OpenCTD)
| Measurement    | Sensor                        | Brand      | Cost    |
|----------------|-------------------------------|------------|---------|
| Pressure + Temp| MS5803-14BA                   | SparkFun   | ~$64    |
| Conductivity   | Gravity EC Sensor (I²C V2)    | DFRobot    | ~$70    |

**NOTE: We can add separate Temp, pH, and any other sensors that are I2C compatible fairly easily.**

### CAN Protocol
- Fixed CAN ID: TBD 
- 6-byte payload structure:
  - Temperature (°C × 100)     → 2 bytes
  - Pressure (mbar × 10)       → 2 bytes
  - Conductivity (mS/cm × 100) → 2 bytes
- Transmit at 1 Hz (TBD??)

## Hardware Cost Estimate

| Component                  | Cost     |
|----------------------------|----------|
| STM32 Blue Pill            | $3–4     |
| ST-Link V2 Programmer      | $3–5     |
| SN65HVD230 CAN Transceiver | $1–2     |
| MS5803-14BA (SparkFun)     | ~$64     |
| DFRobot Gravity EC (I²C)   | ~$70     |
| Wiring, housing, connectors| ~$10–15  |
| **Total (per unit)**       | **~$150–160** |

**NOTE: electronics only estimate**
