---
title: 4. Factorization into A = LU
description: Factorizing matrix into key components based on properties of matrix
toc: true
authors:
tags:
categories:
series:
date: '2021-03-01'
lastmod: '2021-03-02'
---

## Prerequisites

- Inverse matrices satisfy $AA^{-1} = I = A^{-1}A$

    - $(AB)(B^{-1}A^{-1}) = I = (B^{-1}A^{-1})(AB)$

- Transpose and inversion can be done in any order

    - $AA^{-1} = I \implies (AA^{-1})^T = I \implies (A^{-1})^TA^T = I$

    - This gives us $(A^{-1})^T = (A^T)^{-1}$

## A = LU

- This is the most basic factorization of a matrix

- Using elimination, we go from $A \rightarrow U$

    - The identity $A = LU$ tells us how this $A$ is related to the final $U$

- Eg. $E_{2, 1}A = U$ as follows

    - 
    <div>
    \[
        E_{2, 1} \;\;\;\;\;\;\;\; A \;\;\;\;  \;\;\;\;\;\;\;\; U\\
        \begin{bmatrix}
        1 & 0 \\ 
        -4 & 1
        \end{bmatrix}
        \begin{bmatrix}
        2 & 1 \\
        8 & 7
        \end{bmatrix} = 
        \begin{bmatrix}
        2 & 1 \\
        0 & 3
        \end{bmatrix}
    \]
    </div>

    - Then, from $A = LU$ and $A = E^{-1}U \implies L = E^{-1}$
    <div>
    \[
        A \;\;\;\;\;\;\;\;\;\;\;\; L \;\;\;\;\;\;\;\;\; U\\
        \begin{bmatrix}
        2 & 1 \\
        8 & 7
        \end{bmatrix} = 
        \begin{bmatrix}
        1 & 0 \\ 
        4 & 1
        \end{bmatrix}
        \begin{bmatrix}
        2 & 1 \\
        0 & 3
        \end{bmatrix}
    \]
    </div>

    - Here, $U$ is an upper triangular matrix and $L$ is a lower triangular matrix

- For bigger matrices, e.g., $E_{3, 2}E_{3, 1}E_{2, 1}A = U$, then <br>$A = (E_{2, 1})^{-1}(E_{3, 1})^{-1}(E_{3, 2})^{-1}U  \implies L = (E_{2, 1})^{-1}(E_{3, 1})^{-1}(E_{3, 2})^{-1}$

## Why A = LU over EA = U?

- When performing Gauss elimination, the elimination matrices are made up of multipliers that are used to subtract one row from another

    - In the previous example, the elimination matrix would become $E = E_{3, 2}E_{3, 1}E_{2, 1}$

    - This subsequent matrix multiplication of multiple matrices can result in $E$ having coefficients that result from interaction of the different rows

    - E.g. $E_{3, 2}E_{2, 1} = E$
    <div>
    \[
        \begin{bmatrix}
        1 & 0 & 0 \\
        0 & 1 & 0 \\
        0 & -5 & 1
        \end{bmatrix}
        \begin{bmatrix}
        1 & 0 & 0 \\
        -2 & 1 & 0 \\
        0 & 0 & 1
        \end{bmatrix} =
        \begin{bmatrix}
        1 & 0 & 0 \\
        -2 & 1 & 0 \\
        (10) & -5 & 1
        \end{bmatrix}
    \]
    </div>

    - The highlighted $10$ is extra above and is due to the interaction of the two transformations.

- However, when we take $L = E^{-1}$, we do not get these interaction effects. $L$ is a relatively simple matrix

    - E.g. $L = E_{2, 1}^{-1}E_{3, 2}^{-1}$
    <div>
    \[
        \begin{bmatrix}
        1 & 0 & 0 \\
        2 & 1 & 0 \\
        0 & 0 & 1
        \end{bmatrix}
        \begin{bmatrix}
        1 & 0 & 0 \\
        0 & 1 & 0 \\
        0 & 5 & 1
        \end{bmatrix} =
        \begin{bmatrix}
        1 & 0 & 0 \\
        2 & 1 & 0 \\
        0 & 5 & 1
        \end{bmatrix}  
    \]
    </div>

    - Hence, the required multipliers directly sit in $L$ without any additional effects

- **Note:** This property holds only when there are no row exchanges

## Expense of Elimination Process

- The cost of performing elimination for an $n \times n$ matrix

    - $T(n) = n^2 + T(n-1)$

    - $T(n) = \frac{n * (n + 1) * (2n + 1)}{6} \approx \frac{n^3}{3}$

## Permutations

- For $n \times n$ matrices, there are n! permutation matrices

- Two exchange any two rows, take the identity matrix and exchange those rows of the identity matrix to get the required permutation matrix

- The inverse of permutation matrix is its transpose

    - $P^{-1} = P^{T}$