---
title: Understanding Binary Function Similarity
date: 2024-07-05 15:20:00 -0500
categories: [Papers, Reverse Engineering]
tags: [binary function similarity problem]     # TAG names should always be lowercase
image: /assets/img/posts/paper-binary-comparison/cover.png
alt: "How Machine Learning Is Solving the Binary Function Similarity Problem?"
---
Recently, I was reading a paper[^footnote] which I found new for myself. Therefore, I decided to understand the problem described in it and share it with you. In this blog post, we will see what is **binary function similarity** problem, why it is important and we will learn more about the existing approaches to solve this problem.

## Binary Function Similarity
Binary function similarity is the problem of **taking as input the binary representation of a pair of functions, and producing as output a numeric value that captures the “similarity” between them**.

Let's say we have two function written in C++ that implement the Fibonacci numbers up to the `nth` number. Their approach is different but they do the same job.

Approach 1:
```c++
#include <iostream>

int fibonacciIterative(int n) {
    if (n <= 1) return n;
    int a = 0, b = 1, c;
    for (int i = 2; i <= n; i++) {
        c = a + b;
        a = b;
        b = c;
    }
    return b;
}

int main() {
    int n;
    std::cout << "Enter the value of n: ";
    std::cin >> n;
    std::cout << "Fibonacci number is: " << fibonacciIterative(n) << std::endl;
    return 0;
}
```
{: file='fibonacci_iterative.cpp'}

Approach 2:
```c++
#include <iostream>

int fibonacciRecursive(int n) {
    if (n <= 1) return n;
    return fibonacciRecursive(n-1) + fibonacciRecursive(n-2);
}

int main() {
    int n;
    std::cout << "Enter the value of n: ";
    std::cin >> n;
    std::cout << "Fibonacci number is: " << fibonacciRecursive(n) << std::endl;
    return 0;
}
```
{: file='fibonacci_recursive.cpp'}


Let's compile these two programs to get the executable binary files:

```bash
g++ -o fibonacci_iterative fibonacci_iterative.cpp
g++ -o fibonacci_recursive fibonacci_recursive.cpp
```

We can disassemble the object file using `objdump`:
```bash
objdump -d fibonacci_iterative > fibonacci_iterative_disassembly.txt
objdump -d fibonacci_recursive > fibonacci_recursive_disassembly.txt
```

Now if you take a look at the generated files, you can find the corresponding machine code for each of these functions:
```
0000000100002fd0 <__Z18fibonacciIterativei>:
100002fd0: d10083ff    	sub	sp, sp, #32
100002fd4: b9001be0    	str	w0, [sp, #24]
100002fd8: b9401be8    	ldr	w8, [sp, #24]
100002fdc: 71000508    	subs	w8, w8, #1
100002fe0: 1a9fd7e8    	cset	w8, gt
100002fe4: 370000a8    	tbnz	w8, #0, 0x100002ff8 <__Z18fibonacciIterativei+0x28>
100002fe8: 14000001    	b	0x100002fec <__Z18fibonacciIterativei+0x1c>
100002fec: b9401be8    	ldr	w8, [sp, #24]
100002ff0: b9001fe8    	str	w8, [sp, #28]
100002ff4: 1400001d    	b	0x100003068 <__Z18fibonacciIterativei+0x98>
100002ff8: b90017ff    	str	wzr, [sp, #20]
100002ffc: 52800028    	mov	w8, #1
100003000: b90013e8    	str	w8, [sp, #16]
100003004: 52800048    	mov	w8, #2
100003008: b9000be8    	str	w8, [sp, #8]
10000300c: 14000001    	b	0x100003010 <__Z18fibonacciIterativei+0x40>
100003010: b9400be8    	ldr	w8, [sp, #8]
100003014: b9401be9    	ldr	w9, [sp, #24]
100003018: 6b090108    	subs	w8, w8, w9
10000301c: 1a9fd7e8    	cset	w8, gt
100003020: 370001e8    	tbnz	w8, #0, 0x10000305c <__Z18fibonacciIterativei+0x8c>
100003024: 14000001    	b	0x100003028 <__Z18fibonacciIterativei+0x58>
100003028: b94017e8    	ldr	w8, [sp, #20]
10000302c: b94013e9    	ldr	w9, [sp, #16]
100003030: 0b090108    	add	w8, w8, w9
100003034: b9000fe8    	str	w8, [sp, #12]
100003038: b94013e8    	ldr	w8, [sp, #16]
10000303c: b90017e8    	str	w8, [sp, #20]
100003040: b9400fe8    	ldr	w8, [sp, #12]
100003044: b90013e8    	str	w8, [sp, #16]
100003048: 14000001    	b	0x10000304c <__Z18fibonacciIterativei+0x7c>
10000304c: b9400be8    	ldr	w8, [sp, #8]
100003050: 11000508    	add	w8, w8, #1
100003054: b9000be8    	str	w8, [sp, #8]
100003058: 17ffffee    	b	0x100003010 <__Z18fibonacciIterativei+0x40>
10000305c: b94013e8    	ldr	w8, [sp, #16]
100003060: b9001fe8    	str	w8, [sp, #28]
100003064: 14000001    	b	0x100003068 <__Z18fibonacciIterativei+0x98>
100003068: b9401fe0    	ldr	w0, [sp, #28]
10000306c: 910083ff    	add	sp, sp, #32
100003070: d65f03c0    	ret
```
{: file='fibonacci_iterative_disassembly.txt'}

And for the `fibonacci_recursive` function you will also get a representation like this.
Now here comes the question: Given the binary presentations of these two functions, can you tell how much they are similar? The point that matters in this question is that what do you define as similarity? Is it the sequence of binaries? or is it the functionality that is done by a function? Well, it can be anything depending on the context, but usually it means the functionality similarity.
## Read More
[^footnote]: <a href="https://www.usenix.org/conference/usenixsecurity22/presentation/marcelli" target="_blank">How Machine Learning Is Solving the Binary Function Similarity Problem</a>