---
title: "Volatility: Most Useful Commands"
slug: "volatility-useful-commands"
category: "tools"
tool: "Volatility"
use_case: ["triage", "analysis"]
environment: ["windows", "linux"]
risk: "safe"
last_reviewed: "2026-03-03"
---

# Volatility: Most Useful Commands

A practical “I actually use these” command list for Volatility, with placeholders you can swap quickly during triage.

## Conventions used below

- Memory image: `mem.raw`
- Volatility 2 profile: `Win7SP1x64` (replace with the correct profile for your image)
- Output folders:
  - Dumps: `./dumps`
  - Registry hives: `./hives`

---

## Five-command mini-workflow

If you only run a few commands first, these usually give the fastest signal:
```
imageinfo (Vol2) or windows.info (Vol3)
pslist
pstree
cmdline
netscan
```

## Volatility 2 (vol.py) high-value commands
### Image identification and baseline

```bash
# Identify likely profile (starting point)
vol.py -f mem.raw imageinfo

# Basic process listing (baseline)
vol.py -f mem.raw --profile=Win7SP1x64 pslist

# Process tree (quick context)
vol.py -f mem.raw --profile=Win7SP1x64 pstree

# Cross-view process check (find hidden/weird)
vol.py -f mem.raw --profile=Win7SP1x64 psxview

# Command lines (often gold)
vol.py -f mem.raw --profile=Win7SP1x64 cmdline
Network and module/service baselines
# Network connections (commonly used on Win7+)
vol.py -f mem.raw --profile=Win7SP1x64 netscan

# List loaded kernel modules (drivers baseline)
vol.py -f mem.raw --profile=Win7SP1x64 modules

# Scan for kernel modules (find unlinked)
vol.py -f mem.raw --profile=Win7SP1x64 modscan

# Services list (baseline + anomalies)
vol.py -f mem.raw --profile=Win7SP1x64 svcscan
Process investigation and dumping
# DLLs loaded by a process
vol.py -f mem.raw --profile=Win7SP1x64 dlllist -p <PID>

# Suspicious injected code regions (triage)
vol.py -f mem.raw --profile=Win7SP1x64 malfind -p <PID> --dump-dir ./dumps

# Dump a process (when you need the executable sample)
vol.py -f mem.raw --profile=Win7SP1x64 procdump -p <PID> --dump-dir ./dumps

# Dump a specific DLL from a process
vol.py -f mem.raw --profile=Win7SP1x64 dlldump -p <PID> -b <BASE_ADDR> --dump-dir ./dumps
Registry (memory-resident) basics
# Registry hives present in memory
vol.py -f mem.raw --profile=Win7SP1x64 hivelist

# Dump a registry hive to disk
vol.py -f mem.raw --profile=Win7SP1x64 dumpregistry -o <HIVE_OFFSET> --dump-dir ./hives
Volatility 3 (vol) high-value commands
Identification and baseline
# OS and kernel info (sanity check)
vol -f mem.raw windows.info

# Processes
vol -f mem.raw windows.pslist

# Process tree
vol -f mem.raw windows.pstree

# Hidden/anomalous processes (cross-view)
vol -f mem.raw windows.psxview

# Command lines
vol -f mem.raw windows.cmdline
Network, modules, services
# Network artifacts (availability varies by image/OS)
vol -f mem.raw windows.netscan

# Services
vol -f mem.raw windows.svcscan
Deeper per-process inspection
# DLL list per process
vol -f mem.raw windows.dlllist --pid <PID>

# Handles (file/registry/mutex clues)
vol -f mem.raw windows.handles --pid <PID>
Registry basics
# Registry hives
vol -f mem.raw windows.registry.hivelist
