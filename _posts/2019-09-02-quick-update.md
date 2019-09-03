---
excerpt_separator: <!--Excerpt-->
layout: post
title: Quick Update
tags: [osdev, system]
---

I allowed myself to be eaten by work the last few months! I did manage to get a little OS work done, though, so here's the brief update.

<!--Excerpt-->

# C++17 and Build System

I got the build system updated to use Clang and C++17 properly. I also eliminated the nasty 'massive Makefile' and created an include-based Makefile system after reading ["Recursive Make Considered Harmful"](http://lcgapp.cern.ch/project/architecture/recursive_make.pdf). 

# x86_64 Text-Mode VGA

In the kernel::platform::x86_64 namespace, there's now a text-mode VGA class that wraps the classic 80x25 VGA interface. 

# x86_64 Logger

Also in kernel::platform::x86_64, there's a logger class that wraps the VGA class and provides common logging functions at four levels: dbg, inf, wrn, and err. It accepts varargs, but currently doesn't do the formatting expected of a logging class.

# What's next?

After I get the logger properly handling varargs and format strings, I think getting interrupts working will be the next focus. After getting the x86_64 GDT, TSS, and IDT set up, we'll try some software interrupts and see if that works! 