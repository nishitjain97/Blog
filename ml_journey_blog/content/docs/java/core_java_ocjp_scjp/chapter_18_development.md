---
title: 18. Development
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-11-27'
lastmod: '2020-12-04'
---

## javac

- To compile a single or group of java source files

```
javac [options] Test.java
javac [options] A.java B.java
javac [options] *.java
```

- options

    - -version

    - -d

    - -source

    - -verbose

    - -cp

    - -classpath

## java

- To run java class file

```
java [options] Test A B C
```

- options

    - -version

    - -D

    - -cp / -classpath

## classpath

- Describes location where required class files are available

- Compiler and JVM use classpath to locate files

- By default, JVM searches in CWD for class file. If we set classpath explicitly, JVM will search in that location and not CWD

- To set classpath

    - Environment variable: Permanently at system level

    - Set classpath = "": Temporary, command prompt level

    - java -cp "" Test: Command level

- **Note:** Compiler will check one level dependency. JVM will check all level dependencies

- **Note:** Any location created using package statement should be resolved with import statement

- Multiple locations in class path are separated using ';'

- The order in which it is specified is important

## jar files

- For any framework, dependent classes are available in jar files

- To create a jar file

```
jar -cuf test.jar Test.class
jar -cuf test.jar A.class B.class C.class
jar -cuf test.jar *.class
jar -cuf test.jar *.*
```

- To extract jar file

```
jar -xuf test.jar
```

- To display table of contents of jar

```
jar -tuf test.jar
```

- **Note:** Place .jar file in JDK / JRE / lib / ext to make it available to compiler and JVM. This is shortcut to not set classpath every time

## System properties

- For every system. some persistent properties are stored as System Properties. E.g. user country, system OS, JVM vendor, java version etc.

- To set any system property from command line

```
java -Dnishit = abc Test // no space between -D and property name
```

- This helps to customize program behavior

## jar vs war vs ear

- Java archive files. Group of .class files

- Web archive files. Allows zipped transportation or delivery of project

- Enterprise archive file

## Create executable jar file

- E.g. to create exec jar file with two .class files jar Demo.class and jar Demo$1.class

    - Create manifest (.mf) file that contains directions for main class as

    ```
    Main_Class: jarDemo <newline>
    ```

    - Create jar as follows

    ```
    jar -cvfm demo.jar manifest.mf jarDemo.class jarDemo
    ```

    - To execute

    ```
    java -jar demo.jar // or double-click jar
    ```

## Ways to run java program

- java jarDemo: .class file from command prompt

- java -jar jarDemo.jar: jar file from command prompt

- Doublce clikcing jar file

- Double clicking batch file

## JDK

- JDK: Environment to develop and run java application

    - JRE + Development Tools

- JRE: Environment to run Java application

    - JVM + Lib classes

- JVM: Interpreter to run java program line by line

## javaw

- Command to run java class file without console output, i.e., System.out.println() would be ignored

- Used to run GUI based applications

## javaws

- Java web start utility

- To download and launch a java application

- This gives a centralized control to manage any changes