---
title: 15. Garbage Collection
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-11-04'
lastmod: '2020-11-11'
---

## Introduction

- Garbage collection is destruction of useless objects

- This prevents OutOfMemoryErrors

- Java contains a daemon thread that always runs in the background to destroy useless objects

## Ways to make an object eligible for GC

- Object is eligible for GC when there are no references pointing at it

- The ways are

    - Nullifying the reference variable: We can make the reference point at null

    - Reassign the reference variable

    - Objects inside a method are by default available for GC

## Methods for requesting JVM to run GC

- Once object is available for FC, it may not be destroyed immediately

- We can't expect when GC would be run by JVM

- To run GC

    - Use System class

    ```
    System.gc();
    ```

    - Using Runtime class

        - Runtime is singleton class (classes for which only one object is allowed to be made. Hence, they do not use constructors)

        ```
        Runtime r = Runtime.getRuntime();
        r.totalMemory();
        r.freeMemory();
        r.gc();
        ```

    - **Note:** Since System.gc() internally calls Runtime.gc(), it is recommended to call Runtime.gc() directly to reduce the overhaul

## Finalization

```
protected void finalize() throws Throwable
```

- Called just before destruction of object by GC

- It is present in Object class

- **Note:** GC only calls finalize on one Object once. The second time same object is eligible for GC, it is destroyed without calling finalize