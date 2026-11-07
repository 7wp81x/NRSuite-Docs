# Firmware Flashing

> Authorized testing only. Flash only hardware you own or are explicitly
> authorized to modify.

All NRSuite release images are **merged full-flash binaries** and must be written
at offset `0x0`.

## Recommended: flash from the Android app

1. Open **Firmware Flasher** in NRSuite.
2. Connect the ESP32 through USB-OTG.
3. Grant USB permission.
4. Select the matching target:
   - ESP32 — classic ESP32 and compatible Mini/Nano-style boards
   - ESP32-C3 — devkits and C3 SuperMini/Mini/Nano variants
   - ESP32-C5 — C5 devkits and compatible compact variants
   - ESP32-S2 — S2 devkits and S2 Mini/Nano variants
   - ESP32-S3 — S3 boards without PSRAM
   - ESP32-S3 (PSRAM) — S3 boards with 2 MB QSPI PSRAM
5. Download the matching release image or select a local `.bin`.
6. Start flashing.
7. Follow progress in the in-app notification.
8. If the ROM bootloader does not respond, follow the on-screen BOOT/RESET
   recovery instructions.

## Manual esptool

Example for ESP32-C3:

```bash
esptool.py --chip esp32c3 --port /dev/ttyACM0 \
  write_flash 0x0 NRSuite-1.0.0-beta.3.2.0-esp32c3.bin
```

Replace `--chip` and the filename for your board.

| Firmware target | Example boards | Chip argument |
|---|---|---|
| ESP32-C3 | DevKitM-1, C3 SuperMini/Mini/Nano | `esp32c3` |
| ESP32-C5 | DevKitC-1 and compatible compact C5 boards | `esp32c5` |
| ESP32-S3 | DevKitC-1, S3 SuperMini/Mini/Nano without PSRAM | `esp32s3` |
| ESP32-S3 PSRAM | N4R2-class and PSRAM-equipped S3 boards | `esp32s3` |
| ESP32-S2 | Saola-1, S2 Mini/Nano | `esp32s2` |
| Classic ESP32 | DevKit, WROOM, NodeMCU, Mini/Nano-style | `esp32` |

The C5 bootloader is included at `0x2000` inside the merged image, but the image
itself is written at `0x0`.

## Before flashing

Back up custom wordlists, portal templates, captures, and other device-side
storage. Partition layouts vary by target.

## USB-UART bridge notes

Classic ESP32 boards require an external CP2102, CH340, or FTDI USB-UART bridge.
Some compact C3/C5/S2/S3 boards also expose only a UART bridge or both native USB
and UART ports.
If flashing or connecting fails:

- Confirm TX/RX crossover and common ground.
- Try the other USB port on boards with both native USB and UART.
- Hold BOOT, tap RESET, then retry if the ROM bootloader is not reached.
- Replug the device if Windows or Android re-enumerates the USB device.

## After flashing

1. Reconnect the board.
2. Confirm the firmware version in the app.
3. Check the active transport in device details.
4. Run a basic PING/status check before starting active modules.
