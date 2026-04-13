# Shell Scripting

## Introdction 

In unix, the shell is a command line interface that allows a user to interact with the operating system.
The shell is a macro-processor, int that it expands text and symobls to create *larger expressions*.

The shell can be used interactively or non-interactively. In interactive mode, the shell accepts input from the keyboard. 
When executing in non-interactive mode, the shell executes commands read from a file or a string.

There are different types of shells in unix, these include 
- Korn shell
- bash shell
- c-shell

We'll focus on the bash shell.

The bourne again shell (BASH) is the commandline interpretor for the GNU OS. It implements features of  k-shell and c-shell.

## Shell Scripting

A shell script is a file containing shell commands.
To make a shell script executable, you need to use the `chmod +x {name of script}` command to turn on the executable bit.

A script should begin with the `#!` ~ shebang! ~ . This is the common way to tell which interpretor should be used to interprate/execute the program. You can have a file having 
`#! /usr/bin/python3`, In this case, the program willl use the python interpretor to execute the script.



