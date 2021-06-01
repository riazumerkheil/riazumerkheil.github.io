---
title: "Osbuild"
date: 2021-06-01T10:42:58+05:00
draft: false
tags: ["project"]
---

#working

Write Your Own 64-bit Operating System Kernel From Scratch
You can find full code on my Git repo https://github.com/awaisshah2280/myFirstOS.git.

You can find code of this static site on repo https://github.com/awaisshah2280/mysite.git

Prerequisites
A text editor such as VS Code.
Docker for creating our build-environment.
Qemu for emulating our operating system.
Remember to add Qemu to the path so that you can access it from your command-line. (Windows instructions here)
Setup
Build an image for our build-environment:

docker build buildenv -t myos-buildenv
Build
Enter build environment:

Linux or MacOS: docker run --rm -it -v "$pwd":/root/env myos-buildenv
Windows (CMD): docker run --rm -it -v "%cd%":/root/env myos-buildenv
Windows (PowerShell): docker run --rm -it -v "${pwd}:/root/env" myos-buildenv
NOTE: If you are having trouble with an unshared drive, ensure your docker daemon has access to the drive you're development environment is in. For Docker Desktop, this is in "Settings > Shared Drives" or "Settings > Resources > File Sharing".
Build for x86 (other architectures may come in the future):

make build-x86_64
To leave the build environment, enter exit.

Emulate
You can emulate your operating system using Qemu: (Don't forget to add qemu to your path!)

qemu-system-x86_64 -cdrom dist/x86_64/kernel.iso
NOTE: When building your operating system, if changes to your code fail to compile, ensure your QEMU emulator has been closed, as this will block writing to kernel.iso.
Alternatively, you should be able to load the operating system on a USB drive and boot into it when you turn on your computer. (I haven't actually tested this yet.)

Cleanup
Remove the build-evironment image:

docker rmi myos-buildenv -f