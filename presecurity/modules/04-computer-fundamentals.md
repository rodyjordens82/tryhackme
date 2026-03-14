# 💻 Computer Fundamentals

This module covers the essential concepts of computer hardware, operating systems, and basic computing principles.

## 🎯 Key Topics

- Computer Hardware Basics
- Operating Systems
- File Systems
- Command Line Basics
- Basic Scripting

## 📚 Learning Objectives

By the end of this module, you should be able to:
- Identify and describe the main components of a computer system
- Understand how operating systems manage hardware resources
- Navigate file systems and understand file permissions
- Use basic command line operations
- Write simple scripts to automate tasks

## 📖 Module Content

### 1. Computer Hardware Basics

#### Key Components
- **CPU (Central Processing Unit)**: The "brain" of the computer that executes instructions
- **RAM (Random Access Memory)**: Temporary storage for active programs and data
- **Storage (HDD/SSD)**: Permanent storage for files and programs
- **Motherboard**: Main circuit board connecting all components
- **GPU (Graphics Processing Unit)**: Handles graphics rendering and parallel processing
- **Power Supply**: Provides electrical power to components

#### Hardware Interfaces
- USB, HDMI, Ethernet, Wi-Fi, Bluetooth
- Expansion cards and ports

### 2. Operating Systems

#### What is an Operating System?
An operating system (OS) is system software that manages computer hardware and software resources and provides common services for computer programs.

#### Common Operating Systems
- **Windows**: Microsoft's OS for desktops and servers
- **macOS**: Apple's OS for Mac computers
- **Linux**: Open-source OS with many distributions (Ubuntu, Fedora, Debian, etc.)
- **Mobile OS**: Android and iOS

#### OS Functions
- Process management
- Memory management
- File system management
- Device management
- User interface
- Security and permissions

#### Linux Distributions
- Ubuntu: User-friendly, good for beginners
- Fedora: Cutting-edge features, backed by Red Hat
- Debian: Stable, widely used as a base for other distros
- Arch Linux: Minimalist, highly customizable
- CentOS/RHEL: Enterprise-grade, stable releases

### 3. File Systems

#### File System Basics
- Hierarchical structure (directories/folders and files)
- Paths: absolute vs relative
- File permissions (read, write, execute)

#### Common File Systems
- **NTFS**: Windows default
- **ext4**: Linux default
- **FAT32/exFAT**: Compatible with multiple OS
- **APFS**: Apple's file system for macOS

#### File Operations
- Creating, reading, updating, and deleting files
- Copying and moving files
- Searching for files
- File compression and archiving

### 4. Command Line Basics

#### Basic Commands
```bash
# Navigation
cd /path/to/directory       # Change directory
pwd                        # Print working directory
ls                          # List files and directories

# File operations
cp source destination      # Copy files
mv source destination      # Move/rename files
rm file                    # Remove file
mkdir directory            # Create directory
rmdir directory            # Remove directory

# Viewing files
cat file                   # Display file contents
less file                  # View file with pagination
head file                  # View first lines
 tail file                 # View last lines

# Searching
find /path -name "pattern" # Find files by name
grep "pattern" file        # Search for text in files

# System information
df -h                       # Disk space usage
free -h                     # Memory usage
ps aux                      # Running processes
 top                        # Interactive process viewer
```

#### Command Line Tips
- Use tab completion
- Use `man command` for help
- Use `--help` flag for options
- Use `history` to view command history
- Use `!number` to repeat a command from history

### 5. Basic Scripting

#### Why Scripting?
- Automate repetitive tasks
- Combine multiple commands
- Create reusable workflows
- Schedule tasks

#### Scripting Languages
- **Bash**: Built into Linux/Unix systems
- **Python**: Versatile, easy to learn
- **PowerShell**: Windows scripting
- **JavaScript**: For web automation

#### Bash Script Example
```bash
#!/bin/bash

# Simple backup script
SOURCE="/home/user/documents"
DESTINATION="/backup/documents_$(date +%Y%m%d).tar.gz"

# Create backup
tar -czf "$DESTINATION" "$SOURCE"

# Verify backup
if [ -f "$DESTINATION" ]; then
    echo "Backup created successfully: $DESTINATION"
else
    echo "Backup failed"
    exit 1
fi
```

#### Python Script Example
```python
#!/usr/bin/env python3

import os
import shutil
from datetime import datetime

# Configuration
source_dir = "/home/user/documents"
backup_dir = "/backup"

# Create backup filename
backup_name = f"documents_{datetime.now().strftime('%Y%m%d')}.zip"
backup_path = os.path.join(backup_dir, backup_name)

# Create backup
shutil.make_archive(backup_path.replace('.zip', ''), 'zip', source_dir)

# Verify
if os.path.exists(backup_path):
    print(f"Backup created successfully: {backup_path}")
else:
    print("Backup failed")
    exit(1)
```

## 🎯 Practical Exercises

1. **Hardware Identification**: Identify the main hardware components in your computer
2. **OS Exploration**: Explore your operating system's settings and features
3. **File System Navigation**: Practice navigating the file system using command line
4. **File Operations**: Create, copy, move, and delete files using command line
5. **Script Creation**: Write a simple backup script in Bash or Python

## 📚 Additional Resources

- **Books**: "Computer Organization and Architecture" by David A. Patterson
- **Online Courses**: Coursera's "Introduction to Computer Science"
- **Documentation**: Linux man pages, Python documentation

## 🧪 Quiz

1. What does CPU stand for?
2. Name three common operating systems.
3. What command lists files in the current directory?
4. What is the purpose of RAM?
5. What file system is commonly used in Linux?

---

**Reference**: TryHackVault - Computer Fundamentals Module
