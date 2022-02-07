---
title: 2. Operators and Assignments
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-08-08'
lastmod: '2020-08-08'
---

## Increment and Decrement Operators

- Increment

    - Pre-increment: ```++x```

    - Post-increment: ```x++```

- Decrement

    - Pre-decrement: ```--x```

    - Post-decrement: ```x--```

- These operators can be used for variables, not constant values. E.g.

```
int x = 10;
int y = ++10; // CompilerError: Unexpected type found: value; required: variable
System.out.println(y);
```

- Nesting of increment / decrement operators is not allowed

```
int x = 10;
int y = ++(++x);
System.out.println(y);
```

```
final int x = 10;
x = 11; // CompilerError: Cannot assign value to
x++;    // final variable
```

- Increment / decrement operators can be used for all primitive types except boolean

```
int x = 10;
x++;
System.out.println(x); // 11
```

```
boolean b = true;
b++; // CompilerError: operator ++ cannot be applied to boolean
System.out.println(b);
```

```
char ch = 'a';
ch++;
System.out.println(ch); // b
```

```
double d = 10.5;
d++;
System.out.println(d); // 11.5
```

- **Note:** ```b++``` vs ```b = b + 1```

    -  E.g.
    
    ```
    byte b = 10;
    b = b + 1; // CompilerError: possible loss of precision
    System.out.println(b);
    ```

    - E.g.
    ```
    byte b = 10;
    b++;
    System.out.println(b); // 11
    ```

## Arithmetic Operators (+, -, *, /)

- If we apply any arithmetic operator between two variables a and b, result is always **max(int, type of a, type of b)**

    - byte + byte = int

    - byte + short = int

    - byte + long = long

    - long + double = double

    - char + char = int

    - char + double = double

```
System.out.println('a' + 'b') // 195 (97 + 98)

System.out.println('a' + 0.95) // 97.95 (97 + 0.95)
```

```
System.out.println(10 / 0); // RuntimeException: ArithmeticeException: / by zero (because 10 is int)

System.out.println(10 / 0.0); // Infinity (because int and double will result in double)
```

### Infinity

- In integral arithmetic (b, s, i, l) there is no way to represent infinity, so we get ArithmeticException

- In floating point arithmetic (f, d), we can represent infinity

```
System.out.println(0 / 0); // NaN

System.out.println(10 < float NaN); // False

System.out.println(10 <= float NaN); // False

System.out.println(10 > float NaN); // False

System.out.println(10 == float NaN); // False

System.out.println(float NaN == float NaN); // False

System.out.println(10 != float NaN); // True

System.out.println(float NaN != float NaN); // True
```

### ArithmeticException

- Occurs at run-time and not compile-time

- Only in integral arithmetic

- Can only by caused by ```/``` or ```%``` operators

## String Concatenation (+)

- ```+``` is the only overloaded operator in Java

```
String a = "durga";
int b = 10, c = 20, d = 30;

System.out.println(a + b + c + d); // durga102030

System.out.println(b + c + d + a); // 60durga

System.out.println(b + c + a + d); // 30durga30

System.out.println(b + a + c + d); // 10durga2030
```

```
String a = "n";

int b = 10, c = 20, d = 30;

a = b + c + d; // CompilerError: Incompatible types found (LHS String, RHS int)

a = a + b + c; // valid (LHS String, RHS String)

b = a + c + d; // CompilerError: Incompatible types found (LHS int, RHS String)

b = b + c + d; // valid (LHS int, RHS int)
```

## Relational Operators (<, <=, >, >=)

- Can be applied for every primitive type except boolean

- Not applicable for object types

## Equality Operators (==, !=)

```
System.out.println('a' == 97.0); // true

System.out.println(false == false); // true
```

- We can apply for every primitive type

- Can be used for object types if both the references point to the same object

- There needs to be a relation between classes for equality operator to be applied to objects. E.g. parent-child etc.

```
Thread t = new Thread();
Object o = new Object();
String s = new String("A");

System.out.println(t == o); // false (Every class is derived from Object class)
System.out.println(o == s); // false (Every class is derived from Object class)
System.out.println(s == t); // CompilerError: incompatible types: java.lang.String and java.lang.Thread
```

- ```==``` is used for reference comparison. ```equals()``` method is used for content comparison

```
String s1 = new String("A");
String s2 = new String("A");

System.out.println(s1 == s2); // false
System.out.println(s1.equals(s2)); // true
```

- ```r == null``` is always false

## instanceof Operator

- To check if object is of particular type or not

- Useful for heterogeneous collections

```
// l -> list
Object o = l.get(o);

if(o instanceof Student) {
    Student s = (Student)o;
    // perform Student specific tasks
} else if(o instanceof Teacher) {
    Teacher t = (Teacher)o;
    // perform Teacher specific tasks
}
```

- Syntax: ```r instanceof X```

    - ```r``` object reference

    - ```X``` class / interface


- Reference should be related to comparing class / interface

```
Thread t = new Thread();
System.out.println(t instanceof Thread); // true
System.out.println(t instanceof Object); // true (all classes are derived from Object)
System.out.println(t instanceof Runnable); // true (Thread is derived from Runnable interface)
System.out.println(t instanceof String); // CompilerError: Incompatible types; found: java.lang.Thread; required: java.lang.String
```

- ```null instanceof X``` is ```false```

## Bitwise Operator (&, |, ^)

- For boolean, they return boolean

- Can be used for integral types

```
System.out.println(4 & 5); // 4
System.out.println(4 | 5); // 5
System.out.println(4 ^ 5); // 1
```

## Bitwise-Complement Operator (~)

- Only for integral types

```
System.out.println(~true); // CompilerError: Operator ~ cannot be applied to boolean function
System.out.println(~4); // -5
```

## Boolean-Complement Operator (!)

- Only for boolean

## Short-circuit Operators (&&, ||)

- Applicable only for booleans

- Second argument evaluation is optional

```
if (x && y) {
    // y is evaluated only if x i true
    // y is not evaluated if x is false since the whole & operation would be false irrespective of y
}

if (x || y) {
    // y is evaluated only if x is false
    // y is not evaluated if x is true since the whole | operation would be true irrespective of y
}
```

## Type-case Operator

- Implicit

    - Done by compiler

    - Always goes from smaller type to bigger type

    - Widening / upcasting

    - No loss of information

- Explicit

    - Defined by programmer

    - Can go from bigger to smaller

    - Narrowing / downcasting

    - Loss of precision

## Assignment Operators

- Simple

```
int x = 10;
```

- Chained

```
int a = b = 0;
```

- Compound

    - Has internal type-casting

```
a += 20;
```

```
int a, b, c, d;

a = b = c = d = 20;

a += b -= c *= d /= 2;

System.out.println(a + " | " + b + " | " + c + " | " + d); // -160 | -180 | 200 | 10
```

## Conditional Operators (?:)

- Only one ternary operator in Java

- Nesting of conditional is possible

```
int x = (10 > 20) ? 30 : ((40 > 50) ? 60 : 70);
System.out.println(x); // 70
```

## new Operator

- Used to create a new object

```
Test t = new Test(); // new allocates space for the object (creates object), Test() initializes object
```

- No delete operator because Java has automatic garbage collection

## Java operator precedence chart

1. Unary operators

    1. [], x++, x--

    2. ++x, --x, ~, !

    3. new, <type>

2. Arithmetic operators

    1. *, /, %

    2. +, -

3. Shift operators

    1. \>>, \>\>>, \<\<

4. Comparison operators

    1. \<, \<=, \>, \>=, instanceof

5. Equality operators

    1. ==, !=

6. Bitwise operators

    1. &
    2. ^
    3. |

7. Short-circuit operators

    1. &&
    2. ||

8. Conditional operator

    1. ?

9. Assignment operator

    1. =. +=, -=, *=, /=


## new vs newInstance()

- In some places, ```new``` can't be used but ```newInstance()``` can be used

- E.g. creating object of a class based on name given as a command line argument

```
class Test {
    public static void main(String[] args) throws Exception {
        Object o = Class.forName(args[0]) newInstance(); // Class is the class Class object
        System.out.println("Object created for " + o.getClass().getName());
    }
}
```

- ```newInstance()``` always calls the no-arg constructor. If constructor not found ```RuntimeError: InstantiationError```

- NoClassDefFoundError is an unchecked error and is not needed to be handled

```
Test t = new Test(); // RuntimeError NoClassDefFoundError: Test
```

- ClassNotFoundException is a checked error, needs to be handled by programmer

```
Object o = Class.forName(args[0]).newInstance();
```

```
Java Test test123 // RuntimeException: ClassNotFoundException (when using newInstance with a class name that is not defined)
```