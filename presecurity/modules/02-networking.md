# 🌐 Networking Fundamentals

This module covers the essential concepts of computer networking, which is fundamental to understanding cybersecurity.

## 🎯 Key Topics

- What is Networking?
- Network Types
- Network Devices
- Network Models
- IP Addressing
- Subnetting
- Ports and Protocols
- DNS and Domain Names
- Network Security

## 📝 Notes

### What is Networking?

**Definition**: Devices connected together to communicate and share resources.

**Real-world Examples**:
- Friendship circles
- Public transportation systems
- Power grids
- Postal systems

**Computing Networks**:
- Devices: laptops, phones, IoT devices
- Communication: via protocols and standards
- Scale: from 2 devices to billions (Internet)

### Network Types

| Type | Description | Example |
|------|-------------|---------|
| **LAN** | Local Area Network | Home, office network |
| **WAN** | Wide Area Network | Country-wide network |
| **MAN** | Metropolitan Area Network | City-wide network |
| **PAN** | Personal Area Network | Bluetooth, Wi-Fi devices |
| **VPN** | Virtual Private Network | Secure remote access |

### Network Devices

| Device | Function |
|--------|----------|
| **Router** | Connects networks, directs traffic |
| **Switch** | Connects devices within LAN |
| **Hub** | Connects devices (outdated) |
| **Modem** | Converts signals between networks |
| **Firewall** | Filters network traffic |
| **Access Point** | Provides Wi-Fi connectivity |

### Network Models

#### OSI Model (7 Layers)

1. **Physical Layer**: Cables, signals, hardware
2. **Data Link Layer**: MAC addresses, Ethernet, switches
3. **Network Layer**: IP addresses, routing, routers
4. **Transport Layer**: Ports, TCP/UDP, reliability
5. **Session Layer**: Connection management
6. **Presentation Layer**: Data translation, encryption
7. **Application Layer**: User interfaces, protocols

#### TCP/IP Model (4 Layers)

1. **Network Access**: Physical + Data Link layers
2. **Internet**: Network layer (IP)
3. **Transport**: Transport layer (TCP/UDP)
4. **Application**: Session + Presentation + Application layers

### IP Addressing

**IPv4**: 32-bit address (e.g., 192.168.1.1)
- Format: Four octets (0-255 each)
- Classes: A, B, C, D, E
- Private Ranges:
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16

**IPv6**: 128-bit address (e.g., 2001:0db8::1)
- Format: Eight hextets separated by colons
- Advantages: Larger address space, built-in security, better QoS

### Subnetting

**Purpose**: Divide network into smaller sub-networks

**Subnet Mask**: Determines network and host portions
- Example: 255.255.255.0 (/24)

**CIDR Notation**: Network address with prefix length
- Example: 192.168.1.0/24

**Calculations**:
- Number of hosts = 2^n - 2 (where n = 32 - prefix length)
- Subnet size = 2^prefix length

### Ports and Protocols

**Common Ports**:

| Port | Protocol | Description |
|------|----------|-------------|
| 21 | FTP | File Transfer Protocol |
| 22 | SSH | Secure Shell |
| 25 | SMTP | Simple Mail Transfer Protocol |
| 53 | DNS | Domain Name System |
| 80 | HTTP | HyperText Transfer Protocol |
| 110 | POP3 | Post Office Protocol |
| 143 | IMAP | Internet Message Access Protocol |
| 443 | HTTPS | HTTP Secure |

**Transport Protocols**:

| Protocol | Type | Features |
|----------|------|----------|
| **TCP** | Connection-oriented | Reliable, uses ports |
| **UDP** | Connectionless | Faster, unreliable |

### DNS and Domain Names

**DNS Hierarchy**:
- Root servers → TLD servers → Authoritative servers

**Record Types**:

| Type | Description |
|------|-------------|
| **A** | Maps domain to IPv4 address |
| **AAAA** | Maps domain to IPv6 address |
| **CNAME** | Alias for another domain |
| **MX** | Mail exchange server |
| **NS** | Name server |
| **PTR** | Reverse DNS (IP to domain) |
| **SOA** | Start of Authority |
| **TXT** | Text records (SPF, DKIM) |

**DNS Query Types**:
- **Recursive**: Client asks DNS server for complete answer
- **Iterative**: Client asks each DNS server in hierarchy

### Network Security

**Common Threats**:
- Malware (viruses, worms, ransomware)
- Phishing (social engineering)
- Man-in-the-Middle (MITM) attacks
- Denial of Service (DoS/DDoS)
- Unauthorized access

**Security Measures**:
- Firewalls (network and host-based)
- Intrusion Detection/Prevention Systems (IDS/IPS)
- VPNs for secure remote access
- Regular software updates and patching
- Strong authentication (MFA, passwords)
- Network segmentation and VLANs
- Encryption (TLS/SSL, IPsec)

---

**Reference**: TryHackMe Pre-Security Certification - Module 02
