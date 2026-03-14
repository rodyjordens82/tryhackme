You turn on your phone or laptop every day, and everything just works: apps launch, files open, music plays, and the whole system feels seamless. But what actually makes all this possible? In the Computer Fundamentals module (coming soon), you explored the physical components of a computer and the different types of computing devices. Now it’s time to uncover the invisible layer that ties it all together: the operating system, or OS.

A graphic of an airport scene representing the various components of a user's computer.
Scenario

Your friend just upgraded their primary computer and, knowing you're getting into tech, has generously gifted you their old machine. It's been sitting untouched for a while, and he can't remember much about it, only that it “used to run well”. Before you can decide whether to upgrade it, wipe it, sell it, or turn it into your next project, you need to figure out precisely what you're dealing with.
Learning Objectives

    Understand what an operating system is and the role it plays
    Explain the core duties of an operating system
    Identify common OS types and their typical use cases
    Practice interacting with an OS to gather system information

Prerequisites

Before you begin this room, it is recommended that you complete the Computer Fundamentals module (coming soon) of the Pre Security Path. This room builds on core ideas introduced earlier, especially your understanding of computer hardware, device types, and how modern systems boot and operate.

    Inside a Computer System
    Computer Types

Answer the questions below

I understand the learning objectives and am ready to learn about operating systems!

The Invisible Manager

An operating system (OS) is the core software that coordinates everything happening on a computer. It sits between the user, applications, and the system’s physical hardware, acting as the invisible manager that keeps the entire machine running as one unified system.

A visual diagram illustrating the layers of a computer with the physical hardware on the bottom, operating system second, the applications third, and the user on top.

A helpful analogy is to think of your computer as a busy airport, with all its components functioning together.

    Your hardware (CPU, RAM, storage, connected devices): The runways, airplanes, fuel systems, radar, and other physical infrastructure.
    Your applications (web browser, game launcher): The various airlines and their passengers, all trying to take off, land, and request services.
    Your operating system (Windows, Linux, macOS): The entire air traffic control system, directing all of this activity. It schedules resources, manages traffic, resolves conflicts, and ensures safety.

A graphic showing an airport from the perspective of air traffic control which represents the computer's operating system.

We need an operating system because it provides this all-important job of coordination and structuring that makes modern computing possible. Without an OS, each application would need direct control over the CPU, memory, files, devices, and security. This would quickly cause conflicts, and the OS handles this by acting as the central organizer. In the Computer Fundamentals module (coming soon), you learned about various computer components and their duties. Now, we will see how the operating system manages and allocates these resources when you use your PC.
System Privilege Layers

Inside a modern computer, different parts of the system operate at various permission levels. Some components can communicate directly with the hardware, while regular applications run in a safer, restricted environment. This separation is intentional and helps prevent conflicts and security issues.

    Kernel space: The privileged, locked-down core of the OS. This is where the kernel, the part of the operating system that directly manages hardware and system resources, runs. It has unrestricted access to the CPU, memory, storage, and all hardware components.
    User space: Where all standard applications run. Applications in the user space are deliberately prevented from accessing hardware directly. Whenever they need to open or save a file, play a sound, or connect to Wi-Fi, they must make a system call and request that the kernel act on their behalf.

Building on our airport analogy, let's zoom in on the concept of privilege separation. The kernel space is the control tower, a strictly secured area where only trusted air-traffic controllers (the kernel) work. They alone can directly control the runways, radar, and other hardware. Applications in the user space are like airlines and passengers on the ground. They can't enter the tower or touch the equipment. Instead, they radio requests (system calls) to the tower, which handles them safely. This separation keeps the OS reliable: one faulty app can't crash the whole system, just as no airline can operate safely without the tower's control.
Operating System Duties

Now that you know what an operating system is and how system privilege is separated, let’s look at what it actually does behind the scenes. Every OS is responsible for a few core duties that allow your computer to run safely, efficiently, and predictably.
OS Responsibility 	What the OS Does 	Example
Process Management 	Creates, schedules, prioritizes, and terminates running programs. The OS decides how much CPU time each process gets, making multitasking feel seamless 	Opening multiple apps, like your browser, music player, and social media, without your computer freezing
Memory Management 	Allocates RAM to processes, protects the app's memory from other processes, and reclaims memory when apps are closed. When RAM runs low, the OS uses virtual memory to keep your system stable 	Opening multiple app at once, the OS allocates RAM to each one and keeps them isolated so they don’t interfere or crash each other
File System Management 	Organizes files into directories, handles naming, paths, permissions, metadata (name, size, type, timestamps) 	Creating a new folder, saving a photo, or setting a file to "read only"
User Management 	Handles multiple user accounts, authentication, and permissions to determine who can access what 	Logging in with your password and keeping your files inaccessible to other user accounts
Device Management 	Loads drivers and provides a universal interface (hardware abstraction layer), so apps can say “print this” or “play this sound” 	Plugging in a new mouse, printer, or external hard drive and having it work immediately
Operating System Security

It is important to understand that every OS also acts as a security foundation. Before any antivirus, firewall, or security tool is introduced, the OS is already enforcing protections in the background, some of which we covered above.

At a basic level, your operating system handles

    Authentication: Verifies who you are through login passwords and biometrics
    Permissions: Controls exactly what each user and app is allowed to read, write, or execute
    Isolation: Keeps every process in its own protected box (kernel/user space separation)
    System Protection: Safeguards critical system files and settings from unauthorized changes

Getting Hands-on

Now that you have a solid understanding of what an operating system is and its main duties, let's get hands-on with your new computer. Click the Start Machine button below to fire up your new computer. The machine will open in split view, at which time you'll gain access to the computer's Desktop. If split view is not opening, press the Show Split View button at the top of the page.
Set up your virtual environment
To successfully complete this room, you'll need to set up your virtual environment. This involves starting the Target Machine, ensuring you're equipped with the necessary tools and access to tackle the challenges ahead.
Target machineMachine info
Status:Off

Remember, your friend said he doesn't know much about the PC he gave you, so let's dive in and try to gain some initial information about what you're working with. On the Desktop of the machine, there is a shortcut named About This Computer that opens your computer's System Monitor. Go ahead and open it now, as you will need it for some of the questions in this task.

A screenshot of the Ubuntu desktop highlighting the "About This Computer" system monitor launcher.
Answer the questions below

Which OS space has unrestricted access to your computer's hardware?

Which OS responsibility manages user accounts, authentication, and permissions?

After opening the About This Computer shortcut, you are greeted with an overview of the system's specifications.
What version of Ubuntu Mate is your computer running?

Check out the Hardware section of the System tab.
How much memory is allocated to your machine?

OS Interaction and Landscape
OS Interfaces

Now that you have a solid understanding of the operating system and its various responsibilities, let's look at how we interact with the OS. Interaction with the OS can be divided into two main parts: the graphical user interface (GUI) and the command-line interface (CLI).

Graphical User Interface

The GUI is what you're most likely used to interacting with. It provides a graphical representation of all the information you want to access on your computer. Think of folder icons, windows for your applications, and menus for settings. We can imagine the analogy of using a navigation application. You tap an icon of the place you want to visit, and the app generates directions for you, eliminating the need for typing.

Command-line Interface

The CLI is where you enter specific text-based commands to retrieve or manipulate information. Instead of clicking on icons, you tell the computer exactly what you want using words and syntax that the system understands. This gives you far more precision, control, and speed, especially for advanced tasks, but it requires familiarity with the commands. Back to the maps analogy. Using the CLI is like entering the exact GPS coordinates of your destination. It’s direct and extremely accurate, but only if you know the correct information to type.

Later in this module, you will explore the CLI on both Linux and Windows to learn how to navigate files, inspect system information, and interact with your OS beyond the GUI.

In the screenshot below, you can see that the GUI and CLI are both used to retrieve the same information. In this case, to display the contents of the ubuntu user's home directory. The GUI requires a few clicks for folder navigation, whereas the CLI requires a command to list the directory contents.

A composite screenshot of the ubuntu user's home directory listing the directory contents using file explorer (GUI) on the left and command-line (CLI) on the right.
The Operating System Landscape

Nice! We are gaining a much clearer picture of the OS, its responsibilities, and how we can interact with it to manage our computer. Now it's time to look at the bigger picture; not all operating systems are the same. Different devices and jobs demand different designs, ranging from your phone to a web server in a data center. Below are the five major categories you'll run into in the real world:
Operating System Type 	Primary Use Case 	Key Characteristics
Desktop 	Personal computers, daily work, gaming, content creation 	Rich graphic interface, runs many apps at once, user-focused
Server 	Web hosting, databases, cloud services, back-end 	Headless (no GUI), maximum uptime, multi-user, remote access
Mobile 	Smartphones and tablets 	Touch-based UI, power efficient, always connected, app sandboxing
Embedded 	Appliances, cars, IoT devices, smart TVs, routers 	Tiny footprint, runs on limited hardware
Virtual/Cloud 	Virtual machines, containers, cloud instances 	Lightweight, scalable, rapid deployment
Real World Operating Systems

Now that you’ve seen the different types of operating systems and what they’re designed for, let’s look at the major families of operating systems you’ll encounter in the real world. Each family fills one or more of the OS types we just explored. To keep things organized, we’ll highlight the common versions or distributions you’ll see in each and follow the same categories as above: Desktop, Server, Mobile, Embedded, and Virtual/Cloud.

Desktop

    Windows: The most widely used operating system on personal computers
    Windows 10 (end-of-life), Windows 11
    macOS: Apple's desktop OS, known for its polished GUI and integration with other Apple devices
    Sonoma (14), Sequoia (15), Tahoe (26)
    Linux: Not a single OS but a family of open-source operating systems called distributions
    Ubuntu, Debian, Fedora

Server

    Windows: Used in large networks, data centers, and corporate environments
    Server 2016, 2019, 2022, 2025
    Linux: The vast majority of web servers, trusted for its reliability and open-source nature
    Ubuntu Server, Debian, CentOS, Red Hat
    Unix: Large enterprises, finance, telecom, government
    IBM AIX, Oracle Solaris

Mobile

    Android: The most widely used mobile OS, which runs on phones, tablets, and smart devices
    Android 14 - 16, Manufacturer versions
    iOS: Apple's mobile OS running on iPhones, iPads, and other devices
    iOS 17, 18, 26

Embedded and IoT Devices

    Embedded Linux: Specialized OS built into devices with dedicated functions
    OpenWrt, Ubuntu Core, Yocto Project
    Real-Time OS: Designed for apps where tasks need guaranteed response times (aircraft controls)
    FreeRTOS, VxWorks, QNX

Virtual and Cloud

    Cloud/VM: Massive data centers that host websites, apps, and streaming services
    Ubuntu LTS, Amazon Linux, Rocky Linux
    Container-optimized: Lightweight alternatives to VMs that package just the app and its dependencies
    Alpine Linux, Bottlerocket AWS, Flatcar Linux

A composite image of the Windows logo, Tux Linux logo, Apple logo, and Android logo to represent different operating systems discussed.
Why So Many Operating Systems?

Different devices and environments require different capabilities from an OS. A laptop must be user-friendly and support multitasking. Servers require stability, security, and must be able to run continuously without interruption. Mobile devices need power efficiency and hardware integration to extend battery life. Embedded systems use lightweight operating systems designed for a specialized purpose.

The companies and communities that develop these operating systems also have their own goals. Some focus on ease of use, performance, security, openness, or customization. Because each environment values different capabilities, no single OS is the perfect fit for every situation. Instead, an ecosystem of operating systems has evolved.
Continuing Your Investigation

From the previous task, you learned that your new computer is running the Ubuntu distribution of Linux. You were also able to determine the version and release. Let's continue the investigation and gather further information about the system. You will continue to use the About This Computer shortcut, then jump into the Home directory, which can be found on your computer's Desktop.

A graphical representation of a computer homescreen displaying a home icon, folder icon, and open browser with a magnifying glass overlaying it to represent the investigation portion of the task.
Answer the questions below

Open the File Systems tab in System Monitor.
What Type is listed for the /dev/root device?

After opening the Home directory on the Desktop, how many user directories exist?

Navigate to Alex's home directory and explore the Documents folder.
What is the flag value contained in note.txt?

Conclusion

Well done, you've reached the end of Operating Systems Introduction. In this room, you learned what an OS really does behind the scenes and explored key concepts, including privileges, user management, memory handling, and processes. In the practical exercise, you investigated a mystery computer gifted to you by a friend. You used the operating system to take a peek into the hardware and file systems it helps manage.
Key Terminology

Let’s recap the core terms you’ve learned. These definitions will help solidify your understanding before moving on to further learning.

    Operating system (OS)
    The core software that manages hardware, applications, and all system resources.
    Kernel space
    The OS’s highly privileged area with direct hardware access, and the home of the kernel, which directly manages hardware and system resources.
    User space
    The area where regular applications run with limited permissions for safety and system stability.
    Graphical user interface (GUI)
    The visual part of the OS, windows, icons, and menus, that lets you interact through clicking and tapping.
    Command-line interface (CLI)
    A text-based interface where you type commands to control the system with precision and speed.

Further Learning

In the following rooms of the Operating System module (coming soon), you'll dive deeper into Windows and Linux operating systems, learning how to navigate each system using both the GUI and CLI. You'll gain further hands-on experience performing real tasks, gathering system information, and interacting with the OS!

    Windows Basics
    Linux CLI Basics
    Windows CLI Basics

Answer the questions below

Complete the room and continue on your cyber learning journey!

Introduction

Every operating system has its own personality, and if you’ve used a computer at school, work, or home, there’s a good chance you’ve already met the most familiar one: Microsoft Windows. In the previous room, you explored what an operating system is, the behind-the-scenes manager that keeps your device running smoothly. Now it’s time to step into a real example and see the previously learned concepts take shape on a system you may already recognize. In this room, you’ll get hands-on experience with the Windows interface and begin building practical skills that will lay the foundation for the subsequent rooms of the module.
Scenario

In this room, you’ll take on the role of a new employee starting your first day at TryHatMe. Once you log in to your workstation, you’ll get to know the Windows desktop, learn how the interface works, open tools from the Start menu, and find your way through company folders. Your supervisor will guide you in creating and organizing files, changing system settings, checking the Task Manager, and reviewing basic security settings. By the end of these onboarding tasks, you should feel comfortable using Windows and handling the daily tasks you'll be expected to handle.

A graphical illustration of a worker running the assembly line at the fictional company TryHatMe.
Learning Objectives

    Navigate the Windows graphical interface, including the desktop, taskbar, and Start menu
    Use File Explorer to browse folders, understand file paths, and organize files effectively
    Check system settings and personalize the Windows environment using the Settings app
    Use basic system tools like Task Manager and Windows Security to monitor performance and verify system protection

Prerequisites

Before you begin, it is recommended that you complete the following rooms to make sure you have the foundational knowledge needed.

    Work through Inside a Computer System to learn how computers start up and how components like the CPU, RAM, and storage interact
    Go over Computer Types to understand the variety of computing systems and how their roles, capabilities, and designs differ
    Complete Operating Systems: Introduction to build a clear understanding of what an operating system does and how it functions

Machine Access

Click the Start Machine button below to launch your Windows Server 2019 workstation. The machine will open in split-screen mode, giving you access to the Windows desktop used throughout this room.
Set up your virtual environment
To successfully complete this room, you'll need to set up your virtual environment. This involves starting the Target Machine, ensuring you're equipped with the necessary tools and access to tackle the challenges ahead.
Target machineMachine info
Status:Off
Answer the questions below

I understand the learning objectives and am ready to learn about Windows!

Exploring the Windows Workspace

Before Windows had its current polished look, Microsoft’s operating systems were much simpler. Early computers ran MS-DOS, which showed a black screen where you had to type commands instead of clicking icons. In 1985, Microsoft released Windows 1.0, a basic graphical user interface (GUI) built on top of DOS, introducing windows, menus, and mouse controls to personal computers. Over time, Windows has added more features, which turned the original shell into a complete operating system. Today, the modern Windows OS is the result of those changes. Let’s dive into Windows and see how the operating system concepts you learned about in the previous room present themselves in the world’s most widely used desktop operating system.

A composite screenshot showing the evolution of the Windows OS with Windows 1.0 on the left, Windows Me in the center, and Windows 11 on the right.
Logging in and Authentication

Before gaining access to the Windows Desktop, you must authenticate (prove your identity) to the system. The authentication process verifies your identity and determines the actions you're allowed to take once logged in. When a Windows system starts, it displays a login screen where a user account must be selected and authenticated with a password, PIN, or another verification method. Each user is assigned a set of permission levels that determine their access to files, settings, and system functionality. Windows commonly uses the account types below.

    Guest: A restricted account intended for temporary access, with minimal permissions and no ability to change system settings
    Standard: A user account for everyday tasks, such as running applications and changing personal settings, without access to system-wide changes
    Administrator: A privileged account with full control over the system, including software installation, configuration changes, and user management

A screenshot of the Windows Server 2019 login screen showing the Administrator username and blank password.

Upon starting up the machine in the previous task, you are automatically logged in using an Administrator account. This will allow you to explore system settings, install programs, and perform administrative actions without being restricted by permission limitations. 
The Windows Desktop

In the last room of this module, we explored the comparison of an OS to an airport. Let's continue with this analogy. If you, the user, are a passenger, and the login screen represents the airport security checkpoint, you can consider the Desktop to be the airport terminal. After entering, it is the first area you gain access to, and all other subsequent areas branch out from this point. 

A graphical illustration of an airport terminal representing the computer desktop.

Let's have a look at the Windows Desktop and cover some of its core features together. When you first log in, you're presented with two main areas.

    Desktop: The main workspace where files, folders, and shortcuts live
    Taskbar: A control strip that provides access to applications, system tools, settings, and notifications

Let's break these down further to get a better picture. Please note that the instance used in this room and the screenshot below are using Windows Server 2019. While newer Windows versions may differ slightly, these core components and concepts remain consistent.

    Desktop icons: Shortcuts to items like the Recycle Bin, folders, and frequently used applications. It is fully customizable
    Start menu: Primary way to access applications, settings, and power options. From here, you can log out, restart, or power off your machine
    Search: Quickly find applications, files, folders, and system settings by using keywords
    Task View: Allows you to see all currently open windows and quickly switch between them
    Pinned Applications and Folders: Your most used applications and folders can be pinned here
    Network and Audio settings: This section can be customized to suit your needs
    Date and Time: Opens up to a full calendar. Date and time settings can be accessed here, too
    Notifications: Displays computer or application notifications. Network and other settings can also be accessed

A screenshot of the Windows desktop highlighting the desktop icons, start menu, search, task view, pinned apps and folders, network and audio settings, date and time, and notifications.

Start Menu

When using Windows, the Start menu can be accessed by clicking the Windows icon located at the bottom left of the taskbar. If we consider the Windows Desktop to be an airport terminal, the Start menu is the departure board or information desk. It is the area where we see what is available: apps, files, folders, settings, and power options. You can think of it as a quick-access menu.

A screenshot of the Windows Start menu highlighting the different options it provides, including user options, documents, pictures, settings, and power, as well as quickly accessible apps, settings, and folders.
Built-in Tools and Apps

Windows ships with many useful built-in tools and applications that you will use daily. Beyond the wide range of settings available to manage your system, Windows also includes simple but powerful tools such as Notepad for editing text files and File Explorer for navigating and managing files. These tools are available immediately and form the foundation of everyday Windows usage. All of them can be accessed via the Start menu and search bar. The built-in tools on Windows are like airport services and amenities, the things already available in the terminal to help you get tasks done.

A composite screenshot of the Windows built-in applications, including the calculator, file explorer, notepad, and paint.
Getting System Information

Windows includes a built-in Settings application that allows you to configure and view information about your system. To get to know your new work PC better, we’ll start by investigating the machine we’re working with. Within the Settings app, there's a helpful section called About your PC, that provides key details about the system. A shortcut to About your PC has been created on the Desktop. Open it now. Alternatively, you can practice using the Start Menu or Search feature to locate it.

The About your PC page provides an overview of security, device, and operating system information. We’ll use this information to become familiar with our environment and begin answering the first questions in this task.

A composite screenshot of the About your PC Windows application desktop shortcut and the main page of the application displaying security, device, and operating system details.
File Exploration and Management

Great, now we have an understanding of the system we are working with. Let’s take a look at how Windows handles file exploration and management as we access some of the onboarding documents for your new position. Before we dive into using File Explorer, let’s quickly cover how Windows organizes files and directories. Windows uses a hierarchical folder structure, meaning folders can contain other folders and files inside them. This structure helps keep data organized and makes it easier to locate information as systems grow larger. Common locations, such as the Desktop, Documents, and Downloads, serve as primary directories for storing files. Within these locations, subfolders are used to group related files together. Understanding this layout will make navigating the system and managing files much easier.

If we continue the airport analogy, File Explorer acts as the directory and floor map of the terminal, helping you navigate between different areas and locate what you need.

You can now open the TryHatMe Onboarding folder on the Desktop. Alternatively, you can open the File Explorer application, which is pinned to the Taskbar, or use the Start menu to locate the folder.

    Open the TryHatMe Onboarding folder on your Desktop
    This opens the folder in the Windows File Explorer
    Options for viewing, sharing, and editing folders and files
    Clicking the folder name will show us the full path to the chosen folder
    C:\Users\Administrator\Desktop\TryHatMe Onboarding
    The displayed contents of our chosen folder
    We can use the File Explorer's built-in search function to search our folder

A screenshot of the Windows desktop displaying the TryHatMe Onboarding folder and the opened folder with numbers referencing the steps taken to navigate through the folder's contents.
Answer the questions below

Please ensure the virtual machine is open in split-screen, then take a look at the computer's Desktop.
After opening About your PC, navigate to the Device specifications section.
What is the Device name specified?

Continue looking through the Device specifications.
How much RAM is installed on your new work PC?

Scroll down to the Windows specifications section.
Which Version of Windows Server 2019 Datacenter is installed?

Explore the TryHatMe Onboarding folder located on your computer's Desktop.
What is the flag value found within Welcome.txt?

Configuring and Securing Windows

Applications are the programs and tools you use to perform tasks on your computer, from browsing the web and editing photos to managing settings on your PC. We already discussed a few of the built-in applications Windows provides, but knowing how to install, update, and remove applications is a core skill for everyday Windows use. Let's briefly revisit the airport analogy to gain a better understanding of this concept. Updating your OS or apps is like changing flights or reserving a seat. Installing a new app is comparable to scheduling a new flight, and removing apps is like canceling a booking you no longer need. These three processes enable you to make the necessary changes to your system, ensuring you have exactly what you need and that your system remains secure.
Updating Your Applications

Keeping your operating system and applications up to date is an important part of maintaining a secure and stable system. Updates will often include security patches, performance updates, and bug fixes.

Windows Updates

Windows includes a built-in update tool called Windows Update, which keeps the OS and some native applications and security features up to date. Windows Update can be accessed through the Settings app and may install updates automatically, depending on your configuration.

A composite screenshot of Check for updates in System settings with the Windows Update page in Settings showing the current available updates.

Updating Applications

Application updates work differently depending on how the software is installed.

    Built-in applications may update automatically in the background
    Third-party applications often include their own update mechanisms
    Some applications will prompt you to update upon launch
    Some require you to check for updates or download a new installer manually

Installing Applications

Now that you've seen how updates work within the Windows OS and for applications, let's take a look at installing new ones.

    Microsoft Store: Provides a curated and safe option for installing apps to Windows, although it is not available by default on Windows Server
    From the Internet: In many environments, apps are installed by downloading an installer directly from a trusted vendor's website. They usually come in an .exe or .msi file and guide the user through the installation process

A composite screenshot of the Microsoft Store application and Windows download page for 7-Zip.

Hands-On Installation

Great, now you have a solid understanding of updating and installing new applications within a Windows environment. Let's get hands-on and install an app!

    Within the TryHatMe Onboarding folder on your Desktop, you'll find an installer named TryHatMeWelcome
    Proceed by double-clicking the installer to start the installation process, then answer the first question of the task

Note: Feel free to click through the installation options; remember that this is a virtual environment, safe for testing and experimentation.

A screenshot of the TryHatMe Onboarding folder on the Windows desktop and the folder open, highlighting the application installer for TryHatMeWelcome.
Uninstalling Applications

In a Windows environment, there are multiple ways to uninstall programs.

    Using the Microsoft Store for installed applications
    Add or remove programs feature in system settings
    Uninstall a program section of the Control Panel
    Using an application's built-in uninstaller

A composite screenshot of the add or remove program feature and the Control Panel, highlighting Uninstall a program.
Diving Into Settings

In the previous task, you explored the About your PC section of Windows settings. Now, we will take a closer look at the abundance of configurations available to us. There are two primary ways in which a Windows user can modify their environment. There are existing shortcuts for each of the tools below placed on your Desktop.

    Windows Settings: A modern, centralized location for configuring system, device, personalization, and security settings in Windows
    Control Panel: A legacy management interface that provides access to older system configuration tools still required for specific administrative tasks

Windows Settings and the Control Panel enable you to view and modify how your Windows system operates. From these two applications, you can manage system preferences, including display and audio settings, user accounts, apps, network options, accessibility features, and security configurations.

A composite screenshot of the Windows Settings application and the Control Panel.
The Task Manager

Task Manager is a built-in Windows tool that allows you to monitor what is happening on your system in real time. It allows you to view running applications and background processes, as well as check system performance, including CPU and memory usage. A shortcut to Task Manager has been placed on your workstation's Desktop. Go ahead and open it now to view your currently running applications and check on your system's performance.

Task Manager has five tabs to help you keep track of your system.

    Processes: Currently running apps and background processes, and their resource usage
    Performance: Graphs and statistics for system resources such as CPU, memory, and network
    Users: Currently logged-in users and used resources 
    Details: A more technical view of running processes, including process IDs (PIDs)
    Services: Windows services and their current status (running or stopped)

A screenshot of the Task Manager desktop shortcut and the Task Manager application with corresponding numbers to the numbered list above.
Native Windows Security

Windows offers built-in security tools designed to help protect your system from threats such as malware, insecure applications, and unauthorized network access. These are enabled by default and allow the monitoring and control of your system's security. 

Windows Security

The Windows Security application is your central dashboard for managing Windows' built-in protection measures. It is divided into four main sections, each focusing on a different area of system security.

    Virus & threat protection: Helps detect and remove malicious software using real-time protection and customizable scans
    Firewall & network protection: Controls incoming and outgoing network traffic to help prevent unauthorized access
    App & browser control: Protects users from potentially unsafe apps, files, and websites
    Device security: Provides hardware-based protections that help secure the system

Let's take a closer look at the Virus & threat protection section of Windows Security on your workstation. Go ahead and open it up using the Desktop shortcut or via the Start menu now. Next, we will run a custom scan of your onboarding folder to ensure that there are no malicious files present. 

    Open Windows Security using the shortcut on your Desktop
    Select the Virus & Threat protection section
    Choose Scan options
    Select Custom scan, then Scan now
    Select the TryHatMe Onboarding folder on your Desktop as the target of your scan

A composite screenshot of the Windows Security Desktop shortcut, the Windows Security application highlighting virus & threat protection, the scan options, custom scan, and target folder for the scan.

Your custom scan will have found a completely safe test file, and this process shows how Windows is capable of scanning for and detecting threats. Keep in mind that this is just one aspect of the security measures Windows has in place to help you secure your system. Go ahead and click See details to investigate the file and answer the final question of the task.

A screenshot of the scan options page in Windows security highlighting the severity level and see details option.
Windows Defender Firewall

Windows Defender Firewall is a built-in firewall designed to help protect your computer from unauthorized network traffic. It monitors network connections and applies rules that determine whether the connections are allowed or denied. The firewall operates on different network profiles, allowing you to create custom rules or specify applications that are permitted.

    Domain: Used when a system is connected to an organization’s domain network
    Private: Intended for trusted networks, such as a home or lab environment 
    Public: Used for untrusted networks, such as public Wi-Fi

A composite screenshot of the Windows Defender Firewall application alongside a list of allowed apps from the firewall.

Checking out the Advanced settings of Windows Defender Firewall, you can view

    An overview of your firewall's inbound, outbound, and connection rules
    A detailed view of each rule, including name, group, network profile, status, and action
    Create new rules or filter your current view

A screenshot of the Windows Defender Firewall application showing advanced settings with a numbers referencing the corresponding task numbered list.
Answer the questions below

Use the TryHatMeWelcome installer located within the TryHatMe Onboarding folder.
What is the flag value you receive after installing and running the application?

Investigate the Time & Language section of the Windows Settings app.
Which country or region is your computer currently set to?

Open the Task Manager on your workstation's Desktop and navigate to the Users tab.
Which account is currently logged in?

After performing your custom scan, click Virus:DOS/EICAR_Test_File and select See details.
What is the file name shown in the Affected items section?

Conclusion

Nicely done! You’ve reached the end of Windows Basics. In this room, you explored the fundamentals of the Windows operating system. You navigated the Windows interface, examined system properties, learned about application management, worked with files and folders, and managed security settings that make up a Windows environment.

Through a hands-on lab, you completed your first day at TryHatMe, using the Windows Server 2019 operating system to read files, install programs, and run security scans on your new workstation. These skills form the foundation for both general system usage and deeper technical understanding later on in your learning and professional journey.
Key Terminology

Let’s recap the core terminology and applications you’ve learned about in this room. These definitions will help solidify your understanding before moving on to further learning.

    Desktop: The main workspace where files, folders, and shortcuts live
    Taskbar: A control strip that provides access to applications, tools, settings, and notifications
    Start Menu: The primary way to access applications, settings, and power options, signified by the Windows logo
    Search: A quick access method of locating applications, settings, and files by entering search terms
    File Explorer: The built-in Windows tool to browse, manage, and organize files and folders
    Windows Update: A built-in update tool that helps keep your OS, native apps, and security features up to date
    Microsoft Store: The native Windows application for installing trusted applications
    Windows Settings: A centralized location for configuring system, device, personalization, and security settings
    Control Panel: The legacy management interface that provides access to system configuration options
    Task Manager: A Windows tool for monitoring what is happening on your system in real time
    Windows Security: The central dashboard for managing Windows built-in security tools
    Windows Defender Firewall: The firewall designed to help protect your system from unauthorized network traffic

Further Learning

In the following rooms of this module, you'll use the command-line (CLI), a text-based interface for interacting with the operating system, to get to know the Linux OS and further explore Windows.

    Linux CLI Basics
    Windows CLI Basics

Answer the questions below

Complete the room and continue on your cyber learning journey!

Introduction

In cyber security, Linux is everywhere, powering servers, security tools, and even hacking environments. However, before you can defend systems or investigate incidents, you need to know how to navigate the Linux OS using the command-line interface (CLI). This room takes you on a guided mission as a brand-new intern in a cyber security team. We will explore the absolute basics of Linux CLI through hands-on tasks, simple missions, and beginner-friendly explanations.

By the end of this task, you'll understand what the terminal is, why it matters, and how you'll use it throughout the room.
Learning Objectives

    Understand what the Linux terminal is and what it's used for.
    Feel comfortable interacting with the Linux environment.
    Navigate through the Linux filesystem with basic commands.

Prerequisites

    Operating Systems: Introduction
    Windows Basics

Storyline: Your First Day on the Job

Congratulations, today is your first day as an IT Support Engineer with the Cyber Operations Support Team. You were supposed to get a proper introduction and a tour of the tools you'll be using, but things in this field don't always go as planned.

Your supervisor left in a hurry to deal with an urgent incident. Before they ran out the door, they left you a short note on your desk:

Note from the supervisor reading "Welcome! I didn’t have time to walk you through everything, but you’ll pick up the details quickly. Most of our work happens in the Linux terminal, and I’ve set up a few simple tasks on the system to help you get comfortable. Start by opening the terminal and exploring a bit."

So here you are on your own for now, faced with a terminal prompt and a bit of mystery. Don't worry, though. Each step in this room will guide you through exactly what to do. You'll learn how to move around the system, read files, and gather information - the same basic skills that cyber security professionals use every day.

Ready to begin?
Answer the questions below

What does "CLI" stand for?

Navigation Mission: "Find the Missing Notes"

Before starting, click on the Start Machine button below. This will start your target machine in split view. If split view is not visible, press the Show Split View button at the top of the page.
Set up your virtual environment
To successfully complete this room, you'll need to set up your virtual environment. This involves starting the Target Machine, ensuring you're equipped with the necessary tools and access to tackle the challenges ahead.
Target machineMachine info
Status:Off
A Quick Note About the Terminal

Before we begin exploring, let's take a moment to familiarize ourselves with the tool we're using.

The terminal is a text-based interface for controlling a Linux system. Instead of interacting with the graphical interface, you type commands that tell the computer exactly what to do. Cyber security professionals use it because:

    It's faster than clicking around
    It gives more control
    Many security tools only run in the terminal

If the terminal feels unfamiliar at the moment, that's completely normal.

By the end of this room, it will feel far more comfortable,  and you'll see it as a straightforward tool rather than something intimidating. Double-click on the Terminal file present on the Desktop, as shown below:

Image showing linux Desktop pointing to the terminal application
Interacting With the Terminal

Now that you know what the terminal is, it's time to start using it.
Your supervisor mentioned leaving a few tasks in the document mission_brief.txt, somewhere on the system; which means your first mission is to find them. To do that, you'll need to learn how to move around the Linux filesystem.

This task will introduce the core navigation commands that every Linux user learns on their first day.
Step 1: "Where Am I?"

When you first open a terminal, you might not know what part of the system you're in.
Use this command to find out: pwd
PWD Command

ubuntu@tryhackme:~$ pwd
/home/ubuntu

    

It stands for "print working directory", which basically means "show me the folder I'm currently in". 
Step 2: "What's Around Me?"

Now that you know where you are, let's see what files and folders are here: ls
ls Command

      
ubuntu@tryhackme:~$ ls
Desktop    Downloads  Pictures  Templates  logs
Documents  Music      Public    Videos     projects

    

This lists the content of the current directory. If we need more details, we can try: ls -l
ls -l Command

ubuntu@tryhackme:~$ ls -l
total 44
drwxr-xr-x 2 ubuntu ubuntu 4096 Feb 27  2022 Desktop
drwxr-xr-x 6 ubuntu ubuntu 4096 Dec 11 12:45 Documents
drwxr-xr-x 2 ubuntu ubuntu 4096 Feb 16  2024 Downloads
drwxr-xr-x 2 ubuntu ubuntu 4096 Feb 27  2022 Music
drwxr-xr-x 2 ubuntu ubuntu 4096 Feb 27  2022 Pictures
drwxr-xr-x 2 ubuntu ubuntu 4096 Feb 27  2022 Public
drwxr-xr-x 2 ubuntu ubuntu 4096 Feb 27  2022 Templates
drwxr-xr-x 2 ubuntu ubuntu 4096 Feb 27  2022 Videos
drwxr-xr-x 4 ubuntu ubuntu 4096 Dec 11 12:29 logs
drwxr-xr-x 5 ubuntu ubuntu 4096 Dec 11 12:29 projects
drwx------ 3 ubuntu ubuntu 4096 Sep 12  2024 snap

    

The output displays important information about the files and directories like file sizes, permissions, dates, and more.

Hidden Files

In order to get the hidden files in the directory, we can append the command to ls -al, and it will display all the hidden files present in the directory, as shown below:
ls -al Command

      
ubuntu@tryhackme:~$ ls -al
total 144
drwxr-xr-x 24 ubuntu ubuntu  4096 Feb 10 10:48 .
drwxr-xr-x  3 root   root    4096 Feb 10 10:36 ..
-rw-------  1 ubuntu ubuntu   439 Feb 10 06:47 .Xauthority
-rw-rw-r--  1 ubuntu ubuntu     0 Sep 12  2024 .Xresources
-rw-r--r--  1 ubuntu ubuntu   111 Oct  3  2024 .apport-ignore.xml
----------
--------------------
drwxr-xr-x  2 ubuntu ubuntu  4096 Feb 27  2022 Templates
drwxr-xr-x  2 ubuntu ubuntu  4096 Feb 27  2022 Videos
drwxr-xr-x  4 ubuntu ubuntu  4096 Dec 11 12:29 logs
drwxr-xr-x  5 ubuntu ubuntu  4096 Dec 11 12:29 projects
drwx------  3 ubuntu ubuntu  4096 Sep 12  2024 snap

    

Hidden files aren't really secret; they start with a dot ., and Linux hides such files by default.
Step 3: Let’s Move Around

To walk through the filesystem, we can use: cd <directory>. For example: cd Documents, and this will change our directory to Documents, as shown below
cd Command

ubuntu@tryhackme:~$ cd Documents/
ubuntu@tryhackme:~/Documents$ pwd
/home/ubuntu/Documents

    

To go "back" one level, we will use the command cd .., as shown below:
cd Command

      
ubuntu@tryhackme:~/Documents$ cd ..
ubuntu@tryhackme:~$ pwd
/home/ubuntu

    

Step 4: Learn the Power of "Find"

Let's now use one of the handy tools to find. As the name suggests, this built-in utility is used to locate files within the file system. Here's a simple version of the command: find <starting_point> -name <filename>. Since your supervisor mentioned that the file mission_brief.txt resides somewhere in your home directory, begin the home directory symbol: ~. So we will run the command: find ~ -name mission_brief.txt, as shown below:
find Command

      
ubuntu@tryhackme:~$ find ~ -name mission_brief.txt
/<REDACTED-PATH>/mission_brief.txt

    

Please note that this may take a moment, as Linux will check every folder inside your home directory. If the file exists, Linux will print the full path to it. The above result shows that the command has successfully located the file and provided us with its complete path, allowing us to navigate and read the file's content.

Let's use the cd command to navigate to the folder. We can also do ls to confirm the presence of the file, as shown below:
cd Command

ubuntu@tryhackme:~$ cd /<REDACTED-PATH>/     
ubuntu@tryhackme:~/<REDACTED-PATH>$ ls
mission_brief.txt            

    

Step 5: Read the File

Another useful utility is cat. This is used to read the content of the file. To read this file, we will run the command cat mission_brief.txt to get the content, as shown below:
cat Command

      
ubuntu@tryhackme:~/<REDACTED-PATH>$ cat mission_brief.txt 
Great job finding your way around the terminal.

Your next assignment is to collect a small system report:
- Who you're logged in as
- The kernel version
- Total disk space
- The name of this Linux distribution

Once you gather those details, you'll be ready for the next step.

FLAG:<REDACTED>

    

Perfect. This is great progress. You have completed the task. 

After answering the questions, let's proceed to the next task and learn how to retrieve system information using the commands in the CLI.
Answer the questions below

What is the full path of the mission_brief.txt file found on the system using the find command?

What is the flag hidden inside the mission_brief.txt file?

Investigating the System

NImage depicting system being examinedow your supervisor wants you to gather some basic information about the system you’re working on. This kind of information helps cyber security teams understand what environment they’re operating in, what version of Linux they’re using, and what resources are available.

Think of this as taking a quick health check of the machine.
Your Next Assignment

When you opened mission_brief.txt, it contained a new message:

Great job finding your way around the terminal. Your next assignment is to collect a small system report:

    Who you're logged in as
    The kernel version
    Total disk space
    The name of this Linux distribution

You’re still on your own for now, but at least the instructions are clear: collect system info and send it back. Let’s break the job into small steps.
Step 1: "Who Are You Logged in As?"

The simplest command in Linux also happens to be one of the most useful: whoami
whoami Command

ubuntu@tryhackme:~$ whoami
ubuntu

    

This prints your current username.
Step 2: "What System Are You On?"

To see details about the operating system, kernel version, and architecture, use: uname -a
uname -a Command

      
ubuntu@tryhackme:~$ uname -a
Linux tryhackme <REDACTED>-aws #17-Ubuntu SMP Mon Sep  2 13:48:07 UTC 2024 x86_64 x86_64 x86_64 GNU/Linux

    

This gives a full line of system information - great for understanding exactly what environment you're working in.

Breakdown of the Information

    Linux: The system is running the Linux kernel.
    tryhackme: The hostname (the computer’s name).
    <REDACTED>-aws: The kernel version installed on the machine.
    x86_64: The hardware platform (also 64-bit).
    GNU/Linux: The operating system type (Linux kernel + GNU tools).

If you only want the operating system name, you can try: uname
uname Command

ubuntu@tryhackme:~$ uname
Linux

    

But for now, uname -a gives the fuller picture.
Step 3: Check Disk and Storage Info

In real-world environments, you’ll often need to check disk usage or available space, especially before running tools or analyzing logs. A simple command for readable output is: df -h
df -h Command

ubuntu@tryhackme:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        --G   12G   --G  17% /
tmpfs           1.9G     0  1.9G   0% /dev/shm
tmpfs           774M  1.2M  773M   1% /run
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           387M  192K  387M   1% /run/user/1000
tmpfs           387M  172K  387M   1% /run/user/114

    

The -h means "human readable"; it shows sizes like 2G or 500M instead of long bytes-only numbers.

Breakdown of the Information

    /dev/root is the main disk of the system with --G total, 12G used, <REDACTED>G free, and is 17% full.
    tmpfs entries are temporary filesystems stored in RAM, not on the physical disk.
    /dev/shm is a shared memory area with 1.9G available and 0 used.
    /run/user/114 is similar temporary storage for another system user, also 387M total and mostly empty.

Step 4: Read a System File

Linux stores configuration and informational files in the /etc directory.
To practice navigating and reading files, head into /etc by running cd /etc and then list what’s inside: ls
cd Command

ubuntu@tryhackme:~$ cd /etc
ubuntu@tryhackme:/etc$ ls
ImageMagick-6                  cloud                 firefox               hp               logcheck              opt                     rmt                sysctl.d
ModemManager                   compizconfig          fonts                 ifplugd          login.defs            os-release              rpc                sysstat
NetworkManager                 console-setup         fstab                 init             logrotate.conf        overlayroot.conf        rsyslog.conf       systemd
---
-------
chatscripts                    ethertypes            hosts.deny            localtime        openvpn               resolv.conf             sysctl.conf
ubuntu@tryhackme:/etc$ 

    

Let’s now use cat to read the os-release file that almost every Linux system contains: cat os-release, as shown below:
 cat Command

ubuntu@tryhackme:/etc$ cat os-release 
PRETTY_NAME="Ubuntu 24.04.1 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.1 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo

    

This file provides details about the Linux distribution that are often clearer than those provided by the uname command.

Great work. With just a few commands, we were able to retrieve the system information as requested by the supervisor.
Wrapping Up Your First Day 

You’ve navigated the filesystem, searched for hidden files, and gathered system information, solid progress for your first steps into Linux. Before you finish your day, your supervisor has left one final task to test everything you’ve learned so far.
Nothing too hard, just a quick check to make sure you can put the basics together on your own.
Mini Challenge

You only know the name of the file: day1_report.txt
Your job:

    Use the find command to locate it somewhere in your home directory.
    Navigate to the folder where it was found.
    Read the file contents using cat.
    Use it for the the last question in this task.

No step-by-step instructions this time. You’ve earned the confidence to do this on your own.
Answer the questions below

What is the username returned by the whoami command?

What is the kernel version shown by uname -a?

How much free disk space does df -h report?

What is the message written inside day1_report.txt?

Conclusion

And that’s your first day on the Cyber Operations Support Team.
You learned how to:

    Navigate the Linux filesystem
    Search for files
    Inspect system information
    Read important configuration files
    Follow clues and complete missions inside a Linux environment

These skills may seem simple, but they’re the building blocks for everything that comes later: file permissions, users & groups, processes, package management, and eventually real security tooling.
You’re off to a strong start.
Answer the questions below

Continue to complete the room.

Introduction

In the previous Linux CLI Basics room, you took your first steps into the Linux command line. Today, you're continuing your journey, but this time on Windows. Windows is one of the most widely used operating systems in workplaces worldwide. As someone interested in cyber security, you will often investigate or troubleshoot Windows machines, especially user desktops and laptops.

In this room, you'll learn how to use the Windows Command Prompt to navigate files, search for information, and gather basic system details using the same hands-on, story-driven approach as before.

From a security perspective, Windows is important because many real-world attacks and investigations involve Windows systems.
What Is the Windows Command Line?

The Command Prompt (often referred to as CMD) is a text-based interface for interacting with the Windows operating system. Instead of clicking folders and menus, you type commands to tell the system exactly what you want to do, such as listing files, moving between folders, or checking system information. It might look simple, but it's a powerful and widely used tool.
Learning Objectives

By the end of this room, you will be able to:

    Use the Windows command line confidently
    Navigate folders without clicking
    Find files when you only know their name
    Read files using the terminal
    Collect basic system and network information

Prerequisites

This room expects you to have explored the following rooms to understand better:

    Operating Systems
    Linux CLI Basics

Storyline: Day 2 on the Job

You arrive for the second day of your internship. Your supervisor greets you with a quick update:

So here you are on your own for now, faced with a terminal prompt and a bit of mystery. Don't worry, though. Each step in this room will guide you through exactly what to do. You'll learn how to move around the system, read files, and gather information - the same basic skills that cyber security professionals use every day.

Ready to begin?
Answer the questions below

Continue to the next task.

Windows CLI: Navigating Files and Finding Your First File

Before starting, click on the green button Start Machine, shown below:
Set up your virtual environment
To successfully complete this room, you'll need to set up your virtual environment. This involves starting the Target Machine, ensuring you're equipped with the necessary tools and access to tackle the challenges ahead.
Target machineMachine info
Status:Off
A Quick Recap About the Terminal

Before we begin exploring, let's take a moment to familiarize ourselves with the tool we're using.Linux Terminal Image Representation

The terminal is a text-based interface for interacting with the Windows OS. Instead of clicking windows and folders, you type commands that tell the computer exactly what to do. cyber security professionals use it because:

    It's faster than clicking around
    It gives more control
    Many security tools only run in the terminal

By the end of this room, it will feel far more comfortable,  and you'll see it as a straightforward tool rather than something intimidating. Click on the Terminal file present on the Desktop:

Image shows the Windows Terminal interface
Overview

Before you can explore anything on a Windows system, you need to know how to move around and look for files using the command line. In this task, you'll learn how to explore folders, move between directories, search for a file when you don't know where it is, and read the contents of a text file, all using Command Prompt.

These are the same kinds of skills you'll use later when troubleshooting systems.
Task: Find the mission_brief.txt file

Your boss has left you another note, with a task to find the task_brief.txt file:

Note left on stickynote to find the task_brief.txt file

    "I've left a file called task_brief.txt somewhere in your user folder.
    You'll need to find it using the command line and read what it says."

You're only given the name of the file, not its location.

Let's explore how to navigate through the Windows filesystem using the command line and how to locate a file without knowing its actual location.
Step 1: Where Am I?

Before doing anything else, open the terminal on the Desktop, and check your current location by typing the command cd, as shown below: 

Shows output of cd command

This shows the full path of the directory you're currently in. On Windows, this is usually your user folder. Please note that the cd command is also used to change the directory, which we will use later in the task.
Step 2: What's Around Me?

Now, list the contents of the current directory using the command: dir

This command will list down the files and the folders present in the current directory, as shown below:

Shows output of dir command

You'll see files and folders that are visible by default. Take a moment to look around; not everything you need will always be obvious. From the output, we can see that the command has returned 16 directories.
Step 3: Are There Hidden Files?

Some files and folders on Windows are marked as hidden, which means they don't appear in a normal listing. To show everything, including hidden items, run: dir /a

Shows output of dir/a command

The output clearly indicates that more than 12 hidden folders were found. It is important to note that hidden doesn't mean secret; it just means Windows hides them by default.
Step 4: Moving Around the Filesystem

Let's use the cd command to navigate through the folders. We can use the format cd folder_name to move to the specified folder. The command cd Documents will move us to the Documents folder, as shown below. To move back one level, we can use the cd command.

Shows the output of cd command

To become familiar with the environment, use the dir or dir /a command to move to see what's inside each folder. You can explore a few folders to get comfortable, but the file you're looking for probably isn't in an obvious place.
Step 5: Finding the File on the Disk

Instead of guessing where the file is, let Windows search for it. Use the following command: dir /s task_brief.txt. The /s flag tells Windows to search all subfolders starting from your current directory and show you the full path if the file exists.

Shows the command to search for the files on the system

As we can see, the command above helped us locate the file and provided its full path. Take note of the path shown in the output.
Step 6: Navigate to the File

Now that we know where the file is located, let's use the cd command to navigate to the folder using the command format cd <path_to_the task_brief.txt>. Use dir again to confirm that task_brief.txt is in the folder, as shown below:

Shows output of the cd command
Step 7: Read the File

Now read the contents of the file using: type task_brief.txt. This will print the contents of the file directly in the command prompt, as shown below:

Shows the use of type command to read the file content

Perfect.

You have not only learned how to navigate Windows directories using the CLI, but also how to find files and read their contents. 

The content of task_brief.txt leads us to our next task: inquiring about the system we are currently using. Let's explore that in the next task.
Answer the questions below

What is the full path of the task_brief.txt found on the system?

What message and flag are written inside task_brief.txt?
Gathering System Information on Windows
Overview

Now that you know how to move around and find files using the Windows command line, it’s time to learn how to ask the system questions about itself. cyber security and IT professionals do this all the time. Before fixing a problem or investigating an incident, they first want to know:

    Who am I logged in as?
    What machine is this?
    What version of Windows is it running?
    How is it connected to the network?Image depicts a system under observation

In this task, you'll learn how to gather that information step by step.
Step 1: Who Am I Logged In As?

When working on a system, one of the first things to check is which user account you’re using. This matters because different users can have different permissions.

Run the following command:whoami. This command prints the username of the account you’re currently logged into.

Shows output of whoami
Step 2: What Is the Name of This Computer?

Every Windows machine has a name. In workplaces, this helps identify network systems. To see the computer’s name, run: hostname.

You’ll see a short name printed in the terminal.
Step 3: What Version of Windows Is This?

Next, let’s look at details about the operating system itself. Run:systeminfo

This command prints a lot of information. Don’t worry, you’re not expected to understand everything yet.

Focus on these parts:

    OS Name
    OS Version
    System Type

These details indicate the version of Windows the machine is running and whether it’s 32-bit or 64-bit.
Step 4: How Is This Machine Connected to the Network?

Finally, let’s look at basic network information. Run: ipconfig

This shows the machine's network configuration.

Look for:

    An IPv4 Address
    A Default Gateway

This information helps analysts understand how a machine connects to the network.
Summary

In this task, you learned how to ask a Windows system simple but important questions using the command line.

You practiced:

    Identifying who you are logged in as
    Finding the name of the computer
    Checking Windows version and system details
    Viewing basic network information

These are some of the first commands analysts and IT staff run when they start working on a Windows machine.
Answer the questions below

What is the computer name shown by hostname?

What Windows version is listed in the systeminfo output?

Conclusion
Overview

You’ve reached the end of this room - nice work.

In this room, we learned how to interact with a Windows system using the command line instead of relying on the graphical interface. This task is a short wrap-up to reflect on what you’ve learned and why it’s important.
What You Learned

In this room, you practiced using the Windows Command Prompt to:

    Navigate files and folders without clicking
    Locate files even when you didn’t know where they were
    Reveal hidden files and directories
    Read file contents directly from the terminal
    Gather basic system and network information

These are foundational skills that apply across many roles in IT and cybersecurity.
Why This Matters

In real-world environments:

    Not everything is visible in the graphical interface
    Files may be hidden or buried deep in the system
    Analysts often need quick answers without clicking through menus
    Command-line tools are faster, more precise, and easier to automate

Being comfortable with the Windows command line gives you more control and better visibility into a system.
Answer the questions below

Continue to complete the room.

Introduction to Operating System Security

Every day you use a smartphone or a laptop or almost any type of computer, you interact directly or indirectly with an operating system. Operating systems include MS Windows, macOS, iOS, Android, Chrome OS, and Linux. But what is an operating system? To define an operating system, we need to visit one computer term: hardware.

 

Computer hardware refers to all the computer parts and peripherals that you can touch with your hand. Hardware includes the screen, the keyboard, the printer, the USB flash memory, and the desktop board. As shown in the figure below, the desktop board contains many components, in particular, a central processing unit (CPU) and memory chips (RAM). Although not shown in the image below, the desktop board is usually connected to a storage device (HDD or SSD).

The desktop board is the main part of a computer, and all the other pieces of hardware from keyboard and mouse to screen and printer connect to it. However, hardware components by themselves are useless if you want to run your favorite programs and applications. We need an Operating System to control and “drive” them.

Software and hardware

The Operating System (OS) is the layer sitting between the hardware and the applications and programs you are running. Example programs you would use daily might include a web browser, such as Firefox, Safari, and Chrome, and a messaging app, such as Signal, WhatsApp, and Telegram. All the programs and applications cannot run directly on the computer hardware; however, they run on top of the operating system. The operating system allows these programs to access the hardware according to specific rules.

Some operating systems are designed to run on laptops and personal desktops, such as MS Windows 11 and macOS. Other operating systems are designed specifically for smartphones, such as Android and iOS. There are also operating systems intended for servers; examples include MS Windows Server 2022, IBM AIX, and Oracle Solaris. Finally, there are operating systems that you can use on a personal computer and server; one example is Linux. The image below shows the popularity of the different operating systems used to browse the Internet according to Statcounter based on the data collected during January 2022.

Your smartphone might be running Android or iOS, and you might have plenty of private data on it. Examples include:

    Private conversations with your family and friends
    Private photos with family and friends
    Email client that you use for personal and work communications
    Passwords saved in the web browser (or even in notes)
    E-banking apps

The list of confidential and private data goes on. You don’t want someone you don’t trust to open your phone and go through your photos, conversations, and apps. Hence, you need to secure your phone and its operating system.

The same goes for your laptop or computer running MS Windows, macOS, or Linux. Your computer will most likely contain plenty of information such as:

    Confidential files related to your work or university
    Private personal files, such as a copy of your ID or passport
    Email programs, such as MS Outlook and Mozilla Thunderbird
    Passwords saved in web browsers and other apps
    Copy of digital camera and smartphone photos

The list can get very long, depending on the type of user. And considering the nature of the saved data, you want to ensure that your data is secure. When we talk about security, we should think of protecting three things:

    Confidentiality: You want to ensure that secret and private files and information are only available to intended persons.
    Integrity: It is crucial that no one can tamper with the files stored on your system or while being transferred on the network.
    Availability: You want your laptop or smartphone to be available to use anytime you decide to use it.

 

In the next task, we will discuss common attacks against these security pillars.
Answer the questions below

Which of the following is not an operating system?

    AIX
    Android
    Chrome OS
    Solaris
    Thunderbird

Common Examples of OS Security

As we mentioned in the previous task, security is concerned with attacks against:

    Confidentiality
    Integrity
    Availability

In this room, we will focus on three weaknesses targeted by malicious users:

    Authentication and Weak Passwords
    Weak File Permissions
    Malicious Programs

Authentication and Weak Passwords

Authentication is the act of verifying your identity, be it a local or a remote system. Authentication can be achieved via three main ways:

    Something you know, such as a password or a PIN code.
    Something you are, such as a fingerprint.
    Something you have, such as a phone number via which you can receive an SMS message.

Since passwords are the most common form of authentication, they are also the most attacked. Many users tend to use easy-to-guess passwords or the same password on many websites. Moreover, some users rely on personal details such as date of birth and name of their pet, thinking that this is easy to remember and unknown to attackers. However, attackers are aware of this tendency among users.

The National Cyber Security Centre (NCSC) has published a list of the 100,000 most common passwords. Let’s look at the top 20 passwords in the table below.
Rank 	Password
1 	123456
2 	123456789
3 	qwerty
4 	password
5 	111111
6 	12345678
7 	abc123
8 	1234567
9 	password1
10 	12345
11 	1234567890
12 	123123
13 	000000
14 	iloveyou
15 	1234
16 	1q2w3e4r5t
17 	qwertyuiop
18 	123
19 	monkey
20 	dragon

We can see that 123, 1234, 12345, …, 123456789, and 1234567890 are on the list. Dictionary words such as password, iloveyou, monkey, and dragon are commonly used. Words not in the dictionary include qwerty, qwertyuiop, and 1q2w3e4r5t; these seemingly complex passwords are very predictable as they follow the keyboard layout.

In brief, if the attacker can guess the password of any of your online accounts, such as your email or social media account, they will be able to gain access to your private data. Therefore, it is vital that you choose complex passwords and use different passwords with different accounts.
Weak File Permissions

Proper security dictates the principle of least privilege. In a work environment, you want any file accessible only by those who need to access it to get work done. On a personal level, if you are planning a trip with family or friends, you might want to share all the files related to the trip plan with those going on that trip; you don’t want to share such files publicly. That’s the principle of least privilege, or in simpler terms, “who can access what?”

Weak file permissions make it easy for the adversary to attack confidentiality and integrity. They can attack confidentiality as weak permissions allow them to access files they should not be able to access. Moreover, they can attack integrity as they might modify files that they should not be able to edit.
Access to Malicious Programs

The last example we will consider is the case of malicious programs. Depending on the type of malicious program, it can attack confidentiality, integrity, and availability.

Some types of malicious programs, such as Trojan horses, give the attacker access to your system. Consequently, the attacker would be able to read your files or even modify them.

Some types of malicious programs attack availability. One such example is ransomware. Ransomware is a malicious program that encrypts the user's files. Encryption makes the file(s) unreadable without knowing the encryption password; in other words, the files become gibberish without decryption (reversing the encryption). The attacker offers the user the ability to restore availability, i.e., regain access to their original files: they would give them the encryption password if the user is willing to pay the “ransom.”
Answer the questions below

Which of the following is a strong password, in your opinion?

    iloveyou
    1q2w3e4r5t
    LearnM00r
    qwertyuiop

    Practical Example of OS Security

In one typical attack, the attacker seeks to gain access to a remote system. We can accomplish this attack by tricking the target into running a malicious file or by obtaining a username and a password. We will focus on the latter. After discovering a username, we will try to “guess” the password; furthermore, we will try to escalate our privileges to a system administrator. This account is called root on Android, Apple, and Linux systems. While, on MS Windows systems, this account is called administrator. The accounts root and administrator have complete unrestricted access to a system.


In this task, we will try to hack into a Linux system. We assume that you have never used a Linux system before, and we will explain accordingly.

Start the AttackBox by clicking on the “Start AttackBox” button at the top left of the room. Start the attached machine by clicking on the green “Start Machine” button at the top right of this task. It usually takes a minute or two to load fully. Once they are both ready, you should use the AttackBox, which should be taking the right half of your screen by now.


On the AttackBox, start the terminal by clicking on the terminal icon shown in the image above. You will be writing all the commands you need on the terminal shown below.


We will cover the following Linux commands and explain them throughout this task.

    whoami
    ssh USERNAME@MACHINE_IP
    ls
    cat FILENAME
    history

We were hired to check the security of a certain company. When we visited our client’s office, we noticed a sticky note with two words: sammie and dragon on one of the screens. Let’s see if dragon is Sammie’s password on the target machine MACHINE_IP. From the AttackBox’s terminal, we will try to log in to Sammie’s account by executing ssh sammie@MACHINE_IP. The remote system will ask you to provide sammie’s password, dragon.

The first time we connect to a server over SSH, we will get a warning about the server’s authenticity and SSH key. We need to answer “Are you sure you want to continue connecting (yes/no)?” with yes.

Please note the following when entering the password over SSH. When you log in via SSH, you won't see that you are typing the password. In other words, when you are typing the SSH password, you won't see stars, dots, or any indicator on the screen that the password is being typed. However, the system still receives the password you are entering.

The interaction on the AttackBox’s terminal is shown below.
AttackBox Terminal

           
user@AttackBox# ssh sammie@MACHINE_IP
The authenticity of host 'MACHINE_IP (MACHINE_IP)' can't be established.
ECDSA key fingerprint is SHA256:IFP+sTfHTDm72Ta2zfK9XjKASr30+ya4ic/ApEIziio.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'MACHINE_IP' (ECDSA) to the list of known hosts.
sammie@MACHINE_IP's password: 
Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.4.0-100-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Tue  1 Mar 13:20:32 UTC 2022

  System load:  0.03              Processes:              216
  Usage of /:   51.8% of 6.53GB   Users logged in:        1
  Memory usage: 17%               IPv4 address for ens33: MACHINE_IP
  Swap usage:   0%

 * Super-optimized for small spaces - read how we shrank the memory
   footprint of MicroK8s to make it the smallest full K8s around.

   https://ubuntu.com/blog/microk8s-memory-optimisation

0 updates can be applied immediately.


Last login: Tue Mar  1 09:46:11 2022 from MACHINE_IP

        

Amazing! It worked! Let’s confirm that we are logged in as Sammie using the whoami (who am I?) command, which should return sammie.

To list the files in the current directory, we can use ls, short for list. This command will show all the files in the current directory unless they are hidden.

If you want to display the contents of any text file, you can use the command cat FILENAME, short for concatenate. This command will print the contents of the file on the screen.

In the terminal below, we see the usage of the four commands: ssh, whoami, ls, and cat. Please follow along from the AttackBox’s terminal.
AttackBox Terminal

           
user@AttackBox# ssh sammie@MACHINE_IP
sammie@MACHINE_IP's password:
Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.4.0-100-generic x86_64)

[...]

Last login: Tue Mar  1 14:45:53 2022 from 10.20.30.1
sammie@beginner-os-security:~$ whoami
sammie
sammie@beginner-os-security:~$ ls
country.txt  draft.md  icon.png  password.txt  profile.jpg
sammie@beginner-os-security:~$ cat draft.md 
# Operating System Security

Reusing passwords means that your password for other sites becomes exposed if one service is hacked.
sammie@beginner-os-security:~$

        

In our brief introduction to Linux, the last command that we will cover is history. This command prints the commands used by the user.

We have learned about two other usernames that can access the attached machine. They are:

    johnny
    linda

We know that both of these users have little regard for cybersecurity best practices. We can use several ways to guess the passwords for these two users. Here we list two approaches:

    If you are not logged in as sammie or any other user, you can use ssh johnny@MACHINE_IP and manually try one password after the next to see which password works for johnny.
    If you are logged in as sammie or any other user, you can use su - johnny and manually try one password after the next to see which password works for johnny.

Answer the questions below

Based on the top 7 passwords, let’s try to find Johnny’s password. What is the password for the user johnny?

Once you are logged in as Johnny, use the command history to check the commands that Johnny has typed. We expect Johnny to have mistakenly typed the root password instead of a command. What is the root password?

While logged in as Johnny, use the command su - root to switch to the root account. Display the contents of the file flag.txt in the root directory. What is the content of the file?


