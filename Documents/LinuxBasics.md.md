# Introduction to Linux Basics

## Table of Contents
1. [What is Linux?](#what-is-linux)
2. [History of Linux](#history-of-linux)
3. [Linux Distributions](#linux-distributions)
4. [Linux File System](#linux-file-system)
5. [Libraries in Linux](#libraries-in-linux)
6. [Basic Linux Commands](#basic-linux-commands)
7. [User Management](#user-management)
8. [File Permissions](#file-permissions)
9. [Package Management](#package-management)
10. [Libraries in Linux](#libraries-in-linux)
11. [Directory Structure: /lib, /usr/lib, and /include](#directory-structure-lib-usrlib-and-include)
12. [Networking Basics](#networking-basics)
13. [Conclusion](#conclusion)

---

## What is Linux?
- Linux is an open-source operating system based on Unix. 
- 
- Linux is known for its **stability, security, and flexibility**. 

<img src="https://aquatech-esf.com/wp-content/uploads/2021/12/Linux.jpg" alt="Description" width="360" height="200">

### Key Features
- **Open Source**: The source code is freely available for modification and redistribution.
- **Multi-user**: Multiple users can use the system simultaneously without interfering with each other.
- **Multi-tasking**: Supports running multiple processes at the same time.

<img src=https://www.hpe.com/content/dam/hpe/shared-publishing/images-norend/webinars/Frontier-moving-the-future-forward-video-screenshot-v2-16-9.jpg alt="Description" width="500" height="300">

---

## History of Linux
Linux was born out of the desire for a free and open alternative to proprietary Unix systems. 

Key milestones include:
- **1991**: Linus Torvalds releases the first version of the Linux kernel.
- **1994**: The first stable release of the Linux kernel (version 1.0).
- **1996**: Introduction of the first Linux distributions.

---

## Linux Distributions
A Linux distribution (distro) is a packaged version of the Linux operating system, containing theLinux kernel, system utilities, and applications**.   

Popular distributions include:
- **Ubuntu**: User-friendly and widely used for desktops.
- **Fedora**: Focuses on cutting-edge technologies.
- **CentOS/RHEL**: Known for stability, used in enterprise environments.
- **Debian**: Known for its robustness and extensive package repository.

<img src=https://i0.wp.com/takethenotes.com/wp-content/uploads/2023/02/image-4.png alt="Description" width="500" height="360">

---
## Linux on Windows
- Windows Subsystem for Linux (WSL), users can run a Linux environment directly on Windows without the need for dual-booting or using a virtual machine. 
- WSL allows users to run native Linux command-line tools alongside their Windows applications, providing an integrated experience. 

<img src="https://solidstudio.io/_next/image?url=https%3A%2F%2Fcdn.sanity.io%2Fimages%2Flofvu8al%2Fproduction%2F08a06675d7fa6ef8cc5829e4f9dfe25c62f22042-700x540.webp&w=1920&q=75" alt="Description" width="500" height="360">

## Linux File System
The Linux file system is organized in a hierarchical structure. 

Key points include:
- **Root Directory**: Represented as `/`, it is the top of the file system hierarchy.
- **Home Directory**: Each user has a home directory located at `/home/username`.
- **File Types**: Regular files, directories, symbolic links, and special files.

<img src=https://amaharjan.de/wp-content/uploads/2024/03/Standard-Linux-Directories-Explained.png alt="Description" width="550" height="300">

### Common Directories
```bash
- `/bin`: Essential user binaries.
- `/etc`: Configuration files.
- `/var`: Variable files such as logs.
- `/lib`: Contains essential shared libraries needed for the system to boot and run.
- `/usr/lib`: Additional libraries for user applications.
- `/usr/include`: Header files for C and C++ 
```
programming.  Header files typically have a `.h` extension and are crucial for developers when writing applications.

Both directories are crucial for the functioning of applications and the operating system itself.

---
## Libraries in Linux
In Linux, libraries are collections of pre-compiled code that programs can use to perform common tasks. 

They help reduce redundancy and promote code reuse. Libraries can be categorized as:
- **Static Libraries**: Linked to applications at compile-time, becoming part of the executable.
- **Dynamic Libraries**: Loaded at runtime, allowing multiple programs to share the same library code.

---

## Basic Linux Commands
Here are some fundamental commands you will use frequently:

### Navigating the File System
```bash
- `pwd`: Print the current working directory.
- `ls`: List files in a directory.
- `cd <directory>`: Change the current directory.
```
### File Operations
```bash
- `cp <source> <destination>`: Copy files.
- `mv <source> <destination>`: Move or rename files.
- `rm <file>`: Remove files.
```
### Viewing File Content
```bash
- `cat <file>`: Display file content.
- `less <file>`: View file content page by page.
- `head <file>`: Show the first few lines of a file.
- `tail <file>`: Show the last few lines of a file.
```
### Using the `find` Command
The `find` command is used to search for files and directories in a specified location based on various criteria. 

It is a powerful tool for locating files based on name, type, size, modification date, and more.
```bash
find [path] [options] [expression]

find /home/john -name "file.txt"
```

### Using the `grep` Command
The `grep` command is used to search for specific patterns within files or output streams. It is widely used for filtering text based on regular expressions.
```bash
grep [options] pattern [file...]

grep -i "error" /var/log/syslog
```
## User Management
Linux is a multi-user system, and user management is crucial:

### Common Commands
```bash
- `adduser <username>`: Add a new user.
- `deluser <username>`: Remove a user.
- `passwd <username>`: Change a user's password.
```
### User Groups
- Users can be organized into groups for easier permission management.
```bash
- `groups <username>`: Show groups a user belongs to.
```
---

## File Permissions
File permissions in Linux determine who can read, write, or execute a file.

### Understanding Permissions
- **Read ( r )**: Permission to read the file.
- **Write ( w )**: Permission to modify the file.
- **Execute ( x )**: Permission to run the file.

### Changing Permissions
```bash
- `chmod <permissions> <file>`: Change file permissions.
- `chown <owner>:<group> <file>`: Change file ownership.
```
---

## Package Management
Linux distributions typically use package managers to install and manage software.

### Common Package Managers
- **APT** (Debian/Ubuntu):

  - `sudo apt update`: Update package lists.
  - `sudo apt install <package>`: Install a package.

- **DNF** (Fedora):

  - `sudo dnf update`: Update packages.
  - `sudo dnf install <package>`: Install a package.

---

## Networking Basics
Understanding basic networking commands in Linux is essential for system administration.

### Common Networking Commands

- `ifconfig`: Display network interface configuration (use `ip addr` in newer systems).
- `ping <host>`: Check connectivity to a host.
- `ssh <user>@<host>`: Securely connect to a remote machine.

---

## Conclusion
- This introduction covers the basics of Linux, including its history, distributions, file systems, and essential commands. 
- Mastering these fundamentals will provide a solid foundation for further exploration of Linux and its capabilities. 
- Whether you're managing a server, developing software, or simply exploring, Linux offers a powerful and flexible environment for users of all skill levels.

---

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjExOTM1ODU2OSwxMDUwNTY1NTk2LC00Mz
c2NTc0MTddfQ==
-->