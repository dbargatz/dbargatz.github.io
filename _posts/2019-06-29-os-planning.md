---
excerpt_separator: <!--Excerpt-->
layout: post
title: OS Planning
tags: [osdev, system]
---

Now that all the setup is out of the way, the fun stuff can begin! One way I typically kill a project is by over-planning it, so let's avoid that. However, I think a few guiding principles are in order:

* Imperfect
* Minimal
* Modern
* Portable

<!--Excerpt-->

# Imperfect

It's never going to be perfect. Everything in computers...heck, almost everything in life is a compromise! Time/space tradeoffs, whether something belongs in kernel space or user space, Chipotle or Qdoba. This is more for me than anything else, but admitting up front that it's going to be a mess and making that a core feature might help.

# Minimal

I'm a sucker for microkernels at a conceptual level - I've always wanted to make one! What [Google is doing with LittleKernel/Zircon at the heart of Fuchsia](https://fuchsia.dev/fuchsia-src/zircon/concepts) is really exciting to me. I want to export as much policy as possible to user space, especially memory/scheduling algorithms, even though they'll take a performance hit from the context switches. It's always possible to move it in-kernel as a compromise if it's too slow!

# Modern

You can't get much older-skool than writing assembly by hand, but you exit that part of osdev pretty quickly. Once you hit the kernel entry point, you're typically writing C. There have been a lot of [cool new OSes](https://www.redox-os.org) and [tutorials written in Rust](https://os.phil-opp.com), and you should check those out! However, to sharpen my C++ skills, I'm going to write in C++17. Since very little of the OS is written past the boot stage at this point, it shouldn't take long to port the existing code. 

Additionally, I'll probably have to start simpler with a regular ol' PIC (Programmable Interrupt Controller) and PIT (Programmable Interrupt Timer) on Intel/AMD, but hopefully this can move to the local/IO APICs and HPET sooner rather than later. Since [Intel has declared the death of BIOS by 2020](https://arstechnica.com/gadgets/2017/11/intel-to-kill-off-the-last-vestiges-of-the-ancient-pc-bios-by-2020/), UEFI is definitely a goal too; I've written UEFI apps before, and it's much simpler than it initially seems, but figuring out when to call ExitBootServices() and transfer control to the OS is something I've yet to figure out.

# Portable

ARM is everywhere! Raspberry Pi, Pine64, a few billion mobile devices, everywhere! x86_64 isn't going anywhere anytime soon either; it powers the majority of the world's servers and cloud infrastructure. Covering these two architectures ensures the OS can run on a lot of hardware, but making sure it supports ARM and x86_64 from the start reduces the possibility some primitive or abstraction is too closely tied to the underlying architecture. Plus, I get to learn the AArch64 instruction set!

# Conclusion

Next up: porting to C++17! Then, I'll pull in a few logging things from older OS attempts, port those as well, and add some logging. Finally, getting parity between x86_64 and aarch64 on QEMU! 