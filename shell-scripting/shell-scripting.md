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

### Why we need shell scripts

The main reason we need shell scripts, is to minimize the amount of times you need to recall and run a comand, especially if its something done occassionally. With shell scripts, you can modify these commands to do something complex and schedule them to run at specified times using cronjobs.

To further understand why we need them, we will craft a simple command to help us scrape our logfiles,especially the auth files. Say we needed to see which commands needed authentication as sudo and which commands ran. To do this we can write a simple command as follows
    
    ``` $ cat /var/log/auth 
        Apr 13 16:05:01 wild-wolf CRON[78403]: pam_unix(cron:session): session opened for user root(uid=0) by (uid=0)
        Apr 13 16:05:01 wild-wolf CRON[78403]: pam_unix(cron:session): session closed for user root
        Apr 13 16:09:01 wild-wolf CRON[79427]: pam_unix(cron:session): session opened for user root(uid=0) by (uid=0)
        Apr 13 16:09:01 wild-wolf CRON[79427]: pam_unix(cron:session): session closed for user root
        Apr 13 16:15:01 wild-wolf CRON[79776]: pam_unix(cron:session): session opened for user root(uid=0) by (uid=0)
        Apr 13 16:15:01 wild-wolf CRON[79776]: pam_unix(cron:session): session closed for user root
    ```

As we can see,  we get alot of info that's mostly not relevant for us, so we can add in an additional filter to filer for keywords

    ` $ cat /var/log/auth.log | grep -e 'auth\|authentication\|root\|Failed password' `

With this, our command now returns lines containing the strings `authentication, root, Failed password auth and auth `.

Since we are mostly interested in commands that ran a s sudo and the commandas that ran, now we modify our command to 

    ``` $ cat /var/log/auth.log.1 /var/log/auth.log | grep -e 'auth\|authentication\|root\|Failed password' | grep "sudo" | grep -i "COMMAND" ```

Our command takes as input the 2 log files and concats them then applies the filters.

As we can see, it's already alot. The command is long. Imagine having to type that every single day.

That's where shell scripts come in. To solve for all this.

But for us to understand shell scripts, we must learn its structure and basic building blocks. Thus we will cover

    - Output
    - Input 
    - Variables
    - shell arguments
    - Control statements
        - loops
        - if statements
        - if-else statements
        - if-elif-else statements
        - switch statements

## Building Blocks

First off, we will start with printing to standard out put. To print, we will use the `echo` command.

### Running shell scripts

To run a shell script, you need to make it executable then run it. To run a shell script called `myscript` in the current directory, we run the following 

        ``` 
            $ chmod +x myscript

            $ ./myscript

        ```


### Output 

To print something to the console, create a newfile and name it however you want and put the following content inside

```
    echo "Hello world"

```
save the file and [run the script](#running-shell-scripts)

On running you should see 

    ```
        $ chmod +x myscript
        $ ./myscript
          Hello world
        $


    ```

### Input 

To get input from a user, you need to use the `read` command after a prompt