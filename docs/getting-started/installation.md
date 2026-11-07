# Installation

> Authorized testing only. Use NRSuite only on networks, devices, and
> accessories you own or have explicit written permission to test.

## Requirements

### Android

- Android 8.0 or newer
- USB-OTG support
- A compatible USB cable or OTG adapter
- An ESP32 classic, C3, C5, S2, or S3 board supported by NRSuite firmware
  (devkits and compatible SuperMini/Mini/Nano variants)

### Firmware

Use the matching firmware release:

```text
1.0.0-beta.3.2.0
```

Download it from:

<https://github.com/7wp81x/NRSuite-firmware/releases>

## Install the Android app

1. Download the latest signed APK from the
   [NRSuite Android releases](https://github.com/7wp81x/NRSuite-Android/releases).
2. Verify the SHA-256 checksum shown in the release if your download tool
   supports it.
3. Open the APK on the device and allow installation from the app or file
   manager you used.
4. Open NRSuite.
5. Choose a writable storage folder when prompted.
6. Connect the ESP32 through USB-OTG.
7. Grant USB permission when Android asks.
8. Open **Devices** and connect to the detected ESP32.

## Flash the firmware

The recommended method is the built-in **Firmware Flasher** in the app.

See [Firmware Flashing](../firmware/flashing.md) for target selection, USB
bridge notes, and manual esptool commands.

## First connection

After the firmware is flashed:

1. Reconnect the ESP32.
2. Grant USB permission.
3. Wait for the device to appear in **Devices**.
4. Connect and wait for the status information to load.
5. Confirm the firmware version and active transport are displayed.

If the handshake fails but the device is producing NRSuite heartbeats,
unplug/replug the device and retry before flashing again.

## Updating

Install a newer APK over the existing app. Do not uninstall first if you want to
keep local data.

Android Auto Backup is disabled, so keep an independent backup of captures,
credentials, wordlists, portal templates, terminal keys, and other important
files.

For firmware, flash the matching merged image through the app or esptool.
Firmware updates are full-image USB reflashes; OTA firmware updates are not
provided.
