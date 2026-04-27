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

*This document is designed to help you build your cybersecurity career. Master the fundamentals, gain hands-on experience, and stay curious about new threats and technologies.*