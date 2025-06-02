---
title: "Introduction to Linux - Part I"
datePublished: Sun Jun 01 2025 14:44:41 GMT+0000 (Coordinated Universal Time)
cuid: cmbdrv7hj000109jscuzq2qg7
slug: introduction-to-linux-part-i
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1747017771399/7d4bfa46-62c1-4f53-aa7c-de712bd4e242.jpeg
tags: ubuntu, linux, devops, opensource-inactive

---

Hi everyone,

Today, we are diving into the fascinating world of Linux🐧. Whether you’re a beginner or someone who’s looking to sharpen your Linux skills, this blog introduces you to the fundamentals of the Linux terminal and its powerful commands.

This is Part I of the Linux blog series, where we will explore the basics of the Operating system, Linux and its flavours, architecture, and some commands for file management, networking, and file permissions. So, let’s dive in!

---

### **Why should you learn Linux?**

As per **Stack Overflow’s** insights, the most common and most loved platform happens to be Linux. If you do a quick search online on Linux, you’ll come across some fascinating statistics.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747495813024/200122ce-1b11-40a3-83ae-89509e3b78b4.png align="center")

* *All of the fastest* ***500 supercomputers*** *in the world run on Linux.*
    
* ***96.3%*** *of the top* ***1 million web servers*** *run on Linux.*
    
* ***86%*** *of all* ***smartphones*** *are powered by Linux.*
    
    Some great numbers! In the cloud and DevOps world, many modern tools are developed and used in Linux environments first before they are made available on Windows/Mac.
    

***For example:***

* Automation tools like **Ansible** **require a Linux environment** for the Ansible controller (even though Ansible can manage Windows systems as targets).
    
* Containerization tools like **Docker** were **initially exclusive to Linux**\-based systems. Even now on Windows, if you’re containerizing an app, under the hood, it runs a Linux instance on top of a Windows machine.
    

So, you have pretty good reasons😄 to learn Linux and make something out of it.

---

### **What is Operating system?**

Before diving into Linux, let’s brush up on some basics!

An operating system is a system software that acts as an **intermediary between the user and the computer hardware**. It allows you to run programs, use your keyboard and mouse, save files, connect to the internet, and get stuff done.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747026306223/7cddb02c-b376-4f4d-a0ac-61fc21dd8f90.png align="center")

The flow of communication goes like this: As a user, you’re interacting with a software app(any) on your machine, which then forwards the request to the OS, followed by the kernel that’s present on top of the hardware. Here’s what a typical OS looks like,

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747496397529/11121859-22ff-4a03-922c-0cf113a624e9.png align="center")

System software means the software(Java code) that runs on the system, and with every request you make, it runs a process with a compiler(JDK-runtime) and then the system libraries(java package) forward to the kernel, that’s on top of your hardware, which comprises CPU, RAM and I/O. And, that’s how the Operating System works by.

**Some key functions**

* Process management
    
* Memory management
    
* System calls
    
* Device management
    

**Linux Specific Features**

* Fast and stable
    
* Widely used in production systems
    
* Free and open source
    
* Multiple distributions available
    
* Very secure (no need for anti-malware like McAfee on Windows)
    

---

### **Installation and set-up**

In this blog, we will be doing it by installing WSL(**Windows subsystem for Linux**) that allows you to run Linux on your Windows machine, which uses a lightweight virtual machine to run a full Linux kernel.

WSL works by the ***Virtualization principle via Hyper-V***(More on this later). If you’re using,

1. Mac OS - This OS itself is a Unix-based one. So, most of the commands can work on zsh, bash shells. Therefore, you don’t have to install Linux separately.
    
2. Linux - Setup is already done, as the core itself is the Linux OS.
    
3. For Windows, you can use WSL as we saw before. Here’s how you can do it👇!
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747499315520/7dae6c34-13d2-49ef-b765-c8254ec4e5dd.png align="center")

That’s it, we are done with the Installation part✅. Make sure that you’ve the necessary memory space available before doing it. If not, then don’t worry, I’ve got a better solution for that as well😄.

Navigate to [https://killercoda.com/playgrounds/scenario/ubuntu](https://killercoda.com/playgrounds/scenario/ubuntu) and sign up. Toggle on the start playground, and it opens Linux Ubuntu 24.0 kernel right inside your browser. How cool is that🐱? Every command works as it is, but remember it lasts for *just an hour*. And then, you can start with another playaround.

---

### Linux distributions

Similar to Icecream🍨, Linux also has many flavors in it,so called distributions. Each serves for different purposes and has its own usecases. Major distributions are,

| **Arch Linux** | Lightweight,rolling base distro providing full customization. |
| --- | --- |
| **Debian** | Stable one acting as foundation for many distros including ubuntu. |
| **Fedora** | Cutting edge by redhat used for development purposes. |
| **Ubuntu** | user friendly debian based distro for desktops and servers. |
| **CentOS** | RHEL Compatible distro |
| **Open SUSE** | A versatile one by SUSE for sys admins and devs. |

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747503785531/a00fa9e4-87ce-4f7e-980c-b43cc6d4ab77.png align="center")

---

### **Ubuntu - Architecture**

**Everything you install** in your machine is **sort of a executable** — **A folder simply!(Running it actually means like double-clicking on that folder).** When you install Linux, it comes up with below folders featuring a home page,user files,system boot(reboot,off),a temp folder,etc folder consisting config files and then a bin folder like every operating system.  
You can **view the same in File Explorer** on your **Windows** (Literally the same)!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748886559286/192dc4f1-018c-498f-a16a-f7d597acbbd6.png align="center")

---

### **Terminal and shell**

**Shell**: A shell is a **command-line interpreter** that serves as the interface between the user and the operating system. It takes commands from the user, interprets them, and then executes the corresponding programs or system calls. Eg: **Bash,zsh**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747502319623/7e67de6b-601b-42c6-80d7-2cb2a0caf7cc.png align="center")

**Terminal-Emulator**: It’s a software application that **mimics the functionalities of old physical terminals**(like VT100) on modern **graphical user interfaces**.It provides a window where users can interact with the shell. Eg: **Powershell,command prompt.**

---

### **Environmental variables**

Think of them like **digital sticky notes** your system uses. Environment Variables are set at the system level and affect the environment of processes and users.

These’re just **key-value pairs** used by your OS and app to store important configuration info. It’s tells us about **where to find the files,which editor to use,what the system language is**,and some user-specific settings($PATH,$HOME,$SHELL).

| env | Lists all current env variables. |
| --- | --- |
| printenv | Prints a specific or all env variables. |
| export | sets or modifies env vars. |
| source | runs a script in the current shell. |
| where git | shows the path of the installed git. |
| open /usr/bin | open the bin folder |
| echo $PATH | Displays the path vars. |
| ps,kill | used to view running processes and terminate them by process ID. |

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747503512750/2ae7f4b4-25d8-4c81-bec0-8e71be3b5621.png align="center")

---

### **File management**

Linux gives you powerful commands to **create**, **view**, **move**, **search**, **compress**, and **clean** files and folders.

**Navigate & Explore**

| ls | list files and directories |
| --- | --- |
| pwd | prints your current directory |
| cd | changes your directory |
| mkdir | creates new folder |
| cat | display file content |
| less,more | view long pages by page |
| echo | print statement or file content |
| cat | read the file content |

**Organize files**

| cp | copies files/folders |
| --- | --- |
| mv | moves or renames files/folders |
| rmdir | removes empty directory |
| clear | clears your terminal screen |

**Find & search, compression**

| find | Locates files by name,type etc |
| --- | --- |
| grep | searches inside file contents |
| zip/unzip | Compress and extract files |

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747503389229/6e6af4e8-4507-4d6b-b153-323e36512e97.png align="left")

---

### **Networking in Linux**

Networking is how your computer talks to other systems(locally or over the internet).Linux provides handy tools to check connectivity,transfer files,debug and manage network interfaces.

**Test your connectivity**

| ping google.com | checks if a website or IP address is reachable or not. |
| --- | --- |
| ipconfig (or ifconfig in Linux) | Displays your network interface details(IP,subnet, etc..,) |

**Transfer files & Interact**

| curl | Fetches content from a URL/API(GET,POST,etc..,) |
| --- | --- |
| wget | Downloads files from the internet. |
| ftp | Transfers files using the FTP protocol. |

**Remote login & Access**

| ssh | securely connects to a remote server over the network. |
| --- | --- |
| telnet | connects to remote machines(older and insecure) |

**Troubleshooting**

| netstat/traceroute | show open ports,network connections & routing tables. |
| --- | --- |

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747503467129/6a5cca6f-16b2-4007-a911-de51d652a4e4.png align="center")

---

### **File permissions**

File permissions in Linux OS allows us to control who can do what with a file or directory as it is a multi user system.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747502412733/fd918d58-4679-4836-b0cd-214a13cb6845.png align="center")

**Combined values**:

| **7 = 4 + 2 + 1** | **read-write-execute(rwx)** | View the content of file |
| --- | --- | --- |
| **6 = 4 + 2** | **read-write— (rw-)** | Modify or delete the file |
| **5 = 4 + 1** | **read- — -execute(r-x)** | Run the file as a program/script. |
| **0** | **\- - -** | No access at all. |

**Commands**

| **ls -ltr** | shows a long listing of files, sorted by time, with permissions visible. |
| --- | --- |
| **chmod** | **ch**ange **mod**e(read/write/execute) |
| **chown** | **ch**ange **own**er(user or group) |

---

### Conclusion

And that’s it, we reached the end of the blog, and I have walked you through a lot, literally! As a beginner, it might seem overwhelming with its endless commands and configurations, but once you take the plunge, you’ll discover a world of power, flexibility, and control.  
I highly recommend you to try experimenting with these commands in the terminal and play around with them for a while to get you grounded.  
With time, it becomes natural and easy for you!

**Thank you**💙 **so much for your time!** I will see you soon with my next blog😄  
**Until then, Byeeee👋**

![Bye Dog GIFs | Tenor](https://media.tenor.com/X2FM1MIFqy4AAAAM/hi-bye.gif align="left")

💡**Let’s connect!** Feel free to reach out:  
[**LinkedIn**](https://www.linkedin.com/in/devisri-s-0987b6256/)  
[**GitHub**](https://github.com/Devisrisamidurai)