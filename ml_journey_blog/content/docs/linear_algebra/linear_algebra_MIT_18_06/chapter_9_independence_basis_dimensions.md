---
title: 9. Independence, Basis, and Dimension
description: Matrix related concepts
toc: true
authors:
tags:
categories:
series:
date: '2021-03-01'
lastmod: '2021-03-02'
---

## Prerequisites

- For a matrix $m \times n$ with $m \lt n$

    - There are more unknowns than equations

    - There are non-zero solutions to $Ax = 0$, since we will have free variables once we perform elimination

## Independence

- Vectors $x_1, x_2, ..., x_n$ are independent if no combination of these vectors gives 0 (except the 0 combination)

    - This means $c_1x_1 + c_2x_2 + ... + c_nx_n \neq 0$ , $\forall$ $c_1, c_2, ... , c_n \neq 0$

- If we consider vectors $v_1, v_2, ..., v_n$ as columns of matrix $A$

    - They are independent if the nullspace of $A$ is zero vector, making the rank of $A$, $r = n$

    - They are dependent if the nullspace of $A$ is some non-zero vector(s), making the rank of $A$, $r < n$

## Span

- For vectors $v_1, v_2, ..., v_l$ to span a space means that the space consists of all combinations of those vectors

- The columns of a matrix span the column space

- Span: Take all linear combination and put them in a space

## Basis

- Basis for a space is a sequence of vectors $v_1, v_2, ..., v_d$ with 2 properties

    - They are independent

    - They span the space

- Examples

    - Space is $R^3$

        - One basis is

        <div>
        \[
            \begin{bmatrix}
            1 \\ 0 \\ 0
            \end{bmatrix},
            \begin{bmatrix}
            0 \\ 1 \\ 0
            \end{bmatrix},
            \begin{bmatrix}
            0 \\ 0 \\ 1
            \end{bmatrix}
        \]
        </div>

        - Another basis is

        <div>
        \[
            \begin{bmatrix}
            1 \\ 1 \\ 2
            \end{bmatrix},
            \begin{bmatrix}
            2 \\ 2 \\ 5
            \end{bmatrix},
            \begin{bmatrix}
            3 \\ 4 \\ 5
            \end{bmatrix}
        \]
        </div>

        - However, if we had only two vectors, it would not be a basis for $R^3$ as they would span a 2D subspace in $R^3$

        <div>
        \[
            \begin{bmatrix}
            1 \\ 1 \\ 2
            \end{bmatrix},
            \begin{bmatrix}
            2 \\ 2 \\ 5
            \end{bmatrix}  
        \]
        </div>

## Dimension

- Given a space, every basis for this space has the same number of vectors. This number is the **dimension** for that space.

    - Eg. for $R^3$, every basis would have $3$ vectors

    - Eg. for $R^n$, every basis would have $n$ vectors

- For a matrix $A$, dimension of column space $C(A)$ = number of pivot columns = $rank(A)$

    - **Note:** Matrix has rank, space has dimension

- Dimension of nullspace $N(A)$ = number of free variables = $n - r$