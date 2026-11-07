# Troubleshooting

> Authorized testing only.

## Device appears but commands time out

- Confirm the firmware heartbeat is arriving.
- On boards with two USB-C ports, try the other port.
- Check the reported transport:
  - `usb_cdc` — native USB CDC/JTAG
  - `uart0` — UART bridge
- Verify phone-to-ESP32 TX/RX wiring.
- Do not share UART0 with sensor or IR wiring.
- Try another USB-OTG cable or adapter.

If the app detects NRSuite heartbeat activity but the command handshake fails,
unplug/replug the ESP32 and retry. Do not reflash immediately unless the
diagnostic explicitly reports ROM boot or invalid firmware.

## No valid PING response

1. Confirm the correct firmware target and version.
2. Reconnect USB.
3. If using a CP2102/CH340 bridge, verify the correct port and wiring.
4. Check the diagnostic log.
5. Replug the board and retry.
6. If a genuine ROM boot or invalid header is reported, reflash the matching
   image.

## WiFi capture does not start

- Select an NRSuite root/output directory.
- Check the WiFi Config output path.
- Confirm no other radio mode is active.
- Confirm the selected channel is allowed by the regulatory country/channel mask.

## Target capture cannot start

- Scan Wi-Fi and select a target AP.
- Confirm the target still exists and its channel is allowed.
- Enable deauth assist only for an authorized target.

## IR does not transmit

- Check the selected backend.
- Phone IR requires a phone IR emitter.
- ESP32 IR requires configured TX/RX GPIOs and correct LED/driver wiring.
- Long or unusual signals may overflow the receiver buffer.

## Terminal SSH authentication fails

- Confirm Termux `sshd` is running:
  ```bash
  sv up sshd
  ```
- Verify the `authorized_keys` entry.
- Compare the imported key fingerprint.
- If the pinned host key changed after reinstalling Termux, review the old/new
  fingerprints before trusting the new key.

For more detail, see the [Terminal guide](android/terminal-guide.md).

## Firmware download is stuck

Current releases cancel a stalled download after 45 seconds without progress and
show a failure message. If this happens:

1. Check the internet connection.
2. Retry the download.
3. Try Wi-Fi instead of a metered or unstable connection.
