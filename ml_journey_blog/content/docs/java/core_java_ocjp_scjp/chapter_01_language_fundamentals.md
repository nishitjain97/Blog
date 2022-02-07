---
title: 1. Java Language Fundamentals
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-08-01'
lastmod: '2020-08-02'
---

## Identifiers

- These are names used for identification purpose

- This includes method name, class name and label name

- E.g.
```
class Test {
    public static void main(String[] args) {
        int n = 10;
    }
}
```

### Rules for Java Identifiers

- a to z

- A to Z

- 0 to 9

- $

- _

- Can't start with a digit

- Case sensitive

- No length limit

- Keywords can't be used

## Reserved Words

- All use only characters as letter

- All are lowercase

<div>
    <img src="/docs/java/core_java_ocjp_scjp/reserved_words_tree.png" style="height:300px;margin:auto;">
</div>

### Reserved Literals

- ```true```

- ```false```

- ```null```

### Keywords

#### Unused

- ```goto```

- ```const```

#### Used

##### Data Types (8)

- ```byte```

- ```short```

- ```int```

- ```long```

- ```float```

- ```double```

- ```boolean```

- ```char```

##### Modifiers (11)

- ```public```

- ```private```

- ```protected```

- ```static```

- ```final```

- ```abstract```

- ```synchronized```

- ```native```

- ```strictfp```

- ```transient```

- ```volatile```

##### Class-related (6)

- ```class```

- ```extends```

- ```interface```

- ```implements```

- ```package```

- ```import```

##### Object-related (4)

- ```new```

- ```instanceof```

- ```super```

- ```this```

##### Flow control (11)

- ```if```

- ```else```

- ```switch```

- ```case```

- ```default```

- ```while```

- ```do```

- ```for```

- ```break```

- ```continue```

- ```return```

##### Exception Handling (6)

- ```try```

- ```catch```

- ```finally```

- ```throw```

- ```throws```

- ```assert```

##### Return type

- ```void```

##### Enumerator

- ```enum```

    - To define a group of named constants

## Data Types

- Java is a strongly typed language

    - Each assignment is checked by compiler for type compatibility

<div>
    <img src="/docs/java/core_java_ocjp_scjp/data_types_tree.png" style="height:300px;margin:auto;">
</div>

### Integral Data Types

#### Byte

- 8 bits

- -128 to 127

- Useful for streams of input/output

#### Short

- 2 bytes

- $-2^{15}$ to $2^{15}-1$ $\equiv$ -32768 to 32767

#### Int

- 32 bits

- -2147483648 to 2147483647

#### Long

- 64 bits

- $-2^{63}$ to $2^{63}-1$

### Floating Point Data Types

#### Float

- 5-6 places

- Single precision

- 4 bytes

#### Double

- 14-16 places

- Double precision

- 8 bytes

### Non-Integral Data Types

#### Char

- Size is 2 bytes because uses UNICODE

- Escape characters are valid char literals

- 8 escape characters

    - \n - new line

    - \t - horizontal tab

    - \r - carriage return

    - \b - backspace

    - \f - form feed

    - \\' - single quote

    - \\" - double quote

    - \\\ - backslash

#### String literal

- Any sequence of characters in double quotes

**Note:** Java 1.7 version literal enhancements

- For integral data types, we can specify literal values, along with dec, hex, octal etc in binary also

    - E.g. ```int x = OB1111;``` or ```int x = ob1111;```

- Usage of underscore in numeric literals

**Note:**
- Acceptable assignments

    - Byte (1B) to Short (2B)

    - Short (2B) to Int (4B)

    - Char (2B) to Int (4B)

    - Int (4B) to Long (8B) to Float (4B) to Double (8B)

- 8B integral long can be stored in 4B float variable because both follow different memory representation internally

## Arrays

- It is an indexed collection of fixed number of homogeneous data elements

- It can represent a large number of values using single variable name, thereby improving readability of code

    - E.g. instead of creating ```customer1```, ```customer2```, ..., n for very large number of customers, we can create a ```customer``` array

- One dimensional array declaration

    - ```int[] x;``` (recommended)

    - ```int []x;```

    - ```int x[];```

- Two-dimensional array declaration

    - ```int[] a, b;``` (a = 1-D, b = 2-D)

    - ```int[] a[], b;``` (a = 2-D, b = 1-D)

    - ```int[] a[], b[];``` (a = 2-D, b = 2-D)

    - ```int[] []a, b;``` (a = 2-D, b = 2-D)

    - ```int[] []a, b[];``` (a = 2-D, b = 3-D)

    - ```int[] []a, []b;``` (incorrect)

- In Java, two dimensional array is an array of arrays, not a matrix. This saves memory space. E.g.

```
int[][] x = new int[3][]; // Initialize a 2-D array as 3 1-D arrays
x[0] = new int[5]; // Initialize first 1-D array with 5 elements
x[1] = new int[2]; // Initialize second 1-D array with 2 elements
x[2] = new int[8]; // Initialize third 1-D array with 8 elements
```

**Note:**

- When we print a reference variable, the ```toString()``` method gets called

    - E.g.

    ```
    int[] x = new int[3];

    System.out.println(x); // [I@hashcode or classname@hashcode
    System.out.println(x[0]); // 0 (default value for int)
    ```

    ```
    int[][] x = new int[3][2];
    System.out.println(x); // [[I@hashcode
    System.out.println(x[0]); // [I@hashcode
    System.out.println(x[0][0]); // 0
    ```

- We can create, declare and initialize array in a single line

    - E.g.

    ```
    int[] x = {1, 2, 5, 8};
    char[] ch = {'a', 'e', 'i', 'o', 'u'};

    int[][] x = {{1, 2}, {3, 4, 5}}
    ```

**Note:** ```length``` vs ```length()```

- ```length``` variable is a final variable for the size of an array

- ```length()``` is for Objects array. It is a final method in string class and returns number of characters in a string

**Note:** There is no direct way to specify length of multi-dimensional arrays

**Note:** Anonymous arrays

- They have no name

- They are created instantly, for one-time use

    - E.g.
    
    ```
    class Test {
        public static void main(String[] args) {
            sum(new int[] {10, 20, 30}); // Anonymous array
        }

        public static void sum(int[] x) {
            int ans = 0;

            for(int x1: x) {
                total += x;
            }
        }
    }
    ```

### Array and element types

<div>
    <img src="/docs/java/core_java_ocjp_scjp/array_types.png" style="height:300px;margin:auto;">
</div>

**Note:** Element-level promotion is not applicable at array level

## Types of Variables

- Based on value represented

    - Primitive

    - Reference

- Based on behavior

    - Instance

    - Static

    - Local

### Instance Variables

- Value varies from object to object

- Declared in class directly, but outside any block or constructor

- Created at the time of object creation

- Stored in heap memory

- Can't be accessed directly from static area, but can be accessed using object reference

- Can be accessed directly from instance area

    - E.g.

    ```
    class Test {
        int x = 10;

        public static void main(String[] args) {
            System.out.println(x); // Compiler Error: non-static variable can't be accessed from static area

            Test t = new Test();
            System.out.println(t.x); // 10
        }

        public void m() {
            System.out.println(x); // 10
        }
    }
    ```

- JVM provides default values for instance variables

- They are also known as object-level variables or attributes

### Static Variables

- If value of variable does not vary with object, declare them as static

- Lasts till class file lasts

- Stored in method area of memory

- They are also known as class-level variables or fields

### Local Variables

- Temporary requirement inside methods, blocks or constructors

- Stored in stack

- They are also known as stack variables or automatic variables

- Considered thread safe variables because different variables are created for each thread

- Required explicit initialization, i.e., no default values provided

- E.g.

```
class Test {
    public static void main(String[] args) {
        try {
            int j = Integer.parseInt("ten");
        }
        catch(NumberFormatException e) {
            j = 10; // CompilerError: Couldn't find symbol; symbol: variable j; location: class Test
        }
        System.out.println(j); // CompilerError: Couldn't find symbol; symbol: variable j; location: class Test
    }
}
```

- E.g.

```
class Test {
    public static void main(String[] args) {
        int x;
        System.out.println(x); // CompilerError: Variable x might not have been initialized
    }
}
```

### Uninitialized Arrays

- Once array is created, every object has a default value, even if it is a local array

### Var-arg method

- Variable number of arguments

- E.g.

```
class Test {
    public static void m1(int... a) {
        System.out.println("var-args");
    }

    public static void main(String[] args) {
        m1();
        m1(10);
        m1(10, 20, 30);
        m1(10, 20, 30, 100, 120);
    }
}
```

- Normal parameters can be mixed with var-arg parameter

    - Var-arg needs to be at the end of declaration

- Internally, var-args get converted to one-dimensional array

**Note:** To provide compatibility with older versions, if there is a conflict between an older function and a newer function, older function will prevail

- Var-args method has least priority

- E.g.

```
class Test {
    public static void m1(int... x) {
        System.out.println("V");
    }

    public static void m1(int x) {
        System.out.println("G");
    }

    public static void main(String[] args) {
        m1(); // V
        m1(10, 20); // V
        m1(10); // G (older feature)
    }
}
```

- ```m1(int... x)``` $\equiv$ ```int[] x```

- ```m1(int[]... x)``` $\equiv$ ```int[][] x```

### Main method

- Not checked by compiler. At run-time, JVM checks existance of main method.

```
class Test {
    public static void main(String[] args) {
        // public: to call from anywhere (since JVM calls it at the start of program execution)

        // static: to call without an object

        // void: returns nothing
    }
}
```

- Also works as

```
class Test {
    public static void main(String... args) {

    }
}
```

- Additional modifiers can be applied, it will still be a valid program

```
class Test {
    static final synchronized strictfp public void main(String... args) {

    }
}
```

- Main method can be overloaded, but JVM will always call the one with ```String[] args```

- Inheritance applicable for main method

```
class P {
    public static void main(String[] args) {

    }
}

class C extends P {
    // p.java
    // Running javac P.java will give P.class and C.class
    // java P; Valid call from command line
    // java C; Also valid call from command line (will use main() inherited from P)
}
```

```
class P {
    public static void main(String[] args) {
        System.out.println("Parent");
    }
}

class C extends P {
    public static void main(String[] args) {
        System.out.println("Child");
    }
}

// javac P.java will give P.class and C.class
// java P will print Parent
// java C will print Child
```

- **Note:** For main method, inheritance, overloading and method hiding are applicable, over-riding is not applicable

### Command Line Arguments

- JVM makes string arrays with command line arguments and pass them to main method

- Main objective is to customize behavior of the main method

### Java Coding Standards

- When writing any component, the name should represent the purpose of the component

- Improved readability and maintainability of code

- Coding standard for classes

    - Names are nouns

    - Should start with uppercase character

    - For multiple words, inner word should start with uppercase. E.g. StringBuffer

- Coding standard for interfaces

    - Usually adjectives

    - Start with uppercase

    - Inner word start with uppercase

- Coding standards for methods

    - Names are either verbs or verb-noun combination

    - Start with lowercase

    - Inner words start with capital (camel case)

- Coding standards for variable names

    - Usually nouns

    - Camel case

- For constants

    - usually nouns

    - bold letters

    - multiple words separated by underscore

- JavaBean coding standards

    - Java class with private vairables and public getter and setter methods

    - E.g.
    ```
    public class StudentBean {
        private String name;

        public void setName(String name) {
            this.name = name;
        }

        public String getName() {
            return name;
        }
    }
    ```

    - Syntax for setter method

        - public

        - void

        - name prefixed with set

        - should not be no-argument method

    - Syntax for getter method

        - public
        
        - have a return type

        - name prefixed with get

        - no-argument method

- **Note:** For boolean properties, ```isEmpty()``` is meaningful instead of ```getEmpty()```