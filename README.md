# Sunshine Scripts for Nobara Linux

A collection of helper scripts for managing **Sunshine** display configurations on **Nobara Linux** using `kscreen-doctor` and `xrandr`.  
These scripts simplify display handling for headless setups, virtual monitors, and restoring your normal desktop configuration.

***

## Overview

| Script | Description |
|--------|--------------|
| **kscreen-dummy-on** | Enables a dummy HDMI display (`HDMI-A-3`) and disables physical monitors (`DP-1`, `DP-3`). Ideal when using Sunshine without an attached screen. |
| **kscreen-dummy-revert** | Re-enables physical monitors and disables the dummy HDMI output. |
| **kscreen-sunshine-fix** | Automatically sets the dummy display resolution based on Sunshine client parameters (`SUNSHINE_CLIENT_WIDTH`, `SUNSHINE_CLIENT_HEIGHT`, `SUNSHINE_CLIENT_FPS`) and logs the results to `/tmp/sunshine-script.log`. |

***

## Requirements

- Nobara Linux (or another KDE Plasma–based distro)
- `kscreen-doctor`
- `xrandr`
- [Sunshine](https://github.com/LizardByte/Sunshine)

***

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/<your-username>/sunshine-scripts.git
   cd sunshine-scripts
   ```

2. Make the scripts executable:

   ```bash
   chmod +x kscreen-dummy-on kscreen-dummy-revert kscreen-sunshine-fix
   ```

3. (Optional) Install them system-wide:

   ```bash
   sudo cp kscreen-* /usr/local/bin/
   ```

***

## Usage

### Enable dummy HDMI output

```bash
kscreen-dummy-on
```

### Revert to normal local display

```bash
kscreen-dummy-revert
```

### Automatic resolution fix during Sunshine session

Configure Sunshine to run these scripts automatically.

When editing your Sunshine `config.json` or using its Web UI, set:

```
"on_connection_start": "/path/to/kscreen-sunshine-fix",
"on_connection_end": "/path/to/kscreen-dummy-revert"
```

This makes Sunshine trigger the correct dummy display resolution when a client connects.

***

## Logging

`kscreen-sunshine-fix` records its actions to:

```
/tmp/sunshine-script.log
```

To monitor the log:

```bash
tail -f /tmp/sunshine-script.log
```

***

## Example Workflow

1. Start Sunshine on your Nobara system.  
2. Enable the dummy HDMI display: `kscreen-dummy-on`  
3. Connect with Moonlight — the resolution will auto-adjust.  
4. When finished, revert using: `kscreen-dummy-revert`

***

## Notes

- Adjust output names (`HDMI-A-3`, `DP-1`, `DP-3`) to match your system. Use `xrandr` to list available outputs.
- These scripts are designed for KDE/Nobara environments. Other desktops may require different commands.

***

## License

Released under the **MIT License**.  
