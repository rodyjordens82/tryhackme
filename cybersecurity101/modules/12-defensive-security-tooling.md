# Malware Analysis & Digital Forensics Training Guide

## Table of Contents
1. [Introduction to REMnux](#introduction-to-remnux)
2. [INetSim: Internet Services Simulation Suite](#inetsim-internet-services-simulation-suite)
3. [Volatility 3: Memory Forensics](#volatility-3-memory-forensics)
4. [FlareVM: Arsenal of Tools](#flarevm-arsenal-of-tools)
5. [Standard Investigation Tools](#standard-investigation-tools)

---

## Introduction to REMnux

**REMnux** is a Linux distribution for analyzing potentially malicious programs, documents, files, memory, and similar objects. It's designed for cybersecurity professionals conducting malware analysis.

### Key Features
- Specialized tools for reverse engineering, malware analysis, and incident response
- Free and open-source
- Comprehensive toolkit for malware investigation

---

## INetSim: Internet Services Simulation Suite

### What is INetSim?
INetSim is a tool used to simulate a real network environment. It's essential for observing the behavior of potentially malicious software—especially its network activities—without creating complex virtual infrastructures.

### Virtual Machines Setup

#### 1. REMnux Machine
- Your main analysis machine linked to the Machine Access Task
- Runs the REMnux Linux distribution

#### 2. AttackBox
- Provides network access to interact with INetSim
- Click "Start AttackBox" button to launch
- Can switch between boxes by clicking on their names

### Configuring INetSim

#### Step 1: Check IP Address
```bash
ifconfig
# or check the IP from terminal prompt
# ubuntu@MACHINE_IP:~$
```
Note the machine's IP address.

#### Step 2: Edit Configuration
```bash
sudo nano /etc/inetsim/inetsim.conf
```
Find and modify the line:
```bash
#dns_default_ip 0.0.0.0
```
Remove the comment and change to:
```bash
dns_default_ip  MACHINE_IP
```

#### Step 3: Verify Configuration
```bash
cat /etc/inetsim/inetsim.conf | grep dns_default_ip
```

#### Step 4: Start INetSim
```bash
sudo inetsim
```

**Expected Output:**
```
INetSim 1.3.2 (2020-05-19) by Matthias Eckert & Thomas Hungenberg
Using log directory:      /var/log/inetsim/
Using data directory:     /var/lib/inetsim/
Using report directory:   /var/log/inetsim/report/
Using configuration file: /etc/inetsim/inetsim.conf
Parsing configuration file.
Configuration file parsed successfully.
=== INetSim main process started (PID 4859) ===
Session ID:     4859
Listening on:   MACHINE_IP
Forking services...
  * dns_53_tcp_udp - started (PID 4863)
  * http_80_tcp - failed!
  * https_443_tcp - started (PID 4865)
  * ftps_990_tcp - started (PID 4871)
  * pop3_110_tcp - started (PID 4868)
  * smtp_25_tcp - started (PID 4866)
  * ftp_21_tcp - started (PID 4870)
  * pop3s_995_tcp - started (PID 4869)
  * smtps_465_tcp - started (PID 4867)
Simulation running.
```

**Note:** Ignore `http_80_tcp - failed!` - it's normal and doesn't affect functionality.

### Testing INetSim

#### From AttackBox Browser
1. Open browser and navigate to `https://MACHINE_IP`
2. Click "Advanced" then "Accept the Risk and Continue"
3. Should see INetSim's homepage

#### From AttackBox CLI (More Realistic)
```bash
sudo wget https://MACHINE_IP/second_payload.zip --no-check-certificate
```

```bash
sudo wget https://MACHINE_IP/second_payload.ps1 --no-check-certificate
```

#### Verify Downloads
Check the root folder - should see:
- `second_payload.zip`
- `second_payload.ps1`

**Testing Malicious Behavior:**
Open `second_payload.ps1` - it will redirect you to INetSim's homepage, mimicking malware downloading and executing another file.

### Connection Report

#### Stop INetSim
When done, stop INetSim (it automatically creates a connection report):
```bash
# Usually found in /var/log/inetsim/report/
```

**Expected Output:**
```
Report written to '/var/log/inetsim/report/report.2594.txt' (14 lines)
=== INetSim main process stopped (PID 2594) ===
```

#### Read the Report
```bash
sudo cat /var/log/inetsim/report/report.2594.txt
```

**Report Format:**
```
=== Report for session '2594' ===

Real start date            : 2024-09-22 21:04:42
Simulated start date       : 2024-09-22 21:04:42
Time difference on startup : none

2024-09-22 21:04:53  First simulated date in log file
2024-09-22 21:04:53  HTTPS connection, method: GET, URL: https://MACHINE_IP/, file name: /var/lib/inetsim/http/fakefiles/sample.html
2024-09-22 21:16:07  HTTPS connection, method: GET, URL: https://MACHINE_IP/test.exe, file name: /var/lib/inetsim/http/fakefiles/sample_gui.exe
2024-09-22 21:18:37  HTTPS connection, method: GET, URL: https://MACHINE_IP/second_payload.ps1, file name: /var/lib/inetsim/http/fakefiles/sample.html
2024-09-22 21:18:49  HTTPS connection, method: GET, URL: https://MACHINE_IP/second_payload.zip, file name: /var/lib/inetsim/http/fakefiles/sample.html
2024-09-22 21:18:49  Last simulated date in log file
===
```

**Report Provides:**
- Connections made to URLs
- Protocol used
- HTTP method (GET/POST)
- Fake file downloaded

---

## Volatility 3: Memory Forensics

### What is Volatility?
Volatility is a dump analysis framework for memory forensics. It's a standard tool for examining Windows memory images as evidence.

### Windows Volatility Plugins

#### 1. PsTree
Lists processes in a tree based on their parent process ID.

**Command:**
```bash
vol3 -f wcry.mem windows.pstree.PsTree
```

**Use Case:** Understanding parent-child process relationships.

#### 2. PsList
Lists all currently active processes in the machine.

**Command:**
```bash
vol3 -f wcry.mem windows.pslist.PsList
```

**Use Case:** Identifying running processes and their PIDs.

#### 3. CmdLine
Lists process command line arguments.

**Command:**
```bash
vol3 -f wcry.mem windows.cmdline.CmdLine
```

**Use Case:** Understanding how processes were launched and any arguments passed.

#### 4. FileScan
Scans for file objects in a particular Windows memory image.

**Command:**
```bash
vol3 -f wcry.mem windows.filescan.FileScan
```

**Note:** Results often have 1,400+ lines.

**Use Case:** Finding file access patterns and open files.

#### 5. DllList
Lists loaded modules in a particular Windows memory image.

**Command:**
```bash
vol3 -f wcry.mem windows.dlllist.DllList
```

**Use Case:** Identifying loaded DLLs and potential malicious modules.

#### 6. PsScan
Scans for processes present in a particular Windows memory image.

**Command:**
```bash
vol3 -f wcry.mem windows.psscan.PsScan
```

**Use Case:** Comprehensive process enumeration.

#### 7. Malfind
Lists process memory ranges that potentially contain injected code.

**Command:**
```bash
vol3 -f wcry.mem windows.malfind.Malfind
```

**Use Case:** Detecting suspicious code injection or suspicious memory regions.

### Bulk Processing with Loops

**Preprocessing** is a critical investigative practice - running tools and saving results for later examination.

**Command:**
```bash
for plugin in windows.malfind.Malfind windows.psscan.PsScan windows.pstree.PsTree windows.pslist.PsList windows.cmdline.CmdLine windows.filescan.FileScan windows.dlllist.DllList; do vol3 -q -f wcry.mem $plugin > wcry.$plugin.txt; done
```

**Explanation:**
- `$plugin` variable contains each volatility plugin name
- `-q` = quiet mode (no progress display)
- `-f` = read from the memory capture file
- `> wcry.plugin.txt` = output to file with prefix
- Loops through all plugins

**Result:** Creates multiple text files with plugin outputs for easy analysis.

**Expected Files:**
- `wcry.windows.malfind.Malfind.txt`
- `wcry.windows.psscan.PsScan.txt`
- `wcry.windows.pstree.PsTree.txt`
- `wcry.windows.pslist.PsList.txt`
- `wcry.windows.cmdline.CmdLine.txt`
- `wcry.windows.filescan.FileScan.txt`
- `wcry.windows.dlllist.DllList.txt`

### Preprocessing with Strings

The `strings` utility extracts printable text from binaries.

**Commands:**

```bash
# Extract ASCII strings
strings wcry.mem > wcry.strings.ascii.txt

# Extract 16-bit little-endian strings
strings -e l wcry.mem > wcry.strings.unicode_little_endian.txt

# Extract 16-bit big-endian strings
strings -e b wcry.mem > wcry.strings.unicode_big_endian.txt
```

**Explanation:**
- Standard `strings` extracts ASCII text
- `-e l` extracts 16-bit little-endian strings (Unicode)
- `-e b` extracts 16-bit big-endian strings (Unicode)
- All formats can provide useful information about the system

**Result:** Three text files ready for string analysis.

---

## FlareVM: Arsenal of Tools

### What is FlareVM?
**FlareVM** (Forensics, Logic Analysis, and Reverse Engineering) is a comprehensive toolkit curated by the FLARE Team at FireEye. It's designed for reverse engineers, malware analysts, incident responders, forensic investigators, and penetration testers.

### Tool Categories

#### 1. Reverse Engineering & Debugging
- **x64dbg** - Open-source debugger for x64 and x32 binaries
- **OllyDbg** - Debugger for reverse engineering at assembly level
- **Radare2** - Sophisticated open-source reverse engineering platform
- **Binary Ninja** - Disassembler and decompiler
- **PEiD** - Packer, cryptor, and compiler detection tool

#### 2. Disassemblers & Decompilers
- **CFF Explorer** - Editor for analyzing and editing PE files
- **Hopper Disassembler** - Debugger, disassembler, and decompiler
- **RetDec** - Open-source decompiler for machine code

#### 3. Static & Dynamic Analysis
- **Process Hacker** - Sophisticated memory editor and process watcher
- **PEview** - Portable executable file viewer for analysis
- **Dependency Walker** - Displays executable dependencies
- **DIE (Detect It Easy)** - Packer, compiler, and cryptor detection tool

#### 4. Forensics & Incident Response
- **Volatility** - Memory forensics framework
- **Rekall** - Framework for memory forensics in incident response
- **FTK Imager** - Disc image acquisition and analysis tools

#### 5. Network Analysis
- **Wireshark** - Network protocol analyzer
- **Nmap** - Vulnerability detection and network mapping tool
- **Netcat** - Read/write data across network connections

#### 6. File Analysis
- **FileInsight** - Program for editing binary files
- **Hex Fiend** - Light and quick hex editor
- **HxD** - Binary file viewing and editing

#### 7. Scripting & Automation
- **Python** - Automation focused on Python modules and tools
- **Empire** - Post-exploitation framework

#### 8. Sysinternals Suite
- **Autoruns** - Shows executables configured for boot-up
- **Process Explorer** - Information about running processes
- **Process Monitor** - Monitors real-time process/thread activity

### Standard Investigation Tools

#### Procmon (Process Monitor)
**Purpose:** Tracking system activity for malware research, troubleshooting, and forensic investigations.

**Key Features:**
- Records system and Windows file activity in real-time
- Tracks registry activity
- Monitors thread/process activity

**Investigative Value:**
- Filter for LSASS.exe to see authentication-related activity
- LSASS (Local Security Authority Subsystem Service) handles authentication
- Watch for credential dumping attempts (Mimikatz often targets LSASS)
- Look for odd access patterns or processes reading/writing to lsass.exe

#### Process Explorer (Procexp)
**Purpose:** Provides in-depth insights into active processes.

**Key Features:**
- Shows Process and Parent-Child relationships
- Displays DLLs loaded
- Shows process paths
- Identifies which program is accessing specific files/folders

**Investigative Value:**
- Monitor processes spawned from documents (Word, Excel, PDF, ISO files)
- Common technique: Threat actors abuse document formats to spawn malicious processes

#### HxD
**Purpose:** Hex editor for examining or altering malicious files.

**Key Features:**
- View file and memory contents in hexadecimal
- Edit, search, and compare hex data
- Data Inspector for examining individual bytes in multiple data types

**Investigative Value:**
- Identify file types by header bytes (e.g., 4D 5A = Little Endian = PE executable)
- Examine unprocessed binary data for structure identification
- Look for unusual patterns in malicious files

#### CFF Explorer
**Purpose:** Comprehensive file information and analysis.

**Key Features:**
- Generate file hashes (SHA-1, SHA-256, MD5)
- Authenticate system files
- Validate file integrity
- View PE file structure

**Investigative Value:**
- Verify file information and locate possible problems
- Identify unusual alterations in system files
- Confirm file authenticity and origin

#### Wireshark
**Purpose:** Network traffic analysis for investigating suspicious connections.

**Key Features:**
- Capture and examine network traffic
- Analyze protocols
- Identify suspicious connections and data exfiltration

**Investigative Value:**
- Look for TLS/SSL connections that may mask malicious activity
- Analyze encrypted traffic patterns
- Track communication with known malicious infrastructure

#### PEStudio
**Purpose:** Static executable analysis without running the files.

**Key Features:**
- Display file properties
- Generate metadata
- Analyze executable structure

**Investigative Value:**
- Identify executables without execution risk
- Extract various information about suspicious or harmful files

**Example Analysis:**
- **PSexec.exe** (64-bit, compiled with Visual C++ 8)
- **Remote code execution capability**
- **Indicators:** Low to medium for packing/encryption, moderately high
- **Dual-use nature:** Legitimate for admins, potentially exploited by hackers

**Investigative Note:** Presence in compromised environment is concerning, especially for remote code execution.

#### FLOSS (FLARE Obfuscated String Solver)
**Purpose:** Extracts and de-obfuscates strings from malware programs.

**Key Features:**
- Automatically extracts all strings from malware
- Advanced decoding techniques beyond basic strings
- Outputs compatible with IDA Pro or Binary Ninja

**Usage:**
```bash
floss .\cobaltstrike.exe
```

**Example Output:**
```
INFO: floss: extracting static strings
finding decoding function features: 100%|█████████████████████████████████████████████| 74/74 [00:00<00:00, 2370.15 functions/s, skipped 0 library functions]
INFO: floss.stackstrings: extracting stackstrings from 50 functions
extracting stackstrings: 100%|███████████████████████████████████████████████████████████████████████████████| 50/50 [00:00<00:00, 128.00 functions/s]
INFO: floss.tightstrings: extracting tightstrings from 4 functions...
extracting tightstrings from function 0x402e80: 100%|██████████████████████████████████████████████████████████████████| 4/4 [00:00<00:00, 31.99 functions/s]
INFO: floss.string_decoder: decoding strings
emulating function 0x402e80 (call 1/1): 100%|███████████████████████████████████████████████████████████████████████| 21/21 [00:09<00:00,  2.21 functions/s]
INFO: floss: finished execution after 265.61 seconds
```

**Output Types:**
- Static strings (hardcoded)
- Stackstrings (strings stored on stack)
- Tightstrings (strings embedded in code)
- Decoded strings

---

## Certificate Training Preparation

### Key Concepts to Master

#### 1. Network Analysis
- Understanding malware network behavior
- Simulating network environments with INetSim
- Analyzing connection logs and traffic

#### 2. Memory Forensics
- Volatility framework and plugins
- Process analysis (PsList, PsTree, PsScan)
- File and DLL analysis
- Suspicious code detection (Malfind)

#### 3. Static Analysis
- File structure analysis (PE files)
- Hex editing techniques
- String extraction and de-obfuscation (FLOSS)
- Tool usage (HxD, CFF Explorer, PEStudio)

#### 4. Dynamic Analysis
- Process monitoring
- Registry and file activity tracking
- Behavior observation

### Recommended Practice Exercises

1. **INetSim Configuration:**
   - Set up INetSim on REMnux
   - Configure DNS and IP settings
   - Test with AttackBox
   - Analyze connection reports

2. **Volatility Analysis:**
   - Work with sample memory images
   - Run individual plugins
   - Process multiple plugins with loops
   - Extract strings from memory captures

3. **FlareVM Tool Usage:**
   - Practice with each tool category
   - Analyze sample binaries
   - Use FLOSS for string extraction
   - Practice hex editing with HxD

4. **Documentation:**
   - Save all analysis results
   - Create organized reports
   - Document findings systematically

### Remember: Preprocessing is Key

> "One of the most common investigative practices in Digital Forensics is the preprocessing of evidence. This involves running tools and saving the results in text or format. The analyst often relies on tools such as Volatility when dealing with memory images as evidence. The resulting output can be saved to text files for further examination."

Always:
- Run tools and save output to files
- Use loops for batch processing
- Organize results with clear naming conventions
- Document your methodology

---

## Summary

This training guide covers essential tools and techniques for malware analysis and digital forensics:

- **REMnux**: Linux distribution for malware analysis
- **INetSim**: Network simulation for observing malware behavior
- **Volatility**: Memory forensics framework with multiple plugins
- **FlareVM**: Comprehensive toolkit with specialized tools
- **Standard Tools**: Process Monitor, Process Explorer, HxD, Wireshark, CFF Explorer, PEStudio, FLOSS

All these tools are included in REMnux and FlareVM distributions, designed to meet the specific needs of cybersecurity professionals conducting malware investigation.

---

*Note: This document is for educational and training purposes towards certification preparation.*