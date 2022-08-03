---
title: 13. Collections
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-10-20'
lastmod: '2020-10-20'
---

## Introduction

- Problems with array

    - Fixed in size

    - Homogeneous

    - No utility methods

- Collections help overcome these problems

- Collections can hold only objects, but arrays can hold either objects or primitive types

- To represent a group of objects as a single entity, collections should be used

### Collections Framework

- A group of classes and interfaces which can be used for above purposes

### Key Interfaces in Collections Framework

- Collection

- List

- Set

- SortedSet

- NavigableSet

- Queue

- Map

- SortedMap

- NavigableMap

### Collection(I)

- To represent a group of objects as a single entity

- Contains all the common methods of most types of collection object

- Considered root interface of Collection framework

- No concrete class implements it directly

#### Collection vs Collections

- Collection is an interface to represent group of individual objects as a single entity

- Collections is a utility class in java.util, which defines several utility methods for Collection. E.g. searching, sorting etc.

#### Methods

- ```boolean add(Object o)```

- ```boolean addAll(Collection c)```

- ```boolean remove(Object o)```

- ```boolean removeAll(Collection c)```

- ```boolean retainAll(Collection c)```

- ```void clear()```

- ```boolean contains(Object o)```

- ```boolean containsAll(Collection c)```

- ```boolean isEmpty()```

- ```int size()```

- ```Object[] toArray()```

- ```Iterator iterator()```

### List(I)

- Child interface of Collection(I)

- To represent a group of individual objects as a single entity where duplicates are allowed and insertion order must be preserved

<div>
    <img src="/docs/java/core_java_ocjp_scjp/list_interface.png" style="height:300px;margin:auto;">
</div>

- **Note:** In 1.2V, Vector and Stack classes were re-engineered to implement List(I)

- We can differentiate duplicates also by using the index

- Methods

    - Contains 12 methods of Collection(I). Adding to them

    - ```void add(int index, Object o)```

    - ```boolean addAll(int index, Collection c)```

    - ```Object get(int index)```

    - ```Object remove(int index)```

    - ```Object set(int index, Object new)```

    - ```int indexOf(Object o)```

    - ```int lastIndexOf(Object o)```

    - ```ListIterator listIterator()```

#### ArrayList

- Resizable or Growable array

- Duplicates allowed

- Insertion order preserved

- Heterogeneous objects are allowed

- null insertion is possible

- Constructors

    - ```ArrayList l = new ArrayList()```: Creates empty ArrayList object with capacity 10. On reaching max capacity, new ArrayList object is created as: ```new capacity = (current * 3/2) + 1```

    - ```ArrayList l = new ArrayList(int initialCapacity)```

    - ```ArrayList l = new ArrayList(Collection c)```

- **Note:** We get warnings during compile time as we are not using Generics

- **Note:** Every Collection class implements Serializable and Cloneable interface

- **Note:** ArrayList and Vector implement RandomAccess interfaces. This helps in accessing any element in same, constant speed

- ArrayList is best when frequent operation is retrieval. It is wors choice for insertion / deletion

- LinkedList is best for insertion / deletion

|ArrayList|Vector|
|---|---|
|Non-synchronized|Synchronized|
|Thread unsafe|Thread safe|
|Relatively high performance|Relatively low performance|
|1.2V, non-legacy|1.0V, legacy|

#### Synchronized version of ArrayList

```
ArrayList l = new ArrayList();
List l1 = Collections.synchronizedList(l);
```

- ```public static List synchronizedList(List l)```

- ```public static Set synchronizedSet(set s)```

- ```public static Map synchronizedMap(Map m)```

#### RandomAccess(I)

- Present in java.util package

- It is a marker interface

- The required ability is provided by JVM

#### LinkedList

- Implements Serializable and Cloneable, but not RandomAccess

- Constructors

    - ```LinkedList l = new LinkedList()```

    - ```LinkedList l = new LinkedList(Collection c)```

- Usually used to develop stacks and queues

- Methods

    - ```void addFirst(Object o)```

    - ```void addLast(Object o)```

    - ```Object getFirst()```

    - ```Object getLast()```

    - ```Object removeFirst()```

    - ```Object removeLast()```

- It is implemented as a doubly linked list

#### Vector

- Made with underlying array

- Same properties as ArrayList

- Constructors

    - ```Vector v = new Vector()```

    - ```Vector v = new Vector(int initCapacity)```

    - ```Vector v = new Vector(int initCapacity, int incrementalCapacity)```

    - ```Vector v = new Vector(Collection c)```

- Methods

    - ```addElement(Object o)```

    - ```removeElement(Object o)```

    - ```removeElementAt(int index)```

    - ```removeAllElements()```

    - ```Object elementAt(int index)```

    - ```Object firstElement()```

    - ```Object lastElement()```

    - ```int size()```

    - ```int capacity()```

    - ```Enumeration elements()```

- **Note:** Since programmers don't need memory management in Java, the new interfaces in Collection do not show the capacity of it. However, Vector being a legacy class still has capacity() as a method

#### Stack

- Child of Vector

- Specially designed for LIFO

- Constructor

    - ```Stack s = new Stack()```

- Methods

    - ```Object push(Object o)```

    - ```Object pop()```

    - ```Object peek()```

    - ```boolean empty()```

    - ```int search(Object o)```: Returns offset (distance from top of stack) if element is available, else returns -1

### Set(I)

- Child interface of Collection(I)

- To represent a group of individual objects as a single entity where duplicate are not allowed and insertion order not required

- Does not contain any new methods. Contains only the 12 methods of Collection(I)

<div>
    <img src="/docs/java/core_java_ocjp_scjp/set_interface.png" style="height:300px;margin:auto;">
</div>

#### SortedSet(I)

- Child interface of Set(I)

- To represent group of individual objects as a single entity where duplicates are not allowed and all objects should be inserted according to some sorted order

- Special methods for sorted sets

    - ```Object first()```

    - ```Object last()```

    - ```SortedSet headSet(Object obj)```: Returns subset of all objects less than obj

    - ```SortedSet tailSet(Object obj)```: Returns subset of all objects greater than or equal to obj

    - ```SortedSet subSet(Object obj1, Object obj2)```: Returns SortedSet of objects >= obj1 and <= obj2

    - ```Comparator comparator()```: Object defining underlying sorting technique. Returns null for default natural sorting order.

#### TreeSet

- Underlying dataset is balanced tree

- No duplicates, no insertion order

- Heterogenous not allowed. RuntimeError: ClassCastException

- null insertion only once

- Implements Serializable and Cloneable, but not RandomAccess

- Constructors

    - ```TreeSet t = new TreeSet()```: Default natural sorting order insertion

    - ```TreeSet t = new TreeSet(Comparator c)```: Customized sorting order insertion

    - ```TreeSet t = new TreeSet(Collection c)```

    - ```TreeSet t = new TreeSet(SortedSet s)```

- **Note:** Since insertion in TreeSet depends on comparison, null can only be inserted when TreeSet is empty and no other object can be inserted after null. Else we get: RuntimeError: NullPointerException

- **Note:** After version 1.7, null is not allowed in TreeSet at all

- If we are depending on default sorting order along with homogeneity of the objects, the class should also implement Comparable(I)

#### NavigableSet(I)

- Child interface of SortedSet(I)

- Contains methods for navigation purposes

- TreeSet is its implementation class

<div>
    <img src="/docs/java/core_java_ocjp_scjp/navigable_set_interface.png" style="height:300px;margin:auto;">
</div>

#### HashSet

- Hashtable is underlying architecture

- No duplicates, so can contain only one null

- Objects inserted based on hashcode of objects

- Implements Serializable and Cloneable, but not RandomAccess

- Best for use when searching frequently

- **Note:** On adding a duplicate, add() will return false

- Constructors

    - ```HashSet h = new HashSet()```: Initial capacity is 16. Default fill ratio is 0.75 (after filling 75%, a new object with greater capacity will be created)

    - ```HashSet h = new HashSet(int initialCapacity)```

    - ```HashSet h = new HashSet(int initialCapacity, float fillRatio)```

    - ```HashSet h = new HashSet(Collection c)```

- **Note:** These constructors are common to all hashing related Collection objects

#### LinkedHashSet

- Child of HashSet

- Exactly same as HashSet (constructors and methods)

- Underlying data structure is a hybrid of linked list and has table

- Insertion order is preserved

- Introduced in 1.4V

- Commonly used to develop cache-based applications



### Queue(I)

- Child interface of Collection(I)

- To represent group of individual objects prior to processing

- Queue follows FIFO, but we can implement our own order too

<div>
    <img src="/docs/java/core_java_ocjp_scjp/queue_interface.png" style="height:300px;margin:auto;">
</div>

- **Note:** The previous interfaces are meant for representing a group of individual objects. For group of key-value pairs, we need map.

### Map(I)

- Not child interface of Collection, but a part of Collections Framework

- Used to store key-value pairs

- Keys are unique, values can be duplicates

<div>
    <img src="/docs/java/core_java_ocjp_scjp/map_interface.png" style="height:300px;margin:auto;">
</div>

- Methods

    - ```Object put(Object key, Object value)```

### SortedMap(I)

- Child interface of map

- To store key-value pairs according to sorted order of keys. Value never participates in sorting

### NavigableMap(I)

- Child interface of SortedMap, used for navigation of maps

<div>
    <img src="/docs/java/core_java_ocjp_scjp/navigable_map_interface.png" style="height:300px;margin:auto;">
</div>

- **Note:** The following are legacy characters present in collections framework

    - Enumeration(I)

    - Dictionary(AC)

    - Vector(C)

    - Stack(C)

    - Hashtable(C)

    - Properties(C)


### Enumeration

- To get elements from legacy Collection classes one at a time

```public Enumeration elements()```

- Methods

    - ```public boolean hasMoreElements()```

    - ```public Object nextElement()```

- Limitation

    - Applicable for legacy classes only. It is not universal.

    - Allows only read access to objects. We can't perform remove operation.

### Iterator(I)

- Applicable to any Collection, hence it is universal cursor

- We can perform both read and remove operation

- Creation:

```public Iterator iterator()```

```Iterator itr = c.iterator()```

- Methods

    - ```public boolean hasNext()```

    - ```public Object next()```

    - ```public void remove()```

- Limitations

    - We can move onlye in one direction (forward)

    - We can only read / remove. We can not add / replace.

### ListIterator(I)

- It is bi-directional cursor

- We can perform read, remove, replace and add elements

- Creation

```public ListIterator listIterator()```

```ListIterator ltr = l.listIterator()``` for any list object

- Methods: The 3 methods of Iterator are available to ListIterator (it is child of Iterator)

    - ```public int nextIndex()```

    - ```public boolean hasPrevious()```

    - ```public Object previous()```

    - ```public int previousIndex()```

    - ```public void remove()```

    - ```public void add(Object o)```

    - ```public void set(Object o)```

- Only applicable for List objects

### Comparable(I)

- Present in java.lang package

- Contains only one method

```public int compareTo(Object object2)```

- This method works as

    - Returns -ve when object1 comes before object2

    - Returns 0 when equal

    - Returns +ve when object1 comes after object2

- For add() in TreeSet, object1 is object being added and object2 is one already added

### Comparator(I)

- Present in java.util package

- Methods

    - ```public int compare(Object obj1, Object obj2)```

        - Returns +ve if obj1 > obj2

        - Returns 0 if obj1 = obj2

        - Returns -v if obj1 < obj2

    - ```public boolean equals(Object obj)```

- Implementation of Comparator(I) requires implementation of only compare() method because equals() is dummy as its implementation is in Object class, which is the parent