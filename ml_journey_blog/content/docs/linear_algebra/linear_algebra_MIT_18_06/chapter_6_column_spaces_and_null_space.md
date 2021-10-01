---
title: 6. Column Spaces and Nullspace
description: Important subspaces derived from matrices.
toc: true
authors:
tags:
categories:
series:
date: '2021-03-01'
lastmod: '2021-03-02'
---

## Prerequisites

- Vector space requirements: If $v$ and $w$ are vectors in the space, then 

    - $v + w$ and $cv$ are in the space, $\forall c \in R$

    - Or, $cv + dw$ is in the space, $\forall c, d \in R$

- All subspaces need to contain the **zero vector**

- For two subspaces $P$ and $L$

    - $P \cup L$ **is not** a subspace

        - $P \cup L$ means vectors that belong to $P$, to $L$ or to both

        - If we take one vector in $P$ and one in $L$, their sum would not be in either $P$ or $L$, thereby violating the property of a subspace

    - $P \cap L$ **is** a subspace

        - $P \cap L$ means vectors that belong to both $P$ and $L$

        - If $v$ and $w$ are in $P \cap L$, 
        
            - They belong to both $P$ and $L$
            
            - Their sum $v + w$ belongs to both $P$ and $L$

            - Their sum $v + w$ belongs to $P \cap L$

        - Similarly, if $v$ belongs in $P \cap L$

            - $v$ belongs to both $P$ and $L$

            - $cv$ belongs to both $P$ and $L$

            - $cv$ belongs to $P \cap L$


## Column Space of Matrix

- Column space of a matrix $A$, $C(A)$, is made of all possible linear combinations of the columns of $A$

    - E.g. for the following $A$, the column space would be made up of all vectors that can be created using some linear combination of the vectors $\begin{bmatrix}1 & 2 & 5 & 1\end{bmatrix}$, $\begin{bmatrix}3 & 3 & 1 & 1\end{bmatrix}$ and $\begin{bmatrix}7 & 7 & 8 & 1\end{bmatrix}$ which are columsn of $A$

    <div>
    \[
        \begin{bmatrix}
            1 & 3 & 7 \\
            2 & 3 & 7 \\
            5 & 1 & 8 \\
            1 & 1 & 1
        \end{bmatrix}
    \]
    </div>

- For an $n \times m$ matrix $A$, column space would be a subspace of $R^n$

    - In the previous example, since each column vector is made up of $4$ real numbers, column space would be a subspace of $R^4$

- For $n \times m$ matrices where $m < n$, column space cannot fill the complete $n$-dimensional space since we can have at most $m$ independent columns

    - Hence, column space is a subset of $n$-dimensional space

    - The dimension of column space can be found by identifying number of independent columns in $A$

        - Independence of columns means that no column of $A$ can be created from a linear combination of any other column(s)

        - Intuitively, this means that all columns are giving some new information to us

    - In the previous example, $C(A)$ is a $3$-dimensional subspace of $R^4$

- We can solve system of linear equations $Ax = b$ only when $b$ is in the column space of $A$

## Null Space of Matrix

- Null space of $A$, $N(A)$, is made of all $x$s that make up the solutions to the equation $Ax = 0$

    - Taking the same example as above
    <div>
    \[
        \begin{bmatrix}
            1 & 3 & 7 \\
            2 & 3 & 7 \\
            5 & 1 & 8 \\
            1 & 1 & 1
        \end{bmatrix}
        x = 
        \begin{bmatrix}
        0 \\ 0 \\ 0
        \end{bmatrix}
    \]
    </div>

    - The only $x$ that satisfies this equation is the null vector. Hence, $N(A)$ is the null vector

- For an $n \times m$ matrix, this space would be in $R^m$