---
title: 1. Geometry of Linear Equations
description: Chapter 1 of example doc
toc: true
authors:
tags:
categories:
series:
date: '2020-10-16'
lastmod: '2020-10-16'
---

- Eg. 
<div>\[
A = \begin{bmatrix}
2 & -1\\
-1 & 2
\end{bmatrix}
X = \begin{bmatrix}
x \\
y
\end{bmatrix}
B = \begin{bmatrix}
0 \\
3
\end{bmatrix}
\]</div>

- Row Picture: Row is a line. (x, y) give intersection of the two lines
**Note:** 2x-y = 0 goes through origin, since RHS = 0

- Column Picture: B is a linear combination of columns of A, i.e., sum of vectors
<div>\[
x * \begin{bmatrix}
2 \\
-1
\end{bmatrix} + y * \begin{bmatrix}
-1 \\
2
\end{bmatrix} = \begin{bmatrix}
0 \\
3
\end{bmatrix}
\]</div>

**Side:** What do all possible linear combinations of columns of A give?

**Side:** Can we solve $AX = b$ for all $b$ (do linear combinations of columns fill dimensions of $b$)?

**Note:** If columns lie in the same lower dimension, then any $b$ outside that object would be unsolvable