# The Operating system

The operating system is a set of programs that interface the mahine with the application programs. THe operating system controls and dynamically allocated resources to executing programs. In simple words, the operating system is the interface between the application programs and the hardware. It is also responsible for executing application programs.

The operating system is useful because;
- It makes a computer more convenient to use
- It allows the computer to be used efficiently 

Operting systems also need to be able to evolve in such a way that new system functions are able to be added and tested.

### The interface

We say the OS is the interface between application programs and the hardware because, an application program can simply make use systems programs which have been developed to handle some functions like file management and control of I/O devices. If an application programmer were responsible for programing this, they will need to write machine level instructions in the application, and most of these functions are reused by other appliactions as well. To simplify this, the OS provides these functionalities through libraries by making use of APIs. Programs that have been built to hand these cases are called *Utilities or library programs*.  

The OS provides the following services;
- **Program development:** The OS provides facilities such as editors and debuggers to assist programmers in creating programs.
- **Program execution:** The OS handles tasks such as loading a program from disk to main-memory, initializing I/O device files and other resources.
- **Access to I/O devices:** The OS provides a uniform interface that hides details of control signals and peculiar instructions for I/O devices, exposing these functions to the programmers as simple reads/writes.

- **Control access to files:** In a multi-user envronment, the OS provides protection of individual users' files so that other users cannot access files that do not belong to them or have access permissions.
- **Error detection and response:** While running a program, an error can occur, these errors might be hardware errors, memory related issues, software errors or a program requesting access to a resticted memory space. It is the OS's responsibility to handle this error and provide a response. It may responed in various ways including, stoping the program, reporting the error to the program or retrying the operation.

- **Accounting:** The OS should be able to account,  provide statistics of the system resources and monitor perfomance.

The operating system is a suite of  programs, this means that it is executed by the processor along side other programs. The OS directs the processor in the utilization of system resources and in the timing of execution of programs. The operating system will release the processor to go do some work *e.g executing programs*, normally on a fixed amount of time then it get's the processor back. Only potions of the frequently accessed part of the OS source code/ software suite remains in memory at a time.  

Since the processor is a system resource, the OS must determine how much processor time can be devoted to execution of a particular user program.

### Evolution of the Operating system.

In the 1940-mid1950s, computers were very manual. And now you talk to it using natural language, uses statistics to give you the right answer, most of the time. *enyewe tumetoka mbali*. There were no operating systems, you had to write your program on hardware(punch cards), do it using machine code. Weh, you had to interact with the computer's hardware to the point that you had to toggle switches. If it encountered an error, it would signal using the display lights. If the program proceeded to a normal completion, the output appeared on the printer. 

Since you did not have a fancy program to schedule your jobs efficiently, this resulted in wastage of a computer's processing time. For instance, when a user signed up for a timeslot, they'd recieve time in 30s' (minutes). If a user finishes a job in 45 mins, this resulted in the waste of 15mins, and if a user encountered problems and ran out of time, they'd be forced to stop before resolving the problem.

Jobs were loaded manually, you had to load the compiler, the source code and then saving the compiled program, afterwards you had to load and link your program with common functions. This was done by mounting and  dismouting tapes. Now imagine you had an error :(, you'd have to repeat the whole process. During this era, the most common  functions, libraries were available as common software for all users. And that my friends was *serial processing*, get it!, coz the users had access to the computer in series.

#### Batch Processing

Due to the expense of running early computers, processor utilization had to be effective and efficient. To solve this issue, the batch OS was developed. It was developed by General Motors. It was used in the [IBM 701](https://link.springer.com/chapter/10.1007/978-1-4757-3510-9_2).  

The batch OS work in a simple way, it had software known as the monitor. This monitor's job was to load jobs provided by the computer operator. The computer operator's responsibility was to collect job cards or tapes and batch the jobs sequentialy and input them to the monitor. To execute a job, the monitor read the jobs from the input to the user program area one at a time. Each job had control of the processor till end of execution. After a job finishes executing, it returns control back to the monitor which then loads the next job. Parts of the monitor resided in main memory, this portion was referred to as the resident monitor. When a program loaded and needed functionality of  the monitor, it loaded with parts of the monitor as sub-routines.  



