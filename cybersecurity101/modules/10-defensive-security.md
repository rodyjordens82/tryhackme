# Defensive Security: Incident Response and Log Analysis

> Comprehensive study guide for certificate preparation covering incident response frameworks, incident types, and log analysis techniques.

---

## Table of Contents

1. [Incident Response Fundamentals](#incident-response-fundamentals)
2. [Types of Incidents](#types-of-incidents)
3. [Incident Response Frameworks](#incident-response-frameworks)
4. [Incident Response Plan](#incident-response-plan)
5. [Incident Response Tools](#incident-response-tools)
6. [Playbooks and Runbooks](#playbooks-and-runbooks)
7. [Logs Fundamentals](#logs-fundamentals)
8. [Types of Logs](#types-of-logs)
9. [Log Analysis Techniques](#log-analysis-techniques)
10. [Windows Event Logs](#windows-event-logs)
11. [Web Server Access Logs](#web-server-access-logs)

---

## Incident Response Fundamentals

An **incident** is any event that disrupts normal operations, threatens security, or causes damage to an organization's systems or data.

### Key Concepts

- **Security Incident**: Any event that threatens or violates an organization's security policy or security measures
- **Incident Response**: The process of identifying, containing, eradicating, and recovering from security incidents
- **Proactive vs Reactive**: Incident response should be both proactive (preventive measures) and reactive (incident handling)

---

## Types of Incidents

| Incident Type | Description | Impact |
|---------------|-------------|--------|
| **Malware** | Malicious software designed to harm systems | Data theft, system compromise, denial of service |
| **Phishing** | Deceptive attempts to obtain sensitive information | Credential theft, system access |
| **SQL Injection** | Attack that injects malicious SQL code into queries | Data theft, data manipulation, system compromise |
| **Data Leaks** | Unauthorized exposure of confidential information | Reputational damage, legal consequences, competitive disadvantage |
| **Insider Attacks** | Attacks from within the organization | Significant access to resources, difficult to detect |
| **Denial of Service (DoS)** | Flooding systems with false requests | Service unavailability, financial losses |

> **Note**: The impact of incidents varies by organization. What causes minor damage to one organization could be catastrophic to another.

---

## Incident Response Frameworks

### SANS Incident Response Framework (PICERL)

| Phase | Explanation | Example |
|-------|-------------|---------|
| **P**reparation | Build resources, teams, plans, and security solutions | Conducting employee training on email security |
| **I**dentification | Look for abnormal behavior that may indicate an incident | Security team notices unusual data transfer |
| **C**ontainment | Minimize impact by isolating systems, disabling accounts | Isolating compromised host from network |
| **E**radication | Remove threat from the environment | Deep malware scan to remove malicious software |
| **R**ecovery | Recover affected systems from backups or rebuilds | Restoring exfiltrated data from backup |
| **L**essons Learned | Identify and document gaps to improve processes | Post-incident review meeting |

### NIST Incident Response Framework

NIST reduces the SANS framework to **4 phases**:

1. **Preparation**
2. **Detection and Analysis** (replaces Identification)
3. **Containment, Eradication, and Recovery** (combines Containment, Eradication, Recovery)
4. **Post-Incident Activity**

---

## Incident Response Plan

An **Incident Response Plan (IRP)** is a formal document outlining the approach during any incident. It is formally approved by senior management and consists of procedures to follow before, during, and after an incident.

### Key Components of an IRP

| Component | Description |
|-----------|-------------|
| **Roles and Responsibilities** | Define who does what during an incident |
| **Incident Response Methodology** | The approach to follow for incidents |
| **Communication Plan** | How stakeholders and law enforcement are notified |
| **Escalation Path** | Procedures for escalating incidents to appropriate levels |

---

## Incident Response Tools

| Tool | Purpose |
|------|---------|
| **SIEM (Security Information and Event Management)** | Collects and correlates logs to identify incidents |
| **AV (Antivirus)** | Detects known malicious programs and scans systems |
| **EDR (Endpoint Detection and Response)** | Protects against advanced threats, can contain and eradicate |

---

## Playbooks and Runbooks

### Playbooks

- **Purpose**: Comprehensive guidelines for a specific incident type
- **Content**: High-level step-by-step instructions for different scenarios
- **Example**: Email Phishing Playbook
  - Notify all stakeholders
  - Determine if email is malicious (header/body analysis)
  - Analyze email attachments
  - Check if attachments were opened
  - Isolate infected systems
  - Block email sender

### Runbooks

- **Purpose**: Detailed, step-by-step execution of specific procedures
- **Content**: Detailed steps that may vary based on available resources
- **Difference**: Playbooks are guidelines; runbooks are actionable procedures

---

## Logs Fundamentals

Logs are the **digital footprints** left behind by any activity, whether normal or malicious. They are crucial for:

| Use Case | Description |
|----------|-------------|
| **Security Events Monitoring** | Detect anomalous behavior in real-time |
| **Incident Investigation and Forensics** | Provide detailed information about what happened |
| **Troubleshooting** | Diagnose system and application issues |
| **Performance Monitoring** | Gain insights into application performance |
| **Auditing and Compliance** | Establish activity trails for regulatory requirements |

---

## Types of Logs

| Log Type | Usage | Examples |
|----------|-------|----------|
| **System Logs** | Troubleshooting running issues | - System startup/shutdown events<br>- Driver loading events<br>- System error events<br>- Hardware events |
| **Security Logs** | Detect and investigate incidents | - Authentication events<br>- Authorization events<br>- Security policy changes<br>- User account changes<br>- Abnormal activity events |
| **Application Logs** | Application-specific events | - User interaction events<br>- Application changes<br>- Application updates<br>- Application errors |
| **Audit Logs** | Detailed system/user events for compliance | - Data access events<br>- System change events<br>- User activity events<br>- Policy enforcement events |
| **Network Logs** | Network traffic information | - Incoming traffic events<br>- Outgoing traffic events<br>- Network connection logs |
| **Access Logs** | Resource access information | - Webserver access logs<br>- Database access logs<br>- Application access logs |

---

## Log Analysis Techniques

### Manual Analysis Commands

#### cat
Displays contents of text files:

```bash
cat access.log
# Combine multiple files
cat access1.log access2.log > combined_access.log
```

#### grep
Searches for strings and patterns in log files:

```bash
grep "192.168.1.1" access.log
```

#### less
View logs page by page with search capabilities:

```bash
less access.log
# Navigation:
# Space: Next page
# b: Previous page
# /pattern: Search for pattern
# n: Next match
# N: Previous match
```

---

## Windows Event Logs

Windows stores logs in different files categorized by type:

### Primary Windows Log Types

| Log Type | Description |
|----------|-------------|
| **Application** | Application-specific events (errors, warnings, compatibility issues) |
| **System** | OS operations (driver issues, hardware, startup/shutdown) |
| **Security** | Security-related activities (authentication, authorization, policy changes) |

### Important Event IDs

| Event ID | Description |
|----------|-------------|
| 4624 | User account successfully logged in |
| 4625 | User account failed to login |
| 4634 | User account successfully logged off |
| 4720 | User account was created |
| 4724 | Attempt made to reset an account's password |
| 4722 | User account was enabled |
| 4725 | User account was disabled |
| 4726 | User account was deleted |

### Windows Event Viewer Features

1. **Filter Current Log**: Filter logs by specific Event ID or other criteria
2. **Double-click events**: View detailed event information
3. **Key Fields**:
   - **Description**: Detailed activity information
   - **Log Name**: Log file name
   - **Logged**: Activity timestamp
   - **Event ID**: Unique identifier for the activity

---

## Web Server Access Logs

### Sample Log Format

Each log entry typically contains:

| Field | Description | Example |
|-------|-------------|---------|
| **IP Address** | User's IP address | "172.16.0.1" |
| **Timestamp** | Request time | "[06/Jun/2024:13:58:44]" |
| **Request** | HTTP method and URL | "GET /products HTTP/1.1" |
| **Status Code** | Server response | "200" (success), "404" (not found), "500" (error) |
| **User-Agent** | Browser/device information | "Mozilla/5.0 (Windows NT 10.0; Win64; x64)..." |

### Common Status Codes

- **200**: OK - Request successful
- **404**: Not Found - Resource not available
- **500**: Internal Server Error - Server-side error
- **401**: Unauthorized - Authentication required
- **403**: Forbidden - Access denied

---

## Key Takeaways

### For Certificate Preparation

1. **Understand Incident Response Phases**: Memorize SANS PICERL and NIST phases
2. **Know Incident Types**: Be able to identify and describe different incident categories
3. **Memorize Important Event IDs**: Focus on Windows Event IDs 4624, 4625, 4634, 4720-4726
4. **Understand Log Categories**: Know when to use each type of log
5. **Know Analysis Commands**: Be familiar with cat, grep, and less

### Study Tips

- Practice with actual log files from a lab environment
- Create flashcards for event IDs and log types
- Draw flowcharts for incident response processes
- Work through hands-on exercises in a safe environment

---

*This study guide is based on the official defensive security training material.*