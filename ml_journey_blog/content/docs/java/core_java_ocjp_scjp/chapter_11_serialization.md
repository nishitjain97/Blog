---
title: 11. Serialization
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-10-06'
lastmod: '2020-10-06'
---

## Introduction

- The process of converting an object from Java supported form to network or file supported form is serialization

- The process of writing state of an object to a file

- By using FileOutputStream and ObjectOutputStream classes, we implement serialization

```
class Dog {
    int i = 10;
    int j = 20;
}

class SerializationDemo {
    public static void main(String[] args) {
        Dog d1 = new Dog();

        // Serialization
        FileOutputStream fos = new FileOutputStream("abc.ser");
        ObjectOutputStream oos = new ObjectOutputStream(fos);
        oos.writeObject(d1);

        // Deserialization
        FileInputStream fis = new FileInputStream("abc.ser");
        ObjectInputStream ois = new ObjectInputStream(ois);
        Day d2 = (Dog)ois.readObject();
    }
}
```

- An object is serializable if its class implements Serializable(I)

- Serializable(I) is present in java.io package and is a marker interface

- If we wish to create serializable object without implementing Serializable(I), we get RuntimeError: NotSerializableException

### transient modifier

- Applicable only for variables

- At the time of serialization, if we do not want to save the value of some variable due to security issues, we declare it as transient. Values of transient variable are ignored and default values are stored by JVM

- Declaring static variables as transient has no effect because static variables are class level variables and not object level variables. Hence, do not participate in serialization.

- Final variable participates directly in serialization by its value, so no effect of transient

## Object Graphs in Serialization

- **Note:** We can serialize any number of objects, but deserialization occurs in the same order in which they were serialized.

```
class Dog {
    Cat c = new Cat();
}

class Cat {
    Rat r = new Rat();
}

class Rat {
    j = 20;
}

class Test {
    public static void main(String[] args) {
        Dog d = new Dog();
    }
}

// d -> c -> r -> 20 (Object graph)
```

- Set of all objects reachable from a reference is known as the reference's object graph

- If we serialize an object, all objects reachable from it get serialized automatically. Hence, all classes for which the object is being serialized should be Serializable. Else RuntimeError: NotSerializableException

## Customized Serialization

- In default serialization, there can be a loss of information due to transient keyword

- To prevent this, we need customized serialization

- To implement customized serialization, we need two methods

    - ```private void writeObject(ObjectOutputStream oos) throws Exception```

    - ```private void readObject(ObjectInputStream ois) throws Exception```

        - Activities to be performed during serialization and deserialization are defined in these methods respectively as they are executed by JVM automatically

- **Note:** Any method executed by JVM automatically is called callback method. E.g. main, init etc.

- While performing serialization and deserialization of some object if we are required to do extra work, we need to define these methods in the corresponding class of that object

- We use method defaultWriteObject() and then do the extra work

- **Note:** Programmers cannot call private methods from outside the class, but JVM can do so

## Serialization with respect to Inheritance

- Serializable neture is inheritable from parent to child. We can serialize a class object when class does not implement Serializable(I) if parent class implements it.

- If a parent is non-serializable, we can serialize child objects by implementing Serializable(I) in the child. However, while serializing, JVM checks if some value (variable) is coming from non-serializable parent. It ignores this value and stores the default value for that variable

- At the time of deserialization, JVM will check for non-serializable parent classes. For every such class, JVM will execute instance control flow and share its instance variable with the current object

- While executing instance control flow of non-serializable parent, JVM calls no-argument constructor. Hence, every non-serial parent should have no-argument constructor or it generates RuntimeError: InvalidClassException

## Externalization

- In serialization, control is with JVM

- In externalization, programmer has complete control. We can save part of the object based on our requirement.

- To provide externalizable ability to object, we implement Externalizable(I)

- Methods

    - ```public void writeExternal(ObjectOutput out) throws IOException```

        - Executed automatically at the time of serialization

        - At the time of deserialization, if corresponding class is Externalizable, JVM knows that file does not contain the complete object. So it first creates an object by calling the public no-argument constructor

        - Hence, any Externalizable class should contain no-argument constructor, else RuntimeError: InvalidClassException

    - ```public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException```

        - Executed automatically at the time of deserialization

        - There is no impact of transient in Externalization. If you don't want to save data for security reasons, don't save it. All control is with the programmer.

## Serial Version UID

- Serialization and deserialization may be done by different persons, different machines and different locations

- Both sender and receiver should have the class file at the beginning, only the state of object travels from sender to receiver

- At the time of serialization, JVM generates a unique identifier, Serial Version UID, based on the code in the class file and the JVM stores it with the serialized object

- While deserializing, JVM matches the unique identifier with local class file's identifier and deserializes only when both match. Otherwise, we get RutimeError: InvalidClassException

- Problems with default Serial Version UID generated by JVM:

    - Sender and receiver should have same JVM (vendor, platform and version). Otherwise receiver won't be able to deserialize

    - Both sender and receiver should use same class file version

    - Generation of UID requires complex algorithms which may cause performance issues

- We can generate our own SerialVersionUID by defining it in the class as ```public static final long SerialVersionUID```

- **Note:** Some IDEs prompt programmers to enter Serial Version UID. Others may generate it automatically.