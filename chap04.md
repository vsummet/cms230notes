# CHAPTER 4 — Computer Systems
This chapter discusses how computer systems are organized, with special attention paid to main memory. You may know some of this material already, but look it over anyway.

## Chapter Topics:

* Components of a Computer System
* Device Controllers
* Main Memory
* Addresses
* Virtual Memory
* Cache Memory
* Contents of Memory

### Question
<details>
    <summary>
      Does a computer system based upon one type of processor chip (say ARM) look about the same as a system based upon another type of chip (say Pentium)?
    </summary>
    Yes. The main components are about the same and work about the same way.
</details>

## 4.1 - Computer System Components
The diagram shows a general view of how desktop and workstation computers are organized. Different systems have different details, but in general all computers consist of components (processor, memory, controllers, video) connected together with a bus. Physically, a **bus** consists of many parallel wires, usually printed (in copper) on the main circuit board of the computer. Data signals, clock signals, and control signals are sent on the bus back and forth between components. A particular type of bus follows a carefully written standard that describes the signals that are carried on the wires and what the signals mean. The PCI standard (for example) describes the PCI bus used on most current PCs.

<ch04-compsystem.gif>

The processor continuously executes the machine cycle, executing machine instructions one by one. Most instructions are for an arithmetical, a logical, or a control operation. A machine operation often involves access to main storage or involves an i/o controller. If so, the machine operation puts data and control signals on the bus, and (may) wait for data and control signals to return. Some machine operations take place entirely inside the processor (the bus is not involved). These operations are very fast.

### Question
<details>
    <summary>
    Do you think that the various components can put signals and data on the bus at any arbitrary time?
    </summary>
    No. The various devices must cooperate somehow so their data and signals don't get mixed.
</details>

## 4.2 - Input/output Controllers
The way in which devices connected to a bus cooperate is another part of a bus standard.

**Input/output controllers** receive input and output requests from the central processor, and then send device-specific control signals to the device they control. They also manage the data flow to and from the device. This frees the central processor from involvement with the details of controlling each device. I/O controllers are needed only for those I/O devices that are part of the system.

Often the I/O controllers are part of the electronics on the main circuit board (the mother board) of the computer. Sometimes an uncommon device requires its own controller which must be plugged into a connector (an expansion slot) on the mother board.

I/O controllers are sometimes called **device controllers.** The software that directly interacts with a device controller is called a **device driver**. When you install a new device on your computer (say, a new graphics board) you must also install a device driver for it.

### Question (Review)
<details>
    <summary>
    Is there a difference between the memory used to hold programs and the memory used to hold data?     
    </summary>
    No. Potentially any byte of main memory can hold part of a program or part of some data.
</details>

## 4.3 - Main Memory

In practice, data and instructions are often placed in different sections of memory, but this is a matter of software organization, not a hardware requirement. Also, most computers have special sections of memory that permanently hold programs (firmware stored in ROM), and other sections that are permanently used for special purposes.

Main memory (also called main storage, or just memory) holds the bit patterns of machine instructions and the bit patterns of data. Memory chips and the electronics that controls them are concerned only with saving bit patterns and returning them when requested. No distinction is made between bit patterns that are intended as instructions and bit patterns that are intended as data. The amount of memory on a system is often described using the terms in the table below.

These days (Summer, 2019-ish) the amount of main memory in a new desktop computer ranges from about 4 gigabytes to 32 gigabytes. Hard disks and other secondary storage devices hold several terabytes.

For reference:
kilobyte:	210 = 1024 bytes
megabyte:	220 = 1024 kilobytes
gigabyte:	230 = 1024 megabytes
terabyte:	240 = 1024 gigabytes

### Question (Review)
<details>
    <summary>
    (On most computers,) what is the smallest addressable unit of memory? 
    </summary>
    A byte.
</details>

## 4.4 - Addresses
 cells of memory
Each byte of main storage has an **address**. 32-bit addresses are common (and that's what we'll use in this class) so there are 232 possible addresses. Think of main storage as if it were an array.

<ch04-memory01.gif>

A main storage address is an index into memory. A 32-bit address is the address of a single byte. Thirty-two wires of the bus contain an address (there are many more bus wires for timing and control).

Sometimes people talk about addresses like 0x2000, which looks like a pattern of just 16 bits. But this is just an abbreviation for the full 32-bit address. The actual address is 0x00002000.

The first ARM processor (the ARMv1, delivered in 1985) used 26-bit addresses. Beginning with the ARMv6 (1991), ARM used 32-bit addresses. The ARMv8 (2011) supported full 64-bit addressing.  Other recent processor chips from AMD and Intel have 64-bit addresses (32-bit versions are still available although becoming much less frequent).

The assembly language of this course is for the Raspberry Pi 3/3+ which are built on QualComm's ARM Cortex-A53 chip (a variant of the ARMv8).  While this chip supports full 64-bit addressing, we won't be using it to its full capabilities.  We'll most often use 32-bit addresses for demonstration purposes in this course.

### Question (Review)
<details>
    <summary>
    What is the hexadecimal name for the 32-bit pattern that consists of all 1 bits? (Hint: look at the picture.)
    </summary>
    0xFFFFFFFF
</details>

## 4.5 - Virtual Memory

The MIPS has an address space of 232 bytes. A Gigabyte is 230, so the MIPS has 4 gigabytes of address space. Ideally, all of these memory locations would be implemented using memory chips (usually called RAM).

On modern computers, the full address space is present no matter how much RAM has been installed. This is done by keeping some parts of the full address space on disk and some parts in RAM. The RAM, the hard disk, some special electronics, and the operating system work together to provide the full 32 bit address space. To a user or an applications programmer it looks as if all 232 bytes of main memory are present.

This method of providing the full address space by using a combination of RAM memory and the hard disk is called virtual memory. The word virtual means "appearing to exist, but not really there." Some computer geeks have a virtual social life.



