
In contrast of  "Forward Engineering" aka the process of building a programm.

Step of building a programm

1. Design
2. Code
3. Compile
4. Fix tons of bugs
5. Compile
6. Extensive Cursing
7. Fix more bugs
8. Compile
9. Assemble
10. Binary

At every step information is lost.

1. Between the designe and Code
	1. What was the intention of the code, who wrote this code.
2. Information is lost at the compilation process.
	1. Comments
	2. Variables names 
	3. Function names
	4. structure data
	5. Sometimes, entire algorithms (optimization)
3. Information can also be striped with (strip command) to make the binary smaller.

The cpp (c preprocessor) remove comments and include library.
Then the c code is compile into assembly code.

## The reverse engineering process
Put you in the mind of the conceptor of the programm.
1. Dissasemble
2. Decompile
3. Lots of thinking
4. Understand


## Binary files
ELF file, (Executable and Linkable Format), represent a programm as it will be loaded into memory.
	Describes how the program should be loaded (program/segment headers)
	 Contains metadata describing program components (section headers)

Linux, FreeBSD ELF
Windows, PE files
MacOS, MacO

### ELF program headers
They specify information needed to prepare the program for execution 
Most important entry types:
**INTERP**: defines the library that should be used to load this ELF into memory.
**LOAD:**  defines a part of the file that should be loaded into memory.

**readelf** help to read elf informations.
An elf file always start with `7f 45 4c 46` where `45 4c 46` mean 'ELF'

Virtualaddr nowadays are randomize in memory  to make that more resilient against certain attacks.

Headers can be loaded as Readable `R`, Readable Executable `R E` or Readable Writeable `R W`

The **headers** are the ground truth to loading elf files.
So you can build an elf file with only headers, it will executable but not very useful.

Binary Files video at 9:48
## Sources
pwn.college - reverse engineering.