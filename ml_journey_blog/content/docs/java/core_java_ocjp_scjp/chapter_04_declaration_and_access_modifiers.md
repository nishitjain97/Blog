---
title: 4. Declaration and Access Modifiers
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-08-22'
lastmod: '2020-08-22'
---

## Java source files structure

- A program can contain any number of classes

- Atmost one class can be declared as public

- If there is a public class, name of program and name of public class must be matched, otherwise we get CompilerError

- If more than one public class, CompilerError

```
nj.java
-------
class A {
    public static void main(String[] args) {

    }
}

class B {
    public static void main(String[] args) {

    }
}

class C {
    public static void main(String[] args) {

    }
}

class D {
}
```

```
> javac nj.java
// A.class, B.class, C.class, D.class
```

```
> java A // Runs
> java B // Runs
> java C // Runs
> java D // CompilerError: No main method found
> java nj // CompilerError: No class definition found
```

```
class Test {
    public static void main(String[] args) {
        ArrayList l = new ArrayList()); // CompilerError: could not find symbol
                                        // symbol: class ArrayList
                                        // location: class Test
    }
}
```

- Correct way is ```java.util.ArrayList l = new java.util.ArrayList();```

- Fully qualified names prevent CompilerError

- Import statement helps overcome repeated use of fully qualified names

### Types of import statements

- Explicit class import

    - E.g. ```java.util.Scanner;```

    - Recommended because it improves the readability of the code

- Implicit class import

    - E.g. ```java.util.*;```


```
import java.util.*;
import java.sql.*;

class Test {
    public static void main(String[] args) {
        Date d = new Date(); // CompilerError: reference to Date is ambiguous
    }
}
```

- Even in the case of List, we may get same ambiguity problem due to java.util.List and java.awt.List

- For resolving class names, priority is as follows

    1. Explicit class imports

    2. Classes in current workspace directory (default directory)

    3. Implicit class import

- When we import a java package, all classes and interfaces present in the package are available by default but sub-package classes are not available. For that, import statement till sub-level is needed

```
java.util.*; // does not include Pattern
java.util.regex.*; // includes Pattern
java.util.regex.Pattern; includes Pattern
```

- java.lang and default package (current working directory) classes do not have to be imported

- Import statement type only affects compile time. There is no effect on run-time.

### Static import

- Reduces length of code but also reduces readability and creates confusion

- Should be used only when necessary

```
// Without static import
class Test {
    public static void main(String[] args) {
        System.out.println(Math.sqrt(4));
        System.out.println(Math.max(10, 20));
        System.out.println(Math.random());
    }
}
```

```
// With static import
import static java.lang.Math.*;

class Test {
    public static void main(String[] args) {
        System.out.println(sqrt(4));
        System.out.println(max(10, 20));
        System.out.println(random());
    }
}
```

### System.out.println()

- System is a class in java.lang package

- 'out' is a static variable inside the System class. It is of class PrintStream

- println() is a method of class PrintStream

```
import java.lang.Integer.*;
import static java.lang.Byte.*;

class Test {
    public static void main(String[] args) {
        System.out.println(MAX_VALUE); // CompilerError: reference to MAX_VALUE is ambiguous
    }
}
```

```
import static java.lang.Integer.MAX_VALUE;
import static java.lang.Byte.*;

class Test {
    static int MAX_VALUE = 99;
    public static void main(String[] args) {
        System.out.println(MAX_VALUE); // 99
    }
}
```

- Priority is as follows

    - Current class static members

    - Explicit import

    - Implicit import

### Package

- Group of similar / related things is made in a package

- Used to resolve naming conflicts

- Help in modularity and maintainability

- Provides security for our components

- For unique naming, universally accepted convention

```
com.apple.device.var.Whatsapp;

// com.apple = client's domain name in reverse
// device = module
// var = sub-module
// Whatsapp = class name
```

- Creating a package

    ```
    com.nishit.javafiles;
    ```
    
    ```
    public class Test {
        public static void main(String[] args) {
            System.out.println("Hello");
        }
    }
    ```
    
    ```
    > javac Test.java
    ```

    - Current working directory -> Test.class

        - Since Test.class belongs to the package com.nishit.javafiles, its location in current working directory does not make sense

    ```
    > javac -d . Test.java
    ```

    - Current working directory -> com -> nishit -> javafiles -> Test.java

    - The command will create package directory and sub-directories if not present already

    - If -d destination directory is not found, compile time error will occur

    - While executing, we have to use fully qualified name

    - In one source file, atmost one package statement is allowed

    ```
    package p1;
    package p2; // CompilerError: Class, interface, enum expected

    class Test {

    }
    ```

    - <i></i>

    ```
    import java.util.*;
    package p1; // CompilerError: Class, interface, enum expected
    class Test {

    }
    ```

    - First non-comment statement should be package (if available)

    ```
    // order is important
    package statement; // atmost one
    import statement; // any number
    class / interface / enum; // any number
    ```

    - Empty file is also a valid Java file

## Class level modifiers

- Used to provide information of the behavior of class to JVM

- The only modifiers for top level classes are:

    - public

    - default

    - final

    - abstract

    - strictfp

- For inner classes, along with the above, additional modifiers are

    - private

    - protected

    - static

```
private class Test { // CompilerError: modifier private not allowed here
    public static void main(String[] args) {
        System.out.println("Hi");
    }
}
```

### public classes

- Can be accessed from anywhere

### default class

- Package level access

- Can be accessed from within the package only

### final modifier

- Applicable for classes, methods and variables

- Final method can not be overriden

- Final classes can not be inherited

    - Every method inside a final class is final

    - Variable inside final class is not necessarily final

- Though final keyword provides security and unique implementation, it can also lead to missing key benefits of OOPs such as inheritance (final classes) and polymorphism (final methods)

### abstract modifier

- Applicable for classes and methods but not for variables

- Abstract methods have only declaration but not implementation

- Abstract methods in parent class give guidelines to child methods which are compulsarily needed to be defined

```
abstract final void m1(); // CompilerError: illegal combination of modifiers
```

- Abstract makes illegal combinations with final, native, synchronized, static, private, strictfp (those which take mandatory implementation)

- Abstract classes have partial implementation, preventing formation of objects of those classes

- Abstract class has 0 or more abstract methods

- HttpServlet class is abstract class with 0 abstract methods

- Every adapter class is recommended to be declared abstract, but doesn't contain any abstract method

- Abstract keyword encourages OOP concept

### strictfp

- Strict floating point modifier

- Version 1.2

- For classes and methods, not for variables

- Usually result of floating point arithmetic varies from system to system. To prevent this variance, we use strictfp

- In a strictfp method, all floating point calculations follow IEEE 754 standard

- In a strictfp class, all concrete methods follow IEEE 754 standard

```
class Test {
    abstract strictfp void M(); // CompilerError: Illegal combination
}
```

```
abstract strictfp void test {
    // No error
}
```

## Member modifiers

- For methods or variables

### public members

- A public member can be accessed from anywhere as long as the class is also public

```
package pack1;

class A {
    public void M() {
        System.out.println("A");
    }
}
```

```
package pack2;

import pack1.A; // CompilerError: A not public in pack1, can't be accessed outside its package

class B {
    public static void main(String[] args) {
        A a = new A();
        a.M();
    }
}
```

### default members

- Can be accessed from anywhere inside a package

- Also known as package level modifier

### private members

- Access only within the class

### protected members

- Most misunderstood modifier

- Anywhere in current package and in child classes outside the package

```
package pack1;

public class A {
    protected void M1() {

    }
}
class B extends A {
    public static void main(String[] args) {
        A a = new A();
        a.M1();
        B b = new B();
        b.M1();
        A a1 = new B();
        a1.M1();
    }
}
```

```
package pack2;
import pack1.A;

class C extends A {
    public static void main(String[] args) {
        A a = new A();
        a.M1(); // CompilerError: M1() has protected access in pack1.A
        C c = new C();
        c.M1(); // Executes
        A a1 = new C();
        a1.M1(); // CompilerError: M1() has protected access in pack1.A
    }
}
```

- Protected members outside the package can only be accessed using child reference

```
package pack3;
import pack1.A;

class C extends A {

}

class D extends C {
    public static void main(String[] args) {
        A a = new A();
        a.M1(); // CE

        C c = new C();
        c.M1(); // CE

        D d = new D();
        d.M1(); // Works

        A a1 = new C();
        a1.M1() // CE

        A a2 = new D();
        a2.M1() // CE

        C c1 = new D();
        c1.M1() // CE
    }
}
```

- Outside packages protected members can be accessed in a child class using only that particular class reference

### final variables

#### instance variables

- Instance variable is given default value by compiler, but needs to be initialized explicitly if declared final

- For final instance variables, initialization has to be performed before constructor completion

```
// At the time of declaration
class Test {
    final int x = 10;
}
```

```
// Inside instance block
class Test {
    final int x;
    {
        x = 10;
    }
}
```

```
// Inside constructor
class Test {
    final int x;

    Test() {
        x = 10;
    }
}
```

```
class Test {
    final int x;

    public void M() {
        x = 10; // CompilerError: cannot assign a value to final variable
    }
}
```

```
class Test {
    final static int x; // CompilerError: variable x might not have been initialized
}
```

- For final static variables, initialization is compulsary before class loading completion

```
// At the time of declaration
class Test {
    final static int x = 10;
}
```

```
// Inside static block
class Test {
    final static int x;
    static {
        x = 10;
    }
}
```

#### local variables

- Do not get default values and only need to be initialized before use

- Only applicable modifier is final

- Formal parameters of a method act as local variables of that method. Hence, can be declared final.

### static modifier

- Modifier applicable for methods and variables, but not classes

- Only for inner classes, called static nested classes, it is applicable

- Static members can be accessed from both static and non-static areas

- Overloading concept is applicable for static methods, including main method, but JVM always class the one with String[] arguments

- Inheritance is also applicable

```
class P {
    public static void main(String[] args) {
        System.out.println("Main");
    }
}

class C extends P {

}

// javac P.java
// java C
// Main
```

- If inside a method, if we are not using any instance variables, then it should be declared static

- Abstract static combination is illegal

### synchronized

- Applicable for methods and blocks but not for classes and variables

- To prevent data inconsistancy problems

- Method should compulsarily contain implementation, so can't be used with abstract

### native

- only for methods

- Methods implemented in non-Java languages (mostly C/C++)

- A.k.a. foreign method

- Used

    - To improve the performance of program

    - To communicate with the machine at memory level

    - For legacy non-Java code

- Pseudocode to use native keyword in Java

```
class Native {
    static {
        System.loadLibrary(path); // Load library for native declaration
    }

    public native void m1(); // Declare native method (No definition as it is in C/C++)
}

class Test {
    public static void main(String[] args) {
        Native n = new Native();
        n.m1(); // Invoke method
    }
}
```

```
public native void m1();
```

```
public native void m1() {} // CompilerError: native methods can't have a body
```

- \`abstract native\` combination is illegal as abstract methods do not have implementation whereas native methods have implementation in other language

- \`native strictfp\` is illegal because C/C++ do not follow IEEE standards

- It breaks platform independancy of Java

### transient

- Only for variables

- Used in Serialization context

- At the time of serialization, to meet security constraint, if we do not want to save value of some variable, we should declare it transient

- JVM ignores value of variable and uses default

- transient is opposite of serialization

### volatile

- Only for variables

- Multiple threads working on a variable can cause data inconsistancy. To prevent this, variable is declared volatile, so each thread gets its own copy of variable

- Prevents inconsistance, but makes program very complex

- Should never be used (most deprecated keyword)

- ```volatile final int x = 15; // CompilerError```

<table>
    <thead>
        <tr>
            <th rowspan=2>Modifier</th>
            <th colspan=2>Class</th>
            <th rowspan=2>Methods</th>
            <th rowspan=2>Variables</th>
            <th rowspan=2>Blocks</th>
            <th colspan=2>Interfaces</th>
            <th colspan=2>Enum</th>
            <th rowspan=2>Constructors</th>
        </tr>
        <tr>
            <th>Outer</th>
            <th>Inner</th>
            <th>Outer</th>
            <th>Inner</th>
            <th>Outer</th>
            <th>Inner</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Public</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
        </tr>
        <tr>
            <td>Private</td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
        </tr>
        <tr>
            <td>Protected</td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
        </tr>
        <tr>
            <td>Default</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
        </tr>
        <tr>
            <td>Final</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>Abstract</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>Static</td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td></td>
        </tr>
        <tr>
            <td>Synchronized</td>
            <td></td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>Native</td>
            <td></td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>Strictfp</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
            <td>:heavy_check_mark:</td>
        </tr>
        <tr>
            <td>Transient</td>
            <td></td>
            <td></td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>Volatile</td>
            <td></td>
            <td></td>
            <td></td>
            <td>:heavy_check_mark:</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
    </tbody>
</table>

- Only applicable modifier for

    - local variables is final

    - constructor are public, private, protected and default

## Interfaces

- Any service requirement specification (SRS)

- It defines the set of services expected by the client

- It is 100% abstract class

- Every interface method is always public and abstract

- A class can extend only one class at a time, but can implement any number of interfaces

- An interface can extend any number of interfaces

```
interface A {

}

interface B{

}

interface C extends A, B {

}
```

```
class A extends B implements C, D, E {

}
```

- Inside interface, following are equivalent

    - ```void m1()```

    - ```public void m1()```

    - ```abstract void m1()```

    - ```public abstract void m1()```

### Interface variables

- To define requirement level constants

- It is always public static final

    - **public** to make it available for every implementation class

    - **static** no object of interface, so access is only static

    - **final** implementation class should not be allowed to change

- Variable should be initialized when class gets loaded. Two ways

    - While declaration

    - In static block

- Static block is not present for interface

```
interface IF {
    int x; // CompilerError: '=' expected
}
```

```
interface INF {
    int x = 10;
}
```

```
class Trial implements INF {
    public static void main(String[] args) {
        x = 777; // CompilerError: can not assign value to final variables

        System.out.println(x);
    }
}
```

```
class Trial2 implements INF {
    public static void main(String[] args) {
        
    }
}
```

### Interface Naming Conflicts

#### Method naming conflicts

- Case 1

    - If two interfaces have a method with same signature and return type, then in implementation class, we have to provide only one implementation

    ```
    interface left {
        public void m1();
    }

    interface right {
        public void m1();
    }

    class C implements left, right {
        public void m1() {

        }
    }
    ```

    - This is compiled without errors

- Case 2

    ```
    interface left {
        public static m1();
    }

    interface right {
        public static m1(int i);
    }

    class C implements left, right {
        // Overloaded functions
        public static m1() {

        }

        public static m1(int i) {

        }
    }
    ```

    - This will run

- Case 3

    ```
    interface left {
        public void m1();
    }

    interface right {
        public void m1();
    }
    ```

    - It is impossible to implement both interfaces simultaneously, if same signature but return types are non-covariant

#### Variable naming conflict

    ```
    interface left {
        int x = 777;
    }

    interface right {
        int x = 10;
    }

    class C implements left, right {
        public static void main(String[] args) {
            System.out.println(x); // reference to x is ambiguous

            System.out.println(left.x); // 777

            System.out.println(right.x); // 10
        }
    }
    ```

    - All interface variables are static, so can be used with interface name

#### Marker interface

- Interface having no methods, but by implementing it, an object gains some new ability

- E.g. Serializable (I), Clonable (I), RandomAccess (I), SingleThreadModel (I)

- Also known as ability interface or tag interface

- To decrease work of programmer and for simplicity of coding, work is given to JVM

- For custom marker interface, custom JVM is required

#### Adaptor Class

- A simple Java class that implements an interface with only empty implementation

```
interface x {
    m1();
    m2();
    ...
    M1000();
}
```

```
abstract class Adapter implements X {
    m1() {};
    m2() {};
    ...
    m1000() {};
}

class Trial extends Adapter {
    m3() {
        ...
    }
}
```

- Not a language level system, just a programmers' trick so implementation of just one or more methods of interface can be provided

- Increases length of readability and reduces length of code

#### Interface vs Abstract Class vs Concrete Class

- If there is no knowledge of implementation, we only have requirement specification, then go for **interface**. E.g. Servlet (I)

- If we talk only about partial implementation then go for **abstract class**. E.g. GenericServlet (AC) or HTTPServlet (AC)

- If we have complete implementation and ready to provide service, go for **concrete class**

- **Note:** Though abstract classes can not have objects, constructors are allowed in them. This constructor will be executed for initializing objects of child classes for the attributes in parent class.

<table>
    <thead>
        <tr>
            <th>Interface</th>
            <th>Abstract Class</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Requirements only (no implementation)</td>
            <td>Partial implementation</td>
        </tr>
        <tr>
            <td>Pure abstract class (every method public abstract)</td>
            <td>Methods can be concrete</td>
        </tr>
        <tr>
            <td>Not private, protected, static, synchronized, native, final, strictfp methods</td>
            <td>No restrictions on modifiers</td>
        </tr>
        <tr>
            <td>All variables are public, static, final by default</td>
            <td>No such restrictions</td>
        </tr>
        <tr>
            <td>Can't be transient or volatile</td>
            <td>No restrictions</td>
        </tr>
        <tr>
            <td>Variables should be initialized while declaring</td>
            <td>Not needed</td>
        </tr>
        <tr>
            <td>No static / instance blocks</td>
            <td>Allowed</td>
        </tr>
        <tr>
            <td>Constructor not allowed</td>
            <td>Allowed</td>
        </tr>
    </tbody>
</table>

- **Note:** Whenever we are creating child class object, parent and child class constructors will both be used for creating the child class object. Parent class object will not be created.