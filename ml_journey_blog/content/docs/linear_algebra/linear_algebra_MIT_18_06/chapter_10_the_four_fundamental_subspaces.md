---
title: 10. The Four Fundamental Subspaces
description: Subspaces related to a matrix
toc: true
authors:
tags:
categories:
series:
date: '2021-03-01'
lastmod: '2021-03-02'
---

## The Four Spaces

- If $A$ is $m \times n$

### Columns space of $A$, $C(A)$

- Columns of $A$ have $m$ components, hence $C(A)$ is in $R^m$

- Basis of $C(A)$ is made of the pivot columns of $A$

- Dimension when rank is $r$, $dim(C(A)) = r$

### Nullspace of $A$, $N(A)$

- Nullspace is the values of $x$ that satisfy $Ax = 0$

    - $x$ has $n$ components, hence $N(A)$ is in $R^n$

- Basis is the special solutions for $Ax = 0$

    - There is one special solution for each free variable

- Dimension when rank is $r$, $dim(N(A)) = n - r$

### Rowspace of $A$, $C(A^T)$

- Row space = all combinations of rows of $A$ = all combinations of columns of $A^T$, $C(A^T)$

- Columns of $A^T$ have $n$ components, $C(A^T)$ is in $R^n$

- Dimension when rank is $r$, $dim(C(A^T)) = r$

- Row reduction preserves rowspace but changes column space of $A$

    - Basis for rowspace is first $r$ rows of $rref$

### Left nullspace of $A$, $N(A^T)$

- Nullspace of $A^T$ = left nullspace, $N(A^T)$

- Left nullspace is the values of $y$ that satisfy $A^Ty = 0$

    - $y$ has $m$ components, hence $N(A^T)$ is in $R^m$

- Dimension when rank is $r$, $dim(N(A^T)) = m - r$ 

- The basis can be found out by keeping track of the elimination matrix that gives $rref$

    - $EA = R$

    - The row(s) of $E$ that gives the $0$ row(s) in $R$ is the basis of left nullspace

    - E.g. $EA = R$,

    <div>
    \[
        \begin{bmatrix}
        -1 & 2 & 0 \\
        1 & -1 & 0 \\
        \{-1 & 0 & 1\}
        \end{bmatrix}
        \begin{bmatrix}
        1 & 2 & 3 & 1 \\
        1 & 1 & 2 & 1 \\
        1 & 2 & 3 & 1
        \end{bmatrix} = 
        \begin{bmatrix}
        1 & 0 & 1 & 1 \\
        0 & 1 & 1 & 0 \\
        \{0 & 0 & 0 & 0\}
        \end{bmatrix}
    \]
    </div>

## Matrix Space

- Matrix space is a kind of vector space with matrix basis

    - We can form a matrix space since we can add two matrices $A + B$ and multiply matrices with scalars $cA$

- A set of all $3 \times 3$ matrices is a matrix space $M$

- Subspaces of $M$

    - All upper triangular matrices

    - Symmetric matrices

    - Diagonal matrices, dimension is $3$