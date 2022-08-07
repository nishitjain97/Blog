---
title: 13. Generics
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-10-27'
lastmod: '2020-11-03'
---

## Introduction

- To provide type-safety and resolve type-casting problems

- Generics was introduced in 1.5V to make Collections type-safe and resolve their type-casting issues

### Type-Safety

- Arrays are type-safe. We can guarantee the type of object inside any array. In case we add any other type in an array, we get CompilerError: Incompatible types found: java.lang.xx, required: java.lang.yy

- Collections are not type-safe. They can contain heterogeneous objects

### Type-Casting

- Arrays don't require type-casting while retrieving objects from them

- Collections require necessary type-casting because elements are of type Object inside Collection

```
ArrayList<String> l = new ArrayList<String>();

// ArrayList = base type, String = parameter type
```

- **Note:** Polymorphism is applicable for base types but not for parameter types

```
List<String> l = new ArrayList<String>(); // Works

List<Object> l = new ArrayList<String>(); // CompilerError: incompatible types, found: ArrayList<String>, required: ArrayList<Object>

ArrayList<int> l = new ArrayList<int>(); // CompilerError: unexpected type, found: int, required: reference
```

- **Note:** Primitive types can not be parameter types

## Generic Classes

- 1.4V

    - The older version required Object type elements and returned Object type elements, which caused loss of type-safety and requirement of type-casting

    ```
    class ArrayList {
        add(Object o);
        Object get(int index);
    }
    ```

- 1.5V

    - During compilation, compiler will replace every T with our specified type

    ```
    class ArrayList<T> {
        add(T t);
        T get(int index);
    }
    ```

    - Based on our requirement, we can define our own Generic classes also

    ```
    class Account<T> {
        ;
    }
    ```

## Bounded types

- We can bound the type parameter by using extends keyword

    - We can pass any type for T without any restrictions. Hence, it is unbounded.
    ```
    class Test<T> {
        
    }
    ```

    - For bounded

    ```
    class Test<T extends Number> {

    }

    Test<Integer> i = new Test<Integer>(10); // Works

    Test<String> s = new Test<String>("a"); // CompilerError: type parameter java.lang.String is not in its bound
    ```

    - **Note:** We can bind type parameter using interfaces also, still we have to use extends keyword

    ```
    class Test<T extends Runnable> {

    }
    ```

- We can define bound type parameters in combination also using '&' operator. The order is important, i.e., class first, then interfaces.

    - **Note:** Only one class, and multiple interfaces are allowed

    ```
    class Test<T extends Runnable & Comparable> {}

    class Test<T extends Number & Runnable & Comparable> {}

    class Test<T extends Runnable & Number> {} // Error: first interface, then class

    class Test<T extends Number & Thread> {} // Error: only 1 class allowed
    ```

    - **Note:** We can take any valid Java identifier as type parameter, but it is convention to take 'T'

- We can declare any number of type parameters separated with comma.

```
class Test<A, B> {

}

class HashMap<K, V> {

}

HashMap<Integer, String> h = new HashMap<Integer, String>();
```

## Generic Methods and Wildcard character (?)

- Method level generics

    - ```m1(ArrayList<String> l)```

        - Can be called with only ArrayList\<String\>

        - Within the method, we can add only String elements to l

    - ```m1(ArrayList<?> l)```

        - We can call by passing ArrayList of any type

        - Within the method, we can't add anything to the list except null

        - Best suitable for read-only operation

    - ```m1(ArrayList<? extends X> l)```

        - X can be either class or interface

        - If X is a class, we can pass ArrayList of X or its child classes

        - If X is interface, we can pass ArrayList of X or implementation class

        - We can't add anything to the list except null

        - Suitable for read-only operations

    - ```m1(ArrayList<? super X> l)```

        - X can be class or interface

        - If X is class, we can call by ArrayList of X or its parent classes

        - If X is interface, we can pass ArrayList of X or super class of implementation class of X

        - Here we can add objects of type X or null to the list

- **Note:** ```ArrayList<?> l = new ArrayList<?>()``` gives CompilerError: Unexpected type found: ?, required: class or interface without bound

## Communication with non-generic

- We can specify method leve type parameter also

```
class Test {
    public <T> void m1(T object) {

    }
}
```

- A generic object in non-generic area behaves like a non-generic object

- Generics is applicable only for compiler. After compilation, Generics is not available for JVM to check. Hence the following declaration are equal

    - ```ArrayList l = new ArrayList<String>();```

    - ```ArrayList l = new ArrayList<Integer>();```

    - ```ArrayList l = new ArrayList();```

- At compile time

    - Compile code normally by considering generic syntax

    - Remove generic syntax

    - Compiler resultant code again

    ```
    class Test {
        public static void m1(ArrayList<String> l) {
            // m1(ArrayList l)
        }

        public static void m1(ArrayList<Integer> l) {
            // m1(ArrayList l)
        }
    }

    // CompilerError: name clash: both methods have same erasure
    ```