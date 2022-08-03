---
title: 9. Java.Lang Package
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-09-22'
lastmod: '2020-09-22'
---

## Introduction

- The most common classes and interfaces are grouped into a separate package. This is the ```java.lang``` package.

- This package is available to all java programs by default

## Object class
```java.lang.Object```

- Every class in java is either the direct or indirect sub-class of Object class

- The most commonly needed methods for every java class are defined in Object class

- Methods

    - ```public String toString()```: When we print any object reference, this method is called. It gives string representation of object

    - ```public native int hashCode()```: The Object class hashCode() generates int based on address of the object. However, we can override hashCode() to generate our own.

    - ```public boolean equals(Object obj)```
        - Ths Object class equals() method compares the references of the objects

        ```
        Student S1 = new Student("N", 10);
        Student S2 = new Student("N", 10);
        Student S3 = new Student("A", 20);
        Student S4 = S1;

        System.out.println(S1.equals(S2)); // false
        System.out.println(S1.equals(S3)); // false
        System.out.println(S1.equals(S4)); // false
        ```

        - When overriding equals() method, we need to take care of the following
        
            - Meaning of equality according to our needs

            - Return false if the argument belongs to different class than calling object (ClassCastException)

            - Handle null argument (NullPointerException)

        - StringBuffer does not override equals() method

    - ```public final Class getClass()```

        - We can use this method to get runtime class definition of the object

        - We can then use the class object to get class level properties

        - We use it frequently in reflections API

    - ```protected void finalize() throws Throwable```

        - Before destroying an object, garbage collector calls finalize method to conduct clean-up activities

    - ```wait()```

    - ```notify()```

    - ```notifyAll()```

        - All three above used for interthread communication

    - ```protected native Object clone() throws CloneNotSupportedException```

## Strings

### String Class

- These objects are immutable. They are not edited in place and any changes result in a completely new object.

```
String s = new String("Nishit");
s.concat("Jain");
System.out.println(s); // Nishit
```

- String class overrides equals() method to compare content.

- ```String s = new String("Nishit");```

    - This creates two objects. One in heap area to which reference s points. The other in StringConstantPool, for future references.

- ```String s = "Nishit";```

    - This creates one object in StringConstantPool. Any object created using this method with this content would point to this StringConstantPool object. All String constants have only one copy in StringConstantPool. GarbageCollector only works in heap area, so restart is required to delete StringConstantPool.

- String class constructors

    - ```String s = new String()```: Creates an empty string object

    - ```String s = new String(String literal)```: Creates an object in the heap with corresponding literal

    - ```String s = new String(StringBuffer sb)```: Equivalent string object from given StringBuffer object

    - ```String s = new String(char[] ch)```: Equivalent string object from given character array

    - ```String s = new String(byte[] b)```: Equivalent string object from given byte array

- Methods of String class

    - ```public char charAt(int index)```

    - ```public String concat(String s)```

    - ```public boolean equals(Object o)```

    - ```public boolean equalsIgnoreCase(String s)```

    - ```public String substring(int begin)```

    - ```public String substring(int begin, int end)```

    - ```public int length()```

    - ```public String replace(char oldCh, char newCh)```

    - ```public String toLowerCase()```

    - ```public String toUpperCase()```

    - ```public String trim()```: Remove blank space from beginning and end of string

    - ```public int indexOf(char ch)```

    - ```public int lastIndexOf(char ch)```

- **Note:** During runtime, if a string object is created using a method call, only heap area will have that object. It will not be present in StringConstantPool. New object by method call is only created if there is change in previous object, else reference will point only to previous object

```
String s1 = new String("nishit");
String s2 = s1.toUpperCase();
String s3 = s1.toLowerCase();

System.out.println(s1 == s2); // false, s2 points to uppercase NISHIT present only in heap
System.out.println(s1 == s3); // true, s1 and s3 point to the same lowercase nishit present in heap (and is present in StringConstantPool too)
```

- Create our immutable class: Immutability is when we create an object which cannot be changed. If we want to change the contents of an object, new object is created with those changes. If nochanges, the same object is reused.

- Declaring reference variable as final prevents reassignment of that reference variable. However, corresponding object can be changed. On the other hand, immutability means the objet itself cannot change.

### StringBuffer class

- These objects are mutable. Editing an existing objet does not result in creation of a new object.

```
StringBuffer s = new StringBuffer("Nishit");
s.concat("Jain");
System.out.println(s); // NishitJain
```

- StringBuffer does not override equals() method and uses the one in Object class

- If content of string object keeps changing, it is not recommended to use String class. Rather, we should use StringBuffer class

- Constructors

    - ```StringBuffer sb = new StringBuffer();```: Creates empty StringBuffer object of 16 capacity. When capacity is filled, new element is added after creating new StringBuffer object with new capacity equal to (original + 1) * 2

    - ```StringBuffer sb = new StringBuffer(int initialCapacity)```

    - ```StringBuffer sb = new StringBuffer(String s)```: Capacity is s.length + 16

- Important methods

    - ```public int length()```

    - ```public int capacity()```

    - ```public char charAt(int index)```

    - ```public void setCharAt(int index, char ch)```

    - ```public StringBuffer append(String s / int i / long l / char c)```

    - ```public StringBuffer insert(int index, String s / int i / char c)```

    - ```public StringBuffer delete(int begin, int end)```: Delete chars between begin and end - 1

    - ```public StringBuffer deleteCharAt(int index)```

    - ```public StringBuffer reverse()```

    - ```public void setLength(int length)```

    - ```public void ensureCapacity(int capacity)```

    - ```public void trimToSize()```

- Every method present in StringBuffer is synchronized. This may cause performance issues. Hence, StringBuilder was introduced

## Wrapper Classes

- To wrap primitive data types into objects

- There are several utility methods for primitives that can be declared in wrapper classes

- Constructors

    - ```Integer I = new Integer(int primitive)```

    - ```Integer I = new Integer(String s)```: 
    
        - If s is not a number, RuntimeError: NumberFormatException

    - Almost all classes have the above two constructors. Extra constructor are in :

        ```Float f = new Flat(double d)```

    - Character class only has one constructor

        ```Character ch = new Character('a')```

    - **Note:** We can either pass a boolean or string to boolean class constructor. If the string is case insensitive "true" (could be "True" or "TRUE"), it is treated as true. Any other string is treated as false.

- Utility methods

    - ```public static Wrapper valueOf(String s)```

        - We can use valueOf() methods to created objects for given primitives or string

        - Every class except Character containts the method

    - ```public static Wrapper valueOf(String s, inti radix)```

        - Only in integral wrapper classes

        - Radix can only be between 2 and 36 (inclusive). This is because using digits and alphabets, we can only have upto 36 characters

    - ```public static Wrapper valueOf(primitive p)```: In all Wrapper classes

    - ```public primitive xxValue()```

        - We can use these methods to get primitive for given wrapper object

        - Every number Wrapper class contains 6 xxValue() methods for each of the 6 number values

    - ```public static primitive parseXXX(String s)```

        - To convert String to primitive type

        - Every Wrapper class except Character contains static parseXXX() method

    - ```public static primitive parseXXX(String s, int radix)```

        - Every integral type Wrapper class

        - Radix lies between 2 and 36 inclusive

    - ```public String toString()```

        - To convert Wrapper object or primitive to String

        - Every Wrapper class contains this

    - ```public static String toString(primitive p)```

    - ```public static String toString(primitive p, int radix)```

        - Only in Integer and Long classes

    - ```public static String toXXXString(primitive p)```

        - XXX = Binary, Ocatl Hex

        - Only for Integer and Long classes

<div>
    <img src="/docs/java/core_java_ocjp_scjp/interchange_of_values.png" style="height:300px;margin:auto;">
</div>

- **Note:** String, StringBuffer and StringBuilder, along with all Wrapper classes are final.

- **Note:** String and all Wrapper objects are immutable

### Void Class

- It is a final class and the direct child class of Object

- Contains only one variable Void.TYPE

- Used in reflections concept

```
if(getMethod("m1").getReturnType() == Void.TYPE) {

}
```

## Autoboxing and Autounboxing

### Autoboxing

- Automatic conversion of primitive to Wrapper object by compiler

```
Integer I = 10; // autoboxing int to Integer

Integer I = Integer.valueOf(10); // after compilation
```

### Autounboxing

- Automatic conversion of Wrapper object to primitive type by compiler

```
int i = I;
int i = I.intValue(); // after compilation
```

- For null reference, if we try to perform autounboxing, we get RuntimeError: NullPointerException

```
class Test {
    static Integer I;

    public static void main(String[] args) {
        int m = I; // RuntimeError: NullPointerException

        System.out.println(m);
    }
}
```

```
Integer x = 10;
Integer y = x;

x++;

System.out.println(x); // 11
System.out.println(y); // 10
System.out.println(x == y); // false
```

- All Wrapper class objects are immutable. x++ results in x pointing to a new object with value 11. y is still pointing to the original object with value 10.

```
Integer x = new Integer(10);
Integer y = new Integer(10);
System.out.println(x == y); // false
```

```
Integer x = new Integer(10);
Integer y = 10;
System.out.println(x == y); // false
```

```
Integer x = 10;
Integer y = 10;
System.out.println(x == y); // true
```

- Autoboxing and unboxing reuse created objects. Hence, x and y will point to the same object.

```
Integer I = 1000;
Integer J = 1000;
System.out.println(I == J); // false
```

- To provide support for autoboxing, a buffer of Integer objects with values between -128 and 127 are created at the time of class loading. Before creating a new object via autoboxing, JVM will first check whether this object is already present in buffer or not. If present, it will be reused. Else JVM will create a new object.

- Byte -> buffer for all values. Short, Integer, Long -> -128 to 127. Character -> 0 to 127. Boolean -> always

### Widening vs Autoboxing

```
class Test {
    public static void m1(Integer I) {
        System.out.println("Autoboxing");
    }

    public static void m1(long l) {
        System.out.println("Widening");
    }

    public static void main(String[] args) {
        int x = 10;
        m1(x); // widening
    }
}
```

- Widening being an older feature dominates over autoboxing method

### Var-args vs Autoboxing

- Var-args always gets least priority

- Autoboxing followed by Widening is allowed. Widening followed by Autoboxing not implemented.

### Relation between == operator and equals() method

- If r1 == r2 is true, then r1.equals(r2) is always true

- If r1.equals(r2) is false, then r1 == r2 is always false

### Hash related DS

- Two equivalent objects should be placed in same bucket, but all objects in same bucket are not equal

- If two objects are equal by equals() method, they should have the same hashcode

- If we override equals() method, it is compulsory to override hashcode() method to satisfy the contact between equals() and hashcode()

    - If r1.equals(r2) is true, r1.hashcode() == r2.hashcode() is true

- If hashcodes of two objects are not equal, then they are definitely not equal by equals() method

### clone()

- Protected native Object clone() throws CloneNotSupportedException

```
class Test implements Cloneable { // RuntimeError: CloneNotSupportedException
    i = 10;

    public static void main(String[] args) throws CloneNotSupportedException {
        Test t1 = new Test();
        Test t2 = (Test)t1.clone(); // CompilerError: incompatible types
    }
}
```

- Cloneable is a marker interface (it does not contain any methods) in java.lang package

- Shallow cloning

    - The creation of a bitwise copy is called shallow cloning. A bitwise copy is when the target object contains primitive types, their duplicates are made, whereas for reference types, the duplicates of reference is made but the content remains the same.

    - Object class method is meant for shallow cloning only. For deep cloning, we need to override Clone() method.

- Deep cloning

    - Complete duplication of everything occurs

### Interning of String objects

- When we create String object as ```String s1 = new String("Nishit")```

    - Two objects are created, one in heap and the other in StringConstantPool area.

    - The reference s1 is pointing to the heap object

- We use interning to get reference to StringConstantPool object ```String s2 = s1.intern()```

- If corresponding StringConstantPool object is not present, intern() will create the object

### Important of StringConstantPool

- String is most commonly used object in Java. Special memory management is required for it

- Objects are re-used to improve performance and memory

- To prevent unwanted issues with object reuse, String objects are immutable