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