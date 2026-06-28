# Chapter 01 – Why Were Operating Systems Invented?

> **"Before understanding Linux, a penetration tester must first understand why operating systems exist."**

---

# 🎯 Learning Objectives

After completing this chapter, I should be able to:

* Explain why operating systems were invented.
* Understand the problems programmers faced before operating systems.
* Explain how an operating system acts as a bridge between applications and hardware.
* Understand why penetration testers need operating system knowledge.
* Develop the habit of asking "Why?" before learning tools.

---

# 🌍 Computing Before Operating Systems

Modern computers are easy to use.

We double-click an application, open a browser, save files, and connect to the internet without thinking about what happens internally.

However, early computers worked very differently.

There were no graphical interfaces, no multitasking, and no operating systems to manage hardware.

Programmers often had to interact much more directly with the machine, and software was tightly coupled to the hardware it ran on.

This made software development difficult, slow, and error-prone.

---

# ❓ The Problem

Imagine writing a program without an operating system.

Questions immediately arise:

* Who allocates memory?
* Who decides when the CPU executes my program?
* Who controls the keyboard?
* Who writes data to storage?
* Who communicates with the display?

Without an operating system, every program would need to handle many hardware-related tasks itself.

As computers became more powerful and more programs needed to run, this approach became impractical.

---

# 💡 The Solution

Engineers introduced a new layer of software between applications and hardware.

This layer became known as the **Operating System (OS).**

Instead of every application communicating directly with hardware, applications communicate with the operating system.

The operating system then manages the hardware safely and efficiently.

---

# 🏗 Operating System Architecture (Conceptual)

```text
Application
      │
      ▼
Operating System
      │
      ▼
Hardware
```

Applications request resources.

The operating system decides whether those requests are allowed and manages access to the hardware.

---

# 🍽 Restaurant Analogy

Imagine a restaurant.

Without a waiter, every customer would have to:

* Walk into the kitchen.
* Explain the order directly to the chef.
* Collect the food.
* Handle billing.

This would quickly become chaotic.

Instead, the waiter acts as a coordinator between customers and the kitchen.

Similarly, the operating system acts as a coordinator between software and hardware.

---

# 🧠 Operating Systems from a Penetration Tester's Perspective

Many beginners think an operating system is simply Windows or Linux.

A penetration tester sees something much deeper.

The operating system is responsible for controlling access to important resources such as:

* CPU
* Memory
* Storage
* Network interfaces
* Running processes
* User permissions
* Files

Every privilege escalation vulnerability, file permission issue, and process-related attack ultimately involves the operating system.

Understanding operating systems is therefore a fundamental skill for every penetration tester.

---

# 🔍 Observation Lab

## Command Used

```bash
hostnamectl
```

## Purpose

Identify important information about the current operating system.

## Information Observed

The command displayed:

* Hostname
* Operating System
* Kernel Version
* Architecture
* Virtualization Platform
* Hardware Model

This demonstrated that a single command can reveal valuable information about a target system before any enumeration begins.

---

# 📝 Lessons Learned

* Operating systems were invented to simplify communication between software and hardware.
* Applications do not directly control hardware.
* Operating systems manage system resources.
* A penetration tester should understand concepts before learning tools.
* Observation is more important than memorizing commands.

---

# 💼 Real-World Relevance

During a penetration test, one of the first tasks after gaining access to a system is understanding the environment.

Commands such as `hostnamectl` help identify the operating system, kernel version, virtualization platform, and architecture.

This information helps determine suitable enumeration steps and whether known vulnerabilities may apply.

---

# 🎯 Key Takeaways

* Learn concepts before tools.
* Every command should answer a question.
* Observe before acting.
* Think like an investigator, not a script runner.

---

> **"Don't memorize commands. Understand the systems those commands interact with."**
