---
title: hourglass-led-clock
status: in progress
date: "2025 –"
tagline: "A sand simulation hourglass clock — old concept, new hardware. Custom PCB · STM32U073 · dual LED matrices · battery powered."
tags:
  - STM32U073
  - KiCad 9
  - IS31FL3733B
  - TPS61022
  - BQ24232
  - LP5912
  - USB CDC
  - I2C
  - IMU wake
  - JLCPCB
github: "#"
hasSim: true
---

## overview

The hourglass clock reimagines a centuries-old timekeeping metaphor using a sand particle simulation running on a microcontroller. Two circular LED matrices sit at the top and bottom of an hourglass form — sand pixels fall from the upper matrix to the lower one, and the rate of fall tracks real time.

The whole thing runs on a single custom PCB — my first PCB design — built around the STM32U073 for its low power profile and native USB support. It charges over USB-C, runs for hours on battery, and wakes from sleep when you pick it up.

## challenges

### display driver selection

Finding a driver IC that could handle a full circular LED matrix without excessive external components was harder than expected. After evaluating several options, the IS31FL3733B emerged as the right fit — it supports up to 144 LEDs per IC over I2C, handles PWM dimming in hardware, and two of them can be chained to drive both matrices independently.

### power architecture

Running LEDs, a microcontroller, and an IMU from a single LiPo cell required careful power sequencing. The solution uses a TPS61022 boost converter to supply the LED matrices, an LP5912 LDO for clean MCU power, and a BQ24232 for USB-C battery charging — each stage isolated so the LEDs can't pull noise into the MCU rail.

### learning PCB design from scratch

This is my first custom PCB. Every decision — layer stackup, component placement, trace width, decoupling strategy — required research and iteration. Working in KiCad 9 and targeting JLCPCB for fabrication added real constraints that pushed the design toward something manufacturable rather than just functional on paper.

## build status

- done: sand simulation firmware complete
- done: schematic complete
- active: PCB layout — in progress
- todo: fabrication & assembly
- todo: hardware bring-up & testing