---
title: Understanding Graph Attention Networks (GATs)
date: 2024-08-03 15:20:00 -0500
categories: [Understanding Papers, Deep Learning]
tags: [binary function similarity]     # TAG names should always be lowercase
image: /assets/img/posts/gat/cover.png
alt: "How Machine Learning Is Solving the Binary Function Similarity Problem?"
math: true
---

Recently, I started to read a paper[^footnote] which introduces the concept of Graph Attention Networks (GATs). However, I found it hard to understand; therefore, I decided to look for the basic concepts that I need to know before fully comprehending this paper. In this post, I will introduce these prerequisites to you, so if you want to read this paper, it will be much easier for you.

## Background

This research is part of a broader area called **geometric deep learning**, which focuses on extending deep learning methods to non-Euclidean domains, such as graphs. Geometric deep learning includes techniques like graph convolutional networks (GNNs), and more, aiming to capture the complex structures inherent in these domains.

### Graphs and Their Properties

**Graphs** are mathematical structures used to model pairwise relations between objects. They consist of nodes (vertices) and edges connecting them. Understanding graphs is crucial as GATs operate on graph data, leveraging their unique properties.

#### Undirected Graphs

The GAT paper focuses on **undirected graphs**, where edges have no direction. However, the method can also be applied to other types of graphs, such as directed graphs.

<img src="/assets/img/posts/gat/undirected-graph.png" alt="An undirected graph" style="margin: auto" width="40%"/>

#### Feature Vectors

Each node in the graph has a **feature vector** associated with it, which represents the characteristics of the node. For example, if each node represents an state, then one of the features in the feature vector can be number of the cars in that state. Similarly, edges can also have feature vectors that capture the relationship between nodes. For example, a feature for edge can be the roads between states.

#### Adjacency Matrix

An **adjacency matrix** is an $N*N$ matrix (where $N = \|V\|$ is equal to number of nodes or vertices) that describes the connection pattern of the graph. It is a fundamental structure used to represent graphs in mathematical terms. The adjacency matrix for the undirected graph that we saw looks like this:

$$
A = \begin{bmatrix}
0 & 1 & 1 & 1 \\
1 & 0 & 1 & 0 \\
1 & 0 & 1 & 0 \\
1 & 0 & 0 & 0 \\
\end{bmatrix}
$$

Here we assumed that the weight of edges is 1 for all of the edges. However, edges can have different values in different graphs.

### Spectral Methods and Graph Fourier Transform

**Spectral methods** study graphs using the eigenvectors and eigenvalues of matrices related to a graph, such as the graph adjacency matrix and Laplacian matrix. These methods provide insights into the graph's connectivity, clustering, and other properties.

#### Graph Laplacian

The **Graph Laplacian** is a crucial element for graph signal processing. It lays the foundation for the frequency domain analysis of graph signals. The graph Laplacian \( L \) can be defined as:

$$
L = D - W 
$$

where \( W \) is the weights matrix (weights for edges), and \( D \) is the degree matrix of the graph. Based on the eigenvalues and eigenvectors of the graph Laplacian, we define a special Fourier transform for graphs called the **graph Fourier transform**.

#### Graph Fourier Transform

The **Graph Fourier Transform** is the graph version of the traditional Fourier transform. It allows us to analyze signals on a graph by transforming them into the frequency domain, enabling the study of graph signal properties.

#### Signal on a Graph

The **signal on a graph** refers to applying signal processing techniques to graph structures. Unlike traditional signals (e.g., AC signals), graph signals lack an inherent ordering along an axis. For example, a graph signal might indicate the number of cars in each city of a state:

$$
g(i): V \rightarrow \mathbb{R}
$$

### Key Concepts

#### Representation Learning

This work has two parts: 

1. **Representation Learning**: Learning embeddings or representations of graph nodes that capture their structural and feature information.
2. **Applications**: Using these representations for tasks like classification, regression, or clustering.

#### Attention Mechanism

An **attention mechanism** allows models to focus on specific parts of the input data, enabling them to weigh the importance of different features. In tasks like machine translation, the attention mechanism helps by considering all encoder hidden states and assigning weights to each, improving performance over traditional RNN encoder-decoder models.

#### Multi-Head Attention Mechanism

The **multi-head attention mechanism** extends the attention mechanism by allowing the model to jointly attend to information from different representation subspaces at different positions. This improves the model's ability to capture complex relationships within the data.

#### Inductive vs. Transductive Learning

- **Inductive Learning**: Generalizes from observed training data to unseen test data, creating a model applicable to new, unseen examples.
- **Transductive Learning**: Focuses on reasoning from specific training cases to specific test cases, without generalizing to unseen data.

#### Receptive Field

In neural networks, the **receptive field** is the area of the input image that directly influences the output of a neuron in a specific layer of the network. It determines how much of the input the network uses to make a prediction.

#### LeakyReLU

**LeakyReLU** is a type of activation function used in neural networks. It is similar to the ReLU function but allows a small, non-zero gradient when the input is negative, preventing the problem of dying neurons. [^leaky]

$$
\text{LeakyReLU}(x) = \begin{cases} 
x, & \text{if } x \geq 0 \\
\text{negative_slope} \times x, & \text{otherwise}
\end{cases}
$$

### Evaluation Metrics

The paper uses citation datasets for evaluation, applying various metrics to assess performance.

#### Micro-Averaged F1 Score

The **micro-averaged F1 score** is a metric that calculates the F1 score globally by considering the sum of all true positives, false negatives, and false positives across all classes. It is particularly useful when the class distribution is imbalanced.

### Visualization Techniques

#### t-SNE Plot

**t-SNE** (t-distributed Stochastic Neighbor Embedding) is a technique for visualizing high-dimensional data. It reduces the dimensions of the data while preserving its structure, making it easier to visualize complex relationships.

## Conclusion

Understanding the concepts outlined in this post will significantly enhance your ability to comprehend the Graph Attention Networks paper. By familiarizing yourself with graph theory, spectral methods, attention mechanisms, and evaluation metrics, you will be well-prepared to tackle the complexities of GATs and their applications.

## Read More
[^footnote]: <a href="https://arxiv.org/abs/1710.10903" target="_blank">Graph Attention Networks</a>
[^leaky]: <a href="https://pytorch.org/docs/stable/generated/torch.nn.LeakyReLU.html" target="_blank">LeakyReLU</a>