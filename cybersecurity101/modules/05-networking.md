# 🌐 Networking Security

This module covers advanced networking concepts, scanning techniques, and security considerations.

## 🎯 Key Topics

- IP Ranges and Addressing
- DNS Records and Operations
- Network Scanning Basics
- Common Network Attacks
- Network Protocols
- Transport Security (TLS/SSL)
- Nmap Scanning Techniques

## 📝 Notes

### IP Ranges and Addressing

#### IPv4 Address Classes

**Class A** (10.0.0.0 - 10.255.255.255):
- Large network, many hosts
- Used for private networks

**Class B** (172.16.0.0 - 172.31.255.255):
- Medium-sized networks
- Common for enterprise LANs

**Class C** (192.168.0.0 - 192.168.255.255):
- Small networks, few hosts
- Common for home networks

#### Private vs Public IP

**Private IP Ranges** (RFC 1918):
- 10.0.0.0/8 - 10.0.0.0 to 10.255.255.255
- 172.16.0.0/12 - 172.16.0.0 to 172.31.255.255
- 192.168.0.0/16 - 192.168.0.0 to 192.168.255.255

**Special Addresses**:
- 127.0.0.1 - Loopback (localhost)
- 0.0.0.0 - Any address, used in routing
- 255.255.255.255 - Broadcast address

#### IPv6

**Format**: Eight 16-bit hextets separated by colons
**Example**: 2001:0db8::1 (shortened for readability)

**Advantages**:
- Vast address space (2^128 addresses)
- Built-in security features
- Better Quality of Service (QoS)
- Stateless address autoconfiguration
- No NAT required

### DNS Records

#### Common DNS Record Types

| Record | Purpose | Example Usage |
|--------|---------|---------------|
| **A** | IPv4 address | example.com → 93.184.216.34 |
| **AAAA** | IPv6 address | example.com → 2001:db8::1 |
| **CNAME** | Alias | www → example.com |
| **MX** | Mail server | example.com → mail.example.com |
| **NS** | Name server | example.com → ns1.domain.com |
| **PTR** | Reverse lookup | 93.184.216.34 → example.com |
| **SRV** | Service location | _sip._tcp.domain.com |
| **TXT** | Text/SPF/DMARC | v=spf1 include:_spf.google.com ~all |
| **SOA** | Domain authority | Primary, serial, refresh, retry |

#### DNS Query Types

**Recursive Query**:
- Client asks a resolver
- Resolver queries all servers in hierarchy
- Resolver returns complete answer to client

**Iterative Query**:
- Client asks DNS server directly
- DNS server gives best answer or referral
- Client continues with next server

**DNS Spoofing**: Attacker responds to queries before legitimate DNS server

### Network Scanning Basics

#### Purpose of Network Scanning

- Discover live hosts on a network
- Identify open ports and services
- Determine operating system
- Gather information for exploitation
- Assess security posture

#### Basic Scanning Techniques

**Ping Sweep**:
- ICMP Echo Request/Reply
- Host discovery
- `ping -c 4 192.168.1.1`

**Port Scanning**:
- Probe TCP/UDP ports
- Identify open/closed/filtered states
- Various scan types available

#### Nmap Introduction

Nmap ("Network Mapper") is a powerful network scanning tool.

**Features**:
- Port scanning
- Service detection
- OS detection
- Script scanning
- Traceroute
- Network discovery

### Common Network Attacks

#### SYN Flood

**Description**: Attacker sends SYN packets without completing TCP handshake

**How it works**:
1. Attacker sends multiple SYN packets to target port
2. Target allocates resources for each connection
3. Attacker never sends ACK
4. Target waits for timeout (SYN+ACK)
5. Target discards connection
6. Resources exhausted, legitimate requests fail

**Mitigation**:
- SYN cookies
- Rate limiting
- Connection limits

#### Ping of Death

**Description**: Oversized ICMP packets cause buffer overflow

**How it works**:
1. Attacker sends fragmented ICMP packet larger than allowed
2. Receiver's buffer overflows
3. System crashes or becomes unstable

**Mitigation**:
- Proper buffer handling
- ICMP packet validation

#### DNS Spoofing

**Description**: Attacker responds to DNS queries before legitimate server

**Attack Flow**:
1. Attacker intercepts query to domain
2. Attacker responds with forged IP
3. Victim uses attacker's IP instead of real server

**Mitigation**:
- DNSSEC
- DNS over HTTPS (DoH)
- DNS over TLS (DoT)

#### ARP Poisoning

**Description**: Manipulate ARP tables on local network

**How it works**:
1. Attacker sends fake ARP messages
2. Victim updates ARP cache with attacker's MAC
3. All traffic goes through attacker
4. Attacker can sniff or modify traffic

**Victim sees**: MAC address of attacker for gateway
**Attacker's goal**: Intercept or modify traffic (MITM)

**Mitigation**:
- Static ARP entries
- Dynamic ARP inspection (DAI)
- Port security
- 802.1X authentication

#### DHCP Starvation

**Description**: Exhaust DHCP leases for DoS

**How it works**:
1. Attacker requests many IP leases
2. Uses spoofed MAC addresses
3. DHPC server exhausts available addresses
4. Legitimate clients cannot get IP addresses

**Mitigation**:
- DHCP snooping
- IP address limits
- DHCP leak prevention

#### DoS/DDoS Attacks

**Description**: Overwhelm target with traffic

**Types**:
- **Volume-based**: UDP floods, ICMP floods
- **Protocol**: SYN floods, connection floods
- **Application**: HTTP floods, specific protocol attacks

**Mitigation**:
- Rate limiting
- Anycast network distribution
- Cloud-based DDoS protection
- Botnet mitigation

#### MITM Attacks

**Description**: Intercept communication between two parties

**Types**:
- **ARP Poisoning**: Local network
- **DNS Spoofing**: Network-level
- **SSL Stripping**: Downgrade HTTPS to HTTP

**Attack Flow**:
1. Attacker positions between victim and target
2. Victim believes they're talking to target
3. Attacker can read, modify, or block communication

**Mitigation**:
- TLS/SSL encryption
- Certificate pinning
- VPNs
- SSH tunnels

### Network Protocols

#### HTTP vs HTTPS

**HTTP (HyperText Transfer Protocol)**:
- Port: 80
- Unencrypted, plain text
- Vulnerable to eavesdropping, tampering, injection
- Request/Response model
- Stateless

**HTTPS (HTTP Secure)**:
- Port: 443
- Uses TLS/SSL encryption
- Secure against eavesdropping and tampering
- Request/Response model
- Can be stateful (cookies, sessions)

**HTTP Request Structure**:
```
METHOD URL PROTOCOL/VERSION
Header: Value
Header: Value
(empty line)
Body (optional)
```

**HTTP Methods**:
- GET - Retrieve resource
- POST - Submit data
- PUT - Update resource
- DELETE - Remove resource
- HEAD - Get headers only
- OPTIONS - Query capabilities

#### FTP (File Transfer Protocol)

**Ports**:
- 21 - Command port
- 20 - Data port

**Modes**:
- **Active**: Server connects to client (firewall issues)
- **Passive**: Server opens random port, client connects (common)

#### SMTP (Email)

**Ports**:
- 25 - SMTP (default)
- 587 - Submission (with authentication)
- 2525 - Alternative submission

**Commands**:
- HELO/EHLO - Greeting
- MAIL FROM - Sender address
- RCPT TO - Recipient address
- DATA - Message body
- QUIT - Exit

#### POP3 (Post Office Protocol v3)

**Port**: 110
**Purpose**: Download and remove emails from server
**Pros**: Simple, works with slow connections
**Cons**: Email removed from server

#### IMAP (Internet Message Access Protocol)

**Port**: 143
**Purpose**: Access email on multiple devices
**Pros**: Keeps email on server, syncs across devices
**Cons**: Requires more server resources

### Transport Security (TLS/SSL)

#### TLS/SSL Basics

**Purpose**: Secure communication over network

**Components**:
- **Client**: Initiates connection
- **Server**: Responds with certificate
- **Certificate Authority (CA)**: Issues and signs certificates

#### TLS Handshake Process

1. **ClientHello**:
   - Client sends supported TLS versions
   - Client sends supported cipher suites
   - Client sends random value (client random)

2. **ServerHello**:
   - Server selects TLS version
   - Server selects cipher suite
   - Server sends certificate
   - Server sends random value (server random)

3. **Client Key Exchange**:
   - Client generates premaster secret
   - Encrypts premaster secret with server's public key
   - Sends encrypted premaster secret

4. **Master Secret**:
   - Both sides derive master secret from premaster secret and random values

5. **Finished**:
   - Verify handshake integrity
   - Begin encrypted data transfer

#### Certificate Chain

```
Root CA (self-signed)
  ↓
Intermediate CA (signed by Root)
  ↓
Server Certificate (signed by Intermediate)
```

**Trust**: Browser trusts Root CA, which signs Intermediate, which signs Server

#### HTTPS Benefits

1. **Confidentiality**: Data encrypted in transit
2. **Integrity**: Data not tampered with during transit
3. **Authentication**: Server identity verified
4. **Security**: Prevents man-in-the-middle attacks

### Nmap Scanning Techniques

#### Scan Types

**TCP Connect Scan (-sT)**:
- Completes full TCP three-way handshake
- No special privileges required
- Easily detected by intrusion detection systems

**SYN Scan (-sS)**:
- Sends only SYN packet (half-open scan)
- No privilege required but root recommended
- Stealthy, fast
- Not detected by simple filters

**UDP Scan (-sU)**:
- Sends UDP packets
- No response = open/filtered
- Response = open/closed
- Time-consuming and unreliable

**Service Version Scan (-sV)**:
- Identifies service versions
- Useful for vulnerability assessment

**OS Detection (-O)**:
- Determines remote operating system
- Compares TCP/IP fingerprint
- Can be blocked by firewalls

**Aggressive Scan (-A)**:
- OS detection, version detection, scripts, traceroute
- Comprehensive but may trigger IDS

#### Host Discovery

**Ping Scan (-sn)**:
- Host discovery only, no port scan
- Uses ICMP echo requests

**Scan All (Pn)**:
- Treat all hosts as online
- Bypasses host discovery

**Timing Options**:
- `-T0` - Paranoid (very slow, waits 5 min)
- `-T1` - Sneaky (slow, waits 15 sec)
- `-T2` - Polite (moderate, waits 0.4 sec)
- `-T3` - Normal (default)
- `-T4` - Aggressive (fast)
- `-T5` - Insane (very fast, may trigger IDS)

#### Output Formats

**Normal Output (-oN)**:
- Human-readable format
- Easy to read, includes scan results

**XML Output (-oX)**:
- Machine-readable format
- Used by parsers, tools

**Greppable Output (-oG)**:
- Simple text format
- Easy to grep, awk, parse

**All Formats (-oA)**:
- Creates all three formats simultaneously

#### Practical Nmap Usage

**Scan specific port**:
```bash
nmap -p 80,443 192.168.1.1
```

**Scan all ports**:
```bash
nmap -p- 192.168.1.1
```

**Fast scan common ports**:
```bash
nmap -F 192.168.1.1
```

**Scan with version detection**:
```bash
nmap -sV 192.168.1.1
```

**Scan with OS detection**:
```bash
nmap -O 192.168.1.1
```

**Aggressive scan**:
```bash
nmap -A 192.168.1.1
```

**Verbose scan**:
```bash
nmap -v 192.168.1.1
```

**Save output**:
```bash
nmap -sS -oA scan 192.168.1.1
```

**Scan with timing**:
```bash
nmap -T4 -sS 192.168.1.1
```

#### Scanning Best Practices

**Always use sudo**:
- Root privileges enable all Nmap features
- SYN scan requires root
- OS detection may require root

**Respect privacy**:
- Don't scan unauthorized targets
- Use -Pn for automated scanning
- Respect rate limits (-T1 for polite scanning)

**Understand scan results**:
- **open**: Application listening
- **closed**: Port exists but no service
- **filtered**: Port unreachable (firewall)
- **unfiltered**: Port reachable but scan type can't determine
- **open|filtered**: Uncertain (UDP scan)
- **closed|filtered**: Uncertain (ACK scan)

---

## 📚 Quick Reference

### Nmap Common Options

| Option | Description |
|--------|-------------|
| `-sS` | SYN scan (stealth) |
| `-sT` | TCP connect scan |
| `-sU` | UDP scan |
| `-sV` | Service version detection |
| `-O` | OS detection |
| `-A` | Aggressive scan |
| `-F` | Fast scan |
| `-p-` | Scan all ports |
| `-p <ports>` | Specific ports |
| `-Pn` | Skip host discovery |
| `-T<0-5>` | Timing template |
| `-v` | Verbose |
| `-oN <file>` | Normal output |
| `-oX <file>` | XML output |
| `-oG <file>` | Greppable output |
| `-oA <file>` | All formats |

---

**Reference**: TryHackme Cybersecurity 101 - Networking Module