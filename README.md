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
   git clone https://github.com/cg-/sunshine-scripts.git
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

### Automatic resolution fix during Sunshine session

Configure Sunshine to run these scripts automatically.

Do Command 1:
`kscreen-doctor output.HDMI-A-3.enable output.HDMI-A-3.primary output.DP-3.disable output.DP-1.disable`

Undo Command 1:
`kscreen-doctor output.HDMI-A-3.disable output.DP-1.enable output.DP-3.enable output.DP-1.primary output.DP-1.mode.2560x1440@180 output.DP-3.mode.1920x1080@144`

Do Command 2:
`kscreen-sunshine-fix`

This makes Sunshine trigger the correct dummy display resolution on a dummy plug and disable the other displays when a client connects, then revert when disconnect.

### Turn on Dummy Screen When Displays Off

Set up Power Management to run the dummy on script to match your displays off timer.

### Turn Screens Back On After Idle

Set up a global shortcut to run the revert script. Any ideas for a more elegant way to do this?

***

## Logging

`kscreen-sunshine-fix` records its actions to:

```
/tmp/sunshine-script.log
```

***

## Notes

- Adjust output names (`HDMI-A-3`, `DP-1`, `DP-3`) to match your system. Use `xrandr` to list available outputs.
- These scripts are designed for KDE/Nobara environments. Other desktops may require different commands.

***

## License

Released under the **MIT License**.  
