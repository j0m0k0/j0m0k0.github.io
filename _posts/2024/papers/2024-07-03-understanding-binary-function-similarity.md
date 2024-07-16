---
title: Understanding Binary Function Similarity
date: 2024-07-05 15:20:00 -0500
categories: [Papers, Reverse Engineering]
tags: [binary function similarity]     # TAG names should always be lowercase
image: /assets/img/posts/paper-binary-comparison/cover.png
alt: "How Machine Learning Is Solving the Binary Function Similarity Problem?"
math: true
---
Recently, I came across a paper[^footnote] that introduced new concepts to me. Consequently, I decided to delve into the problem it describes and share my findings. In this blog post, we will explore the **binary function similarity** problem, understand its significance, and examine existing approaches to address it.

## Background Knowledge
If you are interested to read papers in this research area, you probably need some background knowledge. Here I put some of the concepts that you should be familiar with to be able to understand this paper easier. [If you just interested in knowing the problem, then skip this part and go directly to the Next Section](#binary-function-similarity).

### Stripped Binaries
Those kinds of binaries that symbolic information (like variable names, function names) has been removed. This stripping process reduces file size and makes the reverse engineering process harder.

### Static Linking
In static linking, libraries and dependencies are included directly into the binary during compilation. This contrasts with dynamic linking, where libraries are linked at runtime.

### Stub
stub is like a little note in a program that says, "Hey, I need to use this function, but I don't know exactly where it is right now." When the program runs, it uses this note to find the function and then updates the note with the exact address, so it knows where to go next time it needs the function.

### Dynamic Linker
When the program runs, a special helper called the "dynamic linker" reads the stub's note. The dynamic linker knows where all the shared libraries (like toolkits) are stored. It looks up the function in these libraries, finds the exact location, and updates the stub with this address. So, next time the program needs that function, it knows exactly where to find it. For example, `dyld` is the dynamic linker used in macOS.

### A Fuzzy Hash, or Similarity ash
A cryptographic hash function that calculates a hash value based on the content of a file or data, but with the property that small changes in the input data result in small changes in the hash value. This is unlike traditional cryptographic hashes (like SHA-256) where even a tiny change in input results in a completely different hash value.

### Function Inlining
A technique used by compilers to improve the performance of a program. Instead of calling a function and jumping to its code, the compiler takes the body of the function and inserts it directly into the place where the function is called. This eliminates the overhead of a function call, such as setting up the stack and jumping to the function's code, making the program run faster. However, it can increase the size of the code if the function is called many times.

### Receiver Operating Character (ROC)
Plots two parameters True Positive Rate (TPR) and False Positive Rate (FPR).

### Area Under Curve (AUC)
A metric derived from the ROC curve. It quantifies the overall ability of a model to discriminate between positive and negative classes. The AUC value ranges from 0 to 1, where: An AUC of 0.5 suggests a model with no discrimination ability, equivalent to random guessing. An AUC of 1.0 indicates a perfect model that perfectly separates the positive and negative classes without error.

## Binary Function Similarity
The binary function similarity problem can be defined as follows:

> Taking as input the binary representation of a pair of functions, and producing as output a numeric value that captures the “similarity” between them.
{: .prompt-tip }

However, before addressing **how** this problem can be solved, it's important to understand **why** it needs to be solved. Here are some applications of binary function similarity:
- Reverse engineering
- Detecting and patching vulnerabilities in third-party libraries
- Binary diffing and patch analysis

## Example
Consider two functions written in C++ that calculate Fibonacci numbers up to the nth term. Although their approaches differ, they perform the same function.

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


Let's compile these two programs to create executable binary files:


```bash
g++ -o fibonacci_iterative fibonacci_iterative.cpp
g++ -o fibonacci_recursive fibonacci_recursive.cpp
```

We can disassemble the object file using `objdump`:
```bash
objdump -d fibonacci_iterative > fibonacci_iterative_disassembly.txt
objdump -d fibonacci_recursive > fibonacci_recursive_disassembly.txt
```

If you examine the generated files, you will find the machine code for each function in the second column. Although represented in hexadecimal, this is equivalent to the binary code executed by the CPU. The rightmost column displays the corresponding assembly code.
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
...
```
{: file='fibonacci_iterative_disassembly.txt'}

Similar representation exists for the fibonacci_recursive function.

Now the question arises: Given the binary representations of these two functions, can you determine how similar they are? The definition of similarity can vary—whether it refers to the sequence of binaries or the functionality executed by a function depends on the context but typically involves functional similarity.

## Solutions
A simple search on Google Scholar reveals numerous papers attempting to address the binary function similarity problem. The paper I referenced earlier, titled How Machine Learning Is Solving the Binary Function Similarity Problem, is a review paper that summarizes notable solutions and compares them.

Here are some images from the paper showing a comparison of different approaches to solving the binary function similarity problem, measured on a dataset, making the results comparable. The metrics are based on the Area Under Curve (AUC), hence they range between 0 and 1.
![Table 3](/assets/img/posts/paper-binary-comparison/table3-marcelli.png)

![Figure 2](/assets/img/posts/paper-binary-comparison/figure2-marcelli.png)

## Read More
[^footnote]: <a href="https://www.usenix.org/conference/usenixsecurity22/presentation/marcelli" target="_blank">How Machine Learning Is Solving the Binary Function Similarity Problem</a>