---
title: 8. Inner Class
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-09-15'
lastmod: '2020-09-15'
---

## Introduction

- A class inside another class

- This feature helped fix bugs in GUIs

- This is basically used in places where one type of object can not exist without other type of object

- E.g. Map is a group of key, value pairs and each pair is called an entry. Wihtout object of Map, objects of entry cannot exist

- The relation between outer and inner class is a 'has-a' relationship (composition or aggregation)

- Types of inner classes

    - Normal or regular

    - Method local
    
    - Anonymous

    - Static nested

## Normal or regular inner class

- A normal class declared directly inside another class without static modifier

```
class Outer {
    class Inner {

    }
}
```

```
javac Outer.java
    - Outer.class

    - Outer$Inner.class

java Outer.class // RuntimeError: NoSuchMethodError: main

java Outer$Inner.class // RuntimeError: NoSuchMethodError: main
```

```
class Outer {
    class Inner {

    }

    public static void main(String[] args) {

    }
}

java Outer.class // Runs successfully
```

```
class Outer {
    class Inner {
        public static void main(String[] args) { // CompilerError: Inner classes cannot have static declaration

        }
    }
}
```

- This is because inner class cannot exist without outer class

```
class Outer {
    class Inner {
        public void m1() {
            System.out.println("Inner");
        }
    }

    public static void main(String[] args) {
        Outer o = new Outer();
        Outer.Inner i = o.new Inner();
        i.m1();

        Outer.Inner i2 = new Outer().new Inner();
        i2.m1();
    }
}
```

- Accessing inner class code from static area of outer class

```
class Outer {
    class Inner {
        public void m1() {

        }
    }

    public void m2() { 
        Inner i = new Inner();
        i.m1();
    }

    public static void main(String[] args) {
        Outer o = new Outer();
        o.m2();
    }
}
```

- It is easier to access inner class code from instance code of outer class

- From outside outer class, the method of accessing inner class code is same as accessing from static area

```
class Outer {
    int x = 10;
    static int y = 20;

    class Inner {
        public void m1() {
            System.out.println(x);
            System.out.println(y);
        }
    }

    public static void main(String[] args) {
        new Outer().new Inner().m1();
    }
}
```

- This is a valid code as we can access instance and static variables of outer class from inner class directly.

```
class Outer {
    int x = 10;

    class Inner {
        int x = 100;

        public void m1() {
            int x = 1000;

            System.out.println(x); // 1000
            System.out.println(this.x); // 100
            System.out.println(Outer.this.x); // 10
        }
    }

    public static void main(String[] args) {
        new Outer().new Inner().m1();
    }
}
```

- Modifiers

    - Outer class

        - public

        - default

        - final

        - abstract

        - strictfp

    - Inner class

        - public

        - default

        - final

        - abstract

        - strictfp

        - private

        - protected

        - static

### Nesting of inner class

```
class A {
    class B {
        class C {
            public void m1() {
                System.out.println("Hello");
            }
        }
    }
}

class Test {
    public static void main(String[] args) {
        A a = new A();
        A.B b = a.new B();
        A.B.C c = b.new C();
        c.m1();
    }
}
```

## Method local inner class

- Inner classes inside a method

- Java classes do not have nested method concept. For a method-specific, repeatedly required functionality, we can declare an inner class within a method and use that class for the functionality. This fulfills the requirements of nested methods

- We can declare inner classes (method local) in both instance and static methods

```
class Test {
    int x = 10;
    static int y = 20;

    public void m1() {
        class Inner {
            public static void m2() {
                System.out.println(x); // CompilerError: non-static variable x cannot be referred from a static context
                System.out.println(y);
            }
        }

        Inner i = new Inner();
        i.m2();
    }

    public static void main(String[] args) {
        new Test().m1();
    }
}
```

- Within a method-local inner class, we cannot access local variables of the method in which the said inner class is declared. If the local variable is declared as final, we can access it.

## Anonymous inner classes

- Most widely used type of inner classes

- Types:

    - Anonymous inner class that extends a class

    - Anonymous inner class that implements an interface

    - Anonymous inner class defined inside arguments

### Class that extends a class

```
// PopCorn.class
class PopCorn {
    public void taste() {
        System.out.println("Salty");
    }
}

class Test {
    public static void main(String[] args) {
        PopCorn p = new PopCorn() { // PopCorn reference with anonymous child class object
            // Test$1.class
            public void taste() {
                System.out.println("Spicy");
            }
        }

        p.taste();

        p = new PopCorn() {
            // Test$2.class
            public void taste() {
                System.out.println("Sweet");
            }
        }

        p.taste();
    }
}
```

```
javac Test.java
// PopCorn.class, Test.class, Test$1.class, Test$2.class
```

### Normal class as anonymous class

- Normal class and anonymous can both extend only one class at a time

- A normal class can implement any number of interface at a time. Anonymous can implement only one

- Normal class can extend a class while simultaneously implementing an interface. Anonymous class can do only one, either extend or implement (that too only one interface)

- No explicit constructor allowed for anonymous classes

- Anonymous class are helpful in GUI based applications for event handling

## Static nested class

- The objects of this class can exist without objects of outer class. Hence, there is no strong association

- Within outer class, the objects of static nested class can be created directly.

```
Nested n = new Nested();
```

- Outside of outer class, it is done as 

```
Outer.Nested n = new Outer.Nested();
```

- Static nested classes can have static members as well because objects of these class can exist without outer class objects. Hence, static nested classes can have main method too.

- Static nested classes can not access non static members of outer classes

### Nested classes / interfaces

- Case 1

    - Class inside class. This is for strong composition

- Case 2

    - Interface within class

    - If within a class multiple implementations of an interface that are related to the class are required, we can define interface within the class.

- Case 3

    - Interface within interface

    - E.g. a map is a group of key, value pairs that are called entry. Without map, entries cannot exist. Hence, interface entry is defined inside map

    - When using outer interface, we do not require to provide implementation of inner interface and vice-versa

- Case 4

    - Class within interface

    - When functionality of class is closely associated with interface and nowhere else is it used

    - It is also used to provide default implementation of interface

    - Class within interface is always public static