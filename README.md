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

# Stage 3: "!" command addition and "os" substring identification and recolouring

In this stage we intend to make a "!" command, in which when the argument "!" is recieved, it will read all following arguments and print them out again.

For instance, if we enter

```Hamid-Sina$ ! Hello! ```

We will recieve

```Hello! ```

To do this, we need to define ! as a command in the shell file, "sh.c".

All inputs in the terminal are parsed via ```parsecmd```, which grabs the string and interprets it as a command. This command is then identified between a switch case of various operations. EXEC is a case for executing commands, which is what we are looking for.

We add an if statement, where if the first (and only first) argument, known as "ecmd->argv[0]", is equal to "!" (this is done using C's ```strcmp()``` function, that compares two strings and gives an integer depending on the alphabetical hierarchy of the first and second argument, and gives a "0" if they are the same), it will then take all remaining arguments and print them out as a message (the last argument i has ecmd->argv[i] equal to 0).

However, there is another feature we want to add to this command. If it detects any instance of "os" as a string or substring within the arguments, it will write them out in blue. The necessary actions for this is to introduce a pointer to the beginning character of the string argument, then cycling through all characters (or a mmzximum 512, a limitation we impose because of the limitations of xv6's virtual space processing) and if it ever finds an instance of "os", it will call a function in assembly code which recolours the font of what is printed, then revert it once that part is printed out.

And like that, the ! command has been added to the shell.

This is *not* a good way to add this command, as it is treating itself as a rather messy subsidiary of an EXEC command, but for the purpose of the beginnning, it does what we need.
