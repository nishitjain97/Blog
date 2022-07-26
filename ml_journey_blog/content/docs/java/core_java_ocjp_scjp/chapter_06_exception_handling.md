---
title: 6. Exception Handling
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-09-01'
lastmod: '2020-09-01'
---

## Introduction

- Any unwanted, unexpected event that disturbs normal flow of a program is an exception

- Main objective is graceful termination of program

## Runtime stack mechanism

- For each thread, JVM creates runtime stack

- Each method call results in stack frame of that method being stored into run-time stack

- Completion of method results in deletion of the stack entry of that method

- Completion of every method and finally main method is at the end followed by distruction of stack by JVM

## Default exception handling

- Inside a method if exception occurs, the method is responsible to create Exception object by including

    - Name of exception

    - Description

    - Location (stack trace) of exception

- Method hands over exception object to JVM

- JVM checks for exception handling code in that method or terminates the method and removes entry from the stack

- JVM repeats this tile all methods are removed from the stack (including main)

- If not handled program is terminated abruptly

## Exception Hierarchy

- Throwable class is the root of Java Exception Hierarchy

- Exception are caused by the program and are recoverable

- Errors are not caused by the program and are mostly due to lack of system resources. They are non-recoverable


<div>
    <img src="/docs/java/core_java_ocjp_scjp/exception_hierarchy.png" style="height:300px;margin:auto;">
</div>

## Checked and unchecked exceptions

```
import java.io.*;

class Test {
    public static void main(String[] args) {
        PrintWriter pw = new PrintWriter("abc.txt");
        pw.println("Hello");
    }
}

// CompilerError: unreported error java.io.FileNotFoundException must be caught or declared to be thrown
```

- Exception checked by compiler for smooth working of program. They should be handled by try-catch, or throws keyword

- Exception not checked by compiler are unchecked exceptions. E.g. ArithmeticException and its child classes, RuntimeError and its child classes etc.

- If checked exception has all its child classes also checked, it is completely checked exception, else it is partially checked exception

## Customized Exception Handling (try-catch)

```
try {
    risky code
}
catch(Exception e) {
    handling code
}
```

- In try block, if exception occurs, the catch block will execute and rest of the try block will not execute. Hence, length of the try block should be as little as possible

- Exception can arise in catch block also and will cause abnormal termination of program

## Methods to print Exception information

```
class Test {
    public static void main(String[] args) {
        try {
            System.out.println(10 / 0);
        }
        catch(ArithmeticException e) {
            e.printStackTrace(); // java.lang.ArithmeticException: / by zero
                                 // at Test.main(Test.java 7)

            System.out.println(e) or System.out.println(e.toString()); // java.lang.ArithmeticException: / by zero

            System.out.println(e.getMessage()); // / by zero
        }
    }
}
```

## Try with multiple catch

- Best programming practice

```
try {
    risky code
}
catch(ArithmeticException e) {
    //
}
catch(SQLException e) {
    //
}
catch(Exception e) {
    //
}
```

```
try {
    risky code
}
catch(Exception e) {
    //
}
catch(ArithmeticException e) { // CompilerError: java.lang.ArithmeticException has already been caught
    //
}
```

- For multiple catch blocks, order is important

## Finally block

- Works with try-catch, and contains clean-up code

- It will be executed irrespective of exception occurring or not, exception handled or not

- **Note:** For try-catch-finally, curly braces are mandatory

## Throw keyword

- Used to hand-over an exception to JVM manually, after explicitly creating exception object

    ```throw new ArithmeticException("/ by zero");```

- Best use is for customized exceptions

```
class Test {
    static ArithmeticException e = new ArithmeticException();

    public static void main(String[] args) {
        throw e; // RuntimeError: ArithmeticException
    }
}
```

```
class Test {
    static ArithmeticException e;

    public static void main(String[] args) {
        throw e; // RuntimeError: NullPointerException
    }
}
```

```
class Test {
    public static void main(String[] args) {
        System.out.println(10 / 0); // RuntimeError: / by zero
        System.out.println("Hello");
    }
}
```

```
class Test {
    public static void main(String[] args) {
        throw new ArithmeticException();

        System.out.println("Hello"); // CompilerError: unreachable statement
    }
}
```

```
class Test {
    public static void main(String[] args) {
        throw new Test(); // CompilerError: incompatible types found: test, required: java.lang.Throwable
    }
}
```

```
class Test extends RuntimeError {
    public static void main(String[] args) {
        throw new Test(); // RuntimeError: Exception in thread "main" Test at Test.main
    }
}
```

## Throws keyword

- Throws keyword is used to delegate responsibility of exception handling to the caller

```
class Test {
    public static void main(String[] arsg) throws InterruptedException {
        Thread.sleep(10000);
    }
}
```

- Used only for checked exceptions

- Applicable for methods and constructors, but not for classes

- Applicable only for throwable classes

```
class Test {
    public static void main(String[] args) throws Test {
        // CompilerError: incompatible types found: Test, required: java.lang.Throwable
    }
}
```

- In a try-block, if there is no chance of an exception, we can not catch that exception (applicable for fully checked exceptions)

## Different CompilerError in Exception handling

- Unreported exception xxx

- Exception xxx has already been caught

- Exception xxx is never thrown in body of corresponding try statement

- unreachable statement

- incompatible types found: xxx, required: java.lang.Throwable

- try without catch or finally

- catch without try

- finally without try

- IllegalArgumentException

    - Child of RuntimeException, hence unchecked

    - Risen explicitly by programmer or API developer, when method is invoked using illegal argument

- NumberFormatException

    - Direct child class of IllegalArgumentException

    - Risen explicitly

    - Improper formatting of string to be converted to number

        ```
        int i = Integer.parseInt("10");
        int j = Integer.parseInt("ten"); // RuntimeError: NumberFormatException
        ```

- IllegalStateException

    - Child of RuntimeException (unchecked)

    - Risen explicitly to indicate invocation of method at the wrong time

- AssertionError

    - Child class of Error (unchecked)

    - Risen to indicate that assert statement failed

## Customized or user defined exception

```
class CustExceptions extends RuntimeException {
    CustException(String s) {
        super(s); // Exception description
    }
}

class Test {
    public static void main(String[] args) {
        if(true) {
            throw new CustException("Hello");
        }
    }
}
```

## Enhancements in 1.7v

- try with resources

    ```
    try(BufferReader br = new BufferReader(new FileReader("input.txt"))) { // br is resource
        // uses br
    }
    catch(IOException e) {
        // handling
    }
    ```

    - Before v1.7, finnaly block was required to free up resources opened within try explicitly by programmer

    - After v1.7, the resouces in resources block are closed (freed) automatically on normal / irregular end of try block

    - Syntax: resources are separated by semi-colon
    ```
    try(R1; R2; R3) {

    }
    ```

    - The resouces should implement AutoClosableInterface. All pre-defined resources implement this.

    - All resource reference variables are implicitly final and can not be reassigned

    - Before v1.7, try without catch / finally was not allowed. Now, try with resources, without catch / finally is allowed

- Multi-catch block

    - Allows single catch block for different types of exceptions

    - Reduces length of code

    ```
    try {
        //
    }
    catch(ArithmeticException | IOException e) {
        e.printStackTrace();
    }
    ```