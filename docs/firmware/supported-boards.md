# Supported Boards

NRSuite provides six firmware targets.

| Board | Environment | Native USB | BLE | BadUSB / MSC | Image |
|---|---|---|---|---|---|
| ESP32-C3 DevKitM-1 | `esp32-c3` | Yes | Yes | No | `esp32c3` |
| ESP32-C5 DevKitC-1 | `esp32-c5` | Yes | Yes | No | `esp32c5` |
| ESP32-S3 DevKitC-1 | `esp32-s3` | Yes | Yes | Yes | `esp32s3` |
| ESP32-S3 N4R2 PSRAM | `esp32-s3-psram` | Yes | Yes | Yes | `esp32s3-psram` |
| ESP32-S2 Saola-1 | `esp32-s2` | Yes | No | Yes | `esp32s2` |
| ESP32 DevKit | `esp32-devkit` | External UART | Yes | No | `esp32classic` |

## ESP32-S3 PSRAM

`esp32-s3-psram` is intended for boards with 2 MB QSPI PSRAM, including
ESP32-S3 DevKitC-1 N4R2-class boards. PSRAM is used for large sniffer queues with
an internal-RAM fallback.

## ESP32-S2 exclusions

ESP32-S2 builds do not provide:

- Captive Portal
- Evil Twin
- NRuGochi

The Android app disables the corresponding cards and displays
`Not supported on ESP32-S2`.

## ESP32-C5 BLE HID

C5 BLE HID startup uses a memory guard of at least:

```text
90 KiB free heap
48 KiB largest allocatable block
```

C5 runtime memory may fall below that threshold. If it does, firmware rejects
BLE HID startup with a structured low-memory error rather than risking an
unstable session.

## Transport

Native-USB boards expose the NRSuite protocol over native USB CDC/JTAG. UART0 is
also supported, including development boards that use an external USB-UART
bridge.
