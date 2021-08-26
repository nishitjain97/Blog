---
title: 3. Multiplication and Inverse Matrices
description: Matrix multiplication and its implications on matrix inversion
toc: true
authors:
tags:
categories:
series:
date: '2021-03-01'
lastmod: '2021-03-02'
---

## Methods of Matrix Multiplication

- Two matrices $A$ (m X n) and $B$ (p X r) can be multiplied to give matrix $C$ iff the number of columns of $A$ match the number of rows of $B$ (n = p)

    - $C$ will have the shape (m X r)

### Method 1: Multiplication by elements

- $C_{i, j}$ comes from dot product of row $i$ of $A$ and column $j$ of $B$

- $C_{i, j} = \sum_{k = 1}^{n}A_{i, k}B_{k, j}$

### Method 2: Column-wise multiplication

- Columns of $C$ are combinations of columns of $A$ in the proportion of a column of $B$

- $C_{:, j}$ comes from multiplying $A$ with $B_{:, j}$

### Method 3: Row-wise multiplication

- Rows of $C$ are combination of rows of $B$ in the proportion of a row of $A$

- $C_{i, :}$ comes from multiplying $A_{i, :}$ with $B$.

### Method 4: Outer product of matrices

- A column vector multiplied with a row vector gives a full matrix

- $A_{:, j}$ multiplied by $B_{i, :}$ gives a matrix. The sum of all such matrices gives $C$

### Method 5: Block multiplication

- Divide $A$ and $B$ into sub-matrices (blocks) of appropriate sizes

- Then applying element-wise multiplication on block level

## Inverses (Square Matrices)

- Not all square matrices would have inverses

- For a square matrix $A$, if inverse exists, then $A^{-1}A = I = AA^{-1}$

    - This implies that the left-inverse and right-inverse is equal

    - These matrices are called invertible or non-singular

- Matrices with no inverse are called singular matrices. This can be explained in several ways

    - Determinant of this matrix is 0, so inversion will have a 0 in denominator

    - When a matrix is multiplied by its inverse, it gives the identity matrix. 
    
        - For singular matrices, there are columns / rows which are multiples of one another, which means they lie on the same line. 
        
        - If they lie on the same line, their multiplication would never give the identity matrix.

    - There won't be an inverse because we can find a non-zero vector $X$ such that $AX = 0$.

        - $A^{-1}AX = 0$

        - $IX = 0$

        - However, $X \neq 0$, which is contradictory to the original assumption

- Inverting square matrix of size n X n is equivalent to simultaneously solving $n$ systems of $n$ linear equations. 

    - Eg. $AA^{-1} = I$
    <div>
    \[
        \begin{bmatrix}
        1 & 3 \\
        2 & 7
        \end{bmatrix}
        \begin{bmatrix}
        a & b \\
        c & d
        \end{bmatrix} = \begin{bmatrix}
        1 & 0 \\
        0 & 1
        \end{bmatrix}
    \]
    </div>
    <div>
    \[
        \begin{bmatrix}
        1 & 3 \\
        2 & 7
        \end{bmatrix}
        \begin{bmatrix}
        a \\ c
        \end{bmatrix} = \begin{bmatrix} 1 \\ 0 \end{bmatrix}
        \text{and}
        \begin{bmatrix}
        1 & 3 \\
        2 & 7
        \end{bmatrix}
        \begin{bmatrix}
        b \\ d
        \end{bmatrix} = \begin{bmatrix} 0 \\ 1 \end{bmatrix}
    \]
    </div>

### Gauss Jordan Idea

- Solving multiple systems at once, i.e., using Gauss' idea of augmented matrix, but tagging along right hand sides of all the systems

    - 
    <div>
    \[
        \begin{bmatrix}
        1 & 3 & | & 1 & 0 \\
        2 & 7 & | & 0 & 1
        \end{bmatrix} = \begin{bmatrix}
        A & | & I
        \end{bmatrix}
    \]
    </div>

    - Performing Gauss elimination first downwards to get upper triangular matrix and then upwards to convert $A$ to $I$ will turn augmented $I$ into $A^{-1}$

    - 
    <div>
    \[
        \begin{bmatrix}
        1 & 0 & | & 7 & 3 \\
        0 & 1 & | & -2 & 1
        \end{bmatrix} = \begin{bmatrix}
        I & | & A^{-1}
        \end{bmatrix}
    \]
    </div>

    - This works because, using elimination matrix $E$

        - $E \begin{bmatrix}A & | & I\end{bmatrix} = \begin{bmatrix}I & | & X\end{bmatrix}$

        - $EA = I \implies E = A^{-1}$

        - $\therefore EI = X \implies X = A^{-1}I = A^{-1}$