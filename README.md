# ZMK Corne Config

This repository contains a ZMK configuration for a split Corne using a `PinMicro NRF52840` controller.

## Why There Is A Custom Board

Using the upstream `nice_nano` board directly was only partially successful on this hardware:

- `nice_nano` could bring up the OLED, but BLE behavior was inconsistent on the current ZMK stack.
- `nice_nano//zmk` gave working BLE, but the OLED stopped working again.

The controller in this kit is not an actual `nice!nano`, so the final working setup uses a custom board:

- [build.yaml](/Users/alexeyyashin/Developer/zmk-config/build.yaml)
- [boards/arm/pinmicro_nrf52840/pinmicro_nrf52840.dts](/Users/alexeyyashin/Developer/zmk-config/boards/arm/pinmicro_nrf52840/pinmicro_nrf52840.dts)
- [boards/arm/pinmicro_nrf52840/pinmicro_nrf52840_defconfig](/Users/alexeyyashin/Developer/zmk-config/boards/arm/pinmicro_nrf52840/pinmicro_nrf52840_defconfig)

## What Was Customized

- A local board definition `pinmicro_nrf52840` was added under [boards/arm/pinmicro_nrf52840](/Users/alexeyyashin/Developer/zmk-config/boards/arm/pinmicro_nrf52840).
- The board keeps the `Pro Micro`-style pin mapping expected by the Corne shield.
- BLE and USB are enabled at the board level so the keyboard works normally on the current ZMK `main`.
- Battery reporting uses `zmk,battery-nrf-vddh`, which matches this controller better than the earlier ADC-divider attempt.
- The board intentionally does not add the `EXT_POWER` behavior from the upstream `nice_nano//zmk` variant, because that combination caused the OLED to stop working on this hardware.

## Current Working State

- BLE works
- OLED works
- Battery percentage works
- Standard Corne keymap works

## Main User Config Files

- [config/corne.conf](/Users/alexeyyashin/Developer/zmk-config/config/corne.conf)
- [config/corne.keymap](/Users/alexeyyashin/Developer/zmk-config/config/corne.keymap)
- [config/west.yml](/Users/alexeyyashin/Developer/zmk-config/config/west.yml)
- [.github/workflows/build.yml](/Users/alexeyyashin/Developer/zmk-config/.github/workflows/build.yml)
