---
excerpt_separator: <!--Excerpt-->
layout: post
title: The System is Down
tags: [osdev, system]
---

![The Cheat...is grounded!](/assets/img/the_system_is_down.gif)

I discovered that my "system" repo had the most recent commit dates, so that's the abandoned operating system repo I'll use as a starting point. This project was a moonshot that reached a maximum altitude of 4 inches, so there's a lot to do to get it into shape! 

<!--Excerpt-->

## Update the directory structure.

**Updated 19 June 2019**: This is complete!

There aren't many files in the system repo, so this isn't a critical need. It does help me organize my thoughts and stay on track, and it's an easy thing to do, so I'll attack this first. While this post doesn't discuss future plans/designs, you can clearly see some of the ideas I have from the structure. The directory structure will look something like this:

* **build/**
    * Makefiles, build/debug scripts, etc. Anything needed to build and/or run system.
* **src/**
    * **api/**
        * System API; interface from apps to kernel. System calls, library functions, etc.
    * **kernel/**
        * **ipc/**
            * Inter-process comms for apps to talk with each other, and kernel <-> app communication.
        * **memory/**
            * Generic memory management functionality built on top of the platform-specific code in platform/.
        * **platform/**
            * **shared/**
                * Platform-specific code shared between two or more platforms.
            * **qemu-system-x86_64/**
                * Platform-specific code for running on QEMU's x86_64 emulator; includes device drivers such as network, APIC, HPET, etc as well as boot code.
            * **qemu-system-aarch64/**
                * Platform-specific code for running on QEMU's AArch64 emulator; includes device drivers such as network, interrupt, etc as well as boot code.
    * **stl/**
        * Bare-bones implementation of the C++ STL that can be used from user-mode or kernel-mode.

## Make the repository public.

**Updated 19 June 2019**: This is complete! [The repository is here.](https://github.com/dbargatz/system)

No point blogging about code nobody can see!

## Move the dev environment to Linux.

**Updated 25 June 2019**: This is complete! Working around snapd issues in Ubuntu 18.04 took the longest, post/tweet incoming.

System was originally developed on the Windows Subsystem for Linux; while this was a great tool and I never had any issues with it, a more traditional build environment on an Ubuntu 18.04 VM makes it less likely I'll run into environment issues.

## Build and run as-is.

**Updated 25 June 2019**: This is complete! Surprisingly easy, just required removing the XWindows DISPLAY setting from the 'make qemu' rules.

I haven't touched this code for a year and a half, so I forget how to build it, debug it, and run it. There are likely to be issues; for all I know, my last checkin in January 2018 broke everything. There's no point in starting from a broken codebase, so I'm going to make sure it works as-is (no matter how janky!) before refactoring or writing new code.

# Conclusion

Once all the above is done, I can move on to the fun stuff! By fun stuff, I mean changing the build system and fixing interrupts, which is likely going to be no fun at all. I'll update this post as I complete each item above!
