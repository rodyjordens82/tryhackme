# Windows and AD Fundamentals

## Windows Fundamentals

### Windows Operating Systems

**Windows Versions**:
- Windows 3.1: First GUI-based OS
- Windows 95/98: Consumer versions with GUI
- Windows NT: Business-focused, introduced Active Directory
- Windows XP: Consumer version with NT kernel
- Windows 7/8/10/11: Modern consumer versions
- Windows Server: Server editions for enterprise use

### Desktop Components

- **Start Menu**: Menu to launch applications
- **Taskbar**: Shows open applications, system tray with clock
- **Notification Area**: Displays system status icons

### NTFS File System

**Features**:
- Security: ACLs (Access Control Lists) for file permissions
- Compression: Built-in file compression
- Encryption: EFS (Encrypting File System) for data protection
- Reparse points: Symbolic links and directory junctions
- Quotas: Limit disk space usage

**Common NTFS Permissions**:
- Read: List contents, read files
- Write: Modify files, create files in directory
- Execute: Run programs
- Modify: Write, delete, and modify files
- Full Control: All permissions and ability to change permissions

### User Accounts

**Types of Accounts**:
- **Local User Account**: Created on a single computer
- **Domain User Account**: Created in Active Directory, valid across all computers in the domain

**User Account Types**:
- Administrator: Full system access
- Standard User: Limited access, cannot make system-wide changes
- Guest: Limited access for temporary users

### UAC (User Account Control)

**Purpose**: Prevents unauthorized changes by requiring admin credentials

**How it works**:
- Standard users have limited privileges
- When admin tasks are needed, UAC prompts for admin credentials
- Admin actions run with elevated privileges only during the action

### System Configuration Tools

**MSConfig**:
- **Location**: `msconfig.exe`
- **Purpose**: Configure system startup, services, and boot options
- **Tabs**:
  - Boot: Configure boot settings
  - Services: Disable services
  - Startup: Disable startup applications
  - Tools: Run diagnostic tools

**Computer Management**:
- **Location**: `compmgmt.msc` or `services.msc`
- **Purpose**: Comprehensive system administration tool
- **Features**:
  - Disk Management
  - Local Users and Groups
  - Event Viewer
  - Services

**Task Scheduler**:
- **Location**: `taskschd.msc` or `control schedtasks`
- **Purpose**: Schedule tasks to run automatically
- **Types**: One-time, recurring, at logon, at startup

**Event Viewer**:
- **Location**: `eventvwr.msc`
- **Purpose**: View system and application logs
- **Log Types**:
  - Application: Application-specific events
  - System: Windows system events
  - Security: Security-related events (auditing)
  - Setup: Setup and installation events
  - Forwarded Events: Remote event logs

### Storage Management

**Disk Management**:
- **Location**: `diskmgmt.msc`
- **Features**:
  - Create/resize/shrink partitions
  - Initialize disks (MBR/GPT)
  - Convert disk formats
  - Create virtual hard disks (VHD)
  - Extend/shrink volumes
  - Mount volumes to folders

---

## Active Directory Fundamentals

### What is Active Directory?

**Definition**: Microsoft's directory service that manages and organizes network resources

**Purpose**:
- Centralized authentication and authorization
- Organize users, computers, and network resources
- Apply security policies across the network
- Simplify administration of large networks

### Active Directory Objects

**Core Objects**:
- **Users**: Individual accounts with credentials
- **Computers**: Workstations, servers, and devices
- **Security Groups**: Collections of users or computers for authorization
- **Organizational Units (OUs)**: Containers to organize objects hierarchically

### Domain Controllers

**Definition**: Server that hosts the Active Directory database and handles authentication requests

**Functions**:
- Store and replicate Active Directory data
- Authenticate users and computers
- Manage domain policies
- Provide centralized management

### Domain Structure

**Single Domain**:
- One domain contains all network resources
- Simple to manage
- Limited scalability

**Tree**:
- Multiple domains that share the same namespace
- Parent-child relationships between domains
- Example: `corp.example.com` and `us.corp.example.com`

**Forest**:
- Multiple trees with different namespaces
- Trust relationships between all domains in the forest
- Example: `corp.example.com` and `us.example.com`

### Organizational Units (OUs)

**Purpose**: Hierarchical structure to organize objects within a domain

**Benefits**:
- Apply Group Policy to specific groups of objects
- Delegate administrative control
- Simplify management by grouping related resources

**Example OU Structure**:
```
corp.example.com
├── IT Department
├── Finance Department
└── HR Department
```

### Group Policy Objects (GPOs)

**Definition**: Set of rules and configurations applied to computers and users

**Application**:
- Link GPOs to OUs or domains
- Apply to all objects in the linked OU
- Settings take effect at logon, startup, or computer startup

**Common GPO Settings**:
- Password policies
- User account controls
- Software installation
- Registry settings
- Folder redirection
- Security settings

**GPO Storage**:
- **GPOs**: Stored in Active Directory
- **SYSVOL**: Shared network folder containing GPOs and scripts
- **Policy definitions**: XML files with GPO settings

### Trust Relationships

**Purpose**: Allow users from one domain to access resources in another domain

**Types**:
- **One-way trust**: Domain A trusts Domain B
  - Users from B can access resources in A
  - Users from A cannot access resources in B
  - Direction: Trust ← Access

- **Two-way trust**: Both domains trust each other
  - Users from A can access resources in B
  - Users from B can access resources in A

**Default Trusts**:
- Domain creation creates two-way trust with parent domain
- Forest creation creates two-way trust between all domains

**Note**: Trust relationships don't automatically grant access - administrators must explicitly configure permissions.

### Authentication Protocols

**Kerberos**:
- **Default** for modern Windows
- Time-based authentication protocol
- Uses ticket-granting tickets (TGT)
- Requires synchronized clocks

**NetNTLM**:
- Legacy authentication protocol
- Used in older Windows systems
- Can be vulnerable to password cracking attacks
- Being phased out in favor of Kerberos

### Delegation of Control

**Purpose**: Grant administrative privileges to specific users for specific OUs

**Types of Delegation**:
- **Simple**: Delegate basic administrative tasks (create users, reset passwords)
- **Advanced**: Delegate complex administrative tasks (create and manage groups, configure GPOs)

**Best Practices**:
- Delegate only what's necessary
- Use "Apply Group Policy only to users or computers that are members of this group" to limit GPO scope
- Regularly review delegated permissions

---

## Key Concepts Summary

| Concept | Description |
|---------|-------------|
| **NTFS** | Windows file system with advanced security features |
| **ACLs** | Access Control Lists for file permissions |
| **Domain Controller** | Server hosting Active Directory |
| **OU** | Organizational Unit for organizing AD objects |
| **GPO** | Group Policy Object for applying configurations |
| **Trust** | Relationship between domains allowing cross-domain authentication |
| **Kerberos** | Default authentication protocol for Windows |

---

## Learning Resources

### Recommended Next Steps

If you want to deepen your understanding of Active Directory:

1. **Active Directory Hardening Room**: Learn how to secure Active Directory installations
2. **Compromising Active Directory**: Learn attack techniques and how to defend against them

---

## Module Questions

1. What is the Windows file system that provides security features like ACLs?
2. What is the role of a Domain Controller in Active Directory?
3. What is the difference between a single domain, tree, and forest?
4. What is the purpose of Organizational Units (OUs) in Active Directory?
5. What protocol is used by default for authentication in modern Windows systems?
6. What is the function of Group Policy Objects (GPOs)?