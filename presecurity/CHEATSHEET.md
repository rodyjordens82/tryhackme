# 📚 TryHackMe Pre-Security Certification Cheatsheet

This comprehensive cheatsheet covers all key concepts for the TryHackMe Pre-Security certification.

---

## 💻 Computer Fundamentals

### Computer Hardware Basics

**Key Components**:
- **CPU (Central Processing Unit)**: Executes instructions
- **RAM (Random Access Memory)**: Temporary storage for active programs
- **Storage (HDD/SSD)**: Permanent storage for files and data
- **Motherboard**: Main circuit board connecting all components
- **GPU (Graphics Processing Unit)**: Handles graphics rendering
- **Power Supply**: Provides electrical power to components

**Input/Output Devices**:
- **Input**: Keyboard, mouse, microphone, scanner
- **Output**: Monitor, printer, speakers, projector

**Computer Architecture**:
- Von Neumann architecture (stored-program concept)
- Components: CPU, memory, I/O, storage
- Data flow: Input → Processing → Output → Storage

### Operating Systems

**Definition**: Software that manages computer hardware and software resources

**Common Operating Systems**:
- **Windows**: Microsoft's OS for desktops and servers
- **macOS**: Apple's OS for Mac computers
- **Linux**: Open-source OS with many distributions
- **Unix**: Multi-user OS

**OS Functions**:
- Process management
- Memory management
- File system management
- Device management
- User interface
- Security and permissions

**Linux Distributions**:
- Ubuntu: User-friendly, good for beginners
- Fedora: Cutting-edge features
- Debian: Stable, widely used
- Arch Linux: Minimalist, highly customizable
- CentOS/RHEL: Enterprise-grade

### File Systems

**File System Basics**:
- Hierarchical structure (directories/folders and files)
- Paths: absolute vs relative
- File permissions (read, write, execute)

**Common File Systems**:
- **NTFS**: Windows default
- **ext4**: Linux default
- **FAT32/exFAT**: Compatible with multiple OS
- **APFS**: Apple's file system for macOS

**File Operations**:
- Creating, reading, updating, and deleting files
- Copying and moving files
- Searching for files
- File compression and archiving

### Command Line Basics

**Basic Commands**:
```bash
# Navigation
cd /path/to/directory       # Change directory
pwd                        # Print working directory
ls                          # List files and directories

# File operations
cp source destination      # Copy files
mv source destination      # Move/rename files
rm file                    # Remove file
mkdir directory            # Create directory
rmdir directory            # Remove directory

# Viewing files
cat file                   # Display file contents
less file                  # View file with pagination
head file                  # View first lines
tail file                  # View last lines

# Searching
find /path -name "pattern" # Find files by name
grep "pattern" file        # Search for text in files

# System information
df -h                       # Disk space usage
free -h                     # Memory usage
ps aux                      # Running processes
top                         # Interactive process viewer
```

**Command Line Tips**:
- Use tab completion
- Use `man command` for help
- Use `--help` flag for options
- Use `history` to view command history
- Use `!number` to repeat a command from history

### Basic Scripting

**Why Scripting?**:
- Automate repetitive tasks
- Combine multiple commands
- Create reusable workflows
- Schedule tasks

**Scripting Languages**:
- **Bash**: Built into Linux/Unix systems
- **Python**: Versatile, easy to learn
- **PowerShell**: Windows scripting
- **JavaScript**: For web automation

**Bash Script Example**:
```bash
#!/bin/bash

# Simple backup script
SOURCE="/home/user/documents"
DESTINATION="/backup/documents_$(date +%Y%m%d).tar.gz"

# Create backup
tar -czf "$DESTINATION" "$SOURCE"

# Verify backup
if [ -f "$DESTINATION" ]; then
    echo "Backup created successfully: $DESTINATION"
else
    echo "Backup failed"
    exit 1
fi
```

**Python Script Example**:
```python
#!/usr/bin/env python3

import os
import shutil
from datetime import datetime

# Configuration
source_dir = "/home/user/documents"
backup_dir = "/backup"

# Create backup filename
backup_name = f"documents_{datetime.now().strftime('%Y%m%d')}.zip"
backup_path = os.path.join(backup_dir, backup_name)

# Create backup
shutil.make_archive(backup_path.replace('.zip', ''), 'zip', source_dir)

# Verify
if os.path.exists(backup_path):
    print(f"Backup created successfully: {backup_path}")
else:
    print("Backup failed")
    exit(1)
```

---

## 💻 Computer Fundamentals

### Computer Hardware Basics

**Key Components**:
- **CPU (Central Processing Unit)**: Executes instructions
- **RAM (Random Access Memory)**: Temporary storage for active programs
- **Storage (HDD/SSD)**: Permanent storage for files and data
- **Motherboard**: Main circuit board connecting all components
- **GPU (Graphics Processing Unit)**: Handles graphics rendering
- **Power Supply**: Provides electrical power to components

**Input/Output Devices**:
- **Input**: Keyboard, mouse, microphone, scanner
- **Output**: Monitor, printer, speakers, projector

**Computer Architecture**:
- Von Neumann architecture (stored-program concept)
- Components: CPU, memory, I/O, storage
- Data flow: Input → Processing → Output → Storage

### Operating Systems

**Definition**: Software that manages computer hardware and software resources

**Common Operating Systems**:
- **Windows**: Microsoft's OS for desktops and servers
- **macOS**: Apple's OS for Mac computers
- **Linux**: Open-source OS with many distributions
- **Unix**: Multi-user OS

**OS Functions**:
- Process management
- Memory management
- File system management
- Device management
- User interface
- Security and permissions

**Linux Distributions**:
- Ubuntu: User-friendly, good for beginners
- Fedora: Cutting-edge features
- Debian: Stable, widely used
- Arch Linux: Minimalist, highly customizable
- CentOS/RHEL: Enterprise-grade

### File Systems

**File System Basics**:
- Hierarchical structure (directories/folders and files)
- Paths: absolute vs relative
- File permissions (read, write, execute)

**Common File Systems**:
- **NTFS**: Windows default
- **ext4**: Linux default
- **FAT32/exFAT**: Compatible with multiple OS
- **APFS**: Apple's file system for macOS

**File Operations**:
- Creating, reading, updating, and deleting files
- Copying and moving files
- Searching for files
- File compression and archiving

### Command Line Basics

**Basic Commands**:
```bash
# Navigation
cd /path/to/directory       # Change directory
pwd                        # Print working directory
ls                          # List files and directories

# File operations
cp source destination      # Copy files
mv source destination      # Move/rename files
rm file                    # Remove file
mkdir directory            # Create directory
rmdir directory            # Remove directory

# Viewing files
cat file                   # Display file contents
less file                  # View file with pagination
head file                  # View first lines
tail file                  # View last lines

# Searching
find /path -name "pattern" # Find files by name
grep "pattern" file        # Search for text in files

# System information
df -h                       # Disk space usage
free -h                     # Memory usage
ps aux                      # Running processes
top                         # Interactive process viewer
```

**Command Line Tips**:
- Use tab completion
- Use `man command` for help
- Use `--help` flag for options
- Use `history` to view command history
- Use `!number` to repeat a command from history

### Basic Scripting

**Why Scripting?**:
- Automate repetitive tasks
- Combine multiple commands
- Create reusable workflows
- Schedule tasks

**Scripting Languages**:
- **Bash**: Built into Linux/Unix systems
- **Python**: Versatile, easy to learn
- **PowerShell**: Windows scripting
- **JavaScript**: For web automation

**Bash Script Example**:
```bash
#!/bin/bash

# Simple backup script
SOURCE="/home/user/documents"
DESTINATION="/backup/documents_$(date +%Y%m%d).tar.gz"

# Create backup
tar -czf "$DESTINATION" "$SOURCE"

# Verify backup
if [ -f "$DESTINATION" ]; then
    echo "Backup created successfully: $DESTINATION"
else
    echo "Backup failed"
    exit 1
fi
```

**Python Script Example**:
```python
#!/usr/bin/env python3

import os
import shutil
from datetime import datetime

# Configuration
source_dir = "/home/user/documents"
backup_dir = "/backup"

# Create backup filename
backup_name = f"documents_{datetime.now().strftime('%Y%m%d')}.zip"
backup_path = os.path.join(backup_dir, backup_name)

# Create backup
shutil.make_archive(backup_path.replace('.zip', ''), 'zip', source_dir)

# Verify
if os.path.exists(backup_path):
    print(f"Backup created successfully: {backup_path}")
else:
    print("Backup failed")
    exit(1)
```

---

## 🖥️ Operating System Basics

### What is an Operating System?

An operating system (OS) is system software that manages computer hardware and software resources and provides common services for computer programs.

### Core OS Functions

- **Process Management**: Creating, scheduling, and terminating processes
- **Memory Management**: Allocating and freeing memory
- **File System Management**: Organizing and accessing files
- **Device Management**: Controlling hardware devices
- **User Interface**: Providing interaction methods (GUI, CLI)
- **Security**: Managing permissions and access control

### Common Operating Systems

**Desktop Operating Systems**:
- Windows 10/11
- macOS
- Linux distributions (Ubuntu, Fedora, etc.)

**Server Operating Systems**:
- Windows Server
- Linux (CentOS, Ubuntu Server)
- FreeBSD

**Mobile Operating Systems**:
- Android
- iOS

### OS Security Fundamentals

**Security Principles**:
- Principle of least privilege
- User account control
- Firewall configuration
- Regular updates and patches
- Antivirus and malware protection

**Common Security Features**:
- User authentication
- File permissions (read, write, execute)
- Process isolation
- Network security settings

**Best Practices**:
- Use strong passwords
- Regularly update the OS
- Disable unnecessary services
- Monitor system logs
- Use encryption for sensitive data

---

## 📦 Software Basics

### Software Development Fundamentals

**Software Development Lifecycle (SDLC)**:
1. Planning
2. Analysis
3. Design
4. Implementation
5. Testing
6. Deployment
7. Maintenance

**Programming Paradigms**:
- Procedural programming
- Object-oriented programming (OOP)
- Functional programming
- Event-driven programming

### Programming Languages Overview

**Low-level Languages**:
- Assembly: Machine-specific, close to hardware
- C: Compiled language, used for system programming

**High-level Languages**:
- Python: Easy to learn, versatile
- JavaScript: Web development
- Java: Platform-independent
- C#: Microsoft .NET framework
- Ruby: Web development (Ruby on Rails)
- PHP: Web development

**Scripting Languages**:
- Bash: Linux/Unix shell scripting
- PowerShell: Windows automation
- Python: General-purpose scripting

### Software Security Principles

**Secure Coding Practices**:
- Input validation
- Error handling
- Authentication and authorization
- Data encryption
- Secure coding standards

**Common Vulnerabilities**:
- SQL injection
- Cross-site scripting (XSS)
- Cross-site request forgery (CSRF)
- Buffer overflow
- Memory leaks

**Security Best Practices**:
- Use parameterized queries
- Validate all user input
- Implement proper authentication
- Use HTTPS for web applications
- Regular security testing

### Software Development Tools

**Version Control**:
- Git: Distributed version control system
- GitHub: Code hosting platform
- GitLab: Complete DevOps platform

**Integrated Development Environments (IDEs)**:
- Visual Studio Code
- PyCharm
- IntelliJ IDEA
- Eclipse
- Xcode

**Compilers and Interpreters**:
- GCC: GNU Compiler Collection
- Python interpreter
- Node.js: JavaScript runtime
- Java Virtual Machine (JVM)

---

## 🛡️ Attacks and Defenses

### Common Cyber Attacks

**Malware**:
- Virus: Self-replicating malicious code
- Worm: Self-replicating, spreads without user action
- Trojan: Disguised as legitimate software
- Ransomware: Encrypts files and demands payment
- Spyware: Monitors user activity

**Network Attacks**:
- Denial of Service (DoS): Overwhelms a system
- Man-in-the-Middle (MitM): Intercepts communications
- Phishing: Fraudulent attempts to obtain sensitive information
- Session Hijacking: Takes over a valid user session
- ARP Spoofing: Poisons ARP cache

**Web Application Attacks**:
- SQL Injection: Injects malicious SQL code
- Cross-Site Scripting (XSS): Injects malicious scripts
- Cross-Site Request Forgery (CSRF): Exploits trusted relationships
- Session Hijacking: Steals session cookies
- File Inclusion: Includes malicious files

### Security Principles (CIA Triad)

**Confidentiality**: Ensuring information is accessible only to authorized users
- Encryption
- Access controls
- Authentication

**Integrity**: Ensuring information is accurate and complete
- Hash functions
- Digital signatures
- Checksums

**Availability**: Ensuring information is accessible when needed
- Redundancy
- Backup and recovery
- Load balancing

### Defense Mechanisms

**Network Security**:
- Firewalls: Filter network traffic
- Intrusion Detection Systems (IDS): Monitor for attacks
- Intrusion Prevention Systems (IPS): Block attacks
- Virtual Private Networks (VPN): Secure remote access

**Endpoint Security**:
- Antivirus software
- Host-based firewalls
- Endpoint Detection and Response (EDR)
- Mobile Device Management (MDM)

**Application Security**:
- Secure coding practices
- Web Application Firewalls (WAF)
- Input validation
- Output encoding

**Data Security**:
- Encryption (AES, RSA)
- Access controls
- Data masking
- Tokenization

### Security Best Practices

**General Security**:
- Regular software updates
- Strong password policies
- Multi-factor authentication
- Least privilege principle
- Regular security audits

**User Education**:
- Security awareness training
- Phishing simulations
- Incident response training
- Security policies and procedures

**Monitoring and Logging**:
- Centralized logging
- Security Information and Event Management (SIEM)
- Real-time monitoring
- Alerting and notification

**Incident Response**:
- Preparation
- Detection and analysis
- Containment
- Eradication
- Recovery
- Lessons learned

---

## 🔐 Introduction to Cybersecurity

### Offensive Security

**Definition**: Proactive approach to security by simulating attacks to find vulnerabilities

**Key Concepts**:
- Penetration Testing: Authorized simulated attacks
- Ethical Hacking: Legal hacking with permission
- Vulnerability Assessment: Identifying security weaknesses
- Red Teaming: Attack simulation
- Blue Teaming: Defense and response

**Offensive Security Tools**:
- Metasploit Framework
- Burp Suite
- Nmap
- Wireshark
- John the Ripper

### Getting Started in Cybersecurity

**Career Paths**:
- Penetration Tester
- Security Analyst
- SOC Analyst
- Incident Responder
- Security Engineer
- Security Architect

**Entry-Level Certifications**:
- TryHackMe Pre-Security
- CompTIA Security+
- Certified Ethical Hacker (CEH)
- Offensive Security Certified Professional (OSCP)

**Learning Resources**:
- TryHackMe (tryhackme.com)
- Hack The Box (hackthebox.com)
- OverTheWire (overthewire.org)
- CyberSec Labs (cyberseclabs.co.uk)

### Career Paths in Cybersecurity

**Offensive Security Path**:
1. Pre-Security Certification
2. Penetration Testing
3. Red Teaming
4. Security Architecture

**Defensive Security Path**:
1. Pre-Security Certification
2. Security Analyst
3. SOC Analyst
4. Incident Response

**Management Path**:
1. Pre-Security Certification
2. Security Engineer
3. Security Manager
4. CISO (Chief Information Security Officer)

---

## 🌐 How the Web Works

### Introduction to the Web
- **Definition**: System of interlinked hypertext documents accessed via the Internet
- **Key Components**: Clients (browsers), servers (web servers), protocols (HTTP/HTTPS), resources (web pages, APIs)
- **How it Works**: User enters URL → Browser requests resource → Server processes request → Server sends response → Browser renders response

### HTTP and HTTPS Protocols

**HTTP (HyperText Transfer Protocol)**:
- Stateless protocol using request/response model
- Runs on port 80
- Methods: GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS

**HTTPS (HTTP Secure)**:
- HTTP with encryption (TLS/SSL)
- Runs on port 443
- Provides security and privacy

**HTTP Status Codes**:
- 200 OK: Request successful
- 201 Created: Resource created
- 301 Moved Permanently: Resource moved
- 302 Found: Temporary redirect
- 304 Not Modified: Resource not modified
- 400 Bad Request: Invalid request
- 401 Unauthorized: Authentication required
- 403 Forbidden: Access denied
- 404 Not Found: Resource not found
- 500 Internal Server Error: Server error
- 502 Bad Gateway: Invalid response from upstream
- 503 Service Unavailable: Server unavailable

### Web Servers and Clients

**Web Servers**:
- Software that serves web content (Apache, Nginx, IIS)
- Handles HTTP/HTTPS requests
- Serves static and dynamic content

**Clients (Browsers)**:
- Software that requests and displays web content (Chrome, Firefox, Safari, Edge)
- Renders HTML, CSS, JavaScript
- Executes client-side scripts

### Web Application Architecture

**Client-Server Model**:
- Client sends request to server
- Server processes request
- Server sends response to client

**Three-Tier Architecture**:
1. Presentation Layer: User interface (HTML, CSS, JavaScript)
2. Application Layer: Business logic (server-side code)
3. Data Layer: Database (MySQL, PostgreSQL, MongoDB)

**RESTful APIs**:
- Representational State Transfer
- Uses HTTP methods (GET, POST, PUT, DELETE)
- Stateless communication
- Resource-based architecture

### Web Security Basics

**Common Vulnerabilities**:
- SQL Injection: Malicious SQL code in input
- XSS (Cross-Site Scripting): Malicious scripts in web pages
- CSRF (Cross-Site Request Forgery): Unauthorized commands
- Security Misconfigurations: Default settings, open ports
- Sensitive Data Exposure: Unencrypted data

**Security Best Practices**:
- Use HTTPS for all communications
- Input validation and sanitization
- Proper authentication and authorization
- Secure session management
- Regular security updates and patches
- Security headers (CSP, HSTS)
- Rate limiting and WAF

---

## 🌐 Networking Fundamentals

### What is Networking?

**Definition**: The practice of connecting computers and devices to share resources and information

**Key Concepts**:
- Communication between devices
- Data transfer and sharing
- Resource sharing
- Security and access control

### Network Types

**LAN (Local Area Network)**:
- Small geographic area (office, home)
- High speed, low latency
- Examples: Home network, office network

**WAN (Wide Area Network)**:
- Large geographic area (country, continent)
- Lower speed, higher latency
- Examples: Internet, corporate networks

**MAN (Metropolitan Area Network)**:
- City-wide network
- Between LAN and WAN
- Examples: City-wide Wi-Fi, ISP networks

**WLAN (Wireless Local Area Network)**:
- Wireless version of LAN
- Uses Wi-Fi technology
- Examples: Home Wi-Fi, office Wi-Fi

### Network Devices

**Router**:
- Connects multiple networks
- Routes traffic between networks
- Has a routing table

**Switch**:
- Connects devices within a network
- Uses MAC addresses
- Creates network segments

**Hub**:
- Connects devices within a network
- Broadcasts traffic to all ports
- Legacy device (replaced by switches)

**Firewall**:
- Controls traffic between networks
- Filters based on rules
- Provides security

**Modem**:
- Connects to ISP
- Modulates/demodulates signals
- Provides internet access

### Network Models

**OSI Model (7 Layers)**:
1. Physical: Cables, signals
2. Data Link: MAC addresses, switches
3. Network: IP addresses, routers
4. Transport: Ports, TCP/UDP
5. Session: Connection management
6. Presentation: Data formatting
7. Application: User interfaces

**TCP/IP Model (4 Layers)**:
1. Network Access: Physical and data link
2. Internet: IP addresses, routing
3. Transport: TCP/UDP, ports
4. Application: Protocols and services

### IP Addressing and Subnetting

**IPv4 Address**: 32-bit address (e.g., 192.168.1.1)
- Divided into network and host portions
- Uses subnet mask to separate

**Subnet Mask**: Defines network portion (e.g., 255.255.255.0)
- Determines network size
- Used for routing

**Subnetting**: Dividing network into smaller networks
- Increases efficiency
- Reduces broadcast traffic
- Improves security

**CIDR Notation**: IP address with prefix length (e.g., 192.168.1.0/24)
- Replaces subnet mask
- More concise

### Ports and Protocols

**Common Ports**:

| Port | Protocol | Service |
|------|----------|---------|
| 21 | FTP | File Transfer |
| 22 | SSH | Secure Shell |
| 23 | Telnet | Remote Login |
| 25 | SMTP | Email |
| 53 | DNS | Domain Name System |
| 80 | HTTP | Web |
| 110 | POP3 | Email |
| 143 | IMAP | Email |
| 443 | HTTPS | Secure Web |
| 3389 | RDP | Remote Desktop |

**Common Protocols**:

| Protocol | Description |
|----------|-------------|
| **TCP** | Reliable, connection-oriented |
| **UDP** | Unreliable, connectionless |
| **ICMP** | Error reporting and diagnostics |
| **IGMP** | Multicast group management |
| **DHCP** | Dynamic IP address assignment |
| **ARP** | MAC address resolution |

### DNS and Domain Names

**DNS (Domain Name System)**:
- Translates domain names to IP addresses
- Hierarchical system
- Uses DNS servers

**Domain Name Structure**:
- Example: www.example.com
- Top-Level Domain (TLD): .com, .org, .net
- Second-Level Domain: example
- Subdomain: www

**DNS Record Types**:

| Record | Description |
|--------|-------------|
| **A** | IPv4 address mapping |
| **AAAA** | IPv6 address mapping |
| **CNAME** | Canonical name alias |
| **MX** | Mail exchange server |
| **NS** | Name server |
| **PTR** | Reverse DNS mapping |
| **SOA** | Start of authority |
| **TXT** | Text information |

### Network Security

**Common Threats**:
- Malware (viruses, worms, ransomware)
- Phishing (fraudulent emails)
- Man-in-the-Middle (MITM) attacks
- Denial of Service (DoS) attacks
- Unauthorized access

**Security Best Practices**:
- Use strong passwords
- Keep software updated
- Use firewalls and antivirus
- Encrypt sensitive data
- Implement access controls
- Monitor network traffic
- Regular security audits

---

## 🔧 Tools and Commands

### Networking Tools

**Basic Networking**:
```bash
ping <host>                # Check connectivity
 traceroute <host>         # Trace network path
 nslookup <domain>         # DNS lookup
 netstat -tuln             # Show network connections
 curl <url>                # Transfer data with URL
 wget <url>                # Download files
```

**Network Scanning**:
```bash
nmap <target>              # Network scanning
 tcpdump -i <interface>    # Packet capture
 wireshark                 # GUI packet analysis
```

### Security Tools

**Web Application Testing**:
```bash
gobuster dir -u <url> -w <wordlist>  # Directory brute-forcing
 nikto -h <url>                          # Web server scanner
```

**Password Attacks**:
```bash
john <hashfile>           # Password cracking
 aircrack-ng <capture>     # Wi-Fi password cracking
```

**Exploitation Frameworks**:
```bash
msfconsole                # Metasploit Framework
 burpsuite                 # Web application security testing
```

---

## 📚 Study Tips

### Effective Learning Strategies

1. **Active Learning**: Apply concepts through hands-on practice
2. **Spaced Repetition**: Review material at increasing intervals
3. **Practice Tests**: Take practice exams to identify weak areas
4. **Teach Others**: Explain concepts to reinforce understanding
5. **Hands-on Labs**: Use virtual machines and lab environments

### Time Management

- **Daily Study**: 30-60 minutes per day
- **Weekly Review**: 1-2 hours per week
- **Practice Exams**: 2-3 full-length exams before the test
- **Break Down Topics**: Study one topic at a time

### Resource Utilization

- **Official Documentation**: TryHackMe study materials
- **Practice Platforms**: TryHackMe rooms, Hack The Box
- **Community Forums**: Reddit (r/netsec, r/cybersecurity), Discord
- **Study Groups**: Join or form study groups

---

## 🎯 Exam Preparation

### Key Focus Areas

1. **Networking Fundamentals**
   - OSI and TCP/IP models
   - IP addressing and subnetting
   - Common ports and protocols
   - DNS and domain names

2. **Cybersecurity Concepts**
   - Offensive vs defensive security
   - Common threats and vulnerabilities
   - Security best practices

3. **Web Technologies**
   - HTTP/HTTPS protocols
   - Web servers and clients
   - Web application architecture
   - Web security basics

### Practice Questions

- **Subnetting**: Practice calculating subnet masks and IP ranges
- **Ports/Protocols**: Memorize common ports and their services
- **HTTP Status Codes**: Understand common status codes and their meanings
- **Security Concepts**: Review common vulnerabilities and mitigation strategies

### Test-Taking Strategies

- **Read Carefully**: Understand what each question is asking
- **Eliminate Wrong Answers**: Narrow down choices
- **Flag and Review**: Mark difficult questions for later review
- **Time Management**: Don't spend too much time on any single question
- **Review Answers**: Check all answers before submitting

---

## 📋 Summary

This cheatsheet provides an overview of the key concepts covered in the TryHackMe Pre-Security certification. Use it as a reference guide during your study journey and as a quick review before the exam.

**Key Topics Covered**:
- 💻 Computer Fundamentals
- 🖥️ Operating System Basics
- 📦 Software Basics
- 🛡️ Attacks and Defenses
- 🔐 Introduction to Cybersecurity
- 🌐 Networking Fundamentals
- 🌐 How the Web Works
- 🔧 Tools and Commands
- 📚 Study Tips
- 🎯 Exam Preparation

**Good Luck!** 🚀
