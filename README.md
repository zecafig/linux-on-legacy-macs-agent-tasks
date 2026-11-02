# Linux on Legacy Macs — Agent-Assisted Recovery Playbook

> Give older Intel Macs a useful life with a current Linux operating system.
>
> A human-controlled, AI-agent-assisted installation and hardware QA playbook for legacy Macs.

This repository documents the recovery of older Intel Macs using current Linux distributions, kernels, and applications. It records the process machine by machine: what was inspected, what was attempted, what worked, what failed, and what remains unknown.

The first target is an Early 2009 24-inch iMac (`iMac9,1`) with an Intel Core 2 Duo and 4 GB of RAM. Its initial hardware inventory is recorded below.

This project complements [linux-on-t2-mac-agent-tasks](https://github.com/zecafig/linux-on-t2-mac-agent-tasks), which documents a separate Linux recovery and QA journey for a Mac with Apple T2 hardware. Procedures and results are not assumed to transfer between generations.

## Project philosophy

The human remains in control. The agent can inspect, explain, propose commands, and interpret results. It must not execute destructive or irreversible operations without the user's explicit confirmation.

For destructive or irreversible operations:

1. Inspect the current state.
2. Show the relevant output.
3. Explain the proposed change and its consequences.
4. Ask for explicit confirmation.
5. Execute only the approved action.
6. Verify the result.
7. Stop if verification fails.

The guiding workflow is:

> Inspect → interpret → show → confirm → act → verify

Discover device names, partition identifiers, mount points, firmware settings, and paths at runtime. Do not hard-code values that can be safely discovered.

## Evidence categories

Every compatibility claim should be labeled as one of the following:

- **Supported upstream** — documented or supported by the relevant upstream project.
- **Tested here** — exercised on the specific Mac and configuration described.
- **Known limitation** — a failure reproduced on that configuration.
- **Not tested** — left open rather than inferred from another Mac.

A successful boot alone does not mean that graphics acceleration, audio, networking, suspend, or the browser experience is working correctly.

## Initial target

### Initial hardware inventory

- Apple iMac (Early 2009), 24-inch, model identifier `iMac9,1`
- Intel Core 2 Duo at 2.66 GHz, two cores, 6 MB shared L2 cache
- 4 GB DDR3-1067 RAM, installed as 2 × 2 GB; Apple lists support up to 8 GB
- NVIDIA GeForce 9400M, up to 256 MB dynamically allocated/shared video memory
- Internal LCD at 1920 × 1200 native resolution
- Kingston SV300S37A120G SATA SSD, approximately 120 GB
- Broadcom BCM43xx Wi-Fi adapter
- Built-in microphone, line input, and internal speakers

The initial inventory resolves the model, display, and GPU identity. Linux driver behavior and native-resolution output remain untested. Keep serial numbers, hardware UUIDs, MAC addresses, BSSIDs, and network names out of public logs and documentation.

## Current recovery status

On 2026-11-02, the iMac booted from the Ubuntu Server 26.04.1 LTS amd64 USB and reached the installer's language-selection screen. The USB image was read back and matched the downloaded ISO. This confirms boot to the text installer; installation has not started, and no Linux hardware support beyond this boot has been established.

### Project goals

- Start with an Ubuntu minimal or server installation without a graphical desktop, so boot and basic hardware can be evaluated independently of the graphics stack.
- Use a current, supported 64-bit Linux kernel and userspace compatible with the CPU and installed GPU.
- Evaluate X11 and Wayland only after establishing reliable graphics modesetting and acceleration.
- Consider XFCE as a lightweight desktop, with X11 as the initial graphical baseline if the hardware supports it.
- Verify that the current Google Chrome release can be installed and launched on the chosen supported Linux distribution.
- Document actual usability with 4 GB RAM and a small number of browser tabs.
- Preserve the existing disk contents during inventory and non-destructive testing. Any decision to repartition, erase, or replace them requires a separate explicit confirmation.

These are goals, not compatibility claims. In particular, the GPU and internal panel must be tested before deciding whether an accelerated desktop session is practical.

## Recovery workflow

### 1. Record hardware inventory

Record the exact model identifier, CPU, memory, GPU, display, storage, network interfaces, audio devices, and firmware version. Check storage health where possible. Keep identifying details such as serial numbers out of public notes.

### 2. Boot and inspect Ubuntu without installing

Use a current Ubuntu image and first determine whether the Mac can boot it reliably. Capture boot messages, identify the detected devices, and confirm that the installer or live environment does not alter the internal disk. Test keyboard, USB, Ethernet or Wi-Fi, audio, and display behavior.

### 3. Install a text-only base, if approved

Install Ubuntu without a desktop environment. Confirm the bootloader path, kernel version, network access, storage layout, and remote or local console access before adding graphical packages.

### 4. Establish graphics behavior

Record the GPU PCI ID, kernel driver, firmware messages, DRM/KMS state, available modes, and whether rendering is hardware-accelerated. Test the internal panel at native resolution and document any artifacts, split-screen output, blanking, or boot regressions. Change one variable at a time and retain a known-good boot entry where possible.

### 5. Add a desktop environment

Evaluate XFCE with X11 as a baseline, then evaluate a Wayland session separately if the driver and compositor support the hardware adequately. Record memory use, stability, display behavior, and any differences in browser performance.

### 6. Verify Chrome and normal use

Install Chrome from Google's official Linux package source only if the selected distribution and CPU meet Google's current requirements. Record the Chrome version, graphics settings, memory use, and results from a modest browsing workload. Do not infer that a current browser will be responsive simply because it installs successfully.

### 7. Exercise the remaining hardware

Test audio input and output, Wi-Fi, Bluetooth, camera, brightness, sleep and wake, fans and temperature reporting, external display output, USB, and any other hardware that matters for the intended use.

## Documentation

As the recovery progresses, this repository is expected to grow to include:

- `INSTALL.md` — the human-controlled installation protocol and task sequence.
- `MACHINES.md` — machine inventory and configuration identifiers.
- `TESTED.md` — evidence-based compatibility matrix per Mac.
- `TROUBLESHOOTING.md` — reproduced failures, diagnostics, and verified mitigations.
- Per-machine notes where results differ across model identifiers or GPU variants.

Until those files exist, the README describes the project scope and the initial target; it is not an installation recipe.

## Scope and attribution

This is an independent field guide. It is not an official Apple or Ubuntu project and does not replace the documentation of Linux distributions, kernel projects, bootloader projects, or hardware vendors. Product names and trademarks belong to their respective owners.

The existing [T2 Mac playbook](https://github.com/zecafig/linux-on-t2-mac-agent-tasks) is a related project, not a source of assumed compatibility for non-T2 Macs.
