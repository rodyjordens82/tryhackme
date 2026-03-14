# 🛡️ Attacks and Defenses

## Summary

This module covers common cyber attacks, security principles, defense mechanisms, and best practices for maintaining system security.

### Key Concepts

**Common Cyber Attacks**

**Malware**:
- Virus: Self-replicating malicious code that attaches to clean files
- Worm: Self-replicating malware that spreads without user intervention
- Trojan: Malicious software disguised as legitimate software
- Ransomware: Malware that encrypts files and demands payment for decryption
- Spyware: Software that secretly observes computer activity

**Network Attacks**:
- DoS/DDoS: Denial of Service attacks that disrupt services
- Man-in-the-Middle: Attacker intercepts communication between two parties
- Phishing: Fraudulent attempt to obtain sensitive information
- SQL Injection: Code injection technique to manipulate databases
- Cross-Site Scripting (XSS): Injection of malicious scripts into web pages

**Security Principles**

**CIA Triad**:
- Confidentiality: Ensuring information is accessible only to authorized users
- Integrity: Maintaining accuracy and consistency of data
- Availability: Ensuring systems are accessible when needed

**Defense in Depth**: Multiple layers of security controls
- Physical controls (biometrics, locks)
- Technical controls (firewalls, encryption)
- Administrative controls (policies, training)

**Defense Mechanisms**

**Network Security**:
- Firewalls: Filter network traffic
- IDS/IPS: Intrusion Detection and Prevention Systems
- VPN: Virtual Private Networks for secure remote access
- Network Segmentation: Dividing network into segments

**Endpoint Security**:
- Antivirus/Anti-malware: Detect and remove malicious software
- Host-based firewalls: Control traffic to/from individual devices
- Endpoint Detection and Response (EDR): Advanced threat detection

**Application Security**:
- Input validation: Prevent injection attacks
- Authentication: Verify user identity
- Authorization: Control access to resources
- Encryption: Protect data confidentiality

**Best Practices**

**Password Security**:
- Use strong, complex passwords
- Implement multi-factor authentication (MFA)
- Regular password changes
- Password managers for secure storage

**Patch Management**:
- Regular software updates
- Vulnerability scanning
- Patch testing before deployment

**Security Awareness**:
- Employee training and education
- Phishing simulations
- Security policies and procedures
- Incident response planning

**Monitoring and Logging**:
- Continuous monitoring of systems
- Comprehensive logging
- Security Information and Event Management (SIEM) systems
- Regular security audits

### Learning Objectives

- Identify common types of cyber attacks
- Understand fundamental security principles
- Learn about various defense mechanisms
- Implement security best practices
- Develop a security-aware mindset

### Prerequisites

- Basic understanding of computer networks
- Familiarity with operating systems
- Understanding of software development concepts

### Practical Examples

**Secure Password Policy**:
```
Minimum password length: 12 characters
Require mix of uppercase, lowercase, numbers, and special characters
Enforce password expiration: 90 days
Allow 3 consecutive failed login attempts before lockout
Implement MFA for all users
```

**Firewall Rules Example**:
```
Allow TCP port 80 (HTTP) from trusted IP ranges
Allow TCP port 443 (HTTPS) from any source
Deny all incoming ICMP (ping) requests
Allow RDP (TCP 3389) only from specific admin IPs
Log all denied connections
```

**Incident Response Plan**:
```
1. Detection: Identify and confirm security incident
2. Containment: Limit impact and prevent further damage
3. Eradication: Remove the cause of the incident
4. Recovery: Restore systems and data
5. Lessons Learned: Analyze and improve security posture
```

### Key Takeaways

1. Security is a continuous process, not a one-time effort
2. Multiple layers of defense provide better protection
3. Regular updates and patches are crucial for security
4. Employee training is essential for overall security
5. Monitoring and quick response improve incident outcomes

### References

- NIST Cybersecurity Framework: https://www.nist.gov/cyberframework
- CIS Controls: https://www.cisecurity.org/controls
- OWASP Top Ten: https://owasp.org/www-project-top-ten/
- ISO 27001: https://www.iso.org/standard/27001.html
