---
title: 17. enum (enumerations)
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-11-19'
lastmod: '2020-11-26'
---

## Introduction

- If we want to represent a group of named constants

- The main objective of enum is to define our own data type

- This came in 1.5V and is more powerful than older language's enum

- Every enum is internally implemented as a class

- Every enum constant is public static final object of type enum

```
enum Dog {
    TIM, CEASAR, TOM;
}

class Test {
    public static void main(String[] args) {
        Dog d = new Dog.TIM;
        System.out.println(d); // TIM
    }
}
```

- The toString() method returns name of constant

- enum can be declared outside or inside the class but inside a method, or we get CompilerError: enum types must not be local

- Enum outside the class can be public, default, strictfp but not final and abstract

- Inside the class public, default, strictfp, private, protected and static

## enum vs switch()

- 1.4V, switch argument were: byte, short, char, int

- 1.5V, switch added Wrapper classes and enum (Byte, Short, Character and Integer)

- 1.7V onwards, even String were allowed

- If we make a case that is not a valid enum, and pass enum as argument to switch, we get CompilerError: unqualified enumerator constant name required

## enum vs inheritance

- Every enum is direct child of java.lang.Enum class so it can not inherit any other classes

- Every enum is always final implicitly so we cannot create a child

- Hence, inheritance is not applicable for enum explicitly

- Enum can implement any number of interfaces

- Methods

    - ```static values()```: Enum contains this method which returns an array of all constants in that enum. Enum keyword implicitly provides this method, i.e., it is not present in either java.lang.Enum or Object class

    - ```public final int ordinal()```: To find ordinal value of enum object

- In Java, enum can contain methods, instance variables etc.

- If we are taking anything else in addition to constants, then list of constants should be in first line and end with semi-colo.

- Empty enum is valid java syntax

## enum vs constructor

- Enum can contain constructor

- enum constructor is executed separately for all constants at the time of class loading

- We can't invoke enum constructor directly

- **Note:** Inside enum only concrete methods are allowed

- For specific constant if we want special implementation, we can apply inner class techniques