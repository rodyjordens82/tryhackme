# 💻 Linux Fundamentals

This module covers the fundamentals of Linux, its widespread use in cybersecurity, and essential commands for getting started.

## 🎯 Key Topics

- What is Linux
- Where Linux is Used
- Linux Distributions/Flavors
- Terminal Basics
- Essential Linux Commands

## 📝 Notes

### What is Linux

**Definition**: Open-source operating system based on UNIX

**Characteristics**:
- Lightweight and efficient
- Open-source (free to use and modify)
- Multiple distributions/flavors available
- Powers many everyday systems

### Where Linux is Used

Linux powers various systems and applications:

- **Websites and web applications** (every website you visit)
- **Car entertainment/control panels**
- **Point of Sale (PoS) systems** (checkout tills and registers)
- **Critical infrastructure** (traffic light controllers, industrial sensors)
- **Servers** (web servers, database servers)
- **IoT devices**
- **Embedded systems**

### Linux Distributions

**Definition**: "Linux" is actually an umbrella term for multiple UNIX-based operating systems

**Characteristics**:
- Because it's open-source, variants come in all shapes and sizes
- Different distributions suited for different use cases

**Common Distributions**:

**Ubuntu**:
- User-friendly, widely used
- Good for beginners
- Can run as server or desktop

**Debian**:
- Stable and widely used
- Foundation for many distributions

**Fedora**:
- Cutting-edge features and technologies
- Less stable but more current

**Arch Linux**:
- Minimalist approach
- Highly customizable
- Not recommended for beginners

**Linux in Cybersecurity**:
- Essential skill for cybersecurity professionals
- Powers most backend systems
- Lightweight enough to run on minimal hardware
- Ubiquitous in the industry

### The Terminal

**Definition**: Text-based interface for executing commands

**Characteristics**:
- No Graphical User Interface (GUI)
- Uses commands instead of clicking
- Intimidating at first but quickly becomes familiar
- Essential for cybersecurity work

**Why Use the Terminal**:
- Running hacking tools (dirb, Gobuster, nmap, etc.)
- File manipulation and administration
- Network testing and configuration
- Automation and scripting

### Essential Linux Commands

**Navigation and Information**:

| Command | Description | Example |
|---------|-------------|---------|
| `whoami` | Display current username | `whoami` |
| `pwd` | Print working directory | `pwd` |
| `ls` | List directory contents | `ls -la` |
| `cd` | Change directory | `cd /home/user` |

**File Operations**:

| Command | Description | Example |
|---------|-------------|---------|
| `echo` | Output text to terminal or file | `echo "Hello"` |
| `cat` | Display file contents | `cat file.txt` |
| `mkdir` | Create directory | `mkdir new_folder` |
| `rm` | Remove file or directory | `rm file.txt` |

**Text Manipulation**:

| Command | Description | Example |
|---------|-------------|---------|
| `cat` | Display file contents | `cat notes.md` |
| `echo` | Create file with text | `echo "text" > file.txt` |
| `head` | Display first N lines | `head -n 10 file.txt` |
| `tail` | Display last N lines | `tail -n 5 file.txt` |

**Command Reference**:

**What `cat` stands for**: concatenate (reads files and outputs them)

**What `ss` stands for**: socket statistics (replaces netstat in modern Linux)

**Where to find help**:
- `man [command]` - Manual pages for any command
- Press `q` to quit man pages
- Search online: `man [command]` in Google

**Practical Tips**:
- Start with basic navigation (pwd, ls, cd)
- Practice file operations regularly
- Use `ls -la` to see all files including hidden ones
- Help is always available via man pages

---

**Reference**: TryHackMe Cybersecurity 101 Certification - Module 02