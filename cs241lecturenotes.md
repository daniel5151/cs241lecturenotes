<script>
(function(i, s, o, g, r, a, m) {
    i['GoogleAnalyticsObject'] = r;
    i[r] = i[r] || function() {
        (i[r].q = i[r].q || []).push(arguments)
    }, i[r].l = 1 * new Date();
    a = s.createElement(o),
        m = s.getElementsByTagName(o)[0];
    a.async = 1;
    a.src = g;
    m.parentNode.insertBefore(a, m)
})(window, document, 'script', '//www.google-analytics.com/analytics.js', 'ga');

ga('create', 'UA-58621690-1', 'auto');
ga('send', 'pageview');
</script>

# CS-241 - Foundation of Sequential Programs
## Fall 2016
### Notes by Daniel Prilik - SE 2020

# Instructor info
- Matt Crane
	- Email: matt.crane@uwaterloo.ca
	- Office Hours: DC2555F 3:00 - 4:00pm Tues / Thurs
- Troy Vasiga
	- Email: troy.vasiga@uwaterloo.ca
	- Office Hours: DC3112 12:00 - 1:30pm Tues / Thurs
- ISA: Max Bardakov 
    - Email: cs241@uwaterloo.ca

# Lecture 1

Oh boy! Here we go again!

## Bookeeping

The course website is www.student.cs.uwaterloo.ca/~cs241/
- Syllabus
- Announcements
- Everyhing else!

A note about Assignments:
- Start early!
- Don't fall behind!
- In total, there are 10 assignments, each with ~9 subparts, so ~100 things to submit

The course uses our favorite program: _Marmoset!_
- This time around though, there are Release Tokens, that give you 3 attempts per 12h to test your programs

Marking breakdown:
- 25% Assignments - Due Thursdays at 7:00pm
- 25% Midterm - Wed Oct. 26th from 7:00-8:50pm
- 50% Final (must pass) - 2.5h sometime in December

## Idyllic Intro

So what is the purpose of this course:
- To learn
- To Meta-think
- To write a program, that reads a program, that outputs a program.
	- Inception. BWUHHH

By the end of this course, we will know what _really_ happens when you compile and run a program, and there will be little to no mystery about what happens when you run a program.

## Technical Intro

In this course, all a computer is a **CPU** and **RAM**.

A CPU **Controls and Manipulates the Data**, and the RAM is just a bunch of **addressed "boxes" that store Data**.

## Binary Data

All data is at a basic level is a sequence of 1s and 0s, or Bits

There are many interpretations for what a specific sequence of bits means (i.e: numbers, ascii, etc...), and there is no one "correct" interpretation.

## Machine Language

There are certain sequences of bits that do in-fact have one specific meaning, or at least they do when it comes to how the machine interprets them. Depending on the Achitecture of the machine (i.e: Intel/Motorola, 32/64bit, etc...) there may be different bit sequences that mean the same things.

These codes are great for machines, super easy, just 0 = off, 1 = off, but they SUCKS for humans.

## Assembly 

**Assembly** on the other hand, sucks less for Humans.

It is a simple, textual representation of machine language. It is more human readable, and makes development less, shall we say, absolutely terrible.

A big plus of assembly is that is it pretty easy to translate Assembly to Machine Code. Assembly is just an _Abstraction_.

## Assembler
The **Assembler** is the program that preforms the translation from Assembly to Machine Code. 

## Back to the Basics: Bits

What is a Bit exactly?

Well, it is just a value that can have 2 states, either 1, or 0. That's it.

The nice thing is that a **sequence of bits** can describle a lot of different value.
- 2 bits can have 4 arrangements
- 3 bits can have 8 arrangements
- n bits can have 2^n arrangements!

We can use Bits to describle certain useful "types":

### Integers

#### Unsigned integers
Each sequence is just a direct representation of a number in base 2.

#### Two's Compliment
What if we want Negative Numbers? Well, then we have to use a more complicated code, called 2s compliemnt.

To get 2s compliemnt, we
1. write the absolute value of a number in banary
2. Negate the bits (to get 1s compliment)
3. Add 1

**So, With 3 bits, we can have the following interpretations for integers...** 

Binary | Decimal | 2's compliment
-----|----- | ------
`000` | 0 | 0
`001` | 1 | 1
`010` | 2 | 2
`011` | 3 | 3 
`100` | 4 | -4
`101` | 5 | -3
`110` | 6 | -2
`111` | 7 | -1

** Notice that in 2s compliment, the left-most bit tells us if it is negative or not...

To hammer in this point, consider `1010`.
What does it mean?
Well, nothing really, not until we know what type is should represent.
It is `10` if it's an unsigned number, but it's `-6` in 2s compliment 

#### Characters
Typically represented with **8 Bits**

Eg: `00001010` is `\n` in ASCII (use the linux command `man ascii` for a full table)

## Hexadecimal

In general, binary SUCKS to work with. Hexadecimal sucks less.

Essentially, we can represent numbers with 16 symbols, instead of just 1 and 0

We use the digits 0-9, A, B, C, D, E, and F.

A nice property of Hexadecimal is that it is easy to convert into Binary, and vice versa.
You just split the binary number into chunks of 4 bits, and then write the digit associated with each chunk.

Eg: `1010 1111 1001 1001` = `xAF99`

# Lecture 2

## Grouping of Bits

The most common grouping of bits is in a **byte**, or a group of **8 bits**

There are **256** possible values that can be encoded by 8 bits. What to encode however, is up to interpretation (see above)

## Files

Files are just long sequences of bytes, and it is up to a program to determine what the byte sequences actually mean.

The command `cat` for example, will interpret any file thrown at it as Text, and print out each byte as a ASCII char.

The command `xxd` on the other hand, will print the file's bits as hexadecimal values (alongside an ascii interpretation of the bits)

So, for example, if there is a file `hasY` with string `Y\n`, then the output of `xxd` would be something like:

```
#Addr     #Hex   #Ascii
00000000: 590a   Y.
```

`59` is the hex code for `Y` in ascii, and `0a` is the hex code for the Newline Char in ascii

## Words

A **Word** is a grouping a bits that a specific CPU "likes" (i.e: can easily do math on, execute ops, etc...)

Words can be any number of bits... from **8 bit** in the 80s, all the way to **64 bit** nowadays.

NOTE: a CPU's specific word-size will limit the total ammount of memory a CPU can ever see! For example, 32 bit CPUs could only address ~3.5gigs of memory, so until the switch to 64 bit CPUS, no matter how much RAM you shoved in a PC, if the OS was 32bit, it couldn't see more than 3.5gigs

## Our Machine

The machine we are using in cs241 is a **Stored Program Computer**

What this means is that the CPU is connected to the Memory (via a "mem bus") not just to use the memory as a place to store data, but also as a place to store actual program code.

To run a program, the CPU calls the memory for an instruction, and the memory returns a string of bits that (should) correspond to a instruction that the CPU can execute.

## CPU

CPUs are not actually just magic boxes. They have things within them that make them work...

There are several places to Store things
- **Program Counter (PC)**- Where in memory to load new instructions from
- **Instruction Register (IR)**- Chunk of memory that holds the instruction to run
- **Registers 0-31 ($0 -> $31)** - "boxes" that can store words of information (think superfast ram)

And there are other places that Do things
- **Control Unit** - reads the PC, retrieves the instruction from memory, puts that instruction in the IR, and then executes the instruction
- **Arithmetic Logic Unit (ALU)** - Can do maths on given bits. Things like adding, subtracting, AND / OR / NOTs, etc...

## Memory (RAM)

RAM is really just a giant block of "boxes" that can store bytes, starting from 0 to denote the 1st byte, 4 to denote the 5th byte, etc...

On a MIPS machine, words are 4 bytes, and as such, when addressing the RAM to ask for instructions, we must ask for words, so we address RAM in increments of 4.

## MIPS

MIPS is a set of instructions that our processor understands. 

In this course, there are **18** different ** 32-bit (4 byte)** instructions encoded in 2 basic instruction formats.

**MIPS assembler** is the **Assembly Language** that translates human-readable instructions into the actual 32-bit / 1 word instructions that the CPU can read.

For example:
- `add $1, $2, $3` are **MIPS instructions** that correspond to...
- `0000 0000 0100 0011 0000 1000 0010 0000` when converted to **Binary**, or 
- `0x00430820` when written in **Hex**

That binary actually means the following...
```
000000      ; Call the ALU
00010       ; $2
00011       ; $3
00001       ; $1
00000100000 ; Add
```

A full list of MIPS instructions can be found here: https://www.student.cs.uwaterloo.ca/~cs241/mips/mipsref.pdf

## Loading and Storing values to / from RAM

The instruction `lw` loads a word from memory, and `sw` stores a word to memory

Eg: `lw $7, 0($3)` will load the value at MEM[$3] into register $7
Eg: `sw $8, 4($3)` will load the value from $8 to MEM[$3+4] (that +4 is needed since we store Words in memory, and Words are 4 bytes each)

## Main Machine Cycle

Every single clock cycle, the following happens:

1) Fetch a word from RAM whose address is in the PC (the PC is initialized to 0 on power-on)
2) Place that word in the IR
3) Increment the PC by 4
4) Decode and Execute the instruction that is in the IR

# Lecture 3

## Special Registers

Register | Description
--- | ---
`$0`  | Constant **value 0**
`$29 and $30` | **Stack** (see below...)
`$31` | The **Return Address (RA)**

## Assembly Code

There is a 1 to 1 correspondance b/w Assembly Language and Machine Language. It translates human-friendlier mnemonic instructions like `add $3, $1, $2` to their related bit form. The **Assembler** is the program that does this automatic translation.

For some example of Assembly Code and the Machine Language equivilents, see the cs241 website.

# Lecture 4

## Labels

Labels identify an address.

```language
; some stuff

loop: add ...
; more instructions...
bne $2, $0, loop ;using label

X: Y: ; can have 2 labels on the same line

```

## Storing and Restoring Registers

What happens if we call a subroutine where it uses some registers, that you need! We only have $32 registers after all!

Consider this example below

```
; Example 6a: Calling a procedure
sw $31, −4($30)		; save $31 on stack
lis $31
.word 4
sub $30, $30, $31
lis $1 				; call sumOneToN(13)
.word sumOneToN
lis $2
.word 13
jalr $1
lis $31				; restore $31 from stack
.word 4
add $30, $30, $31
lw $31, −4($30)
jr $31 				; return to OS

;------------------------

; Example 6b: A procedure
; sumOneToN: sum the integers from 1 to N
; input: $2 is N
; output: $3 is the sum

sumOneToN:
sw $1, −4($30) 		; save $1 on stack
sw $2, −8($30) 		; save $2 on stack
lis $1
.word 8
sub $30, $30, $1
add $3, $0, $0 		; clear $3
beginLoop:
add $3, $3, $2 		; add $2 to $3
lis $1 				; decrement $2
.word −1
add $2, $2, $1
bne $2, $0, beginLoop
lis $1
.word 8
add $30, $30, $1
lw $1, −4($30) 		; restore $1 from stack
lw $2, −8($30) 		; restore $2 from stack
jr $31 				; return from sumOneToN

```

In general, Stack usage rules are:

```
sw
sw
...
sub $30, $30, 4.n
[body]
add $30, $30, 4.n
lw
lw
jr $31
```

## Recursion

Here is an example of recursion

```Assembly
; Save $31 on the stack
sw $31, -4($30)
lis $31
.word 4
sub $30, $30, $31

; Call recSum(13)
lis $4
.word recSum
lis $1
.word 13
jalr $4

; Restore $31 from the stack
lis $31
.word 4
add $30, $30, $31
lw $31, -4($30)

; Return to OS
jr $31

;-----------------------

; recursively sum up the integers from 1 to N
; assume that input (N) is in $1
; output is returned in $3
recSum:
; Save registers on the stack
sw $1, -4($30)
sw $2, -8($30)
sw $4, -12($30)
sw $31, -16($30)
lis $4
.word 16
sub $30, $30, $4
; Initialize sum so far
add $3, $0, $0
; Check to see if we are in the base case (N=0)
beq $1, $0, done
; Otherwise, we must compute the sum of the current N
; and the sum of the rest
; keep a copy of the current value of N
add $2, $1, $0
; put N-1 into register $1
lis $4
.word 1
sub $1, $1, $4
; get ready to call routine (i.e., ourself)
lis $4
.word recSum
jalr $4
; add the value we got back to the current value of N (in $2)
add $3, $3, $2
done:
; restore registers
lis $4
.word 16
add $30, $30, $4
lw $1, -4($30)
lw $2, -8($30)
lw $4, -12($30)
lw $31, -16($30)
jr $31
```

In general, the template for recursion in MIPS is roughly:

- Save registers ($31 in particular)
- Check base case
- Recursive case:
	- Compute next value
	- Call self
	- Compute return value
- Restore registers