---
title: 12. Graphs, Networks and Incidence Matrices
description: Lecture on real-world application of linear algebra
toc: true
authors:
tags:
categories:
series:
date: '2021-03-01'
lastmod: '2021-03-02'
---

## Introduction

- Linear algebra uses matrices which are created from observations in the real world

    - Eg. chemistry professors use row reduction on matrices that contain number of particles of different components in a reaction

- Graph is another such application which is a great source of matrices

    - Eg. social networks, internet, electrical network, hydraulic network etc.

## Graphs

- They are made of nodes and edges

### Incidence Matrices

- These are generated from graphs

- E.g.

    - &nbsp; 
    
    <div>
    <img src="/docs/linear_algebra/linear_algebra_mit_18_06/graph_network.png" style="height:100px;margin:auto;">
    </div>
    
    - This graph can be represented as an incidence matrix
    
    <div>
    \[
        \begin{bmatrix}
        -1 & 1 & 0 & 0 \\
        0 & -1 & 1 & 0 \\
        -1 & 0 & 1 & 0 \\
        -1 & 0 & 0 & 1 \\
        0 & 0 & -1 & 1
        \end{bmatrix}
    \]
    </div> 

    - Any loops in the graph would be made by linearly dependent rows in incidence matrices
    
- The nullspace of a matrix with all linearly independent columns contains only the $\\{0\\}$ vector

    - For the previous example,

    <div>
    \[
        \begin{bmatrix}
        -1 & 1 & 0 & 0 \\
        0 & -1 & 1 & 0 \\
        -1 & 0 & 1 & 0 \\
        -1 & 0 & 0 & 1 \\
        0 & 0 & -1 & 1
        \end{bmatrix}
        \begin{bmatrix}
        x_1 \\ x_2 \\ x_3 \\ x_4
        \end{bmatrix} = 
        \begin{bmatrix}
        0 \\ 0 \\ 0 \\ 0 \\ 0
        \end{bmatrix}
    \]
    </div>

    <div>
    \[
        \begin{bmatrix}
        x_2 - x_1 \\
        x_3 - x_2 \\
        x_3 - x_1 \\
        x_4 - x_1 \\
        x_4 - x_3
        \end{bmatrix} = 
        \begin{bmatrix}
        0 \\ 0 \\ 0 \\ 0 \\ 0
        \end{bmatrix}
    \]
    </div>

    - If $x_1, x_2, x_3, x_4$ are considered as the potentials on the nodes, then this matrix gives the potential differences across edges

    - In this example, the nullspace is not the $\\{0\\}$ vector as columns are dependent. The nullspace is

    <div>
    \[
        c\begin{bmatrix}
        1 \\ 1 \\ 1 \\ 1
        \end{bmatrix}
    \]
    </div>

    - Physical interpretation of nullspace is that there is some combination of values of potentials at each node for which there will be no flow of current. The $c$ is an arbitrary constant and we need to set some initial condition to find the exact value of potentials.

        - The initial condition can be to ground one node, which will make other columns of incidence matrix independent.