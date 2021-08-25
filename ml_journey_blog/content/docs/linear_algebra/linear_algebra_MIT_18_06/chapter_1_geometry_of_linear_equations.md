---
title: 1. Geometry of Linear Equations
description: Introducing the geometry of linear equations used in linear algebra
toc: true
authors:
tags:
categories:
series:
date: '2021-03-01'
lastmod: '2021-03-02'
---

## Introduction

- Fundamental problem of linear algebra: Solve a system of linear equations

- Let's begin with a simple case of $n$ equations and $n$ unknowns

- Eg. $2$ equations and $2$ unknowns

    - Type 1: Linear Algebra, which views it in the form of matrices
    <div>\[
        A = \begin{bmatrix}
        2 & -1\\
        -1 & 2
        \end{bmatrix}
        X = \begin{bmatrix}
        x \\
        y
        \end{bmatrix}
        B = \begin{bmatrix}
        0 \\
        3
        \end{bmatrix}
        \]</div>

    
    - Type 2: Row picture:

        - $2x - y =  0$ and $-x + 2y = 3$

        - Each row is represented in the form of a line

        - **Note:** $2x - y = 0$ passes through the origin as RHS = 0

    - Type 3: Column Picture:
        - <div>\[
            x * \begin{bmatrix}
            2 \\
            -1
            \end{bmatrix} + y * \begin{bmatrix}
            -1 \\
            2
            \end{bmatrix} = \begin{bmatrix}
            0 \\
            3
            \end{bmatrix}
            \]</div>
            
        - $B$ is a **linear combination** of columns of $A$

        - Columns of $A$ are viewed as vectors in $2$ dimensional space

- **Side:** What do all possible linear combinations of columns of A give?

- **Side:** Can we solve $AX = b$ for all $b$ (do linear combinations of columns fill dimensions of $b$)?

- **Note:** If columns lie in the same lower dimension, then any $b$ outside that object would be unsolvable

## Matrix Multiplication

- The different ways to visualize systems of linear equations also help understand matrix multiplication

- Eg. 
    <div>\[
        \begin{bmatrix}
        2 & -1\\
        -1 & 2
        \end{bmatrix}
        \begin{bmatrix}
        0 \\
        3
        \end{bmatrix} = 
        \begin{bmatrix}
        x \\
        y
        \end{bmatrix}
        \]</div>

    - Column Picture:
        - <div>\[
            0 * \begin{bmatrix}
            2 \\
            -1
            \end{bmatrix} + 3 * \begin{bmatrix}
            -1 \\
            2
            \end{bmatrix} = \begin{bmatrix}
            -3 \\
            6
            \end{bmatrix}
            \]</div>

        - Combination of columns of $A$
    
    - Row picture:
        - <div>\[
            \begin{bmatrix}
            2 & -1
            \end{bmatrix}
            \begin{bmatrix}
            0 \\
            3
            \end{bmatrix} + 
            \begin{bmatrix}
            -1 & 2
            \end{bmatrix}
            \begin{bmatrix}
            0 \\
            3
            \end{bmatrix} = \begin{bmatrix}
            -3 \\
            6
            \end{bmatrix}
            \]</div>

        - Sum of dot product of rows of $A$