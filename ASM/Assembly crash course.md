CPU
- As registers
- Control Unit
- Have a cache.
- Cpu acts only on cache and register.

Asssembly is a direct view of binary.
Assembly is name that way because it is assembled into binary code.

Asssembly is composed of instructions made of operation ad operand.

## Operand
The cpu is concerned with three types of data.
- Data we directly git as part of the instruction (What we give to the cpu)
- Data that is close at hand. (Register)
- Data in storage. 
## Operations
- What might you want to do with the data

## Instructions
An instructions look like this.
OPERATION
OPERATION OPERAND
OPERATION OPERAND OPERAND
## Dialects 
Assembly it's very CPU architecture dependent.

## Registers
Registers are very fast, temporary stores for data.
Some general purpose registers.
- rax
- rsp
- rbp
The address of the next instruction is in a register
	- rip (amd64)

- On  a 64-bit  architecture (most) register will hold 64 bits (8 Bytes)
- Some registers can be partialy access.
### Setting Registers
Load data into registers with **mov**.
```Assembly
mov rax , 2
```
this exemple load  the number 2 into the register rax.
Data specified directly int the instruction like this is called an **Immediate Value**

mov copies the data don't move it.


You can copy  data from one register to another.
``` asm
mov rbx, rax
```

### Extend Data
movsx does a sign-extending move, preserving the top bit to the rest of the register.
```
mov eax, -1
movsx rax, eax
```

### Som special registers
You can't directly read/write from **rip** (ip == Insruction Pointer), it contains the address of the next instruction to be executed
Should be careful with **rsp** (sp=Stack Pointer), it contains the address of an region of memory to store temp data.
Som register by convention are used for important things.

## Memory
### Stack
**push** can store data on the stack
**pop** can retrieve data from the stack in reverse order (Logic First In Last Out)
```
mov rax, 2
push rax
```
Set 2 to rbx
```
pop rbx 
```

The CPU knows where the stack is because its address is stored in **rsp.**
### Accessing Memory
```
mov rax, 0x7732
mov rbx, [rax] // Charge dans rbx la valeur stocker a l'addresse 0x7732

mov rax, 0x7732
mov [rax], rbx // Charge la valeur de rbx dans l'addresse 0x7732

sub rsp, 8
mov [rsp], rcx // Equivalent of push rcx.
```

### Controlling Write Sizes
Using Partials register to store/load fewer bits.

### Memory Endiness
Data on most modern systems s stored backwards, in little endian.
The bytes are flipped not the bits.
It only happen when storing and loading multiple bytes register at a time.

### Address Calculation 
Limits = reg+reg(2 or 4 or 8)+value

```
mov rax, 0
mov rbx, [rsp+rax*8]
inc rax
mov rcx,[rsp+rax*8]
```
Load Effective Address (lea)

### rip Relative Addressing
```
lea rax, [rip] // Load the address of the next instruction into rax
lea rax, [rip*8] // Load the address of the next instruction into rax + 8  bytes
```

```
mov rax, [rip] // load 8 bytes from the location pointed to by the address of the next instruction
```

### Writing Immediate Values

```
mov rax, 0x133337
mov DWORD PTR [rax], 0X1337
```

## Control Flow
### Jump
jmp interrupt the sequences.
jmp add X bytes to the execution pointer and then resume execution.
```
mov cx, 1337
jmp STAY_LEET
mov cx, 0
STAY_LEET
	push rcx

```

### Conditional jump
jnz stand for jump if not zero
some operation of jump -> https://www.tutorialspoint.com/assembly_programming/assembly_conditions.htm
```
mov cx, 1337
jnz STAY_LEET
mov cx, 0
STAY_LEET:
push rcx
```

### Conditions 
Conditional jump check Conditions stored in the "flag" register **rflag**
Slide 6 of pwn college assembly crash courses

### Looping
This code increment rax to 10
```
mov rax, 0
LOOP_HEADER:
inc rax
cmp rax, 10
jb LOOP_HEADER
```

### Function Calls
call pushes rip and jumps away ( to the memory address where the function is)
ret popss rp and jump  to it.  (return where we stope before.)
```
mov rdi, 0
call FUNC_CHECK_LEET
mov rdi, 1
call FUNC_CHECK_LEET
call EXIT

FUNC_CHECK_LEET:
	test rdi, rdi
	jnz LEET
	mov ax, 0
	LEET:
	mov ax, 1337
	ret
```

Caler and callee conventions ?

## System calls
It's an instruction that makes a call into the OS
**syscall** is the instruction that call

Here the read syscall
```
mov rdi, 0
mov rsi, rsp
mov rdx, 100
mov rax, 0
syscall
```


# Source
https://pwn.college/fundamentals/assembly-crash-course