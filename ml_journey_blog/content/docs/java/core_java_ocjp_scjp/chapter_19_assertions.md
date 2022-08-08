---
title: 19. Assertions
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-12-04'
lastmod: '2020-12-11'
---

## Introduction

- The most common method to debug a code is to add System.out.println() lines to check where error is occurring. However, these lines need to be removed before production as they can cause performance issues

- Hence, we can replace these System.out.println() lines with assert statements. These need not to be deleted as by default, they are disabled and can be enabled to debug

- Application of assertions is only in development and testing phase, but no production phase

## assert as keyword and identifier

- From 1.4V onwards, we cannot use assert as identifier as it became a keyword

## Types of assert statements

- Simple version

```
assert(x == 10);
assert(b); // Should be boolean true
```

```
java -ea Test // RuntimeError: AssertionError
```

- Augmented Version

```
assert(x > 10): "Here x > 10 but it is not"
```

This gives details of the error if assertion fails

## Various run-time flags

- -ea / -enableassertions

    - Enable assertion in every non-system class. Non-system are user-defied classes

- -da / -disableassertions

    - For non-system classes

- -esa / -enablesystemassertions

    - Enable for system classes

- -dsa / -disablesystemassertions

- **Note:** We can use these simultaneously, JVM considers them from left to right

- **Note:** 

    - To enable in specific class ```java -ea: pack1.B```

    - To enable in every class ```java -ea: pack1...```

    - To enable in every class except B ```java -ea: pack1... -da: pack1.B```

## Appropriate / Inappropriate use of assertions

- It is always inappropriate to use assertion to implement programming logic. This is because assertion may or may not be executed

- Any place where flow should not reach (e.g. default case of switch etc.) is the best place to use assertions

- Inappropriate to validate public method arguments, but appropriate to validate private method arguments

## AssertionError

- Child of Error.Unchecked

- Raised when assert argument is false

- Though it is legal to catch assertion error, it is bad programming practise