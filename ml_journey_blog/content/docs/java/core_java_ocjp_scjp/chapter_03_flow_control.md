---
title: 3. Flow Control
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-08-15'
lastmod: '2020-08-15'
---

## Introduction

- They control the order in which statements will be executed at run-time

## Selection Statements

### if-else

- Syntax

```
if(boolean argument) {
    Action if 'if' is true
} else {
    Action if 'if' is false
}
```

- Arguments must be boolean, else there will be compile-time error

- Curly braces are optional, but without them, only a single statement is allowed, which should not be declarative

### switch

- For several options, it is easiest to use

- Syntax

```
switch(x) {
    case 1: Action 1;
        break;
    case 2: Action 2;
        break;
    ...
    default: Default action;
}
```

- Only allowed types as arguments are byte, short, int, char, Byte, Short, Character, Integer, enum and String

- Case and default are both optional

- E.g.

```
int x = 10;
final int y = 20;
int z = 30;

switch(x) {
    case 10: break;
    case y: break; // final is a constant
    case z: break; // CompilerError: constant expression required
}
```

```
int x = 10;

switch(x + 1) {
    case 10 + 20 + 30: break; // valid code. argument and label can be expressions
}
```

## Iterative Statements

### while-loop

- When number of iterations are not known in advance

```
while(true) {
    System.out.println("a");
}
System.out.println("b"); // CompilerError: unreachable code
```

```
while(false) {
    System.out.println("a"); // CompilerError: unreachable code
}
System.out.println("b");
```

```
final int a = 10, b = 20;

while(a < b) {
    System.out.println("a");
}
System.out.println("b"); // unreachable statement
```

### for-loop

- Number of iterations are known in advance

- Syntax:

```
for(initialization; condition check; increment or decrement) {
    loop body;
}
```

```
int i = 0;
for(System.out.println("Hello"); i < 2; i++) {
    System.out.println("Hi");
}

// Hello
// Hi
// Hi
```

- In initialization section, we can take any valid Java statement

- Conditional part is optional, true by default

```
for(;;) {
    System.out.println("Hello"); // infinite loop
}
for(;;) ; // infinite loop
```

### for-each loop

- Iterating over a list

```
int x[] = {1, 2, 3, 4};

for(int y: x) {
    System.out.println(y);
}
```

```
int x[][] = {{1, 2, 3}, {4, 5}};

for(int x1[]: x) {
    for(int x2: x1) {
        System.out.println(x2);
    }
}
```

- Best choice for arrays and collections. Not a general purpose loop.

- For-each can only print array elements in original order

### Iterable (I)

```
for(each_item: target) {
    // target is an Array / Collection
    // It is an Iterable object
}
```

- ```target``` element's class should implement Iterable interface

    - ```java.lang.Iterable```

- All ```Collection``` classes already implement Iterable (I)

- Iterable contains just one method: ```iterator```

    - ```public Iterator iterator();```

<div>
\[
    \begin{array}{c:c}
        Iterator (I) & Iterable (I) \\
        \hline
        \text{1. Related to collections} & \text{1. Related to for-each loop} \\ \\
        \text{2. To retrieve objects of collection one by one} & \text{2. Target element in for-each loop} \\ \\
        \text{3. java.util.package} & \text{3. java.lang.package} \\ \\
        \text{4. Has 3 methods: hasNext(), next(), remove()} & \text{4. Has 1 method: iterator()} \\
    \end {array}
\]
</div>

## Transfer Statements

### Break

- Inside switch

    - To stop fall-through

- Inside loops

- Inside labelled block

```
class Test {
    public static void main(String[] args) {
        int x = 10;
        l1 {
            System.out.println("Hello");
            if(x == 10) {
                break l1;
            }
            System.out.println("Bye");
        }
        System.out.println("Out");
    }
}
```

```
Hi
Out
```

### Continue

- Only inside loops

- For moving to next iteration

#### Labelled break and continue

```
l1:
    for(...) {
        l2:
            for(...) {
                for(...) {
                    break l1; // Goes to Point A
                    break l2; // Goes to Point B
                    break; // Goes to Point C
                }
                // Point C
            }
        // Point B
    }
// Point A
```

### do-while and continue

```
int x = 0;
do {
    x++;
    System.out.println(x);
    if(++x < 5) {
        continue;
    }
    x++;
    System.out.println(x);
} while(++x < 10);
```

```
1
4
6
8
10
```