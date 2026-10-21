# Bottle Plane Flight Controller

A flight controller I'm building from scratch for a small plastic-bottle RC airplane, written in C on an STM32 microcontroller. The goal is a plane that stabilises itself using an IMU, with GPS logging and basic autonomous features later.

> **Status:** work in progress. See the roadmap below.

## Hardware

🟢 bought · 🔴 not bought yet

| Part | Purpose | Price | Status |
|---|---|---|---|
| STM32F411CEU6 "Black Pill" board | Main microcontroller (96 MHz, USB) | € 7.84 | 🟢 Bought |
| ICM-42688-P IMU | Gyroscope and accelerometer (SPI) | € 21.08 | 🟢 Bought |
| u-blox NEO-M8N GPS | Position and speed (UART) | € 9.81 | 🟢 Bought |
| SG90 servos | Control surfaces | € 1.93 x5 | 🟢 Bought x5|
| Breadboard and dupont cables | Prototyping | € ~€20 | 🟢 Bought (partially) |
| RC transmitter + receiver | Manual control, mode switch, failsafe | ~€40-70 | 🔴 Not bought |
| Brushless motor + ESC | Propulsion | ~€20-35 | 🔴 Not bought |
| LiPo battery | Power | ~€10-20 | 🔴 Not bought |
| 5 V BEC (or AA battery holder) | Servo power supply | ~€3-8 | 🔴 Not bought |
| Propeller | Thrust | ~€2-5 | 🔴 Not bought |
| Soldering iron, solder, pin headers | Assembly | ~€25-45 | 🔴 Not bought |

**Spent so far:** € 57.00 · **Estimated remaining:** ~€100-185 

*Prices include delivery. Most parts were ordered from AliExpress.*
## Software and tools

- STM32CubeIDE, STM32CubeMX (HAL drivers)
- STM32CubeProgrammer (flashing over USB DFU)
- Python (planned: reading logs and plotting)

## Roadmap

- [x] USB virtual COM port, with `printf` output to the PC
- [x] Servo control with timer PWM (50 Hz, 1000-2000 µs pulses)
- [ ] Solder headers and move from loose wires to a proper breadboard setup
- [ ] Read the IMU over SPI (WHO_AM_I check, then raw gyro and accel data)
- [ ] Attitude estimation (complementary filter, later Madgwick/Mahony)
- [ ] Fixed-rate control loop (timer interrupt) and PID stabilisation, bench-tested
- [ ] RC receiver input, flight modes and failsafe
- [ ] Airframe build and first flights
- [ ] GPS parsing and flight logging
- [ ] Data plots and PID tuning results (Python)

## Current pin usage

| Function | Pin |
|---|---|
| Servo signal (TIM2 CH2) | PA1 |
| Status LED | PC13 |
| USB (virtual COM port) | PA11 / PA12 |

## Build and flash

1. Open the project folder in STM32CubeIDE and build it.
2. Put the board in DFU mode: hold BOOT0, tap NRST, release BOOT0.
3. Flash the `.elf` file from `Debug/` with STM32CubeProgrammer (USB).
4. Press NRST. A COM port appears; open it in a serial terminal to see the output.

## Notes

- Clock: 25 MHz crystal, PLL to 96 MHz, with 48 MHz for USB.
- The servo is currently powered from the board's 5V pin for bench testing only. The final design will use a separate regulator or battery.

## Photos and video

_Coming soon._

## What I'm learning

Timers and PWM, SPI, interrupts, sensor fusion, PID control, and debugging real hardware.
