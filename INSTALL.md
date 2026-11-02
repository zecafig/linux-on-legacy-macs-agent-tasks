# Installation and validation protocol

This document defines the recovery workflow for legacy Intel Macs. It is a protocol, not a device-specific command recipe. Confirm model-specific steps against the target machine before running them.

## Operating principles

- The human operator controls the machine and approves all destructive or irreversible actions.
- The agent may inspect, explain, propose commands, and interpret results. It must not execute an approved action beyond its stated scope.
- Discover disk, partition, EFI, and device identifiers immediately before use. Never copy identifiers from an example or an earlier run.
- Keep existing disk contents intact during inventory and non-destructive testing. Repartitioning, erasing, or replacing them requires explicit approval.
- Record the command, relevant output, machine identifier, OS/kernel version, and result for each test. Redact serial numbers, hardware UUIDs, MAC addresses, BSSIDs, and network names from public notes.
- Change one variable at a time. Preserve a known-good boot path when possible.

## Workflow

### 1. Identify and inventory

Record the model identifier, display, CPU, memory layout, GPU, storage, network interfaces, audio devices, and firmware. Inspect storage health and note existing symptoms. Keep identifying data private.

### 2. Prepare removable media

Select a current supported 64-bit Ubuntu image appropriate for the test. Verify its checksum and write it to removable media using a trusted method. Verify the target device before writing; writing an image destroys existing contents on that removable device.

### 3. Boot the live or installer environment

Use the Mac startup manager to boot from USB. First test whether the image boots and remains stable. Record boot messages and hardware detection. Do not start installation until disk layout and target device have been inspected and the user explicitly approves any write to internal storage.

### 4. Validate a text-only Ubuntu base

If approved, install Ubuntu without a graphical desktop. Verify bootloader behavior, storage, networking, kernel version, logs, and local or remote administration before adding a display stack. Keep a recovery path and capture the exact kernel command line.

### 5. Diagnose graphics

Record PCI IDs, loaded kernel module, firmware messages, DRM/KMS state, detected connectors and modes, native panel resolution, and renderer. Confirm whether the panel works without artifacts and whether rendering is accelerated. Do not treat software rendering as equivalent to a working accelerated desktop.

### 6. Add desktop sessions incrementally

Use XFCE with X11 as the initial desktop candidate. Establish a stable baseline before testing a Wayland compositor. Record session type, compositor, driver, kernel, resolution, artifacts, stability, and memory use for each attempt.

### 7. Verify browser support and usability

Check Google's current Chrome requirements against the installed distribution and CPU. Install from Google's official package source only when supported. Record the browser version, graphics status, memory use, and results from a small, repeatable browsing workload. Installation success alone does not establish acceptable usability.

### 8. Exercise remaining hardware

Test audio input/output, Wi-Fi, Bluetooth, camera, brightness, USB, external display, fans/temperature reporting, and suspend/resume as appropriate. Record failures and reproduce them before documenting a workaround as verified.

## Stop conditions

Stop and report before continuing if:

- The target disk or partition cannot be identified with confidence.
- The operation would modify internal storage without explicit approval.
- The machine becomes unstable, overheats, or develops new display artifacts.
- A mitigation changes boot or graphics behavior without a clear, reproducible result.

## Recording a test

For every material test, capture:

- Machine ID from `MACHINES.md`
- Date, distribution/release, kernel, firmware/boot mode, and session type
- Exact command or UI action
- Relevant output or observed behavior
- Status: supported upstream, tested here, known limitation, or not tested
- Recovery or rollback procedure, if a system change was made
