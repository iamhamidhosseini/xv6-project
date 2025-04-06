# Xv6-project

This is a clone of MIT's XV6 OS, running in RISC-V, undergoing edits made by Sina Ehsanzadeh and Seyed Hamid Hosseini.
In this project, we intend to familiarise ourselves with the inner workings of a basic operating system as well as making new features and optimisations.

# Stage 1: Initialisation

The first step necessary is setting up xv6 riscv. For that there are two vital components; Docker Desktop and WSL.
Docker Desktop creates an environment for running the OS, and WSL, or Windows Subsystem for Linux, is a tool that let's us use a virtual machine to load up Linux distributions without doing the usual dual boot.

After both are installed, using a terminal, we clone the xv6-ricv repository using git. Next we operate Docker using a Ubuntu distribution of Linux (usually preinstalled with WSL), loading up an image of xv6-riscv. Ubuntu and many other Linux distributions come with Qemu, an emulation software for building and emulating operating systems, and after going to the correct folder of the image, we can order Qemu to build the OS with the ```make qemu ``` command.

After a short while, once the OS is built, it will start up the kernal and open the shell, and then prompt an input via the shell symbol ```$ ```.

Xv6 is now ready to be used and modified.

# Stage 2: Changing shell prompt

The first thing we want to try altering is the shell input prompt, as ```$ ```.

To do so, we must make necessary adjustments to the shell file, which is the "sh.c" file located in the "user" folder. The shell file holds the necessary functions to recognise commands and operations such as executions, redirections, background proccesses, and pipes. After recieving a list of arguments seperated by spaces (to a maximum of 10 arguments per input, as is defined in the file via MAX_ARGS), it shall read through them all, and call appropriate responses for all, and open a new prompt. This prompt generation is done by this string of code:

```write(2, "$ ", 2);```

The first argument in this command defines the type of message being printed. The second argument is the desired message, and the third argument sets how many characters of the second argument string to allow to be written (this is not very relavent in our case, so we will be keeping it at the same quantity as the string length).

We change the second argument to "Hamid-Sina$ " and the third argument to 12 accordingly.

Once the OS is recompiled, we will now recieve ```Hamid-Sina$ ``` as our shell input prompt.
