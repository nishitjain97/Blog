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

- Methods:

    - ```floor(e)```: returns highest element <= e

    - ```lower(e)```: returns highest element < e

    - ```ceiling(e)```: returns lowest element >= e

    - ```higher(e)```: returns lowest element > e

    - ```pollFirst()```: remove and return first element

    - ```pollLast()```: remove and return last element

    - ```descendingSet()```: returns NavigableSet in reverse order

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

- From 1.5V onwards, LinkedList also implements Queue(I)

- Methods

    - ```boolean offer(Object o)```: Add object to queue

    - ```Object peek()```: To return head element. Returns null if queue is empty

    - ```Object element()```: To return head element. If queue is empty, RuntimeError: NoSuchElementException

    - ```Object poll()```: Remove and return head element. If empty, return null

    - ```Object remove()```: Remove and return head element. If empty, RuntimeError: NoSuchElementException

#### PriorityQueue

- Queue with priority based insertion

- Can be default or customized sorting order

- No null. Duplicates are allowed

- Constructors:

    - ```PriorityQueue q = new PriorityQueue()```

    - ```PriorityQueue pq = new PriorityQueue(int initCapacity)```

    - ```PriorityQueue pq = new PriorityQueue(int initCapacity, Comparator c)```

    - ```PriorityQueue pq = new PriorityQueue(SortedSet s)```

    - ```PriorityQueue pq = new PriorityQueue(Collection c)```

### Map(I)

- Not child interface of Collection, but a part of Collections Framework

- Used to store key-value pairs

- Keys are unique, values can be duplicates

<div>
    <img src="/docs/java/core_java_ocjp_scjp/map_interface.png" style="height:300px;margin:auto;">
</div>

- Methods

    - ```Object put(Object key, Object value)```: Returns old value when duplicate key is entered, i.e., when another value is added for same key, the new value over-writes the older value. In case key is added for first time, null is returned

    - ```void putAll(Map m)```: Add a smaller map to this map

    - ```Object get(Object key)```: Returns null if key is not present

    - ```Object remove(Object key)```

    - ```boolean containsKey(Object key)```

    - ```boolean containsValue(Object value)```

    - ```boolean isEmpty()```

    - ```int size()```

    - ```void clear()```

- Collection views of map

    - ```Set keySet()```

    - ```Collection values()```

    - ```Set entrySet()```

#### Entry(I)

- Inner interface of Map(I) because Entry object cannot exist without a Map

- Methods

    - ```Object getKey()```

    - ```Object getValue()```

    - ```Object setValue(Object key)```

#### HashMap

- Underlying DS is hashtable

- Insertion order not preserved, it is based on hashcode of keys

- Unique keys but values can be duplicated

- Heterogenous keys and values

- Only one null key, any number of null values

- Implements Serializable and Cloneable, not RandomAccess

- Used when searching is the most frequent job

- Constructors

    - ```HashMap m = new HashMap```: Initial capacity = 16 and fill ratio is 0.75

    - ```HashMap m = new HashMap(int initCapacity)```

    - ```HashMap m = new HashMap(int initCapacity, float fillRatio)```

    - ```HashMap m = new HashMap(Map m1)```

|HashMap|Hashtable|
|---|---|
|Not synchronized|Synchronized|
|Not thread safe|Thread safe|
|Higher performance|Lower performance|
|null key and values allowed|Gives CompilerError: NullPointerException|
|Not legacy (1.2V)| Legacy(1.0V)|

- **Note:** To get a synchronized version of hashmap

```
HashMap m = new HashMap();
Map m1 = Collections.synchronizedMap(m);
```

#### LinkedHashMap

- Child of HashMap. Same as HashMap (methods and constructors)

- Underlying DS is hybrid of LinkedList and Hashtable

- Insertion order is preserved

- V1.4

- Commonly used for cache based applications

#### IdentityHashMap

- Child of HashMap. Methods and constructors same as HashMap

- Normally, to check for duplicate keys in HashMap, JVM uses .equals() method for contenet comparison. In IdentityHashMap, HVM uses '==' operator for reference comparison

#### WeakHashMap

- Same as HashMap, except one key difference

- For HashMap, if an object associated with HashMap does not have a reference, it is not eligible for garbage collection.

- For WeakHashMap, no reference object associated with it is eligible for garbage collection

#### SortedMap(I)

- Child interface of map

- To store key-value pairs according to sorted order of keys. Value never participates in sorting

- Methods

    - ```Object firstKey()```

    - ```Object lastKey()```

    - ```SortedMap headMap(Object key)```

    - ```SortedMap tailMap(Object key)```

    - ```SortedMap subMap(Object key1, Object key2)```

    - ```Comparator comparator()```

#### TreeMap

- Underlying data structure in Red-Black trees

- Keys should be homogeneous and comparable for default sorting order, and can be heterogeneous for custom sorting order (comparator)

- Constructors

    - ```TreeMap t = new TreeMap()```

    - ```TreeMap t = new TreeMap(Comparator c)```

    - ```TreeMap t = new TreeMap(Map m)```

    - ```TreeMap t = new TreeMap(SortedMap m )```

#### Hashtable

- Underlying DS is a hash table

- Insertion order not preserved, it is based on hash code of keys

- Values can be duplicated

- Heterogenous allowed, null not allowed

- Serializable and Cloneable, but not RandomAccess

- Synchronized so thread-safe

- Best for frequent search

- Constructors

    - ```Hashtable h = new Hashtable()```: default capacity = 11 and fill ratio = 0.75

    - ```Hashtable h = new Hashtable(int initCapacity)```

    - ```Hashtable h = new Hashtable(int initCapcity, float fillRatio)```

    - ```Hashtable h = new Hashtable(Map m)```

- **Note:** The output of hash table is read top to bottom, right to left from the hash table

#### Properties

- Anything that changes frequently is not recommended to be hard-coded because any change requires re-compilation, re-building, re-deployment and sometimes restart of server

- We can overcome by storing variable things in properties file

- Any change in properties requires only re-deployment of application

- In other Map types, key and value can be any type, but in Properties, key-value should be String only

- Constructors

    - ```Properties p = new Properties()```

- Methods

    - ```String getProperty(String pName)```

    - ```String setProperty(String pName, String value)```

    - ```Enumeration propertyNames()```

    - ```void load(InputStream is)```

    - ```void store(OutputStream os, String comment)```

#### NavigableMap(I)

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

- Methods:

    - ```floorKey(e)```

    - ```lowerKey(e)```

    - ```ceilingKey(e)```

    - ```higherKey(e)```

    - ```pollFirstEntry()```

    - ```pollLastEntry()```

    - ```descendingMap()```


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

        - Returns -ve if obj1 < obj2

    - ```public boolean equals(Object obj)```

- Implementation of Comparator(I) requires implementation of only compare() method because equals() is dummy as its implementation is in Object class, which is the parent.

### Collections

- Defines utility methods for Collection objects

- Sorting

    - ```public static void sort(List l)```: Default natural sorting order. Hence, elements should be homogeneous and Comparable. Also, there should be no null element

    - ```public static void sort(List l, Comparator c)```: Customized sorting

- Searching:

    - ```public static int binarySearch(List l, Object target)```: Returns index where element is present. Returns insertion point if element is not present. Insertion point is the spot where target should have been present, denoted by -1, -2, -3, ...,positions

    - ```public static int binarySearch(List l, Object target, Comparator c)```: For customized searching

    - **Note:** These methods will use binary search internally. If list is not sorted, we will get unpredictable results. For n elements

        - Successful search results: 0 to n-1

        - Unsuccessful search results: (-n+1) to -1

        - Total range = (-n+1) to (n-1)

- Reversing

    - ```public static void reverse(List l)```: To reverse order of elements in a list

    - ```public static Comparator reverseOrder(Comparator c)```: To get reversed Comnparator

### Arrays

- A utility class that defines several utility methods for array objects

- Sorting

    - ```public static void sort(primitive[] p)```: Natural sorting order

    - ```public static void sort(Object[] o)```: Natural sorting order

    - ```public static void sort(Object[] o, Comparator c)```: Customized sorting

- Searching

    - ```public static int binarySearch(primitive[] p, primitive target)```

    - ```public static int binarySearch(Object[] o, Object target)```

    - ```public static int binarySearch(Object[] o, Object target, Comparator c)```

- Conversion

    - ```public static List asList(Object[] o)```: Viewing existing arrays as list, i.e., list is not created

    ```
    String[] s = {"a", "b"};
    List l = Arrays.asList(s);
    ```

    - **Note:** Since array is fixed in length, we cannot use List reference to expand or shrink array. We'll get RuntimeError: UnsupportedOperationException

    - **Note:** Since Arrays are homogeneous, if we try to insert heterogeneous objects using List reference, we get RuntimeError: ArrayStoreException

### Concurrent Collections

- Traditionally, Collection is not threadsafe

- Even if we use threadsafe Collection, there are performance problems

- During iteration by one thread, if any other thread modifies the Collection, we get RuntimeError: ConcurrentModificationException

- Hence, we need Concurrent Collections. They solve all the above problems

#### ConcurrentMap(I)

<div>
    <img src="/docs/java/core_java_ocjp_scjp/concurrent_map.png" style="height:300px;margin:auto;">
</div>

- Contains all the methods of Map(I)

- Methods

    - ```Object putIfAbset(Object key, Object value)```: In put() method, if key already present, old value is replaced by a new value. In putIfAbsent(), if key already resent, value will not be changed and old value will be returned

    - ```boolean remove(Object key, Object value)```: Removes an entry only if both key and values match

    - ```boolean replace(Object key, Object oldValue, Object newValue)```

#### ConcurrentHashMap

- Since a HashMap uses buckets to store key-value pairs, Object level lock is needed by thread to modify it.

- However, in ConcurrentHashMap, we have bucket level locks. Hence, if one thread is modifying one bucket, other threads are allowed to work on other buckets

- **Note:** Concurrency level is the number of buckets that can be updated simultaneously

- For reading, no lock is required

- Constructors

    - ```ConcurrentHashMap m = new ConcurrentHashMap()```: Default capacity = 16, default fill ratio = 0.75 and concurrency level = 16

    - ```ConcurrentHashMap m = new ConcurrentHashMap(int initCapacity)```

    - ```ConcurrentHashMap m = new ConcurrentHashMap(int initCapacity, float fillRatio)```

    - ```ConcurrentHashMap m = new ConcurrentHashMap(int initCapacity, float fillRatio, int concurrencyLevels)```

    - ```ConcurrentHashMap m = new ConcurrentHashMap(Map m)```

#### CopyOnWriteArrayList

<div>
    <img src="/docs/java/core_java_ocjp_scjp/cowal.png" style="height:300px;margin:auto;">
</div>

- It is the threadsafe version of ArrayList present in concurrent package

- When multiple threads are working on a single object, any thread that is performing a write operation would get its own copy of the object. The different copies would later by synced together with the original by the JVM automatically

- Preferred when more read operations are occurring compared to write

- Normal ArrayList has fast-fail iterator, while COWAL has fail-safe iterator

- COWAL can not perform remove operation using iterator, we get RuntimeError: UnsupportedOperationException

- Constructors

    - ```COWAL l = new COWAL()```

    - ```COWAL l = new COWAL(Collection c)```

    - ```COWAL l = new COWAL(Object[] o)```

- Methods

    - ```boolean addIfAbsent(Object o)```

    - ```int addAllAbsent(Collection c)```

#### CopyOnWriteArraySet

<div>
    <img src="/docs/java/core_java_ocjp_scjp/cowas.png" style="height:300px;margin:auto;">
</div>

- Works same as COWAL, only difference is that this is a Set

- Constructors

    - ```COWAS c = new COWAS()```

    - ```COWAS c = new COWAS(Collection c)```