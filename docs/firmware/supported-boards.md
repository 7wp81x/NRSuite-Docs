# Supported Boards

NRSuite firmware is chip-family based rather than tied to one specific devkit.
The same firmware target can run on devkits and compact **SuperMini**, **Mini**,
and **Nano**-style boards using the same ESP32 family.

Board names and pin layouts vary by manufacturer. Choose the target by:

1. MCU family: ESP32, C3, C5, S2, or S3.
2. Flash size: the release layout targets **4 MB flash**.
3. PSRAM: choose `esp32-s3-psram` only when the S3 board has 2 MB QSPI PSRAM.
4. USB transport: native USB CDC/JTAG or an external UART bridge.

## Target selection

| MCU / board family | Example boards | Environment | Native USB | BLE | BadUSB / MSC | Release image |
|---|---|---|---|---|---|---|
| ESP32-C3 | DevKitM-1, C3 SuperMini, C3 Mini, C3 Nano | `esp32-c3` | Usually | Yes | No | `esp32c3` |
| ESP32-C5 | DevKitC-1, compatible C5 Mini/Nano variants | `esp32-c5` | Usually | Yes | No | `esp32c5` |
| ESP32-S3, no PSRAM | DevKitC-1, S3 SuperMini, S3 Mini, S3 Nano | `esp32-s3` | Yes | Yes | Yes | `esp32s3` |
| ESP32-S3 with 2 MB PSRAM | N4R2-class DevKitC-1, PSRAM-equipped S3 variants | `esp32-s3-psram` | Yes | Yes | Yes | `esp32s3-psram` |
| ESP32-S2 | Saola-1, S2 Mini, S2 Nano | `esp32-s2` | Yes | No | Yes | `esp32s2` |
| Classic ESP32 | DevKit, WROOM, NodeMCU, Mini/Nano-style boards | `esp32-devkit` | External UART bridge | Yes | No | `esp32classic` |

> Compact boards may expose USB through native USB, a USB-UART bridge, or both.
> Verify which USB port is connected and check the active transport in the app.

## Is my board supported?

A board is usually compatible when:

- It uses one of the supported ESP32 MCU families.
- It has at least **4 MB flash**.
- It exposes USB serial through native USB or a UART bridge supported by Android.
- Any required PSRAM-specific image is selected for S3 PSRAM boards.

Boards with more than 4 MB flash can still run the 4 MB release layout, but the
extra flash is not used by the current release images.

## ESP32-S3 PSRAM

`esp32-s3-psram` is intended for S3 boards with **2 MB QSPI PSRAM**, including
ESP32-S3 DevKitC-1 N4R2-class boards and PSRAM-equipped SuperMini/Mini/Nano
variants.

PSRAM is used for large sniffer queues with an internal-RAM fallback. Boards
without PSRAM must use the regular `esp32-s3` target.

## ESP32-S2 exclusions

ESP32-S2 builds do not provide:

- Captive Portal
- Evil Twin
- NRuGochi

The Android app disables the corresponding cards and displays
`Not supported on ESP32-S2`.

ESP32-S2 also has no BLE radio. BadUSB, MSC, WPS, IR, and other supported S2
features remain available.

## ESP32-C5 BLE HID

C5 BLE HID startup uses a memory guard of at least:

```text
90 KiB free heap
48 KiB largest allocatable block
```

C5 runtime memory may fall below that threshold. If it does, firmware rejects
BLE HID startup with a structured low-memory error rather than risking an
unstable session.

## GPIO and peripheral wiring

GPIO numbers are board-specific. Before using IR, LD2450, PN532, or other
peripheral features, configure the pins in the relevant App category or
**Settings** screen. Use the firmware-provided safe GPIO choices and avoid pins
used by USB, flash, boot strapping, or the UART command link.

## Transport

Native-USB boards expose the NRSuite protocol over native USB CDC/JTAG. UART0 is
also supported, including classic ESP32 boards and compact boards that use an
external CP2102, CH340, or FTDI bridge.
