---
title: Probability 101 - What Is Probability? [1/9]
date: 2025-03-15 10:00:00 -0500
categories: [Mathematics, Probability Theory]
tags: [probability, probability theory, probability-101, what is probability, part 1/9]     # TAG names should always be lowercase
image: /assets/img/posts/probability-101-1/cover.png
alt: "Markov Chains Simply Explained!"
math: true
---
Probability is one of the most important parts of mathematics and in fact, one of the most important parts of everyone's real life. Whether you are a student or non-student, knowing the probability and how it works, can help you in understanding more situations in real life and in theoretical problems as well.

This series, consisted of nine parts which will be published on my blog over the time. We cover main ideas, how they works and usually avoid the proofs unless it helps us in understanding that formula or theorem easier. This series is not designed for professional mathematicians and I'm also not a mathematician, so there may be some mistakes in the writing and my descriptions. If you saw any of these mistakes or you have suggestions for improvement, please don't hesitate to contact me or just leave a comment below this post.

People who are working in Computer Science or Computer Engineering majors, are expected to know the basics of probability and this series exactly aims this group of people. However, as I said, it can be useful for any person who is seeking to understand probability without going so deep into the proofs.

The main reference for all the material in this series is the great book by Dimitri P. Bertsekas and John N. Tsitsiklis named "Introduction to Probability, second edition". If I use any other reference, I will mention it in the references part of each chapter.

> Last Update: Sets Theory
{: .prompt-info }

## 1.1 Definition of Probability (What? Why? How?)
The first question that may a person ask is, *WHAT* is probability? The term "Probability" can have different interpretations in different situations. To provide a definition that is true in almost all of the situtations, we can define probability as **"The sceince of studying uncertain situtations"**. By uncertain situations we mean those situations that we cannot talk about their final outcome with hundred percent confidence. You throw a ball to the basket, will it always go into the basket? Maybe yes and maybe no. Medical doctors use a medicine on a patient, will it work? Maybe yes maybe no. 

But *WHY*  we are interested in uncertain situations at all? Because in real-life we are dealing with uncertain situations a lot, and it would be great if we could reason about it. You can think of the uncertain situations that you're dealing with in your daily life.

And now the last question is, *HOW* do we reason about uncertain situations? The way we do it here is by using mathematics or more specifically, probability theory. Probability theory is the main mathematical concept that we are going to learn in this series. 

Just one important tip that you should know is that, mathematics is like a wall that is made of many bricks and layers. Bricks of each layer depend on the bricks of the bottom layer. In simpler words, some theories are based on the other theories. So, sometimes it is good to learn about underlying theories, because it helps us to understand the main theory easier. Set theory is one of those theories that we will learn in this chapter.

## 1.2 Sets Theory
Probability uses **sets theory** extensively. So, we will introduce the sets theory here very briefly.

A **set** is a collection of objects, which are the elements of the set. For showing an element $$x$$ belongs to a set $$S$$, we write $$x \in S$$ and if $$x$$ not belongs to $$S$$ we write it as $$x \notin S$$. A set can have no elements, in which case it is called the **empty set**, denoted by $$\varnothing$$.

Also, we use a concept to represent the set of every possible element in the context that we are talking about. We call it **universal set ($$\Omega$$)**. For example, in the context of binary values the universal set is $$\Omega=\{0, 1 \}$$ because it contains all the possible binary values.

We can represent a set, in many ways. For example, if it contains a finite set of elements, we can write it like $$S = \{x_1, x_2, \dots, x_n \}$$. Some lists are countable infinite, meaning that while we can put them in a list, we cannot count the number of elements in it. For these kind of list we can show them like $$S = \{x_1, x_2, \dots \}$$. Another way of presenting a set is to define a set by certain property(ies) that it has:

$$
    \{ x \mid x \text{ satisfies } P \} \tag{1}
$$

If every element of a set $$P$$ is also an element of a set $$Q$$, then we say $$P$$ is a **subset** of $$Q$$ and write it as $$P \subset Q$$. If $$P \subset Q$$ and $$Q \subset P$$, we say $$P$$ and $$Q$$ are **equal**.


There are some operations on the sets you may already know. But if you don't know them, that's totally fine, because you will learn them here!

- **Union operator**, returns a new set that contains all the elements between two or more sets:

> $$
>  A \cup B \cup C \cup \dots = \{ \text{set of all elements in A or in B or in C or ...} \} \tag{2}
> $$
> 
> For example, if $$A = \{\text{apple}, \text{carrot} \}$$ and $$B = \{ \text{banana}, \text{apple} \}$$, then $$A\cup B$$ is $$\{ \text{apple}, \text{carrot}, \text{banana} \}$$. 
> Just keep in mind that there is not duplicate elements in sets.

- **Intersection operator**, returns a new set that contains all the elements that are present in EVERY single set:

> $$
>  A \cap B \cap C \cap \dots = \{ \text{set of all elements in A and in B and in C and ...} \} \tag{3}
> $$
> 
> For example, if $$A = \{\text{apple}, \text{carrot} \}$$ and $$B = \{ \text{banana}, \text{apple} \}$$, then $$A\cap B$$ is $$\{ \text{apple} \}$$.

- **Complement operator**, returns a new set that contains every element that does not belong to a set, but belongs to the universal set:

> $$
>  A^c = \{ \text{set of all elements that are not in A and are in } \Omega \} \tag{4}
> $$
> 
> For example, if $$A = \{\text{apple}, \text{carrot} \}$$ and $$\Omega = \{ \text{apple}, \text{carrot}, \text{banana} \}$$, then $$A^c$$ is $$\{ \text{banana} \}$$.

Two or more sets are said to be **disjoint** if their intersection is empty. 

A collection of sets is said to be a **partition** of a set $$P$$ if the sets in the collection are disjoin and their union is $$P$$.


**De Morgan's laws** have given two useful properties which is widely used in sets Algebra:

$$
    \begin{align*}
    \left(\bigcup_n S_n\right)^c = \bigcap_n S_n^c, && 
    \left(\bigcap_n S_n\right)^c = \bigcup_n S_n^c.
    \end{align*} \tag{5}
$$

## 1.3 Probabilistic Models

## 1.4 Conditional Probability

## 1.5 Total Probability Theorem and Bayes' Rule

## 1.6 Independence

## 1.7 Counting

## Summary

Hello [^footnote]
## References
[^footnote]: <a href="https://www.youtube.com/watch?v=i3AkTO9HLXo" target="_blank">Normalized Nerd Youtube Playlist</a>
