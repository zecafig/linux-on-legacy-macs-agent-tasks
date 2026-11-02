# Compatibility and QA matrix

Statuses describe evidence for a specific machine, not an entire model family.

Status vocabulary:

- **Supported upstream** — documented by the relevant upstream project.
- **Tested here** — exercised on the identified machine/configuration.
- **Known limitation** — a failure reproduced on that machine.
- **Not tested** — no result yet; do not infer from another Mac.

## IMAC9-1-EARLY-2009-24

| Area | Hardware baseline | Linux status |
|---|---|---|
| USB boot and installer | Ubuntu Server 26.04.1 LTS amd64 image, read-back verified | **Tested here (2026-11-02):** boots to installer language selection; installation not started |
| Model, CPU, memory | `iMac9,1`; Core 2 Duo 2.66 GHz; 4 GB DDR3 | Not tested |
| Internal display | 1920 × 1200 | Installer language screen visible; native resolution and graphics acceleration not verified |
| GPU | NVIDIA GeForce 9400M, up to 256 MB shared/dynamic memory | Driver, modesetting, acceleration, and panel stability not tested |
| Storage | Kingston SATA SSD, approximately 120 GB | Internal disk detection, read/write, and Linux SMART attributes not tested |
| Wi-Fi | Broadcom BCM43xx adapter | Driver, firmware, and throughput not tested |
| Audio | Internal microphone, line input, and speakers | Not tested |
| Bluetooth, camera, brightness | Not recorded | Not tested |
| USB, external display | Not recorded | Not tested |
| Suspend/resume, thermals | Not recorded | Not tested |
| X11 with XFCE | Not tested | Not tested |
| Wayland | Not tested | Not tested |
| Current Google Chrome | Browser support and usability not evaluated | Linux compatibility and usability not tested |

Update this table only with observations tied to a date, OS/release, kernel, and the tested machine. Link detailed failures and mitigations from `TROUBLESHOOTING.md`.
