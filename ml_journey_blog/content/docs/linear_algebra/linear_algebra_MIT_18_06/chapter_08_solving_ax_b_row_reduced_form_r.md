---
title: 8. Solving Ax=b, Row reduced form R
description: Solving a complete system of linear equations (where possible)
toc: true
authors:
tags:
categories:
series:
date: '2021-03-01'
lastmod: '2021-03-02'
---

## Solving Ax = b

- Taking the same matrix as the previous example of finding nullspace

    - We are solving $Ax = b$ which is as follows

    <div>
    \[
        \begin{bmatrix}
        1 & 2 & 2 & 2 \\
        2 & 4 & 6 & 8 \\
        3 & 6 & 8 & 10
        \end{bmatrix}
        \begin{bmatrix}
        x_1 \\ x_2 \\ x_3 \\ x_4
        \end{bmatrix} = 
        \begin{bmatrix}
        b_1 \\ b_2 \\ b_3
        \end{bmatrix}
    \]
    </div>

    - Here, we know values of $A$ and $b$. We need to find $x$ by answering the following questions

        - For the given $b$, is it possible to find some $x$?

        - What is the $x$ that solves $Ax = b$?

        - Is there a family of solutions $x$ that solve $Ax = b$?

    - **Note:** In this case, since we know for $A$, $Row_1 + Row_2 = Row_3$, $b$ will also follow the same relation $b_1 + b_2 = b_3$. Method of elimination should find this relationship

    - Performing method of elimination on the following augmented matrix

    <div>
    \[
        \begin{bmatrix}
        1 & 2 & 2 & 2 & | & b_1 \\
        2 & 4 & 6 & 8 & | & b_2 \\
        3 & 6 & 8 & 10 & | & b_3
        \end{bmatrix} \implies
        \begin{bmatrix}
        1 & 2 & 2 & 2 & | & b_1 \\
        0 & 0 & 2 & 4 & | & b_2 - 2b_1 \\
        0 & 0 & 0 & 0 & | & b_3 - b_2 - b_1
        \end{bmatrix} 
    \]
    </div>

    - Hence, we get $b_3 - b_2 - b_1$, condition of solvability on $RHS$

## Condition of Solvability of Ax=b

- We can outline the conditions as follows

    - $Ax = b$ is solvable if $b$ is in column space, $C(A)$

    - If a combination of rows of $A$ gives zero row, then same combination of entries of $b$ must give $0$

## Complete Solution to Ax=b

- **Note:** Since we have $2$ equations and $4$ unknowns ($A$ has $2$ pivot rows and $4$ columns), we expect to find a whole bunch of solutions

- $x_{particular}$:

    - Set all free variables to $0$

    - Solve $Ax = b$ for pivot variables

    - For the previous example

    <div>
    \[
        x_p = \begin{bmatrix}
        -2 \\ 0 \\ 3/2 \\ 0
        \end{bmatrix}
    \]
    </div>

- $x_{nullspace}$:

    - We can add any variable in the nullspace

    - For the example

    <div>
    \[
        x_n = c_{1}\begin{bmatrix}
        -2 \\ 1 \\ 0 \\ 0
        \end{bmatrix} + c_{2}\begin{bmatrix}
        2 \\ 0 \\ -2 \\ 1
        \end{bmatrix}
    \]
    </div>

- $x_{complete} = x_{particular} + x_{nullspace}$, which works because

    - $Ax_{particular} = b$, based on our definition of $x_{particular}$

    - $Ax_{nullspace} = 0$

    - $Ax_{particular} + Ax_{nullspace} = b$

    - $A(x_{particular} + x_{nullspace}) = b$

- **Note:** The complete solution should be a $k$-dimensional subspace created using $k$ independent variables in $x_{nullspace}$, but is not a subspace as it is shifted based on $x_{particular}$ and does not pass through the origin

## Relation Between r, m, n

- We have an $m \times n$ matrix $A$ of rank $r$

    - We know $r \leq m$ and $r \leq n$

### Full column rank, $r = n$

- No free variables

- Null space will have only $0$ vector

- 0 or 1 solution to $Ax = b$

    - This would be $x_{particular}$ as seen in the previous example

    - It would only exist when $b$ is some combination of columns of $A$

    - Example of this would be a tall and thin matrix

    <div>
    \[
        \begin{bmatrix}
        1 & 3 \\
        2 & 1 \\
        6 & 1 \\
        5 & 1
        \end{bmatrix}
    \]
    </div>

### Full row rank, $r = m$

- Pivot variable in all rows

- $Ax = b$ can be solved for every $b$, i.e., $\infin$ solutions

    - After elimination, we would not get any $0$ row as all rows have a pivot element

    - Hence, there is no specific requirements on $b$

- $n - r = n - m$ free variables

- Example would be a short and wide matrix

<div>
\[
    \begin{bmatrix}
    1 & 2 & 6 & 5 \\
    3 & 1 & 1 & 1
    \end{bmatrix}
\]
</div>

### Full rank, $r = m = n$

- Square, invertible matrix

- $rref(A) = I$