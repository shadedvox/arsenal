# Arsenal

A 6-DOF robotic arm built around a custom STM32 motor controller, closed-loop steppers, and a distributed ROS control stack. The project moves through four stages: electronics, mechanical build, firmware/control integration, and final assembly with the end effector.

---

## Stage 1 — Voxboard (electronics)

Voxboard is a custom 4-layer PCB motor controller built to drive all six joints of the arm from a single board. It replaces an earlier ESP32 + 28BYJ-48 stepper setup with a proper closed-loop system capable of real position feedback and real-time multi-axis control.

**Core architecture**
- STM32F446RET6 (LQFP64, 180MHz Cortex-M4 with FPU) handles all real-time motor control
- Raspberry Pi 3B+ runs inverse kinematics (ikpy) and talks to the STM32 over UART
- 3x TMC2209 drivers for the NEMA17 motors at roll, pitch, and yaw
- 3x TMC5160 drivers for the NEMA23 motors at elbow, base and shoulder
- 10 to 20:1 cycloidal gearbox on every joint, with an MT6835 absolute magnetic encoder at each gearbox output shaft for true closed-loop position feedback, no homing required on power-up

**Connectivity**
- CAN (for the end-effector node), USB, dual SPI (encoders + TMC5160s), triple UART (TMC2209s + RPi), I2C, SWD for debug

**Power**
- Single 24V input via XT60, reverse-polarity and surge protected, stepped down to 5V (buck) and 3.3V (LDO) for logic
- USB VBUS backup path with ideal-diode OR-ing, so the board can run off USB power alone for debug/bring-up

**Project Files & Schematics :** [\Stage1 - STM\voxboard](https://github.com/shadedvox/arsenal/tree/main/Stage1%20-%20STM/voxboard)

**Status: design completed - fabrication pending**

![Image 2](./r_imgs/r2.png)
![Image 3](./r_imgs/r3.png)
![Image 4](./r_imgs/r4.png)
![Image 5](./r_imgs/r5.png)
![Image 6](./r_imgs/r6.png)
![Image 7](./r_imgs/r7.png)
![Image 8](./r_imgs/r8.png)

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