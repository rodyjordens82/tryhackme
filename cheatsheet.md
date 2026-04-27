# 🛡️ Cybersecurity Cheatsheet

## 🌐 Networking Fundamentals

### IP Addressing

#### IPv4 Address Ranges

**Public IP Ranges**:
- 0.0.0.0/8 - Reserved (routes to current network)
- 10.0.0.0/8 - Private (RFC 1918)
- 172.16.0.0/12 - Private (RFC 1918)
- 192.0.0.0/24 - Special (IETF Protocol Assignments)
- 192.0.2.0/24 - TEST-NET-1 (Documentation)
- 192.88.99.0/24 - 6to4 relay anycast
- 192.168.0.0/16 - Private (RFC 1918)
- 198.51.100.0/24 - TEST-NET-2 (Documentation)
- 203.0.113.0/24 - TEST-NET-3 (Documentation)
- 224.0.0.0/4 - Multicast
- 240.0.0.0/4 - Reserved

**Special IP Addresses**:
- 127.0.0.1 - Loopback/localhost
- 0.0.0.0 - Any address
- 255.255.255.255 - Broadcast

#### IPv6 Address Format

- 128-bit addresses
- Format: Eight hextets separated by colons
- Example: `2001:0db8::1`
- Advantages: Larger address space, built-in security, better QoS

### DNS Records

| Record Type | Purpose |
|-------------|---------|
| **A** | Maps domain to IPv4 address |
| **AAAA** | Maps domain to IPv6 address |
| **CNAME** | Alias for another domain |
| **MX** | Mail exchange server |
| **NS** | Name server |
| **PTR** | Reverse DNS (IP to domain) |
| **SRV** | Service location |
| **TXT** | Text records (SPF, DKIM, DMARC) |
| **SOA** | Start of Authority |

**DNS Query Types**:
- **Recursive**: Client asks DNS server for complete answer
- **Iterative**: Client asks each DNS server in hierarchy

### Common Network Attacks

| Attack | Description |
|--------|-------------|
| **SYN Flood** | Sends SYN packets without completing handshake |
| **Ping of Death** | Oversized ICMP packets cause buffer overflow |
| **DNS Spoofing** | Fake DNS responses redirect traffic |
| **ARP Poisoning** | Manipulate ARP tables on local network |
| **DHCP Starvation** | Exhaust DHCP leases for DoS |
| **DoS/DDoS** | Overwhelm targets with traffic |
| **MITM** | Intercept communication between parties |

### Network Protocols

| Protocol | Port | Layer | Description |
|----------|------|-------|-------------|
| **HTTP** | 80 | 7 | HyperText Transfer Protocol (unencrypted) |
| **HTTPS** | 443 | 7 | HTTP with TLS/SSL encryption |
| **FTP** | 21, 20 | 7 | File Transfer Protocol |
| **SSH** | 22 | 7 | Secure Shell |
| **SMTP** | 25, 587, 2525 | 7 | Email transmission |
| **POP3** | 110 | 7 | Email retrieval |
| **IMAP** | 143 | 7 | Email retrieval |
| **DNS** | 53 | 5 | Domain Name System |
| **NTP** | 123 | 4 | Network Time Protocol |
| **Telnet** | 23 | 7 | Remote terminal (unencrypted) |
| **ICMP** | N/A | 3 | Internet Control Message Protocol |

### Transport Protocols

| Protocol | Type | Features |
|----------|------|----------|
| **TCP** | Connection-oriented | Reliable, ordered, error-checked, uses ports |
| **UDP** | Connectionless | Fast, unreliable, no ordering, uses ports |

### OSI Model (7 Layers)

1. **Physical Layer** (1): Cables, signals, hardware, bits
2. **Data Link Layer** (2): MAC addresses, Ethernet, switches
3. **Network Layer** (3): IP addresses, routing, routers
4. **Transport Layer** (4): Ports, TCP/UDP, flow control
5. **Session Layer** (5): Connection management, synchronization
6. **Presentation Layer** (6): Data translation, encryption, compression
7. **Application Layer** (7): User interfaces, protocols, APIs

### TCP/IP Model (4 Layers)

1. **Network Access**: Physical + Data Link layers
2. **Internet**: Network layer (IP)
3. **Transport**: Transport layer (TCP/UDP)
4. **Application**: Session + Presentation + Application layers

### Network Scanning with Nmap

#### Basic Scans

| Command | Description |
|---------|-------------|
| `nmap -sS <IP>` | SYN scan (stealth) - root required |
| `nmap -sT <IP>` | TCP connect scan - no root required |
| `nmap -sU <IP>` | UDP scan |
| `nmap -sC` | Default script scan |
| `nmap -sV` | Service version detection |
| `nmap -O <IP>` | OS detection |
| `nmap -A` | Aggressive scan (OS, version, scripts) |
| `nmap -p <port>` | Scan specific port(s) |
| `nmap -p- <IP>` | Scan all 65535 ports |
| `nmap -F <IP>` | Fast scan (100 common ports) |
| `nmap -sn <IP>` | Ping scan (no port scan) |

#### Timing Templates

| Option | Name | Description |
|--------|------|-------------|
| `-T0` | paranoid | Very slow, waits 5 min between probes |
| `-T1` | sneaky | Slow, waits 15 sec between probes |
| `-T2` | polite | Moderate, waits 0.4 sec between probes |
| `-T3` | normal | Default speed |
| `-T4` | aggressive | Fast |
| `-T5` | insane | Very fast, may trigger IDS |

#### Output Formats

| Command | Description |
|---------|-------------|
| `-oN <file>` | Normal (human-readable) output |
| `-oX <file>` | XML output |
| `-oG <file>` | Greppable output (for grep/awk) |
| `-oA <basename>` | All formats (normal, XML, greppable) |

#### Verbosity & Debugging

| Command | Description |
|---------|-------------|
| `-v` | Verbosity level (add more for -vv, -vvv) |
| `-vv` | More verbose output |
| `-d` | Debugging level (add more for -d2, -d9) |
| `--open` | Only show open ports |
| `--min-rate <pps>` | Minimum packets per second |
| `--max-rate <pps>` | Maximum packets per second |
| `--host-timeout <time>` | Max time to wait for host |

#### Useful Options

| Command | Description |
|---------|-------------|
| `-Pn` | Treat all hosts as online |
| `-sn` | Disable port scan (host discovery only) |
| `-PE, -PP, -PM` | ICMP ping types |
| `-iL <file>` | Input from file |
| `-iR <num>` | Scan random IPs |
| `--exclude <hosts>` | Exclude hosts from scan |
| `--exclude-from <file>` | Exclude from file |

### Network Security Tools

| Tool | Purpose |
|------|---------|
| **nmap** | Network scanning, port scanning |
| **netcat (nc)** | Network utility, port scanning, data transfer |
| **Wireshark** | Protocol analyzer, packet inspection |
| **tcpdump** | Command-line packet capture |
| **ssh** | Secure remote access |
| **ping** | Network connectivity test |
| **traceroute** | Path to destination |
| **nslookup** | DNS lookup |
| **dig** | DNS lookup (more detailed) |

### Transport Security

**TLS/SSL Features**:
- Encrypts communication in transit
- Uses asymmetric encryption for key exchange
- Uses symmetric encryption for data transmission
- Provides integrity and authentication

**Certificate Chain**:
- Root CA → Intermediate CA → Server Certificate

**HTTPS Benefits**:
- Confidentiality (encrypted data)
- Integrity (data not tampered with)
- Authentication (server identity verified)
- Prevents man-in-the-middle attacks

---

## 🔐 Cryptography

### Password Hashing Fundamentals

**What is Password Hashing?**
- Converting plaintext password to fixed-length string (hash)
- Cannot be reversed (unlike encryption)
- Prevents plaintext exposure if database compromised
- Time-consuming process slows down brute-force attacks

**Common Hash Formats**:
| Format | Algorithm | Description |
|--------|-----------|-------------|
| `$6$` | SHA-512crypt | Strong, Unix-like hashing |
| `$2a$` / `$2b$` | Blowfish | bcrypt variant |
| `$5$` | SHA-256crypt | SHA-256 based hashing |
| `$1$` | MD5crypt | Legacy Unix hashing |
| `raw-sha256` | SHA-256 | Raw hash without salt |

**Hash Locations**:
- `/etc/passwd`: User account info (unencrypted)
- `/etc/shadow`: Encrypted passwords (root only)

### John the Ripper

**Definition**: Fast password cracker for Linux/Unix, Windows, macOS

**Installation** (Kali/AttackBox):
```bash
sudo apt-get install john
```

**Wordlist Mode** (Most Common):
```bash
john --wordlist=[wordlist] --format=[format] [hash_file]
```

**Common Commands**:

| Command | Description |
|---------|-------------|
| `unshadow /etc/passwd /etc/shadow > unshadowed.txt` | Combine pass and shadow files |
| `john --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt` | Crack hashes |
| `john --show unshadowed.txt` | View cracked passwords |

**Wordlists**:
- `rockyou.txt` (~14 million) - Most popular
- `password.txt` (~10,000) - Simple list
- `common.txt` (~20,000) - Common passwords

**Single Crack Mode**:
```bash
john --single --format=[format] [hash_file]
```
- Uses username and GECOS for password generation
- Creates words like "Username1!", "UPPERCASE", "lowercase"

**SSH Key Cracking**:
```bash
ssh2john id_rsa > id_rsa_hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
```

**Archive Cracking**:

| Archive | Tool | Command |
|---------|------|---------|
| `zip` | `zip2john` | `zip2john zipfile.zip > zip_hash.txt` |
| `rar` | `rar2john` | `rar2john rarfile.rar > rar_hash.txt` |

**Custom Rules**:
```bash
john --wordlist=rockyou.txt --rule=RULE_NAME unshadowed.txt
```

**Common Rule Modifiers**:
| Modifier | Description |
|----------|-------------|
| `c` | Capitalize first character |
| `u` | Convert to uppercase |
| `l` | Convert to lowercase |
| `Az"[0-9]"` | Append digit to end |
| `A0"[0-9]"` | Prepend digit to start |
| `lC` | Lowercase except first char |
| `s` | Swap case |

**Examples**:
```bash
# SHA-512crypt cracking
john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt

# Mask pattern cracking
john --wordlist=rockyou.txt --mask='?l?d?d?d?d?d' hashes.txt

# Single mode
john --single --format=sha512crypt unshadowed.txt
```

**Key Files**:
| File | Purpose |
|------|---------|
| `/etc/passwd` | User account info |
| `/etc/shadow` | Encrypted passwords |
| `/usr/share/wordlists/rockyou.txt` | Wordlist file |

**Performance**:
- GPU acceleration available for supported formats
- Use `-t <num>` for parallel processing
- Incremental mode: `john --incremental id_rsa_hash.txt`

**GECOS Field**:
- Contains user info: full name, office, phone
- Format: `username:x:UID:GID:GECOS:HOME_DIR:SHELL`
- Used for generating predictable passwords

### SSH Key Passwords

**Why Crack SSH Keys?**
- Private keys may be password-protected
- Stronger security than passwords
- Still vulnerable if weak password used

**Cracking Steps**:
```bash
# Convert SSH key to John hash
ssh2john id_rsa > id_rsa_hash.txt

# Crack the hash
john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt

# Use cracked password
ssh -i id_rsa username@target_ip
```

**Alternative Tools**:
- `sshpass` for non-interactive SSH
- `fcrackzip` for password cracking
- `hashcat` for GPU-accelerated cracking

### Best Practices

**Secure Passwords**:
- Minimum 12+ characters
- Mixed case, numbers, symbols
- Unique for each site
- Use password manager

**Avoid Common Patterns**:
❌ `Password123!`, `Password@2024`, `Admin@123`
✅ `correct-horse-battery-staple`, `3j#9K$2mP@5nL`

**Defense**:
- Strong hashing algorithms (bcrypt, Argon2)
- Slow hashing (slow down attacks)
- Salted passwords
- Multi-factor authentication

**Reference**: Compiled from TryHackme cybersecurity study materials