eduOS - A teaching operating system
===================================

Introduction
------------

eduOS is a Unix-like computer operating system based on a monolithic architecture for educational purposes.
It is derived from following tutorials and software distributions.
 
0. bkerndev - Bran's Kernel Development Tutorial

   The first steps to realize eduOS based on Bran's Kernel Development 
   Tutorial (http://www.osdever.net/tutorials/view/brans-kernel-development-tutorial).
   In particular, the initialization of GDT, IDT and the interrupt handlers are derived
   from this tutorial.

1. kprintf, umoddu3, udivdi3, qdivrem, divdi3, lshrdi3, moddi3, strtol, strtoul, ucmpdi2

   This software contains code derived from material licensed
   to the University of California by American Telephone and Telegraph
   Co. or Unix System Laboratories, Inc. and are reproduced herein with
   the permission of UNIX System Laboratories, Inc.

2. JamesM's kernel development tutorials
   The first version of eduOS's virtual filesystem and its initial
   ramdiks is is derived from JamesM's kernel development tutorials.
   (http://www.jamesmolloy.co.uk/tutorial_html/index.html)

3. newlib
   The C library "newlib" is used to build user-level aplications on the top
   of eduOS. Newlib is a collection of source code, it is
   distributed under the terms of several different licenses. All of the
   licensing is either public domain or BSD-like, which means that even
   proprietary applications can adopt newlib because its use does not
   require distribution of the end work's source code. For convenience, all
   of newlib's licenses are gathered up into the file COPYING.NEWLIB,
   which is included in the directory newlib or in newlib's source code.


Requirements of eduOS
---------------------

* Currently, eduOS supports only x86-based architectures (32 & 64 bit).
* Following command line tools have to be installed:
  make, gcc, binutil, git, qemu, nams, gdb
* The test PC has to use grub as bootloader.

Building eduOS
--------------

0. Copy on a 64 bit system Makefile64.example or on 32 bit system Makefile32.example to Makefile. Edit this Makefile to meet your individual convenience.
1. Copy include/eduos/config.h.example to include/eduos/config.h and edit this config file to 
   meet your individual convenience.
2. Build kernel with "make"

Start eduOS via qemu
--------------------
0. Install qemu to emulate an x86 architecture
1. Start emulator with "make qemu"

Boot eduOS via grub
-------------------
0. Copy eduos.elf as eduos.bin into the directory /boot. (cp eduos.elf /boot/eduos.bin)
1. Create a boot entry in the grub menu. This depends on the version of grub, which is used by 
   the installed Linux system. For instance, we added following lines to /boot/grub/grub.cfg:

<pre>
   ### BEGIN /etc/grub.d/40_custom ###
   # This file provides an easy way to add custom menu entries.  Simply type the
   # menu entries you want to add after this comment.  Be careful not to change
   # the 'exec tail' line above.
   menuentry "Boot eduOS!" {
          multiboot       /boot/eduos.bin
          boot
   }
</pre>

Overview of all branches
------------------------
0. stage0 - Smallest HelloWorld of the World 

   Description of loading a minimal 32bit kernel

1. stage1 - Non-preemptive multitasking

   Introduction into a simple form of multitasking, where no interrupts are
   required.

2. stage2 - Synchronisation primitives

   Description of basic synchronization primitives

3. stage3 - Preemptive multitasking

   Introduction into preemptive multitasking and interrupt handling

4. stage4 - Support of user-level tasks

   Add support of user-level tasks with an small interface for basic system calls

5. stage5 - Enabling paging

   Add support of paging. See http://www.noteblok.net/2014/06/14/bachelor
   for a detailed description.

6. stage6 - Add UART support

   Add basic support of a serial device

7. stage7 - A simple file system

   Add a virtual filesystem and a prototype of an initial ramdisk

8. stage8 - HelloWorld in user space

   Add HelloWorld example with a small C library (newlib)

9. stage9 - FPU & 64bit support

   Add FPU and SSE support, switch to newlib 2.2.0, add basic x86_64 support

10. stage10 - APIC support

   Add support of the Local APIC and preliminary support of the I/O APIC

Usefull Links
-------------
0. http://www.gnu.org/software/grub/manual/multiboot/
1. http://www.osdever.net/tutorials/view/brans-kernel-development-tutorial
2. http://www.jamesmolloy.co.uk/tutorial_html/index.html
3. http://techblog.lankes.org/tutorials/
4. http://www.os.rwth-aachen.de
5. http://www.noteblok.net/2014/06/14/bachelor
6. https://sourceware.org/newlib/
