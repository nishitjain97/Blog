---
title: 5. Transposes, Permutations, Spaces $R^n$
description: Special kinds of matrices and their properties
toc: true
authors:
tags:
categories:
series:
date: '2021-03-01'
lastmod: '2021-03-02'
---

## Permutations

- They are used to execute row exchanges

    - This is done when we get 0 in pivot positions

    - We might require to do this multiple times

- For any invertible, square matrix, $A = LU$ will then become $PA = LU$ 

## Transposes

- This operation is valid for all matrices (square and rectangular)

    - $(A_{i, j})^{T} = A_{j, i}$

- Symmetric matrices

    - Special kind of matrix for which $(A_{i, j}^{T} = A_{i, j}) \equiv A^{T} = A$

    - For rectangular matrices $R$, $R^TR$ is always symmetric

        - To prove, take transpose of $R^TR$

        - $(R^TR)^T = R^TR$

## Vector Spaces

- A collection of vectors that is closed under linear combination makes a vector space. This entails

    - Addition of two vectors in the collection should result in a vector that is part of the same collection

    - Multiplication of a scalar to any vector in the collection should give another vector in that collection

- E.g. $R^2$ is a space of all two-dimensional vectors of real numbers

- E.g. $R^3$ is a space of all three-dimensional vectors of real numbers

- $0$ vector is present in all vector spaces

### Vector Subspace

- A subspace is a vector space within another vector space
    
    - E.g. A line in $R^2$ passing through origin is a subspace of $R^2$

    - **Note:** A line in $R^2$ is different from $R^1$ even though they are both lines. $R^1$ is a space of vectors having 1 component, while a line in $R^2$ is a space of vectors having 2 components

- Subspaces of $R^2$

    - all of $R^2$

    - any line through 
    <div>
    \[
        \begin{bmatrix} 
        0 \\ 0 
        \end{bmatrix}
    \]
    </div>

    - zero vector by itself

- Subspaces of $R^3$

    - all of $R^3$

    - any plane through 
    <div>
    \[
        \begin{bmatrix} 
        0 \\ 0 \\ 0
        \end{bmatrix}
    \]

    - any line through 
    <div>
    \[
        \begin{bmatrix} 
        0 \\ 0 \\ 0
        \end{bmatrix}
    \]
    </div>

    - zero vector by itself

### Subspaces from Matrices

- We can derive important subspaces from a matrix

#### Column Space

- We take the columns of a matrix and all their linear combinations to get the **column space**, $C(A)$

    - E.g. the following matrix has a column space that lies in $R^3$ and is made up of the columns of this matrix and all their linear combinations 
    <div>
    \[
        \begin{bmatrix}
        1 & 3 \\
        2 & 3 \\
        4 & 1
        \end{bmatrix}
    \]
    </div>

    - **Note:** For this example, the $C(A)$ would be a plane in 3-D space