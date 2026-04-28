# 🚀 TryHackMe Cybersecurity 101 Certification Repository

This repository contains study materials and cheatsheets for the TryHackMe Cybersecurity 101 certification, covering 14 comprehensive modules from basic cybersecurity fundamentals to offensive and defensive security concepts.

## 📁 Repository Structure

```
cybersecurity101/
├── README.md                      # 📋 Main repository documentation
├── CHEATSHEET.md                  # 📚 Comprehensive cheatsheet
├── modules/                       # 📁 Module-specific content
│   ├── 01-start-your-cyber-security-journey.md    # Introduction to Cybersecurity
│   ├── 02-linux-fundamentals.md                     # Linux Fundamentals
│   ├── 03-command-line.md                          # Command Line Mastery
│   ├── 04-windows-ad-fundamentals.md               # Windows and AD Fundamentals
│   ├── 05-networking.md                             # Networking Fundamentals
│   ├── 06-cryptography.md                          # Cryptography and Password Cracking
│   ├── 07-exploitation-basics.md                   # Exploitation Basics
│   ├── 08-web-hacking.md                           # Web Hacking Basics
│   ├── 09-offensive-security-tooling.md            # SQLMap and Offensive Tooling
│   ├── 10-defensive-security.md                    # Defensive Security & Incident Response
│   ├── 11-security-solution.md                     # Security Solutions
│   ├── 12-defensive-security-tooling.md            # Malware Analysis & Forensics
│   ├── 13-build-your-cybersecurity-career.md       # Career Development
│   └── 14-owasp-top-10-2025.md                     # OWASP Top 10 2025
└── references/                    # 📖 Reference materials
    └── (placeholder for future reference files)
└── .gitignore                     # Git ignore file
```

## 🚀 Getting Started

1. Clone this repository:
   ```bash
   git clone https://github.com/rodyjordens82/cybersecurity101.git
   ```

2. Navigate to the repository:
   ```bash
   cd cybersecurity101
   ```

3. Open the cheatsheet:
   ```bash
   open CHEATSHEET.md
   ```

4. Review all 14 modules to prepare for the TryHackMe Cybersecurity 101 certification

## 📚 Modules

### 01. Start Your Cyber Security Journey
- Introduction to Offensive Security
- Getting started in cybersecurity
- Career paths in cybersecurity
- Tools like dirb for web application testing
- Terminal basics

### 02. Linux Fundamentals
- Where Linux is used (websites, IoT, POS systems, infrastructure)
- Linux distributions and flavors
- Terminal interface and commands
- Basic Linux commands (echo, whoami, etc.)
- Navigating the file system

### 03. Command Line Mastery
- **Windows PowerShell**: Basic commands, system information, file operations, remote scripting
- **Linux Bash Shell**: Basic commands, shell types (Bash, Fish, Zsh), scripting fundamentals
- Shell scripting with variables, loops, and conditional statements
- Command history and tab completion

### 04. Windows and AD Fundamentals
- Windows operating system versions and components
- NTFS file system and permissions
- User accounts and UAC
- Active Directory concepts and objects
- Domain controllers and AD structure
- Organizational Units (OUs) and Group Policy Objects (GPOs)
- Trust relationships and authentication protocols

### 05. Networking
- IP addressing and subnetting
- DNS records and queries
- OSI and TCP/IP models
- Network protocols and ports
- Network scanning with Nmap
- Common network attacks and defenses
- Transport security (TLS/SSL)

### 06. Cryptography
- Password hashing fundamentals
- John the Ripper: Wordlist mode
- Single crack mode and word mangling
- Custom rules for password complexity
- Cracking password-protected Zip and RAR archives
- SSH key password cracking

### 07. Exploitation Basics
- Key concepts: Vulnerability, Exploit, Payload, Handler
- Metasploit Framework components (msfconsole, msfvenom, database, modules)
- Finding and using exploit modules
- Payload types (Reverse Shell, Bind Shell, Meterpreter)
- Creating payloads with msfvenom
- Post-exploitation techniques and privilege escalation

### 08. Web Hacking
- Web application basics (HTML, CSS, JavaScript)
- HTTP protocols (GET, POST, PUT, DELETE)
- JavaScript essentials (DOM, AJAX, Cookies)
- XSS and CSRF vulnerabilities
- SQL fundamentals and SQL injection
- Burp Suite interface and proxy configuration
- Certificate installation for HTTPS
- Client-side filter bypasses
- Scoping and interception techniques

### 09. Offensive Security Tooling
- SQLMap for SQL injection detection and exploitation
- Automated web vulnerability testing
- Database management system support
- Advanced SQL injection techniques
- Custom payload creation
- Output and reporting options

### 10. Defensive Security
- Incident response fundamentals
- Types of security incidents (malware, phishing, SQL injection, data leaks, insider attacks, DoS)
- Incident response frameworks (NIST, SANS, ISO)
- Incident response plan development
- Playbooks and runbooks
- Log fundamentals and analysis
- Windows Event Logs
- Web server access logs

### 11. Security Solutions
- Firewalls (packet filter, stateful inspection, proxy, next-generation)
- Intrusion Detection Systems (IDS)
- Intrusion Prevention Systems (IPS)
- Vulnerability scanners
- Network security controls
- Application-layer security

### 12. Defensive Security Tooling
- REMnux Linux distribution for malware analysis
- INetSim for network simulation
- Volatility 3 for memory forensics
- FlareVM as a forensic toolset
- Standard investigation tools
- Malware behavior analysis
- Digital forensics techniques

### 13. Build Your Cybersecurity Career
- Security principles: CIA Triad, Parkerian Hexad, security models
- ISO/IEC 19249 principles
- Security concepts and requirements
- Job roles in cybersecurity (SOC analyst, penetration tester, etc.)
- Required skills and certifications
- Training impact on security teams
- Vendor selection for security solutions

### 14. OWASP Top 10 2025
- IAAA failures (Identity, Authentication, Authorisation, Accountability)
- Broken access control (IDOR)
- Authentication failures
- Logging and alerting failures
- Application design flaws
- Insecure data handling
- Secure web application design principles
- Attack mitigation techniques

## 📖 Cheatsheet

For a comprehensive cheatsheet, see [CHEATSHEET.md](CHEATSHEET.md).

## 🔧 Tools

### Basic Security Tools
- **dirb**: Brute-force tool for finding hidden website pages
- **Terminal**: Command-line interface for executing tools
- **Burp Suite**: Web application security testing tool
- **SQLMap**: Automated SQL injection detection and exploitation tool
- **Nmap**: Network scanning and vulnerability detection
- **John the Ripper**: Password cracking tool

### Linux Commands
- `echo`: Output text to the terminal
- `whoami`: Display current user
- `cd`: Change directory
- `ls`: List files and directories
- `pwd`: Print working directory
- `cat`: Display file contents
- `mkdir`: Create directory
- `rm`: Remove file or directory
- `grep`: Search text in files
- `ssh`: Secure shell connection
- `nc`: Netcat for network communication

### Windows PowerShell Commands
- `Get-Date`: Get current date and time
- `Get-Process`: Get running processes
- `Get-Service`: Get list of services
- `Get-ComputerInfo`: Get detailed system info
- `Get-FileHash`: Calculate file hash
- `Invoke-Command`: Execute remote commands
- `Get-EventLog`: Retrieve event logs

### Malware Analysis Tools
- **REMnux**: Linux distribution for malware analysis
- **INetSim**: Internet services simulation for network behavior analysis
- **Volatility 3**: Memory forensics toolkit
- **FlareVM**: Forensic analysis toolset

### Cybersecurity Training Tools
- **TryHackMe**: Virtual learning environment
- **Kali Linux**: Offensive security platform
- **Metasploit**: Exploitation framework

## 🎯 Exam Preparation

- Review all 14 modules thoroughly
- Practice using the terminal
- Understand offensive security concepts
- Familiarize yourself with Linux commands
- Learn about career paths in cybersecurity
- Practice password cracking techniques
- Study network fundamentals
- Understand exploitation basics and Metasploit
- Learn web application basics and HTTP protocols
- Practice Burp Suite for web penetration testing
- Understand XSS, CSRF, and SQL injection concepts
- Practice SQLMap for SQL injection testing
- Learn defensive security and incident response
- Study security solutions and controls
- Understand malware analysis and forensics
- Review CIA Triad and security principles
- Study OWASP Top 10 2025 vulnerabilities

## 📄 License

This repository is licensed under the MIT License.

---

**Created for**: TryHackMe Cybersecurity 101 Certification
**Maintained by**: Rody Jordens
**Module Coverage**: All 14 modules (Start Journey → OWASP Top 10 2025)
