---
layout: post
title: Hello World in assembly!
author: Giulio Umbrella
categories: binary
---


Hello world is the very first step for every programming language. But no matter what language you choose, your code will be eventually be transformed and executed in assembly form. So, let's see how we can directly interact with the processor to print a message.


## A C introduction

Before we jump into assembly, let's go through a simple C program to print hello world. We'll use this as a working example to introduce assembly related concepts:

{% highlight c %}
#include <unistd.h>
#include <string.h>

int main() {
    char msg[] = "hello world"; // Define the string
    
    // Write the string of length 11 to standard output
    write(1, msg, 11);
    
    // Exit the program
    return 0;
}
{% endhighlight %}

The structure of the program is pretty self-explanatory:

- It contains a `main` function - the program's entry point
- It defines a string with the message
- It invokes the `write` function
- It exits the program


Let's focus on the [write](https://man7.org/linux/man-pages/man2/write.2.html) function, which contains three parameters. Clearly, one it the message we want to print, to be more specific a **pointer** to the string. But how about the other two?

The program uses the value `1` value to print the string to the **standard output**. If you checked the function description in the link above - I'm sure you did it - you saw that the first argument is a **file descriptor**. But wait, we wanted to print the message in our shell, so why bother and consider file descriptors in the first place? Simply put, from the program point of view, both standard input and standard output are just **files**. Behind the curtains, the OS handles input and output with the same mechanisms as the other files. 

The values 0 and 1 have a special meaning and are associated with standard input and standard output respectively. As we want to write in our shell, we use the value 1 to send the message to standard output.

Lastly, we must tell the function how many byte of the string we want it to print and we pass the value `11`.

## Assembly

Armed with the previous example knowledge, let's walk through to the assembly code:

> In a Linux machine - like ubuntu - create an hello.s file and copy and paste the following code:


{% highlight s %}
.intel_syntax noprefix        ; use intel syntax
.global _main 	              ; define global variable
_main:                        ; program entry point

mov rdi, 1                    ; standard output file descriptor
lea rsi, [rip + msg]          ; string pointer
mov rdx, 11                   ; number of byte to read
mov rax, 1                    ; write syscall
syscall                       ; invoke syscall

mov rdi, 0                    ; set exit value
mov rax, 60                   ; exit syscall
syscall                       ; invoke syscall

msg:                          ; label
.string "hello world"         ; string 
{% endhighlight %}

Next, compile and execute the program:

{% highlight bash %}
gcc -static -nostdlib hello.s -o hello 
./hello
{% endhighlight %}


The program structure resembles the C examples. We can identify four different blocks:

- A `.global _main` variable - the entry point
- A write syscall block
- An exit syscall
- A message string

Although the syntax is quite strange, we can recall the same functioning described in our C program. We declare where the program starts, we write a message and we exit the program.

To fill in the additional details, let's inspect each block.

### Assembly registers

Before analyzing the code, it is better to clarify a few concepts about assembly. The CPU applies logical and mathematical functions on numerical values. Where exactly does it store these values?

The CPU holds the value in local memory areas called [**registers**](https://en.wikipedia.org/wiki/Processor_register). There are several different registers serving different purpose. For the scope of this article, we just need to know how to insert values in the registers.

Let's consider the following example:

{% highlight bash %}
mov rax, 60 
{% endhighlight %}

We are using the `mov` instruction for moving the value 60 in the register `rax`.

### Entry point

{% highlight s %}
.intel_syntax noprefix        ; use intel syntax
.global _main 	              ; define global variabe
_main:                        ; program entry point
{% endhighlight %}

The entry points has two components

- We declare which syntax we are using 
- The declaration of the global variable _main and its usage

The `_main` variable is quite reasonable. The program must start somewhere and so we provide an entry point.

The `.intel_syntax noprefix` is more mysterious. Why bother and declare a syntax? 

To understand this, let take a step back and remember that assembly is the lowest possible level. We are telling directly to the process what to do. Which kind of input does a processor take? Well raw bytes. Turns out that write programs directly in binary format is quite tricky, so we have **mnemonics** to help us out.

Simply put, assembly is just a collection of mnemonics representing the processor operations. Hence, we can create whatever codification we want. [Intel syntax](https://en.wikipedia.org/wiki/X86_assembly_language) is a popular choice for this task, but remember it is not the only one.


### String message 

{% highlight s %}
msg:                          ; label
.string "hello world"         ; string 
{% endhighlight %}

The string block is very simple. We use the `msg:` to declare a point in our code and associate it with a string. Assembly handles different types of variables, such as string, int, double, ecc ecc.

So far we have showed how we enter in our program and how we declare basic variables. It is time to level up and ask the OS to do something for us. 

### Exit

{% highlight s %}
mov rdi, 0                    ; set exit value    
mov rax, 60                   ; exit syscall
syscall                       ; invoke syscall
{% endhighlight %}

Everything that has a beginning, has an end. Programs make no difference. In this block, we are telling the program to exit and return control to whoever called it. To understand what's going on, let's start from the bottom of this block.

The `syscall` is an assembly command telling the processor we want to execute a syscall. But what is a syscall? Remember that a process does not operate in the void - it lives in an operating system. And the operating system simplify our lives by providing a lot of different services, commonly known as [**system calls**](https://en.wikipedia.org/wiki/System_call). 

How do we specify which one to call? The `mov rax, 60` serves this purpose. The exit syscall is associated with the value 60. Check this [reference](https://x64.syscall.sh) for a quick review of syscall. 

By convention, the syscall number is placed in the **rax register**.

Finally, what is a function without parameters? With the `mov rdi, 0` we are setting the first and only function parameter to the value zero. Why this register? Like the syscall numbers, the syscall parameters are placed in well-know registers. The registers associated with the first three parameters are the following:

1. rdi - first parameter
2. rsi - second parameter
3. rdx - third parameter


### Write 

{% highlight s %}
mov rdi, 1                    ; standard output file descriptor
lea rsi, [rip + msg]          ; string pointer
mov rdx, 11                   ; number of byte to read
mov rax, 1                    ; write syscall
syscall                       ; invoke syscall
{% endhighlight %}

Now we can face the final boss, the write function. Well, things should look less confusing right now. The structure is the same the exit syscall.

- Place the parameters in the `rdi`, `rsi`, `rdx` registers 
- Place the syscall code in the `rax` register
- invoke the syscall

Observe that we are passing 3 parameters and the values are similar to the write function in the C example. The value `1` is the standard output, the value `11` is the number of bytes to print. But we need a third value, a pointer to the strings.

In this example we are using a little trick to provide a pointer at run time to a position-independent string. Confused by this sentence? Well, you should. This topic goes beyond our current scope and will be covered in a future post.

### Summing up

In this post we stepped into the assembly realm and saw the basic structure of a program. 

### Extra

To conclude, let's see how the same assembly code can have different representations. We'll use the shell command `objdump` which allow to print the content of file as raw bytes and assembly mnemonics. 

Open and shell and move to the directory with the .hello file. Type the following command:

{% highlight bash %}
objdump -d hello
{% endhighlight %}

Objdump will provide the raw bytes in hexadecimal format and assembly in AT&T syntax - the default one.

{% highlight bash %}
./hello:     file format elf64-x86-64

Disassembly of section .text:

0000000000401000 <_start>:
  401000:       48 c7 c7 01 00 00 00    mov    $0x1,%rdi
  401007:       48 8d 35 19 00 00 00    lea    0x19(%rip),%rsi
  40100e:       48 c7 c2 0d 00 00 00    mov    $0xd,%rdx
  401015:       48 c7 c0 01 00 00 00    mov    $0x1,%rax
  40101c:       0f 05                   syscall 
  40101e:       48 c7 c0 3c 00 00 00    mov    $0x3c,%rax
  401025:       0f 05                   syscall 

0000000000401027 <msg>:
  401027:       68 65 6c 6c 6f          pushq  $0x6f6c6c65
  40102c:       20 77 6f                and    %dh,0x6f(%rdi)
  40102f:       72 6c                   jb     40109d <msg+0x76>
  401031:       64 0a 00                or     %fs:(%rax),%al
  
{% endhighlight %}


To use the Intel syntax use the flag `-M Intel`


{% highlight bash %}
objdump -d -M intel hello
{% endhighlight %}


{% highlight bash %}

./hello:     file format elf64-x86-64

Disassembly of section .text:

0000000000401000 <_start>:
  401000:       48 c7 c7 01 00 00 00    mov    rdi,0x1
  401007:       48 8d 35 19 00 00 00    lea    rsi,[rip+0x19]   
  40100e:       48 c7 c2 0d 00 00 00    mov    rdx,0xd
  401015:       48 c7 c0 01 00 00 00    mov    rax,0x1
  40101c:       0f 05                   syscall 
  40101e:       48 c7 c0 3c 00 00 00    mov    rax,0x3c
  401025:       0f 05                   syscall 

0000000000401027 <msg>:
  401027:       68 65 6c 6c 6f          push   0x6f6c6c65
  40102c:       20 77 6f                and    BYTE PTR [rdi+0x6f],dh
  40102f:       72 6c                   jb     40109d <msg+0x76>
  401031:       64 0a 00                or     al,BYTE PTR fs:[rax]
{% endhighlight %}

What can we say from the two outputs? The raw bytes are the same, while the syntax is different. 