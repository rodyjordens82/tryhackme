# 📦 Software Basics

## Summary

This module covers the fundamentals of software development, programming languages, and software security principles.

### Key Concepts

**Software Development Fundamentals**

**Software Development Lifecycle (SDLC)**:
1. Planning: Define project scope, requirements, and objectives
2. Analysis: Gather and analyze requirements
3. Design: Create system architecture and design specifications
4. Implementation: Write and test code
5. Testing: Verify software functionality and quality
6. Deployment: Release software to production
7. Maintenance: Update and improve software post-release

**Programming Paradigms**:
- Procedural programming: Linear sequence of function calls
- Object-oriented programming (OOP): Organizes code into objects with properties and methods
- Functional programming: Treats computation as evaluation of mathematical functions
- Event-driven programming: Code execution triggered by events

**Programming Languages Overview**

**Low-level Languages**:
- Assembly: Machine-level programming
- C: Systems programming language

**High-level Languages**:
- Python: General-purpose scripting
- JavaScript: Web development
- Java: Enterprise applications
- C#: .NET framework

**Scripting Languages**:
- Bash: Shell scripting
- PowerShell: Windows automation
- Python: General scripting

**Software Development Tools**

**Version Control**:
- Git: Distributed version control
- GitHub: Code hosting platform
- GitLab: Complete DevOps platform

**Integrated Development Environments (IDEs)**:
- Visual Studio Code: Lightweight editor
- PyCharm: Python IDE
- IntelliJ IDEA: Java IDE
- Eclipse: Multi-language IDE

**Compilers and Interpreters**:
- GCC: GNU Compiler Collection
- Python interpreter
- Node.js: JavaScript runtime
- Java Virtual Machine (JVM)

### Learning Objectives

- Understand the software development lifecycle
- Identify different programming paradigms
- Recognize common programming languages and their uses
- Apply secure coding practices
- Use version control systems effectively
- Understand software development tools

### Prerequisites

- Basic understanding of computers and operating systems
- Familiarity with file systems and permissions

### Practical Examples

**Basic Python Script**:
```python
# Simple Python script to calculate factorial
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n-1)

# Get user input
num = int(input("Enter a number: "))

# Calculate and display result
result = factorial(num)
print(f"The factorial of {num} is {result}")
```

**Bash Script for File Operations**:
```bash
#!/bin/bash

# Create a backup directory
BACKUP_DIR="backup_$(date +%Y%m%d)"
mkdir -p "$BACKUP_DIR"

# Copy all .txt files to backup directory
cp *.txt "$BACKUP_DIR/"

# Compress the backup
tar -czf "$BACKUP_DIR.tar.gz" "$BACKUP_DIR"

# Clean up
rm -rf "$BACKUP_DIR"

echo "Backup completed: $BACKUP_DIR.tar.gz"
```

**Git Commands**:
```bash
# Initialize a new Git repository
git init

# Add files to staging area
git add .

# Commit changes
git commit -m "Initial commit"

# Create a new branch
git branch feature-branch

# Switch to the new branch
git checkout feature-branch

# Push to remote repository
git push origin feature-branch
```

### Key Takeaways

1. Software development follows a structured lifecycle from planning to maintenance
2. Different programming paradigms suit different types of problems
3. Security should be integrated throughout the development process
4. Version control is essential for collaborative development
5. Proper tooling improves development efficiency and code quality

### References

- Python Documentation: https://docs.python.org/3/
- Git Documentation: https://git-scm.com/doc
- OWASP Top Ten: https://owasp.org/www-project-top-ten/
- Secure Coding Practices: https://www.securecoding.cert.org/
