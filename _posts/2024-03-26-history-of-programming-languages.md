---
layout: post
title: History of Programming Languages
author: Marco Ferrati
categories: computer_science
---

With this blog post we will see when your favorite programming languages came to life and their principal characteristics.

| Programming language         | Year | Date added |
|------------------------------|------|------------|
| [Assembly](#assembly---1947) | 1947 | 2024-03-25 |

# Assembly - 1947
Assembly is one of the first programming languages, originated in the mid-20th century as a solution to the complexities of directly interacting with early computers. Prior to its development, programmers had to toggle switches and wire circuits to execute instructions, or using punched cards. Assembly language introduced a symbolic representation of machine instructions, using mnemonic symbols to represent operations and memory addresses. 

This abstraction allowed programmers to write code in a more human-readable format, which was then translated into machine code by an **assembler**. Nowadays, assembly remains relevant in fields such as system programming, embedded systems, and performance-critical applications. Its low-level nature provides precise control over hardware resources, making it indispensable for tasks requiring direct hardware manipulation. 

The first thing you need to know when you start writing assembly code is that the instruction set depends on the [computer architecture](https://en.wikipedia.org/wiki/Comparison_of_instruction_set_architectures#Instruction_sets) where we want to execute the program. You have to choose the right "Assembly language" for your computer architecture if you want to write programs with it.

In any case, it is different from any other programming language you have ever seen. The classic instructions you can find in any other programming language like: variable declaration, `if-then-else`, and `while` are, let's say, "missing".
In Assembly you are telling directly to the processor what to do (that's why it is architecture dependent). The processor execute one line at the time and everything can be seen as read from memory, write to memory, jump to a line different from the next one. With these three type of instructions we can model all the behaviors that other programming languages achieve with `a = 1`, `if (a == 1) {do_something()}`, and`while(a != 10) {do_something(a)}`.

You have to keep in mind that there is not a standard library for assembly but do not despair: you have access to functions provided by your operating system through system calls and you can also call functions which are present in any library installed.

#### Hello World in Assembly
We have already wrote a blog post about how the classic "Hello World" program works in Assembly. [Check it out]({% post_url 2024-03-19-hello-assembly%})!

Here the source code and how to `assemble` it
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

{% highlight bash %}
gcc -static -nostdlib hello.s -o hello 
./hello
{% endhighlight %}
