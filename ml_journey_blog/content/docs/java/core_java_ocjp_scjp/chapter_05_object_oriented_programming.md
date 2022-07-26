---
title: 5. Object Oriented Programming
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-08-29'
lastmod: '2020-08-29'
---

## Data Hiding

- Outsider can't access internal data directly. It can be done only after authorization.

```
public class Account {
    private double balance;

    public double getBalance() {
        // Validation of authorization
        return balance;
    }
}
```

- Helps in security

- Highly recommended to declare data members as private

### Abstraction

- Hiding internal implementation and showing the services that we provide

- Advantages

    - Security

    - Easier enhancement

    - Improves easiness for users

    - Maintenance is easier

### Encapsulation

- Binding data and corresponding methods into a single unit

    - Encapsulation = Data hiding + Abstraction

```
public class Account {
    private double balance;
    public double getBalance() {
        // validation

        return balance;
    }

    public void setBalance(double balance) {
        // validation

        this.balance = balance;
    }
}
```

- Advantages

    - Security

    - Easier enhancement

- Every variable of a class, if declared private, then class is tightly encapsulated

- If parent class is not tightly encapsulated, none of the child class can be tightly encapsulated

## Inheritance

- Also known as 'is-a' relationship

- Done using 'extends' keyword

- Code reusability

```
class P {
    public void m1() {
        System.out.println("Parent");
    }
}

class C extends P {
    public void m2() {
        System.out.println("Child");
    }
}

class Test {
    public static void main(String[] args) {
        P p = new P();
        p.m1();
        p.m2(); // CompilerError: cannot find
                // symbol: method m2()
                // location: class P

        C c = new C();
        c.m1();
        c.m2();

        P p1 = new C();
        p1.m1();
        p1.m2(); // CompilerError: cannot find
                 // symbol: method m2()
                 // location: class P

        C c = new P(); // CompilerError: incompatible types
                       // found: P
                       // required: C
    }
}
```

- Java API is totally implemented based on inheritance

- **Note:** Object class contains 11 methods

### Multiple inheritance

- Java does not provide support for multiple inheritance

    ```
    class A extends B {
    }
    ```

    - The above will not be represented as
    <div>
        <img src="/docs/java/core_java_ocjp_scjp/inheritance1.png" style="height:300px;margin:auto;">
    </div>

    - But will be represented as
    <div>
        <img src="/docs/java/core_java_ocjp_scjp/inheritance2.png" style="height:300px;margin:auto;">
    </div>

    - A java class is the direct child of Object class only when it does not extend any other class

    - There may be a chance for ambiguity problem

    ```
    class P1 {
        public void m1();
    }

    class P2 {
        public void m1();
    }

    class C extends P1, P2 {
        public void m() {
            C c = new C();
            c.m1(); // Ambiguous
        }
    }
    ```

    - **Note:** Through interfaces, we do not get inheritance as there is no code reusability

    - **Note:** Cyclic inheritance is not allowed in Java

    ```
    class A extends A {

    }
    ```

    ```
    class A extends B {

    }

    class B extends A {

    }
    ```

## 'Has-a' relationship

- Most widely used

- Also known as composition or aggregation

- No specific keyword for implementation. Mainly 'new' keyword is used

- Helps in code reusability

```
class Engine {
    // engine specific functionality
}

class Car {
    Engine e = new Engine();
}

// Car 'has-a' engine
```

### Composition vs Aggregation

- If university closes, all departments are shub down, i.e., they cannot function without a university. This **strong association** is called composition.

- In aggregation, **weak association** takes place, i.e., contained objects can exist without container object.

### 'is-a' vs 'has-a'

- 'Is-a' relation is used when total function is to be reused

- 'Has-a' relation is used when partial functionality is to be reused

```
class Demo {
    // methods
}

class Trial extends Demo {
    // IS-A relationship
    // demo methods
}
```

```
class Test {
    public void m1() {}

    public void m2() {}
}

class Trial {
    public void m() {
        Test t = new Test();
        t.m1(); // Specific functionality
        t.m2();
    }
}
```

### method signature

- Method name

- Argument types

- Return types, modifiers etc. are not part of the signature

```
public static int m1 (int i, float f); // m1, int and float are part of method signature
```

- Compiler will use method signature to resolve method calls

```
class Test {
    public void m1(int i) {

    }

    public void m2(String s) {

    }
}

Test t = new Test();
t.m1(10);
t.m2("Nishit");
t.m3(10.5); // CompilerError: cannot find symbol
            // method: m3(double)
            // location: class Test
```

```
class Test {
    public static void m1(int i) {
        // m1(int)
    }

    public static int m1(int x) {
        // m1(int)
    }

    // CompilerError: m1(int) is already defined
}
```

### Overloading

- Two methods having same name but different arguments

- Makes programming easier by providing flexibility to programmers

```
class Test {
    public void m1() {
        System.out.println("No-args");
    }

    public void m1(int i) {
        System.out.println("Int arg");
    }

    public void m1(double d) {
        System.out.println("Double arg");
    }

    public static void main(String[] args) {
        Test t = new Test();

        t.m1(); // No-args
        t.m1(10); // Int arg
        t.m1(10.5); // Double arg
    }
}
```

- In overloading, method resolution is done by compiler based on reference type. Hence, it is called compile-time polymorphism, static polymorphism or early binding.

- Case 1: Automatic promotion in overloading

    ```
    class Test {
        public void m1(int i) {
            System.out.println("Int-args");
        }

        public void m1(float f) {
            System.out.println("Float-args");
        }

        public static void main(String[] args) {
            Test t = new Test();

            t.m1(10); // Int-args
            t.m1(10.5); // Float-args
            t.m1('a'); // int-args
            t.m1(10l); // float-args
            t.m1(10.5); // CompilerError: Can not find
                        // symbol: method m1(double)
                        // location: class Test
        }
    }
    ```

    - Priority

        - Exact match

        - Type conversion then match

        - Compiler error

- Case 2: Child class will be given preference over parent class
    ```
    class Test {
        public void m1(String s) {
            System.out.println("String");
        }

        public void m1(Object o) {
            System.out.println("Object");
        }

        public static void main(String[] args) {
            Test t = new Test();

            t.m1(new Object()); // Object
            t.m1("Nishit"); // String
            t.m1(null); // String
        }
    }
    ```

- Case 3: 
    ```
    class Test {
        public void m1(String s) {
            System.out.println("Nishit");
        }

        public void m1(StringBuffer s) {
            System.out.println("StringBuffer");
        }

        public static void main(String[] args) {
            Test t = new Test();

            t.m1("Nishit"); // Nishit
            t.m1(new StringBuffer()); // StringBuffer
            t.m1(null); // CompilerError: reference to m1() is ambiguous
        }
    }
    ```

    - null is valid value for both String and StringBuffer

- Case 4
    ```
    class Test {
        public void m1(int i, float f) {
            System.out.println("Int float");
        }

        public void m1(float f, int i) {
            System.out.println("Float int");
        }

        public static void main(String[] args) {
            Test t = new Test();

            t.m1(10, 10.5); // Int float
            t.m1(10.5, 10); // Float int
            t.m1(10, 10); // CompilerError: reference to m1() ambiguous
            t.m1(10.5f, 10.5f); // CompilerError: cannot find symbol
                                // symbol: method m1(float, float)
                                // location: class Test
        }
    }
    ```

- Case 5: Var-arg will get least priority in general. This is because var-arg is modern feature and the preference is for a program to be backwards compatible
    ```
    class Test {
        public void m1(int i) {
            System.out.println("Int");
        }

        public void m1(int... x) {
            System.out.println("Var-args");
        }
        
        public static void main(String[] args) {
            Test t = new Test();

            t.m1(); // Var-args
            t.m1(2, 2); // Var-args
            t.m1(2); // int
        }
    }
    ```

### Overriding

- The methods available in parent class are by default available to child class through inheritance. In case child is not satisfied with the implementation, the child can redefine th eimplementation by method overriding process.

```
class P {
    public void m1() {
        System.out.println("Parent m1");
    }

    public void m2() {
        System.out.println("Parent m2");
    }
}

class C extends P {
    public void m2() { // Overridden
        System.out.println("Child m2");
    }
}

class Test {
    public static void main(String[] args) {
        P p = new P();
        p.m2(); // Parent m2

        C c = new C();
        c.m2(); // Child m2

        P p1 = new C();
        p1.m2(); // Child m2
    }
}
```

- Compiler will check in P if m2() method is present, as compiler checks using reference object type.

- JVM will check run-time object (child here) for m2() method. If c is not overriding, parent m2() is by default available to it and will execute, else child m2() will be executed by JVM.

- In overriding, method resolution is based on run-time object. Hence, it is called run-time polymorphism, dynamic polymorphism or late binding

- Rules for overriding

    - Method names and argument types, i.e., method signature must be same

    - Till version 1.4, return type had to be same. From 1.5 onwards, co-variant return types are also allowed.

    - **Note:** co-variant is equivalent to child class
    ```
    class P {
        public Object m1() {
            return null;
        }
    }

    class C extends P {
        public String m1() {
            return null;
        }
    }
    ```

    - Not applicable for private methods

    - Not applicable for final methods

    - Abstract method should be overridden to provide implementation

    - Non-abstract methods can be overriden as abstract

    - Synchronized to non-synchronized and vice versa is allowed

    - Native to non-native and vice versa are allowed

    - strictfp to non-strictfp and vice versa are allowed

    - Can not reduce access privileges after overriding

        private > default > protected > public

- Exception handling

    - Allowed <br> P: public void m1() throws Exception <br> C: public void m1()

    - Not allowed <br> P: public void m1() <br> C: public void m1() throws Exception

    - Allowed <br> P: public void m1() throws Exception <br> C: public void m1() throws IOException

    - Not allowed <br> P: public void m1() throws IOException <br> C: public void m1() throws Exception

    - Allowed <br> P: public void m1() throws IOException <br> C: public void m1() throws FileNotFoundException, EOFException

    - Not allowed <br> P: public void m1() throws IOException <br> C: public void m1() throws EOFException, InterruptedException

    - Allowed <br> P: public void m1() throws IOException <br> C: public void m1() throws ArithmeticException, NullPointerException

- If child class method throws any checked exception, parent class should throw same or its parent exception

- No such rule present for unchecked exception

- **Note:** CompilerError: m1() in C cannot override m1() in P <br> Overridden method does not throw xyz Exception

- Cannot override static as non-static

- If both overriden and overriding methods are static, it is not overriding, it is method hiding

#### Overriding w.r.t. var-args methods

```
class P {
    public void m1(int... x) {
        System.out.println("Parent");
    }
}

class C extends P {
    public void m1(int x) {
        System.out.println("Child");
    }
}

class Test {
    public static void main(String[] args) {
        P p = new P();

        p.m1(10); // Parent

        C c = new C();
        c.m1(10); // Child

        P p1 = new C();
        p1.m1(10); // Parent
    }
}
```

- This is not overriding but overloading, because for overriding the method name and arguments (method signature) must be the same. Overriding var-args can only be done with another var-args method. Hence, the reference type will decide the method.

#### Overriding w.r.t. variables

```
class P {
    int x = 100;
}

class C extends P {
    int x = 200;
}

class Test {
    public static void main(String[] args) {
        P p = new P();
        System.out.println(p.x); // 100

        C c = new C();
        System.out.println(c.x); // 200

        P p1 = new C();
        System.out.println(p1.x); // 100
    }
}
```

- Overriding is only done for methods. Variable resolution is done by compiler based on reference type, whether variables are static or non-static

#### Overloading vs Overriding

<table>
    <thead>
        <tr>
            <th>
            Property
            </th>
            <th>
            Overloading
            </th>
            <th>
            Overriding
            </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
            Method name
            </td>
            <td>
            Same
            </td>
            <td>
            Same
            </td>
        </tr>
        <tr>
            <td>
            Argument type
            </td>
            <td>
            Different (at least order)
            </td>
            <td>
            Same
            </td>
        </tr>
        <tr>
            <td>
            Method signature
            </td>
            <td>
            Different
            </td>
            <td>
            Same
            </td>
        </tr>
        <tr>
            <td>
            Return types
            </td>
            <td>
            No restrictions
            </td>
            <td>
            Same as covariant
            </td>
        </tr>
        <tr>
            <td>
            Private, static, final methods
            </td>
            <td>
            Allowed
            </td>
            <td>
            Not allowed
            </td>
        </tr>
        <tr>
            <td>
            Access modifiers
            </td>
            <td>
            No restrictions
            </td>
            <td>
            Same or increased scope
            </td>
        </tr>
        <tr>
            <td>
            Throws clause
            </td>
            <td>
            No restrictions
            </td>
            <td>
            Child class throws checked exception, parent should throw same or parent exception. <br>
            No restrictions for unchecked exceptions.
            </td>
        </tr>
    </tbody>
</table>

### Polymorphism

- One name, multiple functions

- Examples

    - Overriding

    - Overloading

    - Parent reference to hold child object

### Coupling

- The degree of dependency between components

- Loosely coupled or tightly coupled

```
class A {
    static int i = B.j;
}

class B {
    static int j = C.k;
}

class C {
    static int k = D.m1()
}

class D {
    public static int m1() {
        return 10;
    }
}

// They are tightly coupled
```

- Tight coupling or greater dependence is bad programming practise

### Cohesion

- High cohesion is having individual components with clear, well-defined functionality

## Object Type-casting

- We can use parent reference to hold child object

- Interface reference can hold implemented class object

- Type casting syntax is of the form:
    
    - A b = (C) d;

    - Where A and C are Class / Interface, b and d are reference variables

- Compiler will check

    - d and C must have some relation, else <br> CompilerError: inconvertible types <br> found: d type <br> required C

    - c should be derived type of A or same as A, else CompilerError

- JVM will check

    - Underlying object type of d must be either C or derived type of C, else <br> RuntimeError: ClassCastException

- Through type-casting, we are not creating any new object. Another type of reference variable is being made for existing object

## Static Control Flow

- Order in which statements will get executed

```
class Base {
    static int i = 10; // 1
    // i = 0 [Read Indirectly Write Only]
    // j = 0 [Read Indirectly Write Only]
    // i = 10 [Read and Write], 7

    static { // 2
        m1(); // 8
        System.out.println("First static block"); // 10
    }

    public static void main(String[] args) { // 3
        m1(); // 13
        System.out.println("Main method"); // 15
    }

    public static void m1() {  // 4
        System.out.println(j); // 9, 14
    }

    static { // 5
        System.out.println("Second static block"); // 11
    }

    static int j = 20; // 6
    // j = 20 [Read and Write], 12
}
```

- The flow will be as follows

    - Identification of static members from top to bottom [1 to 6]

    - Execution of static variable assignments and static blocks from top to bottom [7 to 9]

    - Execution of main method [13 to 15]

### Read Indirectly Write Only [RIWO]

- Inside a static block, if variable is read, it is direct read

- Inside static block, a method is called and in this method if a variable is read, it is indirect read

- If variable is identified but not assigned a value, it is RIWO

- RIWO can be read indirectly, but direct read causes CompilerError: illegal forward reference

### Static blocks

- Executed at the time of class loading

- Needed for implementing native methods or default drivers

### Static Control Flow (In Parent and Child Classes)

- Identification of static members from parent to child

- Execution of variable assignments and static blcok from parent to child

- Execution of child main method (when child class is executed)

## Instance Control Flow

```
class Test {
    int i = 10; // 3: i = 0 [Read Indirectly Write Only], 9: i = 10 [Read and Write]

    { // 4
        m1(); // 10
        System.out.println("First instance block"); // 12: First instance block
    }

    Test() { // 5
        System.out.println("Constructor"); // 15
    }

    public static void main(String[] args) { // 1
        Test t = new Test; // 2
        System.out.println("Main"); // 16
    }
    
    public void m1() { // 6
        System.out.println(j); // 11: 0
    }

    { // 7
        System.out.println("Second instance block"); // 13: Second instance block
    }

    int j = 20; // 8: j = 10 [Read Indirectly Write Only], 14: j = 20 [Read & Write]
}
```

- If object is not created, only static will execute and nothing will happen

- If object is created:

    - Identification of isntance member from top to bottom [3 - 8]

    - Execution of instance variable assignment and instance block from top to bottom [9 - 14]

    - Execution of constructor

- For every object created, all three steps will be repeated. Hence, object creation is the most costly operation and is not recommended without specific needs.

## Inheritance Control Flow

- Flow is as follows

    - Identification of instance members from parent to child

    - Execution of instance variable assignments and instance blocks in parent

    - Execution of parent constructor

    - Execution of instance variable assignment and instance blocks in child

    - Execution of child constructor

- Ways to create an object

    - Using new operator

        ```Test t = new Test();```

    - Using newInstance() method

        ```Test t = (Test)Class.forName("Test").newInstance();```

    - By using factor method

        ```
            Runtime r = Runtime.getRuntime();
            Dateformat df = Dateformat.getInstance();
        ```

    - clone() method

        ```
            Test t = new Test();
            Test t2 = (Test)t.clone();
        ```

    - Using deserialization

        ```
            FileInputStream fis = new FileInputStream("abs.ser");
            ObjectInputStream ois = new ObjectInputStream(fis);

            Test t = (Test)ois.readObject();
        ```

## Constructor

- Used to initialise object

- Only applicable modifier are public, private, protected and default

- Default constructor is responsibility of compiler, not JVM

- Prototype of default constructor

    - no-arg

    - access modifier same as class modifier

    - contains only one line of code

        ```
            Test() {
                super();
            }
        ```

- First line inside every constructor should be either super(); or this();, else compiler will automatically place super();

- ```super()``` or ```this()``` should only be inside constructor, else CompilerError: call to super must be first statement in constructor

- Inheritan ce and overriding not applicable for constructors

- Every class (including abstract) can contain an constructor. Interfaces cannot

- Recursive method call is a run-time error, only if that method is called once.

- Recursive constructor call is a compile-time error

```
class Test {
    Test() {
        this(10);
    }

    Test(int i) {
        this();
    }

    public static void main(String[] args) {
        System.out.println("Hello");
    }

    // CompilerError: Recursive constructor invocation
}
```

```
class P {
    P(int i) {

    }
}

class C extends P {

}

// CompilerError: Cannot find symbol
// symbol: constructor
// location: class P
```

- If parent class constructor throws a checked exception, child class constructor should also throw similar or parent exception mandatorily

## Singleton Classes

- For any java class, if we are allowed to create only one object. E.g. Runtime, BusinessDelegate, ServiceLocator etc.

- To reuse single object for all similar requirements

```
class Test {
    private static Test t = new Test();

    private Test() {

    }

    private static Test getTest() {
        return t;
    }
}
```

- To prevent inheritance without using final, declare constructor as private