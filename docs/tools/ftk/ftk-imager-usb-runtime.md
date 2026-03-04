---
title: "Run FTK Imager from a USB Flash Drive"
slug: "ftk-imager-usb-runtime"
category: "tools"
tool: "FTK Imager"
use_case: ["triage", "collection"]
environment: ["windows"]
risk: "caution"
last_reviewed: "2026-03-03"
---

# Run FTK Imager from a USB Flash Drive

This guide shows how to set up **FTK Imager** to run from a USB flash drive on a Windows machine. This is a **runtime** setup (portable execution), not a bootable forensic environment.

## What you need

- A USB flash drive (dedicated to DFIR use is ideal)
- A Windows computer to perform the initial setup
- FTK Imager installed on that setup computer
- Admin rights on the setup computer (to access the install directory and system files)

## Goal

You will copy the FTK Imager installation folder to a USB drive so you can run FTK Imager on other Windows machines without installing it again.

## Setup steps

### 1) Install FTK Imager on a setup machine

On a machine **other than the system you want to image**, install FTK Imager normally.

### 2) Plug in the USB drive

Insert the USB drive you want to use for your portable FTK Imager setup.

### 3) Copy the FTK Imager program folder to USB

Copy the entire **FTK Imager installation folder** to the USB drive.

Common default paths:

- `C:\Program Files\AccessData\FTK Imager`
- `C:\Program Files (x86)\AccessData\FTK Imager`

Place the copied folder somewhere sensible on the USB, for example:

- `X:\Tools\FTKImager\`

(Replace `X:` with your USB drive letter.)

### 4) Copy required MFC runtime files (64-bit FTK Imager)

For **64-bit** versions of FTK Imager (version **3.4.3 and higher**), you may need additional Microsoft Foundation Class runtime files.

On the setup machine, open:

- `C:\Windows\System32\`

Find and copy these file families:

- `mfc100*`
- `mfc110*`
- `mfc120*`
- `mfc140*`

Copy them to one of the following locations on the USB:

- Preferred: the same folder as the FTK Imager executable (for example `X:\Tools\FTKImager\`)
- Alternate: the root of the USB drive (for example `X:\`)

## Verification

On a different Windows machine:

1. Plug in the USB drive.
2. Browse to your FTK Imager folder.
3. Launch the FTK Imager executable.

If FTK Imager fails to start, re-check that the MFC files were copied correctly and are accessible in the same folder as the executable.

## Notes and cautions

- **Scope and authorization:** Only image systems and media you are authorized to collect.
- **Minimize writes:** When collecting evidence, aim to reduce changes on the target system. Running tools from USB can help, but execution still creates artifacts on the host (prefetch, recent files, etc.).
- **USB hygiene:** Keep this USB dedicated to DFIR work and avoid mixing it with personal files.

## Change log

- 2026-03-03: Initial version
