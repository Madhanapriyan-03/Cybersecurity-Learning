
# Chapter 02 – Program, Process and Resource Management

> **"Every command you execute in Linux becomes a process managed by the Operating System."**

---

# 🎯 Learning Objectives

After completing this chapter, I should be able to:

* Explain the difference between a Program and a Process.
* Describe how Linux converts a program into a running process.
* Understand the role of the Shell and the Kernel.
* Explain why the PATH environment variable exists.
* Understand Process IDs (PID) and terminal sessions (PTS).
* Explain CPU Scheduling at a high level.
* Describe why Linux is called a Resource Manager.
* Interpret the output of basic monitoring commands.

---

# 🌍 Introduction

Every application that runs on Linux starts as a simple executable file stored on disk.

When the user executes that file, Linux transforms it into a running process.

Many beginners think that a Program and a Process are the same thing.

They are not.

Understanding this difference is one of the most fundamental concepts in operating systems.

Without understanding processes, topics such as privilege escalation, malware analysis, process injection, and Linux administration become much more difficult.

---

# 📀 What is a Program?

A Program is a collection of instructions stored on secondary storage.

Examples include:

* Firefox
* Python
* Nmap
* VS Code
* Bash

Programs occupy disk space but consume no CPU while inactive.

They simply wait until the operating system executes them.

---

# 🏃 What is a Process?

A Process is a program that is currently executing.

When a user launches an application, Linux creates a process.

Unlike a program, a process has:

* Process ID (PID)
* Allocated Memory
* CPU Scheduling Information
* User Information
* Group Information
* Open Files
* Environment Variables
* Current Working Directory

A process is therefore much more than simply "a running program."

It represents an entire execution environment created by the operating system.

---

# 📊 Program vs Process

| Program              | Process                   |
| -------------------- | ------------------------- |
| Stored on Disk       | Stored in RAM             |
| Passive              | Active                    |
| Does not use CPU     | Uses CPU Time             |
| No PID               | Has a PID                 |
| Exists until deleted | Exists only while running |

---

# 🎮 Real-World Analogy

Imagine purchasing a game DVD.

While the DVD is sitting on your desk, nothing is happening.

The game exists only as stored data.

This is similar to a **Program**.

The moment you install and launch the game, memory is allocated, the CPU begins executing instructions, and the operating system creates everything needed for execution.

Now it has become a **Process**.

---

# 🥷 Pentester's Perspective

Understanding processes is extremely important during penetration testing.

Examples include:

* Identifying suspicious running processes.
* Detecting malware.
* Finding privileged services.
* Monitoring active applications.
* Investigating persistence mechanisms.

Security professionals spend much more time analyzing running processes than simply examining program files.

---

# 🧪 Observation Lab

During this chapter the following commands were executed.

Locate executable:

```bash
which python3
```

View terminal processes:

```bash
ps
```

View all running processes:

```bash
ps aux
```

Search for Python processes:

```bash
ps aux | grep python
```

These commands demonstrated that:

* Programs exist on disk.
* Running applications become processes.
* Multiple processes can originate from the same executable.
* Every process receives a unique Process ID.


# 🧠 From Program to Process

When a user executes a program, Linux does much more than simply "run" a file.

The operating system performs several important tasks before the program begins execution.

These include:

* Locating the executable file.
* Requesting the Kernel to create a process.
* Allocating memory.
* Assigning a unique Process ID (PID).
* Preparing the execution environment.
* Scheduling the process on the CPU.

Only after these steps are completed does the CPU begin executing instructions.

---

# 🔄 Process Creation Flow

```text
User
 │
 ▼
Types Command

 │
 ▼
Shell Receives Command

 │
 ▼
Searches PATH

 │
 ▼
Kernel Creates Process

 │
 ▼
Memory Allocated

 │
 ▼
PID Assigned

 │
 ▼
CPU Executes Instructions
```

This flow represents the basic lifecycle of every command executed in Linux.

---

# 🖥 Shell

A Shell is the program that allows users to communicate with the operating system.

Examples include:

* Bash
* Zsh
* Fish

When a user types a command, the shell receives it first.

The shell is responsible for locating the executable and requesting the kernel to create a process.

The shell itself does not directly execute hardware instructions.

---

# ⚙ Kernel

The Kernel is the core component of the operating system.

Unlike the shell, the kernel has direct control over hardware resources.

Its responsibilities include:

* Creating processes
* Managing CPU scheduling
* Managing memory
* Managing devices
* Handling file systems
* Managing permissions
* Managing networking

Every running application depends on the kernel.

Without it, applications cannot safely communicate with hardware.

---

# 📌 Process ID (PID)

Every running process receives a unique identifier known as the Process ID.

Example:

Firefox → PID 2100

Python → PID 2343

Nmap → PID 4567

The operating system uses this identifier to uniquely manage each process.

Two active processes cannot have the same PID simultaneously.

After a process terminates, its PID may later be reused.

---

# 🖥 Terminal (TTY / PTS)

Processes often execute inside terminal sessions.

Modern Linux systems usually represent terminal sessions using identifiers such as:

pts/0

pts/1

pts/2

These identifiers do **not** represent processes.

Instead, they identify the terminal session to which a process belongs.

One terminal session may contain multiple running processes.

---

# Example

Terminal (pts/0)

├── python3

├── vim

└── bash

All three processes belong to the same terminal session.

---

# 🔍 Practical Commands Used

During this lesson the following commands were executed.

## Locate Program

```bash
which python3
```

Purpose:

Locate the executable file associated with a command.

---

## View Running Processes

```bash
ps
```

Purpose:

Display processes associated with the current terminal session.

---

```bash
ps aux
```

Purpose:

Display detailed information about running processes across the system.

---

## Search for Specific Processes

```bash
ps aux | grep python
```

Purpose:

Search for running Python-related processes.

During the lab several Python processes were observed.

These included:

* Bluetooth service
* Printer service
* Python interpreter started manually

This demonstrates that multiple processes may originate from the same programming language while serving completely different purposes.

---

# 📷 Screenshot References

Include the following screenshots inside the Screenshots folder.

* 02-ps-aux-python.png

These screenshots demonstrate process enumeration performed during the lab.

---

---

# ⚡ CPU Scheduling

Modern computers run many applications simultaneously.

For example:

* Firefox
* VS Code
* Spotify
* Python
* Discord

Although a computer may have only a few CPU cores, it appears that all applications run at the same time.

This is possible because the operating system rapidly switches CPU execution between multiple processes.

Each process receives a small amount of CPU time known as a **time slice**.

This decision is made by the CPU Scheduler inside the Kernel.

The switching happens so quickly that users perceive all applications as running simultaneously.

---

# 🖥 Operating System as a Resource Manager

One of the primary responsibilities of an operating system is resource management.

Resources include:

* CPU
* RAM
* Storage (Disk)
* Network Interfaces
* Files
* Input/Output Devices

The operating system decides which process receives each resource and for how long.

Without this coordination, multiple programs attempting to access the same hardware simultaneously could lead to crashes, corruption, or unpredictable behaviour.

---

# 💾 Memory Observation

Command Used:

```bash
free -h
```

Purpose:

Display current memory usage in a human-readable format.

Information Observed:

* Total Installed Memory
* Used Memory
* Free Memory
* Available Memory
* Swap Memory

This command is useful during penetration testing to understand available system resources and determine whether memory-intensive activities are appropriate.

---

# 💽 Disk Observation

Command Used:

```bash
df -h
```

Purpose:

Display filesystem disk usage.

Information Observed:

* Filesystem Name
* Total Disk Size
* Used Space
* Available Space
* Percentage Utilized
* Mount Points

Understanding disk usage is important because many attacks, uploads, log files, and forensic artefacts depend upon available storage.

---

# 🧪 Practical Commands Learned

| Command      | Purpose                                              |
| ------------ | ---------------------------------------------------- |
| `which`      | Locate executable files                              |
| `ps`         | Display processes attached to the current terminal   |
| `ps aux`     | Display detailed information about running processes |
| `grep`       | Filter command output                                |
| `top`        | Monitor running processes and CPU usage              |
| `free -h`    | View RAM usage                                       |
| `df -h`      | View disk usage                                      |
| `echo $PATH` | Display executable search paths                      |

---

# 💼 Penetration Tester's Perspective

Operating system knowledge forms the foundation of penetration testing.

After gaining access to a Linux system, a penetration tester commonly performs activities such as:

* Identifying active processes.
* Enumerating system resources.
* Determining available memory.
* Checking available disk space.
* Understanding running services.
* Identifying user sessions.
* Locating installed programs.

Rather than immediately launching exploits, professional penetration testers first understand the environment they are operating within.

Strong observation often leads to better attack paths than blindly executing tools.

---

# 🚨 Common Beginner Mistakes

* Assuming a Program and a Process are identical.
* Memorizing commands without understanding their purpose.
* Ignoring system resource usage.
* Assuming high CPU usage always indicates malicious behaviour.
* Forgetting that multiple processes may originate from the same application.
* Treating command output as facts without analysing it.

---

# ❓ Interview Questions

1. What is the difference between a Program and a Process?

2. What is a Process ID (PID)?

3. Why can't two active processes have the same PID?

4. What is the purpose of the PATH environment variable?

5. What is the role of the Shell?

6. What is the role of the Kernel?

7. Why is Linux called a Resource Manager?

8. What information does the `free -h` command display?

9. What information does the `df -h` command display?

10. Why is process enumeration important during penetration testing?

---

# 📝 Chapter Summary

After completing this chapter, I learned that:

* A Program is a passive executable stored on disk.
* A Process is an actively executing instance of a program.
* The Shell receives user commands.
* The Kernel creates and manages processes.
* Every running process receives a unique PID.
* Terminal sessions are represented using PTS identifiers.
* CPU time is shared among processes through scheduling.
* Linux manages CPU, memory, storage, networking, files, and devices.
* Basic monitoring commands provide valuable insight into system behaviour.

---

# 📸 Screenshots Included

* 02-ps-aux-python.png
* 03-free-memory.png
* 04-df-disk-usage.png

---

# ✅ Revision Checklist

Before moving to the next chapter, I should be able to answer:

* What is a Program?
* What is a Process?
* How does Linux create a process?
* What is the difference between the Shell and the Kernel?
* Why does the PATH variable exist?
* What is a PID?
* What is a PTS?
* Why is Linux called a Resource Manager?
* What do the `ps`, `top`, `free`, and `df` commands show?

If I can confidently explain these concepts without referring to notes, I am ready to continue.

---

> **"A penetration tester should understand the operating system before attempting to attack it. Understanding the system leads to better observations, better decisions, and better assessments."**

**End of Chapter 02**
