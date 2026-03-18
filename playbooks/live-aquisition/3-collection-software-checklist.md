# Collection Software Checklist

**Use case:** tool readiness | field collection capability | lab review support  
**Environment:** windows | macos | linux | mixed forensic workflows  
**Risk:** caution  

> **Caution:** Software readiness includes both collection and follow-on review capability. Capturing an artifact in the field is only half the job. The team should already know how it will validate, mount, parse, and review that artifact back in the lab.

---

## Purpose

This checklist identifies specific software categories, recommended utilities, and practical alternatives that should be staged before conducting rapid evidence collection. It covers both **field collection** and **lab-side review**, because a toolset is incomplete if it can acquire evidence that no one is prepared to examine later. :contentReference[oaicite:0]{index=0}

---

## Readiness philosophy

A good collection stack should answer two questions before deployment:

1. **Can we collect the artifact in the field?**
2. **Can we do something useful with it in the lab?**

That means the software kit should be built in pairs whenever possible:
- memory capture + memory analysis
- disk image acquisition + image mounting/review
- artifact collection + artifact parsing
- log export + log review
- browser extraction + browser review :contentReference[oaicite:1]{index=1}

---

## Core software categories

A prepared software stack should usually cover:

1. Documentation and notes
2. Live system information collection
3. Memory acquisition
4. Memory analysis
5. Targeted artifact collection
6. Disk and logical imaging
7. Image mounting and review
8. Browser and user-activity review
9. Hashing and integrity validation
10. Network review
11. Timeline / artifact parsing
12. Full case review in the lab

---

## 1. Documentation and notes

### Recommended
- Plain text editor for field notes
- Spreadsheet or template-ready note sheet for collection logs
- PDF export capability for final packaging notes
- Screenshot utility when policy allows

### Why this matters
These support:
- initial scene documentation
- collection logs
- artifact inventory
- hash record tracking
- handoff notes

This category is not glamorous, but it is the difference between “forensically sound” and “I swear I had a reason for that filename.”

---

## 2. Live system information collection

### Recommended categories
- system info tools
- process listing tools
- service listing tools
- session / logged-in user enumeration
- network connection review
- mounted drive review
- command-history access where appropriate

### Strong practical option
- **KAPE** for rapid triage collection and parsing workflows. Kroll describes KAPE as a way to find, collect, and process forensically useful artifacts quickly, including collecting key artifacts before imaging. :contentReference[oaicite:2]{index=2}

### Why this matters
This category supports fast preservation of:
- host context
- user context
- execution context
- targeted forensic artifacts before the machine state changes

---

## 3. Memory acquisition

This is the category where you do not want to be improvising in the field.

### Recommended primary option
- **Belkasoft RAM Capturer**
  - Belkasoft describes it as a free, portable RAM acquisition tool for Windows, with separate 32-bit and 64-bit builds and support for dumping the full contents of volatile memory. Belkasoft also states it is designed to work even against some anti-debugging or anti-dumping protections. :contentReference[oaicite:3]{index=3}

### Recommended alternatives
- **Magnet RAM Capture**
  - Magnet describes it as a free memory imaging tool for capturing physical memory from a suspect computer so investigators can recover artifacts often only found in RAM. :contentReference[oaicite:4]{index=4}
- **WinPmem**
  - The Velocidex project describes WinPmem as an open-source physical memory acquisition tool for Windows with multiple reading methods. :contentReference[oaicite:5]{index=5}

### Why memory capture matters
RAM may preserve:
- fileless malware artifacts
- injected code
- active network state
- decrypted content
- process state
- tokens or active sessions
- volatile evidence that vanishes after shutdown :contentReference[oaicite:6]{index=6}

### Practical recommendation
If you want a default answer for a Windows field USB, **Belkasoft RAM Capturer** is a very reasonable primary pick, with **Magnet RAM Capture** or **WinPmem** as secondary options depending on your environment and comfort level. :contentReference[oaicite:7]{index=7}

---

## 4. Memory analysis

You are exactly right that collection without analysis capability is half a toolbox.

### Recommended primary option
- **Volatility 3**
  - The Volatility Foundation describes Volatility 3 as its modern memory forensics framework, and its GitHub project describes it as a widely used framework for extracting digital artifacts from volatile memory samples. The Foundation also announced official parity with Volatility 2 for modern investigations in 2025. :contentReference[oaicite:8]{index=8}

### Recommended commercial / integrated options
- **Belkasoft X / Belkasoft Evidence Center**
  - Belkasoft states its platform can analyze RAM dumps acquired with Belkasoft RAM Capturer. :contentReference[oaicite:9]{index=9}
- **Magnet AXIOM**
  - Magnet provides material on reviewing RAM captures with AXIOM. :contentReference[oaicite:10]{index=10}

### Why this matters
Memory analysis tooling supports review of:
- suspicious processes
- loaded modules / DLLs
- command execution traces
- network artifacts
- injected or hidden code
- evidence that may not exist on disk anymore :contentReference[oaicite:11]{index=11}

### Practical recommendation
For a serious lab baseline, **Volatility 3** should be in the stack even if you also own commercial suites. It is the flashlight everyone should have before buying more lasers. :contentReference[oaicite:12]{index=12}

---

## 5. Targeted artifact collection

### Recommended primary option
- **KAPE**
  - KAPE is particularly strong here because it is built to target and collect high-value forensic artifacts quickly, and its companion target/module ecosystem is extensive. Official KAPE target and module repositories include browser artifacts, evidence-of-execution artifacts, and many Eric Zimmerman tool integrations. :contentReference[oaicite:13]{index=13}

### Good companion ecosystem
- **Eric Zimmerman tools**
  - Eric Zimmerman’s toolset is widely used for artifact parsing, and the official documentation/download hub and repositories cover tools for LNKs, SQLite, SRUM, registry parsing, and more. :contentReference[oaicite:14]{index=14}

### Why this matters
This category helps with:
- recent activity
- evidence of execution
- browser artifacts
- user profile artifacts
- removable media traces
- targeted triage before full imaging :contentReference[oaicite:15]{index=15}

### Practical recommendation
For Windows-heavy rapid collection, **KAPE + Eric Zimmerman tools** is one of the strongest combos you can stage ahead of time. :contentReference[oaicite:16]{index=16}

---

## 6. Disk and logical imaging

### Recommended primary option
- **FTK Imager**
  - Exterro describes FTK Imager as a free preview and imaging tool used to acquire electronic evidence in a forensically sound manner by creating copies of data and generating hash reports. :contentReference[oaicite:17]{index=17}

### Expanded option
- **FTK Imager Pro**
  - Exterro says the Pro edition adds features such as encryption detection/decryption and direct decrypted live data workflows. :contentReference[oaicite:18]{index=18}

### Why this matters
This category supports:
- logical acquisition
- image creation
- quick preview before deeper processing
- hash-supported acquisition workflows :contentReference[oaicite:19]{index=19}

### Practical recommendation
If you want one imaging utility on the field media almost by default, **FTK Imager** is still a very sensible baseline.

---

## 7. Image mounting and review

### Recommended primary option
- **Arsenal Image Mounter**
  - Arsenal states that AIM mounts disk images as complete disks in Windows and supports features such as Disk Manager integration, BitLocker-protected volume handling, Volume Shadow Copy mounting, and launching virtual machines from disk images. :contentReference[oaicite:20]{index=20}

### Why this matters
This category is huge for lab work because it allows you to:
- mount and inspect acquired images quickly
- work with BitLocker-protected material
- access VSCs
- validate what you actually acquired
- move from acquisition into review without heroic nonsense :contentReference[oaicite:21]{index=21}

### Practical recommendation
If your lab handles Windows images regularly, **Arsenal Image Mounter** is one of the most useful “why didn’t we stage this sooner?” tools.

---

## 8. Browser and user-activity review

### Lightweight quick-look option
- **BrowsingHistoryView**
  - NirSoft describes it as a utility that reads history data from multiple browsers and can display browsing history from local systems and external drives. :contentReference[oaicite:22]{index=22}

### Focused browser option
- **ChromeHistoryView**
  - NirSoft describes it as a utility for viewing Chrome browser history with details including URL, title, visit time, typed count, and referrer. :contentReference[oaicite:23]{index=23}

### Heavier options
- **KAPE targets + Eric Zimmerman tools**
- **Autopsy**
  - Autopsy is described by Sleuth Kit Labs as an end-to-end open-source digital forensics platform, and the Sleuth Kit site describes it as a GUI-based platform used by law enforcement, military, and corporate examiners. :contentReference[oaicite:24]{index=24}

### Why this matters
Browser review helps preserve or analyze:
- access to phishing or staging sites
- downloads
- search activity
- portal logins
- user navigation around an incident window :contentReference[oaicite:25]{index=25}

---

## 9. Hashing and integrity validation

### Required capability
Whatever stack you choose, it should include:
- file hashing
- manifest generation
- integrity validation after transfer

### Why this matters
Hashing supports:
- evidentiary defensibility
- transfer validation
- repeatability
- confidence that the lab is examining what the field actually collected

This category is not optional. It is the adult supervision.

---

## 10. Network review

### Recommended option
- **Wireshark**
  - Wireshark describes itself as the world’s leading network protocol analyzer, supporting live capture and offline analysis across many platforms. The documentation also notes Windows installs include Npcap for packet capture. :contentReference[oaicite:26]{index=26}

### Why this matters
Network tooling supports:
- packet review
- quick pcap validation
- exfil review support
- protocol-level inspection when captures are available :contentReference[oaicite:27]{index=27}

### Practical recommendation
Even if you are not doing full packet forensics every day, **Wireshark** belongs in the lab stack.

---

## 11. Full case review in the lab

### Recommended open-source option
- **Autopsy**
  - Autopsy supports case-based review and multiple data sources, including disk images and logical files. :contentReference[oaicite:28]{index=28}

### Recommended commercial options already mentioned
- **Belkasoft X / Evidence Center**
