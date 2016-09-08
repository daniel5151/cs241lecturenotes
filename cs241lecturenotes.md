# CS-241 - Foundation of Sequential Programs
## Fall 2016
### Notes by Daniel Prilik - SE 2020

# Instructor info
- Matt Crane
	- Email: matt.crane@uwaterloo.ca
	- Office Hours: DC2555F 1:00 - 2:00pm Tues / Thurs
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
- 25% Assignments - Due thursdays at 9
- 25% Midterm - Wed Oct. 26th from 7:00-8:50pm
- 50% Final (must pass) - 2.5h sometime in december

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

Eg: `00001010` is `\n` in ASCII

## Hexadecimal

In general, binary SUCKS to work with. Hexadecimal sucks less.

Essentially, we can represent numbers with 16 symbols, instead of just 1 and 0

We use the digits 0-9, A, B, C, D, E, and F.

A nice property of Hexadecimal is that it is easy to convert into Binary, and vice versa.
You just split the binary number into chunks of 4 bits, and then write the digit associated with each chunk.

Eg: `1010 1111 1001 1001` = `xAF99`