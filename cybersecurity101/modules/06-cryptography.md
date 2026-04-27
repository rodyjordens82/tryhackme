# 🔐 Cryptography Fundamentals

This module covers password hashing, cracking techniques, and cryptographic tools for cybersecurity.

## 🎯 Key Topics

- Password Hashing Basics
- John the Ripper: Wordlist Mode
- Single Crack Mode and Word Mangling
- Custom Rules for Password Complexity
- Cracking Password-Protected Archives
- SSH Key Password Cracking

## 📝 Password Hashing Basics

### What is Password Hashing?

**Definition**: Password hashing is the process of converting a plaintext password into a fixed-length string of characters (hash) that cannot be reversed.

**Why Hash Passwords?**
- Stored passwords cannot be reversed (unlike encryption)
- Prevents plaintext exposure if database is compromised
- Enables verification without knowing the actual password
- Time-consuming process slows down brute-force attacks

### Common Hash Formats

| Hash Format | Algorithm | Description |
|-------------|-----------|-------------|
| `$6$` | SHA-512crypt | Strong, Unix-like hashing |
| `$2a$` or `$2b$` | Blowfish | bcrypt variant |
| `$5$` | SHA-256crypt | SHA-256 based hashing |
| `$1$` | MD5crypt | Legacy Unix hashing |
| `raw-sha256` | SHA-256 | Raw hash without salt |

### Reading /etc/passwd and /etc/shadow

**/etc/passwd** contains user account information:
```
username:x:UID:GID:GECOS:HOME_DIR:SHELL
```

**/etc/shadow** contains encrypted passwords (only readable by root):
```
username:encrypted_password:last_changed:min:max:warn:expire:inactive:reserved
```

## 🛠️ John the Ripper

John the Ripper is a fast password cracker for Linux/Unix, Windows, macOS, and other systems.

### Installation

**Kali Linux / AttackBox**:
```bash
sudo apt-get install john
```

**From Source**:
```bash
wget http://www.openwall.com/john/john-1.9.0.tar.xz
tar -xvf john-1.9.0.tar.xz
cd john-1.9.0
./configure
make
sudo make install
```

## 📚 Wordlist Mode

### What is Wordlist Mode?

Wordlist mode is the most common approach to password cracking. It uses a pre-built list of possible passwords (wordlist) to attempt against hashed passwords.

### Common Wordlists

| Wordlist | Size | Description |
|----------|------|-------------|
| `rockyou.txt` | ~14 million | Most popular English wordlist |
| `password.txt` | ~10,000 | Simple password list |
| `common.txt` | ~20,000 | Common passwords and variations |

### Basic Usage

**Syntax**:
```bash
john --wordlist=[wordlist] --format=[format] [hash_file]
```

**Flags**:
- `--wordlist`: Specifies the wordlist file
- `--format`: Specifies the hash format (optional if auto-detected)

### Examples

#### 1. Crack /etc/shadow hashes

```bash
# Convert /etc/passwd and /etc/shadow to readable format
unshadow /etc/passwd /etc/shadow > unshadowed.txt

# Crack using rockyou.txt (auto-detect SHA-512crypt)
john --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt

# Specify format explicitly
john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt
```

#### 2. Crack SHA-256 hashes

```bash
# Create hashes.txt with raw SHA-256 hashes
echo "password" | sha256sum > hashes.txt

# Crack using wordlist
john --wordlist=/usr/share/wordlists/rockyou.txt --format=raw-sha256 hashes.txt
```

#### 3. View cracked passwords

```bash
# Show all cracked passwords
john --show unshadowed.txt

# List candidates that were attempted but failed
john --list=wordlists unshadowed.txt
```

### Hash File Format

For John to work properly, your hash file should be in this format:
```
username:hash_value
```

Example:
```
root:$6$2nwjN454g.dv4HN/$m9Z/r2xVfweYVkrr.v5Ft8Ws3/YYksfNwq96UL1FX0OJjY1L6l.DS3KEVsZ9rOVLB/ldTeEL/OIhJZ4GMFMGA0:18576::::::
```

## 🧠 Single Crack Mode

### What is Single Crack Mode?

Single Crack mode uses heuristic techniques to crack passwords by modifying the username and GECOS field information. This exploits predictable password patterns.

### How It Works

John takes the username and GECOS information to create a wordlist:
- Add numbers to the username (user1, user2, user3)
- Capitalize letters (Uppercase, Lowercase)
- Add special characters (password!, password$)
- Use information from GECOS field (full name, home directory)

### Word Mangling Examples

**Original username**: "Markus"

**Possible passwords generated**:
```
Markus1, Markus2, Markus3
MArkus, MARkus, MARKus
Markus!, Markus$, Markus*
```

### Usage

**Syntax**:
```bash
john --single --format=[format] [hash_file]
```

**Example**:
```bash
# Single mode for SHA-256
john --single --format=raw-sha256 hashes.txt

# Single mode with format specified
john --single --format=sha512crypt unshadowed.txt
```

### GECOS Field Information

GECOS stands for General Electric Comprehensive Operating System. It contains general user information:
- Full name
- Office number
- Telephone number
- Home directory

**Format**: `username:x:UID:GID:GECOS:HOME_DIR:SHELL`

Example GECOS:
```
root:x:0:0:root:/root:/bin/bash
```

John can use "root" to generate wordlists like "Root", "rOot", "root1", etc.

## 📋 Custom Rules

### What are Custom Rules?

Custom rules allow you to define password generation patterns that exploit predictable password structures, particularly for passwords that meet complexity requirements.

### Why Use Custom Rules?

Most users create passwords that meet complexity requirements but follow predictable patterns:
```
Password1! (capital first, number, symbol at end)
MyPassword123 (word + numbers)
```

### Rule Syntax

**Location**: `/opt/john/john.conf` (Kali/AttackBox) or `/etc/john/john.conf` (installed)

**Format**:
```ini
[List.Rules:RULE_NAME]
rule_sequence
```

### Common Modifiers

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

### Character Sets

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

### Creating Custom Rules

**Example 1: Password pattern "Polopassword1!"**
```ini
[List.Rules:PoloPassword]
cAz"[0-9] [!£$%@]"
```

Breakdown:
- `c` → Capitalize first letter: "polopassword"
- `Az"[0-9]"` → Append digit: "polopassword1"
- ` ` → Space (append literal space)
- `[!£$%@]` → Append one of these symbols: "!"

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

### Using Custom Rules

**Syntax**:
```bash
john --wordlist=[wordlist] --rule=RULE_NAME [hash_file]
```

**Example**:
```bash
# Use custom rule named "PoloPassword"
john --wordlist=/usr/share/wordlists/rockyou.txt --rule=PoloPassword unshadowed.txt

# Full example
john --wordlist=/usr/share/wordlists/rockyou.txt --rule=PoloPassword hashes.txt
```

### Built-in Rule Files

John comes with extensive built-in rules at:
- `/opt/john/john.conf` (lines ~678 onwards)
- `/etc/john/john.conf`

Check the built-in rules if custom rules aren't working:
```bash
cat /opt/john/john.conf | grep -A 50 "List.Rules:"
```

### Rule Examples from John

Common patterns in John's rule files:
```
# Common password patterns
lC0s
cU0s
# Append digits and special chars
Az"[0-9]"
Az"[0-9a-zA-Z]"
# Prepend numbers
A0"[0-9]"
# Swap case and add special chars
sAz"[!@#$%^&*]"
```

## 📦 Cracking Password-Protected Archives

### Zip Files

#### 1. Convert Zip to John hash

**Tool**: `zip2john`

**Syntax**:
```bash
zip2john [options] [zip file] > [output file]
```

**Example**:
```bash
# Basic usage
zip2john zipfile.zip > zip_hash.txt

# With options (rarely needed)
zip2john -o [checksum] zipfile.zip > zip_hash.txt
```

**Output format**:
```
zipfile.zip/john:$zip$2*0*3000*4*8*8*b4be6e0*5*30*c4b4f7*4*0*0*6bae8b*
```

#### 2. Crack the hash

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
```

### RAR Files

#### 1. Convert RAR to John hash

**Tool**: `rar2john`

**Syntax**:
```bash
rar2john [rar file] > [output file]
```

**Example**:
```bash
# Basic usage
rar2john rarfile.rar > rar_hash.txt
```

**Output format**:
```
rarfile.rar:$rar5$*3e*4*0*0*e0b3c4f8a1d6b2e4*1*4*a7b3d8f2c5e1a4b6*...
```

#### 2. Crack the hash

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt
```

## 🔑 SSH Key Password Cracking

### What is SSH Key Authentication?

SSH keys are more secure than passwords. A private key (`id_rsa`, `id_ecdsa`, etc.) is used for authentication, but the private key itself may be password-protected.

### Cracking SSH Key Passwords

**Tool**: `ssh2john`

#### 1. Convert SSH private key to John hash

**Syntax**:
```bash
ssh2john [id_rsa file] > [output file]
```

**Example**:
```bash
# Basic usage
ssh2john id_rsa > id_rsa_hash.txt

# On systems with Python instead of ssh2john
python3 /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt
# Or on Kali
python /usr/share/john/ssh2john.py id_rsa > id_rsa_hash.txt
```

**Output format**:
```
id_rsa:$ssh2$1024$2a3e4f5g6h7i8j9k0l1m2n3o4p5q6r7s8t9u0v1w2x3y4z5a6b7c8d9e0f1g2$h3k4l5m6n7o8p9q0r1s2t3u4v5w6x7y8z9a0b1c2d3e4f5g6h7i8j9k0l1m2n3o4p5q6r7s8t9u0v1w2x3y4z5a6b7c8d9e0f1g2*
```

#### 2. Crack the hash

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
```

### Using the Cracked Password

Once cracked, use the password to access the SSH key:
```bash
ssh -i id_rsa username@target_ip
```

## 📊 Additional John Features

### Password Cracking Modes

| Mode | Description |
|------|-------------|
| `--wordlist` | Standard wordlist mode |
| `--single` | Heuristic single crack mode |
| `--incremental` | Incremental mode (generate words by incrementing) |
| `--mask` | Mask mode (pattern-based cracking) |
| `--rules` | Apply custom rules |

### Incremental Mode

Generate passwords based on character sets:
```bash
john --incremental id_rsa_hash.txt
```

### Mask Mode

Use patterns to crack passwords:
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt --mask='?l?d?d?d?d?d' hashes.txt
```

### Performance Optimization

**GPU Acceleration** (if supported):
```bash
# John can use GPU with john-jumbo
john --format=raw-sha256 --gpu id_rsa_hash.txt
```

**Parallel Processing**:
```bash
# Use multiple cores
john -t 4 --wordlist=rockyou.txt unshadowed.txt
```

## 🎓 Learning Tips

### Understanding Password Security

1. **Use strong, unique passwords**: Minimum 12+ characters, mixed case, numbers, symbols
2. **Use a password manager**: Generate and store complex passwords
3. **Enable multi-factor authentication (MFA)**: Even if passwords are cracked
4. **Don't reuse passwords**: Compromise on one site doesn't affect others

### Understanding Attackers

1. **Time is their enemy**: Complex passwords slow down cracking
2. **Predictability is their friend**: People use patterns they can predict
3. **Comprehensive wordlists**: Attackers use massive wordlists
4. **Parallel processing**: They use GPU/cloud computing for speed

### Common Password Patterns to Avoid

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

## 📖 References

- **John the Ripper Official Wiki**: http://www.openwall.com/john/
- **Openwall Password Cracking**: http://www.openwall.com/john/
- **Hashcat Wiki**: https://hashcat.net/wiki/
- **TryHackMe Cybersecurity 101 Module**: Cryptography

---

**Reference**: TryHackMe Cybersecurity 101 Certification - Module 06