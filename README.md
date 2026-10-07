# Arsenal

A 6-DOF robotic arm built around a custom STM32 motor controller, closed-loop steppers, and a distributed ROS control stack. The project moves through four stages: electronics, mechanical build, firmware/control integration, and final assembly with the end effector.

---

## Stage 1 — Voxboard (electronics)

Voxboard is a custom 4-layer PCB motor controller built to drive all six joints of the arm from a single board. It replaces an earlier ESP32 + 28BYJ-48 stepper setup with a proper closed-loop system capable of real position feedback and real-time multi-axis control.

**Core architecture**
- STM32F446RET6 (LQFP64, 180MHz Cortex-M4 with FPU) handles all real-time motor control
- Raspberry Pi 3B+ runs inverse kinematics (ikpy) and talks to the STM32 over UART
- 4x TMC2209 drivers for the NEMA17 motors at roll, pitch, yaw, and elbow
- 2x TMC5160 drivers for the NEMA23 motors at base and shoulder
- 20:1 cycloidal gearbox on every joint, with an MT6835 absolute magnetic encoder at each gearbox output shaft for true closed-loop position feedback, no homing required on power-up (swapped in for the AS5048A due to availability, used in SPI-only mode)

**Connectivity**
- CAN (for the end-effector node), USB, dual SPI (encoders + TMC5160s), triple UART (TMC2209s + RPi), I2C, SWD for debug

**Power**
- Single 24V input via XT60, reverse-polarity and surge protected, stepped down to 5V (buck) and 3.3V (LDO) for logic
- USB VBUS backup path with ideal-diode OR-ing, so the board can run off USB power alone for debug/bring-up

**Design choices worth noting**
- Through-hole connectors throughout, chosen for hand-solder reliability and vibration resistance on a moving arm
- Single unified ground plane rather than a split motor/logic ground, with noise controlled through tight current loops, local decoupling at every driver, and liberal ground stitching instead
- Fabricated via JLCPCB: 4-layer, ENIG finish, PCBA for SMD parts, hand-soldered connectors

**Status: in progress** — schematic complete and locked, currently in PCB routing/layout phase in KiCad.



![Image 1 - schematic](./j_imgs/D18-1.png)




![Image 2 - routing layer](./j_imgs/D22-3.png)




![Image 3 - routing](./j_imgs/D22-4.png)




![Image 4 - routing layer](./j_imgs/D22-5.png)




![Image 5 - routing layer](./j_imgs/D22-6.png)




![Image 6 - routing layer](./j_imgs/D22-7.png)




![Image 7 - pcb render](./j_imgs/D22-8.png)




![Image 8 - pcb render](./j_imgs/D22-9.png)



---

## Stage 2 — Mechanical build

3D-printed cycloidal gearboxes and joint assemblies, structural frame for the arm.

**Status: in progress**

---

## Stage 3 — Firmware & control

Real-time motor control on the STM32, distributed ROS architecture with MoveIt running on the Pi/PC side.

**Status: in progress**

---

## Stage 4 — Integration & end effector

Final assembly, end-effector design, and full-arm bring-up.

**Status: in progress**

---

*© 2026 Atharva Chauhan, Vox*
