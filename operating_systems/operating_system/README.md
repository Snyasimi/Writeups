# The Operating system

The operating system is a set of programs that interface the mahine with the application programs. THe operating system controls and dynamically allocated resources to executing programs. In simple words, the operating system is the interface between the application programs and the hardware. It is also responsible for executing application programs.

The operating system is useful because;
- It makes a computer more convenient to use
- It allows the computer to be used efficiently 

Operting systems also need to be able to evolve in such a way that new system functions are able to be added and tested.

### The interface

We say the OS is the interface between application programs and the hardware because, an application program can simply make use systems programs which have been developed to handle some functions like file management and control of I/O devices. If an application programmer were responsible for programming this, they will need to write machine level instructions in the application, and most of these functions are reused by other applications as well. To simplify this, the OS provides these functionalities through libraries by making use of APIs. Programs that have been built to hand these cases are called *Utilities or library programs*.  

The OS provides the following services;
- **Program development:** The OS provides facilities such as editors and debuggers to assist programmers in creating programs.
- **Program execution:** The OS handles tasks such as loading a program from disk to main-memory, initializing I/O device files and other resources.
- **Access to I/O devices:** The OS provides a uniform interface that hides details of control signals and peculiar instructions for I/O devices, exposing these functions to the programmers as simple reads/writes.

- **Control access to files:** In a multi-user environment, the OS provides protection of individual users' files so that other users cannot access files that do not belong to them or have access permissions.
- **Error detection and response:** While running a program, an error can occur, these errors might be hardware errors, memory related issues, software errors or a program requesting access to a restricted memory space. It is the OS's responsibility to handle this error and provide a response. It may respond in various ways including, stopping the program, reporting the error to the program or retrying the operation.

- **Accounting:** The OS should be able to account,  provide statistics of the system resources and monitor performance.

The operating system is a suite of  programs, this means that it is executed by the processor along side other programs. The OS directs the processor in the utilization of system resources and in the timing of execution of programs. The operating system will release the processor to go do some work *e.g executing programs*, normally on a fixed amount of time then it get's the processor back. Only potions of the frequently accessed part of the OS source code/ software suite remains in memory at a time.  

Since the processor is a system resource, the OS must determine how much processor time can be devoted to execution of a particular user program.

### Evolution of the Operating system.

In the 1940-mid1950s, computers were very manual. And now you talk to it using natural language, uses statistics to give you the right answer, most of the time. *enyewe tumetoka mbali*. There were no operating systems, you had to write your program on hardware(punch cards), do it using machine code. Weh, you had to interact with the computer's hardware to the point that you had to toggle switches. If it encountered an error, it would signal using the display lights. If the program proceeded to a normal completion, the output appeared on the printer. 

Since you did not have a fancy program to schedule your jobs efficiently, this resulted in wastage of a computer's processing time. For instance, when a user signed up for a timeslot, they'd receive time in 30s' (minutes). If a user finishes a job in 45 mins, this resulted in the waste of 15mins, and if a user encountered problems and ran out of time, they'd be forced to stop before resolving the problem.

Jobs were loaded manually, you had to load the compiler, the source code and then saving the compiled program, afterwards you had to load and link your program with common functions. This was done by mounting and  dismounting tapes. Now imagine you had an error :(, you'd have to repeat the whole process. During this era, the most common  functions, libraries were available as common software for all users. And that my friends was *serial processing*, get it!, coz the users had access to the computer in series.

#### Batch Processing

Due to the expense of running early computers, processor utilization had to be effective and efficient. To solve this issue, the batch OS was developed. It was developed by General Motors. It was used in the [IBM 701](https://link.springer.com/chapter/10.1007/978-1-4757-3510-9_2).  

The batch OS work in a simple way, it had software known as the monitor. This monitor's job was to load jobs provided by the computer operator. The computer operator's responsibility was to collect job cards or tapes and batch the jobs sequentially and input them to the monitor. To execute a job, the monitor read the jobs from the input to the user program area one at a time. Each job had control of the processor till end of execution. After a job finishes executing, it returns control back to the monitor which then loads the next job. Parts of the monitor resided in main memory, this portion was referred to as the resident monitor. When a program loaded and needed functionality of  the monitor, it loaded with parts of the monitor as sub-routines.  


The batch operating system handled scheduling of jobs using monitor. To pass control to the monitor, jobs made use of a special language known as the *Job control language*. Whenever the processor encounters an instruction starting with '$' this meant the job is ready to pass control back to the monitor in order for it to perform a privileged instruction or prepare the next job. There are two way in which the monitor and the computer executed jobs, the first method involved loading the compiler in memory, compiling the program to object code and saving the object in memory. This operation was referred to as *"compile, load and go"*. If the object code was stored in mass storage, the monitor had to read a special function known as  the `$LOAD` instruction which invokes the loader to load the object program to memory.

When a user program read input, data was transferred to the program through input routines, these routines were part of the operating system. The input routines checked the nature of instructions, preventing any job from reading a JCL instruction. If this were to happen, an error occurred and control was passed back to the monitor. Some of the other features included;

* *Memory protection*: A running job cannot alter the memory area which had the monitor. If this happened, the processor hardware detects this as an error and control is transferred to the monitor which aborts the job, prints the error and loads the next job. 
* *Timer*: A timer prevents the jobs from monopolizing the system. A timer is set once a job starts execution.

* *Privileged instructions*: Some instructions were executed only by the monitor. If the processor encounters a privileged instruction while executing a user program, an error occurred and control was passed to the monitor.

TO solve the problem of executing privileged instructions as a user program, 2 modes of executions were introduced; The kernel mode and the user mode. In user mode, certain memory regions are restricted and cannot be read by the user program thus preventing the execution of some instructions. In kernel mode, which the monitor operates in, allows the execution of privileged instructions and access to memory regions that are restricted, this mode is also known as the *system mode*.

#### Multiprogrammed batch operating systems

Simple batch operating system  solved the problem of job sequencing and scheduling, but there is one bottleneck, processor time is being wasted because it is idle during I/O operations. The simple batch operating system did not support multiprogramming, or multitasking. To solve this, more programs need to be loaded in-memory so that, when a job is waiting for I/O, the processor can branch of to a different job. 

The processor relies on interrupts to know when a device controller finishes an I/O operation. But interrupt are not enough, some form of memory management is needed to manage the multiple programs in-memory.
