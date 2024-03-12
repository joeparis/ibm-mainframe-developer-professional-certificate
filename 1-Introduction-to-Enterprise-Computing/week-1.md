## Course Intro


Fortune 500 companies - billions of transactions per day.

Paychecks, health care, insurance, credit cards, bank accounts.

Must be fast, secure, and available.

That's what mainframes do.

It's the computer behind the scenes that specializes in scale, security, and reliability.

The mainframe is a computer that is physically purpose-built for big critical business applications.

It earns its up time through design, testing, and features.

OS: Linux, **z/OS**.

Special accelerators for cryptography, compression, network comms, managing data, virtualization, data management...

"Tell you what, you walk into a job interview, you tell them you know IOCDS, sis plex, palm live, and DFSMS, trust me, you're in a good place."

## Intro to Mainframe Architecture

### Computer Architecture

> "... the set of rules and methods that describe the functionality, organization, and implementation of the  computer system. ... this includes hardware, software, and everything in between, and all around it."

## Mainframe Architecture

[Why Do Mainframes Still Exist? What's Inside One? 40TB, 200+ Cores, AI, and more! ](https://youtu.be/ouAG4vXFORc?si=z9w0qiAYQI5fqHJ5)

Mainframes auxillary (AUX) storage (virtual memory) using **direct-access storage devices (DASD)**. Full of hard drives (SSD or spinning rust).


**Storage** includes both on-chip and AUX memory.

z/OS gives users and applications thier own address space, all the way up to 16 exabytes.

Still 4K pages.

Pages in real memory are called **frames**. Pages in AUX storage are called **slots**. **Paging** is still the process of swapping the two.

A **page** is a fixed-length block of main memory that is used as a unit for the transfer of data between the AUX storage and main memory. The size of a page is typically 4K in a mainframe system.

A **frame** is a fixed-length block of main memory that is used as a unit for the allocation of memory to processes. In other words, it's the smallest unit of memory that the operating system's memory manager can allocate.

So, the difference between a page and a frame is essentially about their usage: a page is a unit of data transfer, while a frame is a unit of memory allocation.

## Virtualization

Mainframes are physically comprised of many processors, a lot of storage and I/O, and it's got all the cooling and the power and the network required to make it run, along with other resources. 

Virtual systems can be and are built out of some subset of these resources running some OS.

These virtual systems are called a logical partition or LPAR. (Building an LPAR is like putting together LEGO bricks.)

TEST and PRODUCTION running in the same mainframe, for example. 

From the outside, an LPAR appears to be an actual computer.

The processors in a mainframe can be configured to run in various ways:

It can be a processor as we are familiar with them from desktop machines in which case it would run the OS and/or applications. These are call a **Central Processor (CP)**.

A **System Assist Processor (SAP)** sits between the CP and I/O as a dedicated I/O unit freeing the CP from handling I/O.

The **Integrated Facility for Linux (IFL)** are dedicated to running Linux on the mainframe. IFLs have special licensing associated with them so they are more cost-effective than using a CP for running an instance of Linux.

**z Integrated Information Processors (ZIIP)** allow you to offload certain workloads off the CP and onto them. For example, Java programs, certain parts of DB2, and XML processing. When doing so, the main CP is freed up for other tasks improving overall system throughput. Like IFLs, ZIIP are subject to special licensing that may make them more cost effective for certain applications.

I/O adaptors connect to AUX storage, network adapters, network attached storage, other mainframes, etc.

I/O adaptors are identified with **Channel Path Identifiers (CHPIDS)**. The CHPIDS is associate with a physical port location, or **Physical Channed ID (PCHID)**, and the logical subsystem that it's acssociated with. A subsystem is the connection between the LPAR and the I/O devices or other LPAR's that it needs to communicate directly with. 

You can put everything into one large sybsystem or you can partition into multiple logical subsystems.

![alt text](images/figure-1-1.png)

The CHPID is the association betwen the physical port and teh subsystem, you can think about it like being a line that connects the two, can be fulllly dedicated to a single LPAR or shared between LPARs 

![alt text](images/figure-1-2.png)