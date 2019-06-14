---
layout: post
title: OS Planning
tags: [osdev]
---

Operating systems and their kernels are amazing pieces of code; they form the thin, magical line between hardware and software. One of my goals for the coming years is to understand this barrier much better; while I have a decent academic grasp of these concepts, my practical understanding is lacking. 

# Minimal (Microkernel, hardware-specific)
Microkernel because I've always wanted to build a microkernel! It's been re-hashed over and over again whether micro-, monolithic, modular, hybrid, exo-, or whatever-kernels are best; I'm building a microkernel because I like the concept and prefer to keep as much as possible outside of the kernel. Likely won't be a "pure" microkernel, but then again, what microkernel is?

Async IPC; sync interface on top

Interfaces will be common and clean, but implementations of drivers will be specific to a piece of hardware; while abstraction is nice, it's rare (in my experience) to have a "generic" implementation that is satisfactory as anything more than a starting point

Target only certain platforms/hardware devices; instead of a generic NIC driver that has separate hardware drivers it abstracts over (like the TCP/IP stack in Windows), have a hardware-specific e1000 driver that presents a generic NIC interface. This potentially reduces reusability/hotplugging of device drivers, but makes understanding the code much easier (since you can say "this process handles all network comms" instead of "this IP process sends a message to this Ethernet process which sends a message to the e1000 driver which...").

# Modern (UEFI, HPET/APIC/etc, C++17)
Since drivers will be hardware-specific, OS will only run on certain platforms, so no reason to support legacy technologies like BIOS, PIC, etc. Can choose to support only "modern"* technologies like UEFI, HPET, APIC, etc.
* Some of these "modern" technologies are from 1995

Can use C++17 features supported by LLVM without standard library to reduce development burden (smart pointers, strings, etc)

UTF-8

# Portable (ARM/AMD64)
To ensure OS can be ported to other platforms/hardware, develop AMD64 and ARM versions in lockstep using QEMU platforms. At most twice as much work, but does make clear where HAL boundaries need to be drawn.

# Iterative
I'm constantly starting over with new projects, not iteratively fixing/upgrading projects I already have. This one I need to be continuously improving, rather than abandoning it whenever it seems like a mess or re-writing it from scratch. This is purely a personal challenge!





Recently, I've been planning out the next hobby OS I want to work on. While I've done hobby kernels before, I've never gotten past the basic memory management and interrupts stage; usually a few weeks of frantic work, then I drop it entirely. In an effort to learn more and establish a better cadence, I'm going to blog my way through the design, implementation, and iteration of the OS. 

# At A Glance
Style: Microkernel
* Userspace servers
** Scheduler
** Memory management
* Userspace apps
* Kernel: IPC, basic memory management, timer
Platforms: 
* X86_64
** SYSENTER/SYSEXIT-style system calls
** HPET
** APIC (Local/IO)
** IPIs for multiprocessing
** GDT
** IDT
** TSS
** 2M, 4K pages
* AARCH64
** ???``    
Firmware: UEFI (QEMU OVMF/whatever the EFI implementation is for AARCH64)
Languages: 
* C++
* x86_64 asm
* aarch64 asm
I/O: 
* Serial output
* Classic Mac-like GUI
Concepts:
* Domains model based on Merkel DAG (generic addressing by hash)
