# 🖥️ Command Line Mastery

This module covers both Windows PowerShell and Linux Bash shell usage, including shell scripting fundamentals.

## 🎯 Key Topics

- **Windows PowerShell**:
  - Basic PowerShell commands
  - System information commands
  - File operations and hashing
  - Scripting with Invoke-Command

- **Linux Bash Shell**:
  - Basic shell commands
  - Different shell types (Bash, Fish, Zsh)
  - Shell scripting fundamentals
  - Variables, loops, and conditional statements

## 📝 Windows PowerShell

### Basic Commands

| Command | Description | Example |
|---------|-------------|---------|
| `Get-Date` | Get current date and time | `Get-Date` |
| `Get-Host` | Get host information | `Get-Host` |
| `Get-Service` | Get list of services | `Get-Service` |
| `Get-Process` | Get running processes | `Get-Process` |
| `Get-ComputerInfo` | Get detailed system info | `Get-ComputerInfo` |
| `Get-NetIPConfiguration` | Get network configuration | `Get-NetIPConfiguration` |

### File Operations

| Command | Description | Example |
|---------|-------------|---------|
| `Get-FileHash` | Calculate file hash | `Get-FileHash -Algorithm SHA256 path.txt` |
| `Get-ChildItem` | List directory contents | `Get-ChildItem` |
| `Set-Content` | Write to file | `Set-Content path.txt "content"` |
| `Get-Content` | Read file contents | `Get-Content path.txt` |

### Viewing Alternate Data Streams (ADS)

**Purpose**: View hidden data stored in ADS

**Command**: `Get-Content path.txt -Stream ads_name`

**Example**: `Get-Content password.txt -Stream ads_password`

### Scripting with Invoke-Command

**Purpose**: Execute commands on remote computers

**Basic Syntax**: `Invoke-Command -ComputerName [TARGET] -ScriptBlock { [COMMAND] }`

**Example**: `Invoke-Command -ComputerName target.com -ScriptBlock { Get-Process }`

### Command History

**List commands**: `Get-History`

**Clear history**: `Clear-History`

## 📝 Linux Bash Shell

### Basic Commands

| Command | Description | Example |
|---------|-------------|---------|
| `whoami` | Display current user | `whoami` |
| `pwd` | Print working directory | `pwd` |
| `ls` | List files and directories | `ls -la` |
| `cd` | Change directory | `cd /home/user` |
| `echo` | Output text to terminal | `echo "Hello World"` |
| `cat` | Display file contents | `cat filename.txt` |
| `grep` | Search for text in file | `grep pattern filename.txt` |

### File Operations

| Command | Description | Example |
|---------|-------------|---------|
| `mkdir` | Create directory | `mkdir new_folder` |
| `rm` | Remove file or directory | `rm filename.txt` |
| `history` | Display command history | `history` |

### Shell Types Comparison

| Shell | Full Name | Features |
|-------|-----------|----------|
| **Bash** | Bourne Again Shell | Default shell, scripting, tab completion, command history |
| **Fish** | Friendly Interactive Shell | User-friendly, syntax highlighting, auto spell correction |
| **Zsh** | Z Shell | Advanced tab completion, customization, scripting |

### Shell Features

- **Tab Completion**: Press TAB to complete commands or paths
- **Command History**: Use UP/DOWN arrows to access previous commands
- **Current Shell**: `echo $SHELL` or `ps -p $$`

### Shell Scripting Basics

**Shebang**: Must start with `#!/bin/bash`

**Execution Permissions**: `chmod +x script.sh`

**Running**: `./script.sh`

### Shell Script Components

#### Variables

```bash
#!/bin/bash
name="John"
echo "Welcome, $name"
```

#### Loops

```bash
for i in {1..10}
do
    echo $i
done
```

#### Conditional Statements

```bash
if [ "$name" = "John" ]; then
    echo "Authorized"
else
    echo "Denied"
fi
```

#### Comments

```bash
# This is a comment
echo "This will execute"
```

## 🔍 Output Interpretation

### HTTP Status Codes

| Code | Meaning |
|------|---------|
| 200 | Page found |
| 301 | Redirect |
| 403 | Forbidden |
| 404 | Not found |

## 🛠️ Practical Skills

### Windows PowerShell

- Use `Get-Command` to find available commands
- Use `Get-Help` to learn command syntax
- Use `Get-FileHash` to verify file integrity
- Execute remote commands with Invoke-Command

### Linux Bash

- Master basic navigation and file commands
- Use `grep` to search file contents
- Write shell scripts for automation
- Understand different shell types and their features

## 🎓 Key Concepts

### Shell Importance

- Text-based interface for executing commands
- Essential for running hacking tools
- Intimidating at first but quickly becomes familiar

### Scripting Benefits

- Automate repetitive tasks
- Combine multiple commands into single execution
- Save time on routine operations

### Shell Types

- Each shell has unique features and syntax
- Choose based on your needs and familiarity
- Common shells: Bash (most common), Fish (user-friendly), Zsh (advanced)