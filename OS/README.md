## Operating System Fundamental

### Definition
An operating system is a program that acts as an interface between the user and the computer hardware and controls the execution of all kinds of programs.
An operating system performs basic tasks like file management, memory management, process management, handling input and output, and controlling peripheral devices such as disk drives and printers.
Following are some of important functions of an operating System:
  - Memory Management
  - Processor Management
  - Device Management
  - File Management
  - Security
  - Control over system performance
  - Job accounting
  - Error detecting aids
  - Coordination between other software and users

### Purpose
The purpose of an operating system is to organize and control hardware and software so that the device it lives in behaves in a flexible but predictable way.

### Detailed OS fuctions & activities
#### Memory Management
  Memory management refers to management of Primary Memory or Main Memory.   
  Main memory is a large array of words or bytes where each word or byte has its own address.  
  Main memory provides a fast storage that can be accessed directly by the CPU.   
  For a program to be executed, it must in the main memory.   
  An Operating System does the following activities for memory management:
    - Keeps tracks of primary memory, i.e., what part of it are in use by whom, what part are not in use.
    - In multi-programming, the OS decides which process will get memory when and how much.
    - Allocates the memory when a process requests it to do so.
    - De-allocates the memory when a process no longer needs it or has been terminated.

#### Processor Management
  In multiprogramming environment, the OS decides which process gets the processor when and for how much time. 
  This function is called process scheduling. An Operating System does the following activities for processor management:
  - Keeps tracks of processor and status of process. The program responsible for this task is known as traffic controller.
  - Allocates the processor (CPU) to a process.
  - De-allocates processor when a process is no longer required.

#### Device Management
  An Operating System manages device communication via their respective drivers. 
  It does the following activities for device management:
  - Keeps tracks of all devices. The program responsible for this task is known as the I/O controller.
  - Decides which process gets the device when and for how much time.
  - Allocates the device in the most efficient way.
  - De-allocates devices.

#### File Management
  A file system is normally organized into directories for easy navigation and usage. 
  These directories may contain files and other directions.
  An Operating System does the following activities for file management:
  - Keeps track of information, location, uses, status etc. The collective facilities are often known as file system.
  - Decides who gets the resources.
  - Allocates the resources.
  - De-allocates the resources.

#### Other Important Activities
  Following are some of the important activities that an Operating System performs:
  - Security: By means of password and similar other techniques, it prevents unauthorized access to programs and data.
  - Control over system performance: Recording delays between request for a service and response from the system.
  - Job accounting: Keeping track of time and resources used by various jobs and users.
  - Error detecting aids: Production of dumps, traces, error messages, and other debugging and error detecting aids.
  - Coordination between other software and users: Coordination and assignment of compilers, interpreters, assemblers and other software to the various users of the computer systems.
        
### Service
An Operating System provides services to both the users and to the programs.
- It provides programs an environment to execute.
- It provides users the services to execute the programs in a convenient manner.

Following are a few common services provided by an operating system:
- Program execution
- I/O operations
- File System manipulation
- Communication
- Error Detection
- Resource Allocation
- Protection
    
### Detailed OS services:
#### Program Execution
  Operating systems handle many kinds of activities from user programs to system programs like printer spooler, name servers, file server, etc. 
  Each of these activities is encapsulated as a process.
  A process includes the complete execution context (code to execute, data to manipulate, registers, OS resources in use). 
  Following are the major activities of an operating system with respect to program management:
  - Loads a program into memory
  - Executes the program
  - Handles program's execution
  - Provides a mechanism for process synchronization
  - Provides a mechanism for process communication
  - Provides a mechanism for deadlock handling

#### I/O Operation
  An I/O subsystem comprises of I/O devices and their corresponding driver software.
  Drivers hide the peculiarities of specific hardware devices from the users.
  An Operating System manages the communication between user and device drivers.
  - I/O operation means read or write operation with any file or any specific I/O device.
  - Operating system provides the access to the required I/O device when required.

#### File System Manipulation
  A file represents a collection of related information. 
  Computers can store files on the disk (secondary storage), for long-term storage purpose. 
  Examples of storage media include magnetic tape, magnetic disk and optical disk drives like CD, DVD. 
  Each of these media has its own properties like speed, capacity, data transfer rate and data access methods.
  A file system is normally organized into directories for easy navigation and usage. 
  These directories may contain files and other directions. 
  Following are the major activities of an operating system with respect to file management:
  - Program needs to read a file or write a file.
  - The operating system gives the permission to the program for operation on file.
  - Permission varies from read-only, read-write, denied, and so on.
  - Operating System provides an interface to the user to create/delete files.
  - Operating System provides an interface to the user to create/delete directories.
  - Operating System provides an interface to create the backup of file system.

#### Communication
  In case of distributed systems which are a collection of processors that do not share memory, peripheral devices, or a clock, the operating system manages communications between all the processes. 
  Multiple processes communicate with one another through communication lines in the network.
  The OS handles routing and connection strategies, and the problems of contention and security. 
  Following are the major activities of an operating system with respect to communication:
  - Two processes often require data to be transferred between them.
  - Both the processes can be on one computer or on different computers, but are connected through a computer network.
  - Communication may be implemented by two methods, either by Shared Memory or by Message Passing.

#### Error Handling
  Errors can occur anytime and anywhere. 
  An error may occur in CPU, in I/O devices or in the memory hardware. 
  Following are the major activities of an operating system with respect to error handling:
  - The OS constantly checks for possible errors.
  - The OS takes an appropriate action to ensure correct and consistent computing.

#### Resource Management
  In case of multi-user or multi-tasking environment, resources such as main memory, CPU cycles and files storage are to be allocated to each user or job. 
  Following are the major activities of an operating system with respect to resource management:
  - The OS manages all kinds of resources using schedulers.
  - CPU scheduling algorithms are used for better utilization of CPU.

#### Protection
  Considering a computer system having multiple users and concurrent execution of multiple processes, the various processes must be protected from each other's activities.
  Protection refers to a mechanism or a way to control the access of programs, processes, or users to the resources defined by a computer system. 
  Following are the major activities of an operating system with respect to protection:
  - The OS ensures that all access to system resources is controlled.
  - The OS ensures that external I/O devices are protected from invalid access attempts.
  - The OS provides authentication features for each user by means of passwords.
        
        
### Reference: 
- https://computer.howstuffworks.com/operating-system.htm
- https://www.loyolacollege.edu/e-document/computerscience/Dr.%20Rexline/EVEN18_19/pdf/OS_UG/operating_system_tutorial.pdf
