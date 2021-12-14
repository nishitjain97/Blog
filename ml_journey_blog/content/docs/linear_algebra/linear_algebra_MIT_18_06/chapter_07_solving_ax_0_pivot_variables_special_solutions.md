---
title: 7. Solving Ax=0, Pivot Variables, Special Solutions
description: Null space and other information related to Ax=0
toc: true
authors:
tags:
categories:
series:
date: '2021-03-01'
lastmod: '2021-03-02'
---

## Elimination for Null Space

- We can find null space by solving $Ax=0$ using elimination method

    - **Note:** The steps taken for elimination (row operations) do not change the null space

- 
<div>
\[
    A = \begin{bmatrix}
    1 & 2 & 2 & 2 \\
    2 & 4 & 6 & 8 \\
    3 & 6 & 8 & 10
    \end{bmatrix}
\]
</div>
 
- Performing elimination on $A$, we get $U$

    - 
    <div>
    \[
        U = \begin{bmatrix}
        (1) & 2 & 2 & 2 \\
        0 & 0 & (2) & 4 \\
        0 & 0 & 0 & 0
        \end{bmatrix}
    \]
    </div>

    - Though this matrix is not a truly upper triangular matrix, it is in the **echelon form** (stair-case around non-zero elements can be created to separate them from zero elements)

    - Highlighted eliments are **pivots**

    - **Note:** Since we have $2$ pivots, the **rank** of the matrix $A$ is $2$

    - **Note:** A row of zeros in the $U$ matrix shows that the particular row in the original matrix $A$ was a linear combination of other rows

    - In this matrix, we have

        - Two pivot columns (columns containing pivot values), corresponding to pivot variables

        - Two free columns (columns without pivot values), corresponding to free variables

    - We assign some arbitrary values (usually 0 and 1) to free variables and solve the pivot columns to get the final solution

        - In our example, we have $x_2$ and $x_4$ as free variables and $x_1$ and $x_3$ as pivot variables

        - We assign $x_2 = 0$ and $x_4 = 1$ first to get

            - 
            <div>
            \[
                c_1\begin{bmatrix}
                2 \\ 0 \\ -2 \\ 1
                \end{bmatrix}
            \]
            </div>

        - We assign $x_2 = 1$ and $x_4 = 0$ to get

          - 
          <div>
          \[
              c_2\begin{bmatrix}
              -2 \\ 1 \\ 0 \\ 0
              \end{bmatrix}
          \]
          </div>

        - These are both infinitely long lines in $R^4$

- Rank of matrix $A$, which is $m \times n$, is the number of pivot variables

    - In the previous example, $r = 2$

- Number of free variables is $n - r$

    - Same example, $n - r = 2$

## Reduced Row Echelon Form (rref)

- This form directly follows from the echelon form mentioned above 

- Once we have discovered all pivot elements, we can get the **rref** by

    - Performing elimination upwards (normally we eliminate downwards to get the upper triangular $U$ matrix)

    - Dividing rows by relevant constants to get $1$ in all pivot positions

- Taking the same example as above, we will start from the $U$ form

    - $U=$

    <div>
    \[
        \begin{bmatrix}
        (1) & 2 & 2 & 2 \\
        0 & 0 & (2) & 4 \\
        0 & 0 & 0 & 0
        \end{bmatrix}
    \]
    </div>

    - Elimination upwards

    <div>
    \[
        \begin{bmatrix}
        (1) & 2 & 0 & -2 \\
        0 & 0 & (2) & 4 \\
        0 & 0 & 0 & 0
        \end{bmatrix}
    \]
    </div>

    - Getting $1$ in all pivot positions by dividing $row_2$ by $2$

    <div>
    \[
        R = \begin{bmatrix}
        (1) & 2 & 0 & -2 \\
        0 & 0 & (1) & 2 \\
        0 & 0 & 0 & 0
        \end{bmatrix} = rref(A)
    \]
    </div>

- Properties of rref

    - It gives us the pivot and free variables directly

    - It can be represented as

        - rref

        <div>
        \[
            rref = \begin{bmatrix}
            I & F \\
            0 & 0
            \end{bmatrix}
        \]
        </div>

        - $I$ is $r \times r$ identity matrix that represents the pivot columns

        - $F$ is the matrix representing $n - r$ free columns

    - We can get the null space (special solutions) by solving $RN = 0$, where $N$ is the null space matrix with columns representing special solutions

        - Here,

        <div>
        \[
            N = \begin{bmatrix}
            -F \\ I
            \end{bmatrix}
        \]
        </div>

- Demonstrating by taking transpose of previous example

    - E.g.
    
    <div>
    \[
        \begin{bmatrix}
         1 & 2 & 3 \\
         2 & 4 & 6 \\
         2 & 6 & 8 \\
         2 & 9 & 10
        \end{bmatrix}
    \]
    </div>

    - Performing elimination (there would be one row exchange required for this case), we get

        - $U$
        
        <div>
        \[
            U = \begin{bmatrix}
            (1) & 2 & 3 \\
            0 & (2) & 2 \\
            0 & 0 & 0 \\
            0 & 0 & 0
            \end{bmatrix}
        \]
        </div>
    
        - Pivot columns, $r = 2$
        
            - **Note:** Number of pivot columns for $A$ is same as that of $A^T$
          
        - Free columns, $n - r = 3 - 2 = 1$
        
        - Now solving $Ux = 0$, and giving free variable the value $1$, we get
        
            - Null space,

            <div>
            \[
                x = c\begin{bmatrix}
                -1 \\ -1 \\ 1
                \end{bmatrix}
            \]
            </div>

            - **Note:** We can not consider $0$ as special solution for free variable as it will give every variable as 0

    - Going further to get rref

        - $R$

        <div>
        \[
            R = \begin{bmatrix}
            1 & 0 & 1 \\
            0 & 1 & 1 \\
            0 & 0 & 0 \\
            0 & 0 & 0
            \end{bmatrix} = 
            \begin{bmatrix}
            I & F \\
            0 & 0
            \end{bmatrix}
        \]
        </div>

        - This gives null space matrix $N$ as

        <div>
        \[
            x = c\begin{bmatrix}
            -F \\ I
            \end{bmatrix} = 
            c\begin{bmatrix}
            -1 \\ -1 \\ 1
            \end{bmatrix}
        \]
        </div>