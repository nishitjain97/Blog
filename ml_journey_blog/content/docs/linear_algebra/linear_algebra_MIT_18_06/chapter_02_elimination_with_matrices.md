---
title: 2. Elimination with Matrices
description: Using elimination of matrices to solve system of linear equations
toc: true
authors:
tags:
categories:
series:
date: '2021-03-01'
lastmod: '2021-03-02'
---

## Introduction

- Elimination of matrices is how most programming softwares solve systems of linear equations

- It was given by Gauss and is an intuitive solution

- There are also some cases where this fails

## Elimination Approach

- Eg.
<div>
\[
x + 2y + z = 2 \\
3x + 8y + z = 12 \\
4y + z = 2
\]
</div>

<div>
\[
    A = \begin{bmatrix}
    1 & 2 & 1 \\
    3 & 8 & 1 \\
    0 & 4 & 1
    \end{bmatrix}
\]
</div>

<div>
\[
    B = \begin{bmatrix}
    2 \\
    12 \\
    2
    \end{bmatrix}
\]
</div>

- Steps of algorithm

    1. Select first coefficient of first row as **pivot element**, then first row becomes **pivot row**

        - We are selecting the coefficient of $x$ in the first row and will use that value to eliminate $x$ from all other rows

        - &nbsp;
        <div>
        \[
            A = \begin{bmatrix}
            (1) & 2 & 1 \\
            3 & 8 & 1 \\
            0 & 4 & 1
            \end{bmatrix}
        \]
        </div>

    2. Eliminate coefficient of $x$ from all other rows **below the pivot row** by adding scalar multiples of row 1 such that coefficient of $x$ in other rows becomes $0$

        - $R2 = R2 - 3 * R1$

        - &nbsp; 
        <div>
        \[
            A = \begin{bmatrix}
            (1) & 2 & 1 \\
            0 & 2 & -2 \\
            0 & 4 & 1
            \end{bmatrix}
        \]
        </div>

    3. Select the second pivot element and eliminate coefficients from all rows **below the pivot row**

        - $R3 = R3 - 2 * R2$

        - &nbsp; 
        <div>
        \[
            \begin{bmatrix}
            (1) & 2 & 1 \\
            0 & (2) & -2 \\
            0 & 0 & 5
            \end{bmatrix}
        \]
        </div>

    4. Select the third pivot element

        - &nbsp; 
        <div>
        \[
            U = \begin{bmatrix}
            (1) & 2 & 1 \\
            0 & (2) & -2 \\
            0 & 0 & (5)
            \end{bmatrix}
        \]
        </div>

        - $U$ represents upper triangular matrix

    5. Same set of steps are followed for $B$ as well, to get vector $C$

        - $B$ can be latched on with $A$ in the form of an augmented matrix $\begin{bmatrix}A | B \end{bmatrix}$ to get to $\begin{bmatrix}U | C \end{bmatrix}$

        - &nbsp; 
        <div>
        \[
            C = \begin{bmatrix}
            2 \\
            6 \\
            -10
            \end{bmatrix}
        \]
        </div>

    6. Back-substitution will be done to solve $UX = C$

     - &nbsp; 
     <div>
     \[
         \text{Row 3: } 5z = -10 \implies z = -2 \\
         \text{Row 2: }2y - 2z = 6 \implies y = 1 \\
         \text{Row 1: }x + 2y + z = 2 \implies x = 2
     \]
     </div>

     - Solving system in reverse order as system is triangular

- **Note:** We do not use $0$ pivot. If $0$ comes on the pivot position, we exchange the row with one of the rows below and continue with the process

- **Note:** In case we are not able to get any non-zero pivot even with row exchange, it implies that the matrix is non-invertible

## Matrix Multiplication

- Let there be a matrix $A$, a column vector $C$ and a row vector $R$ (with appropriate shapes for matrix multiplication)

- $A * C$ gives a column vector

    - We are taking sum of columns of $A$ in the proportion of scalars in $C$ to get a column vector

- $R * A$ gives a row vector

    - We are taking sum of rows of $A$ in the proportion of scalars in $R$ to get a row vector

- **Note:** We need to keep an eye on what matrix multiplication does to vectors

## Elimination Matrices

- These are a form of elementary matrices that help us perform row / column operations on a matrix

- These can be used for elimination step of Gauss' method of solving linear equations

- Looking at the same example above

    1. Select first coefficient of first row as **pivot element**, then first row becomes **pivot row**

        - We are selecting the coefficient of $x$ in the first row and will use that value to eliminate $x$ from all other rows

        - &nbsp; 
        <div>
        \[
            A = \begin{bmatrix}
            (1) & 2 & 1 \\
            3 & 8 & 1 \\
            0 & 4 & 1
            \end{bmatrix}
        \]
        </div>

    2. Eliminate coefficient of $x$ from all other rows **below the pivot row** by adding scalar multiples of row 1 such that coefficient of $x$ of other rows becomes $0$

        - Here, we can write the step $R2 = R2 - 3 * R1$ in the form of an elimination matrix as

        - &nbsp; 
        <div>
        \[
            E_{2, 1} = \begin{bmatrix}
            1 & 0 & 0 \\
            -3 & 1 & 0 \\
            0 & 0 & 1
            \end{bmatrix}
        \]
        </div>

        - $E_{2, 1}$ can be understood as:

            - The subscript $\\{2, 1\\}$ implies we are fixing pivot at position $\(2, 1\)$ 
            - First row => 1 * $A_{1, :}$ + 0 * $A_{2, :}$ + 0 * $A_{3, :}$

                - This can be read as: take $1$ times Row 1 of $A$, add $0$ times Row 2 of $A$ and then add $0$ times Row 3 of $A$
            
                - $A_{k, :}$ implies taking the $k$th row of $A$ 
                
                - To take the $k$th column, we will use $A_{:, k}$

            - Second row => -3 * $A_{1, :}$ + 1 * $A_{2, :}$ + 0 * $A_{3, :}$

                - This can be read as: tak $-3$ times Row 1 of $A$, add $1$ times Row 2 of $A$ and then add $0$ times Row 3 of $A$

            - Third row => 0 * $A_{1, :}$ + 0 * $A_{2, :}$ + 1 * $A_{3, :}$

    3. Select the second pivot element and eliminate coefficients from all rows **below the pivot row**

        - Similarly, $R3 = R3 - 2 * R2$ can be represented as

        - &nbsp; 
        <div>
        \[
            E_{3, 3} = \begin{bmatrix}
            1 & 0 & 0 \\
            0 & 1 & 0 \\
            0 & -2 & 1
            \end{bmatrix}
        \]
        </div>

        - $E_{3, 3}$ can be understood as:

            - The subscript $\\{3, 3\\}$ implies we are fixing pivot at position $\(3, 3\)$ 
            - First row => 1 * $A_{1, :}$ + 0 * $A_{2, :}$ + 0 * $A_{3, :}$
            - Second row => 0 * $A_{1, :}$ + 1 * $A_{2, :}$ + 0 * $A_{3, :}$
            - Third row => 0 * $A_{1, :}$ + -2 * $A_{2, :}$ + 1 * $A_{3, :}$

        - &nbsp; 
        <div>
        \[
            \begin{bmatrix}
            (1) & 2 & 1 \\
            0 & (2) & -2 \\
            0 & 0 & 5
            \end{bmatrix}
        \]
        </div>

    4. Select the third pivot element

        - &nbsp; 
        <div>
        \[
            U = \begin{bmatrix}
            (1) & 2 & 1 \\
            0 & (2) & -2 \\
            0 & 0 & (5)
            \end{bmatrix}
        \]
        </div>

        - $U$ represents upper triangular matrix

- We can go from $A$ to $U$ in one shot using a single matrix as follows:

    - $E_{3, 3}(E_{2, 1}A) = U \\ \implies (E_{3, 3}E_{2, 1})A = U $

- There's another type of elementary matrix, called permutation matrix, used to exchange rows or columns

    - These can be formed by doing the target operation on an identity matrix

    - Eg. to exchange row 1 and row 2 of a $2 \times 2$ matrix, exchange row 1 and row 2 of identity matrix to get the required permutation matrix
    <div>
    \[
        \begin{bmatrix} 
        0 & 1 \\ 
        1 & 0 
        \end{bmatrix}
    \]
    </div>

    - For column exchange, we use the same permutation matrix but multiply it on the right side of the matrix

- **Note:** $AB \neq BA$ for matrices

## Inverses

- With these matrices, we are looking to reverse the operations that we did with elimination / elementary matrices

- $E^{-1}E = I$