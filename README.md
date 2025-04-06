# Xv6-project

This is a clone of MIT's XV6 OS, running in RISC-V, undergoing edits made by Sina Ehsanzadeh and Seyed Hamid Hosseini.
In this project, we intend to familiarise ourselves with the inner workings of a basic operating system as well as making new features and optimisations.

# Stage 1: Initialisation

The first step necessary is setting up xv6 riscv. For that there are two vital components; Docker Desktop and WSL.
Docker Desktop creates an environment for running the OS, and WSL, or Windows Subsystem for Linux, is a tool that let's us use a virtual machine to load up Linux distributions without doing the usual dual boot.

After both are installed, using a terminal, we clone the xv6-ricv repository using git. Next we operate Docker using a Ubuntu distribution of Linux (usually preinstalled with WSL), loading up an image of xv6-riscv. Ubuntu and many other Linux distributions come with Qemu, an emulation software for building and emulating operating systems, and after going to the correct folder of the image, we can order Qemu to build the OS with the ```make qemu ``` command.

After a short while, once the OS is built, it will start up the kernal and open the shell, and then prompt an input via the shell symbol ```$ ```.

Xv6 is now ready to be used and modified.
