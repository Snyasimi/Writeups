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
