- The core components of Linux (kernel, user space, init/systemd)
- How processes are created and managed
- What systemd does and why it matters

Core components of linux are Kernel, shell, user space and init/systemd
Kernel--
Kernel is the heart of linux its interface between computer hardware and the processes i.e software and hardware
There is code inside kernel writtrn in C programming language
It manages system resources and makes sure applications work properly


Shell--
Shell acts as interface between the user and the kernel. It interprets user commands and translates it to actions performed by kernel.
UNIX supports various types of shells, such as Bourne Shell (sh), C Shell (csh), Korn Shell (ksh), and Bash (Bourne Again Shell). Each shell offers unique features, ranging from basic command execution to advanced scripting capabilities.

System Libraries--
System libraries provide predefined functions that allow applications to interact with the kernel without requiring direct kernel access.libraries simplify development by offering reusable code for common tasks.

System Utilities--
System utilities are command-line tools that perform various administrative and user-level tasks. These include file management, system monitoring, network configuration, and user management

Applications--
Applications are user-level programs that run on top of the UNIX architecture. This can be installed and works on the underlying hardware and shell.

User space--
Its space where application software and drivers execute. Each user space typically runs on its own virtual space. User space applications run with limited privileges to ensure system stability and security. They cannot directly access hardware or system resources; instead, they must make system calls to request services from the kernel.

Systemd/init--
Its the first process of kernel and it has PID of 1. It will be first process to start after this all other processes will execute.


HOW PROCESSES ARE CREATED AND MANAGED
Process is instance of program running its lifecycle includes stages like creation, execution and deletion.

WHAT SYSTEMD DOES AND WHY IT MATTERS??
Systemd/init is the first process of kernel.It is the init system that most modern Linux distributions use to boot the system, start services and manage system processes


