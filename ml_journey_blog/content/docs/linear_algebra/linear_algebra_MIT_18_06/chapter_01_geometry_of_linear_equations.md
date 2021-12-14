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

- The fundamental problem of linear algebra is to **solve a system of linear equations**

### Linear Equations

- Linear equations, as the name suggests, are equations of a line

    - They are of the form $a_1x_1 + a_2x_2 + a_3x_3 + ... + a_nx_n = b$

    - Here $x_1, x_2, ..., x_n$ are called variables, $a_1, a_2, ..., a_n$ are called coefficients of variables and $b$ is the constant term

    - Eg. of an equation with $2$ variables is $x_1 + 3x_2 = 5$

        - $a_1 = 1$, $a_2 = 3$, $b = 5$

- A linear equation has infinitely many solutions as we can find infinitely many combinations of $x_1, x_2, ..., x_n$ that satisfy the equation for the given values of $a_1, a_2, ..., a_n, b$

### System of Linear Equations

- Multiple linear equations with the same variables make up a system of linear equations

- A system of $m$ equations in $n$ variables can be written as

<div>
\[
    a_{11}x_{1} + a_{12}x_{2} + ... + a_{1n}x_{n} = b_{1} \\
    a_{21}x_{1} + a_{22}x_{2} + ... + a_{2n}x_{n} = b_{2} \\
    \vdots \\
    a_{m1}x_{1} + a_{m2}x_{2} + ... + a_{mn}x_{n} = b_{m}
\]
</div>

- A solution of the system of linear equations is of the form $(s_1, s_2, ..., s_n)$ of values for $x_{1}, x_{2}, ..., x_{n}$ that simultaneously satisfies all equations in the system.

    - A set of all possible solutions is called the solution set

## Distinct Representations

- A system of linear equations can be represented (and geometrically interpreted) in different ways

### Matrix Representation (Linear Algebra)

- A system of $m$ linear equations with $n$ variables can be represented in the matrix form as $Ax = b$

    - $A$ is an $m \times n$ matrix of coefficients of variables

    - $x$ is a column vector of $n$ dimension of variables

    - $b$ is a column vector of $m$ dimension of constants
    
    <div>
    \[
        \begin{bmatrix}
        a_{11} & a_{12} & ... & a_{1n} \\
        a_{21} & a_{22} & ... & a_{2n} \\
        \vdots & \vdots & & \vdots \\
        \vdots & \vdots & & \vdots \\
        a_{m1} & a_{m2} & ... & a_{mn}
        \end{bmatrix}
        \begin{bmatrix}
        x_{1} \\ x_{2} \\ \vdots \\ x_{n}
        \end{bmatrix} = 
        \begin{bmatrix}
        b_{1} \\ b_{2} \\ \vdots \\ \vdots \\ b_{m}
        \end{bmatrix}
    \]
    </div>

- Eg. $2$ equations and $2$ unknowns
<div>\[
        A = \begin{bmatrix}
        2 & -1\\
        -1 & 2
        \end{bmatrix}
        x = \begin{bmatrix}
        x_{1} \\
        x_{2}
        \end{bmatrix}
        b = \begin{bmatrix}
        0 \\
        3
        \end{bmatrix}
        \]</div>

### Row Representation (Geometrical Representation)

- It is called row representation because from the matrix representation, we can take each row of the coefficient matrix separately and convert into this representation

- Row representation is in the form of geometric lines

- For $2$ equations and $2$ unknowns, taking the previous example

    - $2x_{1} - x_{2} = 0$ and $-x_{1} + 2x_{2} = 3$

    - **Note:** $2x_{1} - x_{2} = 0$ passes through the origin as RHS = 0

### Column Representation (Vector Representation)

- It is called column representation because from the matrix representation, we can take each column of the coefficient matrix separately and convert into this representation

- Column representation views $b$ as a **linear combination** of columns of $A$ in the proportion of the values of $x$

    - In this sense, columns of $A$ are viewed as vectors in $m$ dimensional space

- Taking the same example

<div>
\[
    x_{1} * \begin{bmatrix}
    2 \\
    -1
    \end{bmatrix} + x_{2} * \begin{bmatrix}
    -1 \\
    2
    \end{bmatrix} = \begin{bmatrix}
    0 \\
    3
    \end{bmatrix}
\]
</div>

### Addendum

- **Side:** What do all possible linear combinations of columns of A give?

- **Side:** Can we solve $Ax = b$ for all $b$ (do linear combinations of columns fill dimensions of $b$)?

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
        -3 \\
        6
        \end{bmatrix}
        \]</div>

    - Column representation:
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
    
    - Row representation:
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