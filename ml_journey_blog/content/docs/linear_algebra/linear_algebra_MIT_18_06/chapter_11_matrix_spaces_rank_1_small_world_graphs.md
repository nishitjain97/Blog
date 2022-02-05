---
title: 11. Matrix Spaces, Rank 1 and Small World Graphs
description: Matrix Spaces, Rank 1 and Small World Graphs
toc: true
authors:
tags:
categories:
series:
date: '2021-03-01'
lastmod: '2021-03-02'
---

## Prerequisites

- Matrices can be considered like vectors to give matrix spaces

    - They can be added, $A + B$, and can be multiplied by scalars, $cA$

## Matrix Spaces

- All $3 \times 3$ matrices form a matrix space $M$

    - It is a $9$ dimensional space, i.e., there are $9$ matrices in the basis for $M$

- Symmetric $3 \times 3$ is a subspace, $S$, for $M$

    - It is a $6$ dimensional space, i.e., there are $6$ matrices in the basis for $S$

- Upper triangular $3 \times 3$ is a subspace, $U$, for $M$

    - It is a $6$ dimensional space, i.e., there are $6$ matrices in the basis for $U$

- Intersection, $S \cap U$ gives diagonal matrices

    - Dimension is $3$

- Sum, $S + U$ = any element in $S$ + any element in $U$ = all $3 \times 3$ matrices

    - Dimension is $9$

- Dim($S$) + Dim($U$) = Dim($S + U$) + Dim($S \cap U$) 

## Other Alternate Spaces

- Solving a differential equation such as

    - &nbsp; 
    <div>
    \[
        \frac{d^2y}{dx^2} + y = 0
    \]
    </div>

    - We get, $y = cos(x)$ and $y = sin(x)$

    - Complete solution is, $y = c_1cos(x) + c_2sin(x)$

- Even though the solutions are functions, we can consider them as vectors as they can be added and multiplied with scalars

- Hence, these solutions become the basis make up the solution space

    - The dimension of solution space in this example is $2$

## Rank 1 Matrix

- Rank 1 matrices are made by multiplying one column vector with a row vector

    - $A = uv^T$

- E.g.

    - &nbsp; 
    
    <div>
    \[
        \begin{bmatrix}
        1 & 4 & 5 \\
        2 & 8 & 10
        \end{bmatrix}
    \]
    </div>

    - This is a rank 1 matrix with the first row as a basis

    - This can be written as a multiplication of one column and one row vector as follows

    <div>
    \[
        \begin{bmatrix}
        1 \\ 2
        \end{bmatrix}
        \begin{bmatrix}
        2 & 5
        \end{bmatrix}
    \]
    </div>

- E.g. if we take all $5 \times 17$ matrices, the subset of all rank 1 matrices would not be a subspace

    - This is because when we add two rank 1 matrices that are $5 \times 17$, it is likely that the sum would have a rank greater than 1

## Graph

- Made of nodes and edges

- Social network connections or web connections are important for a lot of analyses

    - They require understanding of graphs