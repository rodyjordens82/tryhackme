# 🚀 Start Your Cyber Security Journey

This module introduces you to offensive security concepts, getting started in cybersecurity, and practical tools for discovering hidden website pages.

## 🎯 Key Topics

- Offensive Security Fundamentals
- Getting Started in Cybersecurity
- Using dirb for Brute Force Discovery
- Terminal Basics
- Career Paths in Cybersecurity

## 📝 Notes

### Offensive Security

- **Definition**: Simulating hacker actions to find vulnerabilities in systems
- **Goal**: Understand hacker tactics to improve system defenses
- **Key Concept**: "To outsmart a hacker, you need to think like one"
- **Offensive Security**: Breaking into systems, exploiting bugs, finding loopholes in applications
- **Legal Practice**: All exercises are performed in safe, legal environments

### Getting Started in Cybersecurity

**Learning Approach**:
- TryHackMe provides simulated environments
- Labs can be reverted to initial state - don't be afraid to experiment
- Learn by doing: hack your first website in a safe environment
- Focus on ethical hacking practices

**Practical Lab Example**:
- Simulated bank environment (FakeBank)
- Goal: Find hidden features and exploit vulnerabilities
- Use legal and ethical approach throughout

### Using dirb - Brute Force Directory Discovery

**What is dirb**:
- Brute-force tool for finding hidden website pages
- Uses list of potential page names to test one by one
- Works because people often use predictable names

**Usage**:
```bash
dirb [TARGET_URL]
```

**Example**:
```bash
dirb http://fakebank.thm
```

**Output Interpretation**:
- `+ http://URL (CODE:200|SIZE:bytes)` - Page found
- `CODE:301` - Redirect
- `CODE:403` - Forbidden
- `CODE:404` - Not found

### Terminal Basics

**What is a Terminal**:
- Text-based interface for executing commands
- Essential for running hacking tools like dirb
- Intimidating at first but quickly becomes familiar

**Accessing the Terminal**:
- Click on Terminal icon (usually on the right side of screen)
- Enter commands and press ENTER to execute

### Career Paths in Cybersecurity

**Offensive Security Roles**:
- **Penetration Tester**: Tests products for exploitable vulnerabilities
- **Red Teamer**: Simulates adversary attacks and provides feedback
- **Security Engineer**: Designs, monitors, and maintains security controls

**Defensive Security Roles**:
- **Security Analyst**: Monitors and responds to cyber threats
- **Incident Responder**: Investigates and mitigates security incidents
- **Security Architect**: Designs secure systems and infrastructure

### Defensive Security

**Definition**: The practice of preventing intrusions and responding when they occur

**Key Areas**:
- Preventing intrusions
- Detecting intrusions
- Responding properly

**Blue Team**: Team focused on defensive security

**Defensive Security Tasks**:
- User cybersecurity awareness training
- Asset documentation and management
- System updating and patching
- Setting up preventative security devices (firewalls, IPS)
- Setting up logging and monitoring systems

**Security Operations Center (SOC)**:
- Team of professionals monitoring network and systems
- Main areas of interest:
  - Vulnerabilities
  - Policy violations
  - Unauthorized activity
  - Network intrusions

**Threat Intelligence**:
- Information about actual and potential adversaries
- Collects, processes, and analyzes data
- Helps companies prepare against potential attacks
- Identifies threat actors and their motives
- Enables threat-informed defense

**Digital Forensics and Incident Response (DFIR)**:

**Digital Forensics**:
- Application of science to investigate crimes and establish facts
- Analyzing evidence of attack and perpetrators
- Key areas:
  - Forensics images (low-level copy of system storage)
  - System memory
  - System logs
  - Network logs

**Incident Response**:
- Methodology for handling cyber attacks
- Four major phases:
  1. **Preparation**: Team trained and ready, preventive measures in place
  2. **Detection and Analysis**: Detect incidents and analyze severity
  3. **Containment, Eradication, and Recovery**: Stop incident, eliminate threat, recover systems
  4. **Post-Incident Activity**: Create reports, share lessons learned

**Malware Analysis**:
- Malware: malicious software (viruses, Trojans, ransomware)
- **Static Analysis**: Inspecting malware without running it
- **Dynamic Analysis**: Running malware in controlled environment and monitoring

### Search Skills

**Information Evaluation**:
- Assess source credibility
- Check evidence and reasoning
- Evaluate objectivity and bias
- Validate with corroboration from multiple sources

**Search Operators**:
- `"exact phrase"` - Find pages with exact phrase
- `site:domain` - Limit search to specific domain
- `term -exclude` - Exclude results with specific term
- `filetype:format` - Find specific file types (pdf, doc, xlsx, ppt)

**Specialized Search Engines**:

**Shodan**:
- Search engine for Internet-connected devices
- Search for servers, networking equipment, IoT devices
- Example: `apache 2.4.1`

**Censys**:
- Focuses on Internet-connected hosts, websites, certificates
- Use cases: enumerate domains, audit open ports, discover rogue assets

**VirusTotal**:
- Virus-scanning service using multiple antivirus engines
- Upload files or provide URLs to scan
- Input file hashes to check previously uploaded files

**Have I Been Pwned (HIBP)**:
- Tells if email appeared in leaked data breaches
- Indicates leaked passwords
- Essential for checking password exposure

**Reference Databases**:
- **CVE Program**: Dictionary of vulnerabilities with standardized IDs
  - Format: `CVE-YYYY-NNNNN`
  - Visit: cve.org
  - Alternative: NVD (National Vulnerability Database)
- **Exploit Database**: Repository of exploit codes
- **GitHub**: Contains proof-of-concept (PoC) and exploit codes

**Documentation Sources**:
- **Manual Pages (man pages)**: Built-in documentation for Unix/Linux commands
  - Command: `man [command]`
  - Press `q` to quit
- **Official Product Documentation**: Most up-to-date and reliable source
  - Examples: Snort, Server, Node.js documentation

**Social Media**:
- **LinkedIn**: Learn about technical background of company employees
- **Twitter/X**: Stay updated with security trends
- **Facebook**: Look for answers to secret questions in social media posts
- **Best Practices**: Use temporary accounts, don't use primary email

**News Outlets**:
- Hundreds of security news websites
- Subscribe to relevant outlets for staying updated

---

**Reference**: TryHackMe Cybersecurity 101 Certification - Module 01