# Storage and Android 16 SAF

NRSuite uses Android's **Storage Access Framework (SAF)** instead of broad
storage permissions.

## Granting access

1. Open **Settings → Storage access → Grant storage access**.
2. Select a writable folder using the system folder picker.
3. NRSuite creates and uses these subdirectories:

```text
Pcap/
Logs/
Portals/
DuckyEditor/
```

## What the directory is used for

The selected root is used for:

- PCAP captures
- log exports
- portal HTML templates
- DuckyScript files
- credential and history exports
- IR imports and learned buttons
- other user-managed files

## If access is lost

Android may revoke a persisted folder grant after a restore, provider change, or
permission reset. NRSuite detects the invalid folder and prompts you to grant
access again.

If downloads, imports, or exports fail:

1. Re-open storage settings.
2. Re-select the NRSuite root folder.
3. Verify the folder is writable.
4. Retry the operation.

The app does not request a broad storage permission, and Auto Backup is disabled.
Back up important files independently.
