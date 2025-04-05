# xv6-project

This clone of MIT's xv6 OS is a coding project by Sina Ehsanzadeh and Seyed Hamid Hosseini, to learn more of how operating systems work and how to add features and make improvement to its processes. 

This file shall document the steps preformed during all stages of the project.


# Stage 1: Initialisation

Necessary preperations were concluded in this stage.

WSL, or Windows Subsystem for Linux, is an environment developed by Microsoft to allow Linux and Linux based operating systems to work via virtual machines as an alternative to dualbooting.

Desktop Docker is a collaborative software developed for the purpose of running containerized programs or microservices, something that we intend to make use of for running xv6.

Once these two software were installed, we could begin preparing to setup the OS.

Using the terminal and, we cloned the repository of xv6. WSL comes with Ubuntu prepared on it, and with Qemu, an emulator for compiling operating systems, preinstalled.

After booting into Ubuntu and getting to run Docker in the directory of xv6, we call Qemu to build the program. The first time it takes extra time to set it up, but following that the next builds are relatively fast.

The shell initialises via running the "sh.c" file within the OSes directory, and we are given the environment to interact with the newly built OS.

# Stage 2: Changing the shell input prompt

The "sh.c" file provides the input prompt to enter various commands that will come in use for an operating system, such as executing commands, redirections, pipes, and background processing.

Once all arguments given by the user have been completed, it sets up a new prompt for the nes set of arguments (of which there can only be a maximum of 10 at a time).

Normally, this prompt is symbolised by a "$" at the beginning of a new line, via this line within "sh.c":

``` write(2, "$ ", 2); ```

The first argument in the write function tells what sort of message is being written, whereas the next two feature the string to be written and the amount of characters to be written, respectively.

By changing the middle argument to "Hamid-Sina$ ", and the last argument to 12, now the code works as such that after all previous arguments provided by the user have been completed, it will open a new prompt, starting with

``` Hamid-Sina$ ```
