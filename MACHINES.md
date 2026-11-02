# Machine inventory

This file tracks non-sensitive hardware identity and the state of each recovery. Keep serial numbers, hardware UUIDs, MAC addresses, BSSIDs, Wi-Fi names, and personal data out of this file and all public logs.

## IMAC9-1-EARLY-2009-24

**Status:** Inventory started; Linux not yet installed.

### Hardware

- Model: Apple iMac (Early 2009), 24-inch
- Model identifier: `iMac9,1`
- Display: internal LCD, 1920 × 1200
- CPU: Intel Core 2 Duo, 2.66 GHz, two cores, 6 MB shared L2 cache
- RAM: 4 GB DDR3-1067, two 2 GB SO-DIMMs; Apple lists maximum supported memory as 8 GB
- GPU: NVIDIA GeForce 9400M, dynamically allocated/shared video memory (up to 256 MB)
- Storage: Kingston SV300S37A120G SATA SSD, approximately 120 GB
- Wireless: Broadcom BCM43xx adapter
- Audio hardware: built-in microphone, line input, and internal speakers

### Still to inspect

- Exact PCI IDs and Linux driver for the GPU and wireless adapter
- Linux boot mode and EFI/bootloader behavior
- Storage SMART attributes and test results under Linux
- Bluetooth, camera, brightness, external display, fans/temperature, and suspend/resume under Linux
- Ubuntu release and kernel selected for the installation
- X11/XFCE, Wayland, and current Chrome behavior

### Evidence source

Initial hardware values were inventoried before Linux installation. Keep any supporting output private if it contains identifying data. Add dated Linux observations as the recovery proceeds.
