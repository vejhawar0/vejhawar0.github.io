---
layout: post
title: On the Cybersecurity Grind
date: 2025-03-11 11:29 +0700
modified: 2025-03-12 01:07 +07:00
description: The hopeful beginning of this blog
tag:
  - tips
  - git
  - software
  - cybersecurity
  - midterm
  - notes
---
Note that this page is designed to be a study guide. As a result, note the items with a __*__ right next to them as they may be important for the midterm, or just in general are things worth knowing.

# Table of Contents
1. [Chapter 1] (# Chapter 1)


# Chapter 1 
Chapter 1 deals with the idea of fundamental principles regarding security. Note the following down:

1. Know your threat model*
2. Consider Human Factors*
3. Security is Economics*
4. Detect if you can't prevent*
5. Defense in Depth*
6. Least Privilege*
7. Separation of Responsibility*
8. Ensure Complete Mediation*
9. Shannon's Maxim*
10. User fail-safe defaults*
11. Design Security in From the Start*
12. TCB*
13. TOCTTOU Vulnerabilities*


## Know your threat model
Make a mental picture of the attackers and the kind of resources that they have. With this, we assume that they have any information about your operating system, can attack often to get lucky, have something worth attacking for, and can devote resources, and if they can coordinate complex attacks.

## Consider Human Factors
Security systems are ultimately used a lot by ordinary people. As a result, you have to make the system user friendly. Furthermore, designers are also human and may make mistakes. These are things that you have to keep in mind.

## Security is Economics
Pretty straightforward. Use more resources on more valuable stuff. For both attackers as well as defenders.

## Detect if you can't Prevent
Just figures out if you've been tampered with. Prepare systems for worst case outcome.

## Defense in Depth
Layer multiplyt ypes of defenses so an attacker would have to breach all the defenses to attack a system. Choose whether you care about false alarms or not when layering detectors in parallel or series

## Least Privilege
Only give as much access as someone needs. Nothing more.

## Separation of Responsibility
Like our government system, make it so that more than one party has to approve before something happens.

## Ensure Complete Mediation
When enforing access control policies, think about access to every object. This is helpful to figure out where the vulnerabilities are. Need ot ensure that all access is monitored and proteted. Create a single reference monitored, which is a single point through which all access must occur (firewall). 

## Shannon's Maxim
Don't rely on security through obscurity. In other words, assume that your attacker knows your system. Kerckhoff's Principle says that a cryptographic system should remain secure even when an attacke rknows all the internal details of the system. Secret key is the only thing that must be kept secret.

## User fail-safe defaults
When things fail, make sure that they fail in a safe state (default), not an unsafe or unsecure state.

## Design security in from the start
As it says, design with security in mind from the very beginning, not as an afterthought.

## The Trusted Computer Base
TCB is a portiono f the system that must operate correctly fo the security goals of the system to be assured. 
### Unbypassable
No way to breach system security by bypassing the TCB
### Tamper resistant:
TCB should be protected from tampering by anyone else. There should be no one for things outside the TCB to modify the TCB code or state.
### Verifiable:
It should be possible to verify how correct the TCB is. Should be simple to make it easy to verify

## TOCTTOU (Time of Check to Time of Use) Vulnerabilities:
Using time between function calls to take advantage and create a vulnerability. Basically, vulnerability of time instead of space.

# Chapter 2
*As a note for memory vulnerabilities note the following:

- atoi converts a character string to an integer value
- functions push arguments from 
- printf with no explicit arguments for the location of the format string identifiers, looks 4 bytes up and sees the 

We use x86
- Compiler converts to assembly instructions
- Assembler converts assembly into machine code
- linker resolved dependencies.
- loader sets up and address space to runt eh machine code

## Registers
In addition to $2^32$ bytes of memory in the address space, there are also registers, which store memory directly on the cpu. 

- eip is teh instruction pointer which is the address of where the machine code currently being executed is.
- ebp is the base pointer: address of the top of the current stack frame
- esp: Address of the bottom of the current stack frame.

### Types of Instructions:
- pop %eax: Takes the value at the current bottom of the stack (where esp is) and pushes the value into register eax. Increments stack pointer to go up by a word too.
- push %ebx: Takes value in ebx, decrements stack pointer and pushes value into that spot.


Looking through the whole chapter, the parts that really matter are the following:
- Arguments are pushed onto the stack in reverse order by value. They are usually pass by value type things. As a result the order of methods are the following:
- Push arguments for function
- eip of function
- ebp of function
- function local variables
- 


# Chapter 3

Stack smashing is a concept that is already familliar to you
for format string, this is how the function would look

memcpy works as follows (dest, src, n)

&buf (address fo format string)
rip of printf
sfp of printf
printf internal pointer points ot the location on the stack 8 bytes above the RIP of printf. This pointer tells teh function where to find the actual arguments.

Dangling pointers are also exploits taht can be used.

ret2ret: Takes advantage of ret instruction location to redirect execution to shellcode dynamically.

# Chapter 4: Ways to mitigate vulnerabilties:
- ASLR (randomizing address space)
- non-executable pages (certain pieces of memory can't execute code)
- pointer auth. Put a hash with the pointer (stored in cpu level code)


# Chapter 5: Cryptography

- Confidentiality*: Attacker cannot read messages
- Integrity*: Attacker cannot change messages
- authenticity*: Message is from claimed author
- IND-CPA*: Eve sends M0 and M1 and needs to figure out which of M0 or M1 the message is. If probability of guessing text is around 50% then it IND-CPA secure


## Types of Encryption
- One-time pad: Keygen(), xor message and key for encryption, xor again for original. Only practical if key was securely distributed.
- Block Ciphers: Encrypts a fixed size of bits. Initially not IND-CPA because its deterministic. ECB mode: Segregates blocks with no relation to each other.
- CBC mode (cipher block chaining):  plain text xors with iv and goes through encryption. This ciphertext is used as the input to the next block. For decription, decrypt cipher text and xor with the IV. Then send cipher text to input of the decriptin and xor with the previous ciphertext (uses padding)
- CFB mode: Takes IV and puts it thorugh encryption and xors with plain text.
- CTR mode: Like CFB except instead of ciphertext being placed into the next value, we instead use a counter + nonce in order to change the values around.



