---
title: 7. Multithreading
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-09-08'
lastmod: '2020-09-08'
---

## Introduction

- Executing multiple tasks at the same time is called multi-threading

- It is of two types

    - Process based: Each task is a separate, independent process. It is at an OS level. E.g. music, word editor, web browser running simultaneously

    - Thread based: Each task is a separate, independent part of a single process. It is at a program level.

- Improves performance of processor by reducing response time of system

- Help in multimedia processing, develop web and application servers

- Java has a rich API for multithreading

## Ways to define a thread

- We can define a thread in the following ways

    - By extending Thread class

    - By implementing Runnable(I)

### By extending Thread class

```
class MyThread extends Thread {
    public void run() {
        // Job of thread
    }
}

class ThreadDemo {
    public static void main(String[] args) {
        MyThread t = new MyThread(); // Thread instantiation
        t.start(); // Starting of thread
    }
}
```

- The start() method calls the overwritten run() method

- Direct call to run() method would not result in multiple threads. It would be a regular function call

- start()

    - Register this thread with Thread scheduler

    - Perform other mandatory activities

    - Invoke run()

```
class MyThread extends Thread {
    public void run() {
        //
    }

    public void run(int i) {
        //
    }
}

class ThreadDemo extends Thread {
    //
}
```

- Overloading run() method is always possible, but start() method would call no-argument run() method

- If we do not override run() method, starting a thread would call the Thread class, no output (empty) run method.

- If we override start() method, parent class Thread class start() method would not be called and no new thread will be created

- After starting a thread, if we restart that thread, we get RuntimeException

    - RuntimeException: IllegalRuntime

    - RuntimeException: Illegal Thread State Exception

### By implementing runnable interface

- Runnable(I) is available in java.lang package and contains only one method

    ```public void run()```

```
class MyRunnable implements Runnable {
    public void run() {
        //
    }
}

class ThreadDemo {
    public static void main(String[] args) {
        MyRunnable r = new MyRunnable();
        Thread t = new Thread(r); // Target runnable
        t.start();
    }
}
```

- This approach is recommended as it allows us to extend / implement other classes / interfaces

#### Thread class constructors

- ```Thread t = new Thread()```

- ```Thread t = new Thread(Runnable r)```

- ```Thread t = new Thread(String name)```

- ```Thread t = new Thread(Runnable r, String name)```

- ```Thread t = new Thread(ThreadGroup g, Runnable r)```

- ```Thread t = new Thread(ThreadGroup g, String name)```

- ```Thread t = new Thread(ThreadGroup g, Runnable r, String name)```

- ```Thread t = new Thread(ThreadGroup g, Runnable r, String name, long stackSize)```

### Hybrid Approach

```
class MyThread extends Thread {
    public void run() {
        System.out.println("Child Thread");
    }
}

class Test {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        Thread t1 = new Thread(t);
        t1.start();
        System.out.println("Main");
    }
}
```

## Getting and Setting thread name

```
class MyThread extends Thread {

}

class Test {
    public static void main(String[] args) {
        System.out.println(Thread.currentThread().getName()); // main

        MyThread t = new MyThread();
        System.out.println(t.getName());

        Thread.currentThread().setName("Nishit");
        System.out.println(Thread.currentThread().getName());
    }
}
```

- Using static method currentThread()

## Thread priorities

- Every thread has either default (by JVM) or user-defined priority

- Ranges between 1 and 10

- 1 is min priority, 10 is max

    - Thread.MIN_PRIORITY = 1

    - Thread.NORM_PRIORITY = 5

    - Thread.MAX_PRIORITY = 10

- Two threads with same priority depend on thread scheduler. No predictions can be made of which goes first

- Priority methods

    - ```public final int getPriority()```

    - ```public final void setPriority(int p)```

- If range out of 1 and 10 given to setPriority, RuntimeException: IllegalArgumentException

- For main, default priority is 5. For all else, default will be inherited from the parent

- Some platforms do not provide support for thread priorities

## Methods to prevent thread excecution

- Three ways

    - yield()

    - join()

    - sleep()

### yield()

- Causes current executing thread to pass and give chance to waiting threads of same priority

- In case no waiting threads or all threads of lower priority, the current thread can continue

- Multiple waiting threads with same priority, which will get chance can not be predicted

- public static native void yield();

```
class MyThread extends Thread {
    public void run() {
        for(int i = 0; i < 10; i++) {
            System.out.println(i);
        }
        Thread.yield();
    }
}
```

### join()

- When one thread has to wait till the completion of another thread

- E.g. if t1 wants to wait until t2 finishes, t1 has to call t2.join()

- Function calls

    - public final void join() throws InterruptedException

    - public final void join(long ms) throws InterruptedException

    - public final void join(long ms, int ms) throws InterruptedException

- If two threads call join method on one another, this would lead to a deadlock condition

- If thread calls join method on itself, it would be like deadlock

### sleep()

- If the thread does not want to perform any task for specific amount of time

- Calls

    - public static native void sleep(long ms) throws InterruptedException

    - public static void sleep(long ms, int ms) throws InterruptedException

#### public void interrupt()

- A thread can interrupt sleeping / waiting thread by this method

- If target thread is not sleeping / waiting, the interrupt command waits for it to get in these states. Once it enters, the interrupt executes immediately

- Interrupt would go to waste if target thread neve enters sleep / wait state in its lifetime

## Synchronization

- 'synchronized' is a modifier only applicable to methods

- If multiple threads are working on same object, data inconsistency can occur. Here, synchronization is needed

- However, it also increases waiting time of thread and creates performance issues

### Working

- It uses lock concept internally

- Every object in Java has a unique lock

- To access the object, a thread needs to get lock of object to execute synchronized methods

- Another thread won't get the lock until the previous thread completes the synchronized method and releases the lock

- Non-synchronized methods can be executed anytime by any thread

### static synchronized

- Normally, if different threads are calling a synchronized method on different objects, there is no need for synchronization

- However, if the method is 'static synchronized', even with different objects, the threads would operate only one at a time

- This is due to class level lock

- Every class in Java has this unique lock. It works same as object level lock, but for 'static synchronized' methods

- Even if one thread has class-level lock, another thread can take the object-level lock to execute non-static synchronized methods

### synchronized block

- For very long methods, synchronizing the whole method can cause performance inssues

- Here, we can synchronize just few lines of code that need to be synchronized, using synchronized block

- Three things can be done

    - To get lock of current object

    ```
    synchronized(this) {

    }
    ```

    - To get lock of particular object

    ```
    synchronized(b) {

    }
    ```

    - To get class level lock

    ```
    synchronized(Classname.Class) {

    }
    ```

- There are no object level locks for primitive types

```
int x = 10;

synchronized(x) {
    // CompilerException: unexpected type
    // found: int
    // required: reference
}
```

- A thread can have multiple locks, each should be from a different object

```
class X {
    public synchronized void m1() {
        Y y = new Y();

        synchronized(y) {
            Z z = new Z();

            synchronized(z) {

            }
        }
    }
}
```

## Interthread communication

- Two threads can communicate with each other by using

    - wait()

    - notify()

    - notifyAll()

- Thread responsible for performing updation calls notify() method, which causes other threads that are waiting to continue

- Thread expecting update calls wait() method. Thread performing updation calls notify() after completing updation

- These methods are present in object class, not in Thread class

- To call wait() method on an object, the thread should have the lock of the object (should be in synchronized area)

    - RuntimeException: IllegalMonitorStateException

- On calling wait() on an object, the thread immediately releases lock of that particular object and moves to wait state

- If a thread calls notify() or notifyAll() method on an object, it releases the lock of that object. The release may not necessarily be immediate.

- Prototypes

    - ```public final void wait() throws InterruptedException```

    - ```public final native void wait(long ms) throws InterruptedException```

    - ```public final void wait(long ms, int ns) throws InterruptedException```

    - ```public final native void notify()```

    - ```public final native void notifyAll()```

### Producer-Consumer Problem

- Producer thread is responsible to produce items in the Queue, while consumer consumes from the Queue

- If Queue is empty, consumer will call wait() method and go to waiting state

- The producer calls notify() method after producing

- Producer Thread

```
class ProducerThread {
    produce() {
        synchronized(q) {
            // produce items to q
            q.notify()
        }
    }
}

class ConsumerThread {
    consume() {
        synchronized(q) {
            if(q is empty) {
                q.wait()
            } else {
                consume item
            }
        }
    }
}
```

### notify() vs notifyAll()

- notify() method gives notification to only one thread, even if multiple threads are waiting. The other threads need to be notified individually. The thread that will be receiving the notification cannot be determined (it is upto the JVM)

- notifyAll() is used to send notification to all waiting threads of a particular object. Execution would still be performed one by one because of unique lock.

## Deadlock

- If two threads are waiting for each other forever, it is called deadlock

- No resolution for this problem, only preventive measures

## Daemon Thread

- Threads executing in the background

- E.g. garbage collector, signal dispatcher, attach listener etc.

- They provide support for non-daemon threads (main thread)

- Usually daemon threads have low priority, but when needed they can have high priority as well

- ```public boolean isDaemon()```

    - Checks if thread is Daemon thread or not

- ```public void setDaemon(boolean b)```

    - If b is true, makes the thread daemon

    - If b is false, makes the thread non-daemon

    - This method can only be alled before thread starts, else we will get runtime error

        - ```RuntimeError: IllegalThreadStateException```

- By default, main thread is always non-daemon. For all other threads, the nature is inherited from parent

- It is impossible to change the daemon nature of main

- Since daemon threads are present to support non-daemon threads, once all non-daemon threads are completed, all daemon threads are terminated immediately irrespective of their state

### Green thread model

- There are two ways in which multithreading is handled in Java

    - Green thread model

    - Native OS model

- The GTM requires only JVM to handle multithreading without any help from the underlying operating system. A deprecated system, very few OS (like Sun Solaris) provided support for the same.

### t.stop()

- To kill a thread in the middle of its lifecycle

- It is deprecated because it can lead to resource mismanagement

### t.suspend() and t.resume()

- ```public void suspend()```

- ```public void resume()```

- Deprecated methods, not recommended to use

<div>
    <img src="/docs/java/core_java_ocjp_scjp/thread_lifecycle.png" style="height:300px;margin:auto;">
</div>

## Enhancements in Multithreading

### ThreadGroup

- Based on functionality, we can group threads into ThreadGroups

- We can perform common operations to the group as a whole

- The root of all threads is the SystemThreadGroup (directly or indirectly)

- SystemThreadGroup contains several system level threads: Finalizer (Garbage Collector), Reference Handler, Signal Dispatcher, Attach Listener etc.

- ThreadGroup is a Java class present in java.lang package and is direct descendent of Object class

- ```ThreadGroup g = new ThreadGroup(String name)```

    - This creates a thread group with given name

    - The parent of this group is the thread group of current executing thread

- ```ThreadGroup g = new ThreadGroup(ThreadGroup m, String name)```

    - This customizes the parent of `g` to be group `m`

- Important ThreadGroup methods

    - ```String getName()```

    - ```int getMaxPriority()```

    - ```void setMaxPriority(int p)```

    - ```ThreadGroup getParent()```

    - ```void list()```

    - ```int activeCount()```

    - ```int activeGroupCount()```

    - ```int enumerate(Thread[] t)```

    - ```int enumrate(ThreadGroup[] g)```

    - ```boolean isDaemon()```

    - ```void setDaemon(boolean b)```

    - ```void interrupt()```

    - ```void destroy()```

### Alternative to synchronized

- ```java.util.concurrent.locks``` (1.5v)

    - Provides enhancements and more flexibility to programmers

- Lock(I)

    - Similar to implicit object lock, but allows more functionality

    - Important methods

        - ```void lock()```: Used to acquire the lock of object. If lock is available, it will be given to current thread. Else, it will wait to get the lock (same as synchronized)

        - ```boolean tryLock()```: If lock available, thread gets the lock. If lock not available, method returns false and alternate tasks can be done without waiting

        ```
        if(l.tryLock()) {
            // Perform safe operations
        } else {
            // Perform alternate operations
        }
        ```

        - ```boolean tryLock(long time, TimeUnit unit)```

            - If lock is available, thread gets it. If not available, the thread willwait for specific time and then continue with alternate execution

            - TimeUnite present in java.util.concurrent.TimeUnit

                ```
                enum TimeUnit {
                    NANOSECONDS;
                    MICROSECONDS;
                    MILLISECONDS;
                    SECONDS;
                    MINUTES;
                    HOURS;
                }
                ```

        - ```void lockInterruptibly()```: Gets lock if available and returns. If not available, it will wait. While waiting, if thread is interrupted, it won't get the lock.

        - ```void unlock()```

            - To release the lock

            - If lock not available with the thread, RuntimeError: IllegalMonitorStateException

- ReentrantLock(C)

    - The implementation class of Lock(I) and the direct child class of Object

    - Reentrant because thread can acquire same lock multiple times. This increments the thread's personal count by 1 every time ```lock()``` is called, and decrements by 1 every time ```unlock()``` is called. The lock is released when count becomes 0.

    - Constructors

        - ```ReentrantLock l = new ReentrantLock()```

        - ```ReentrantLock l = new ReentrantLock(boolean fairness)```

            - If fairness is true, then the lock goes to the thread waiting for the longest when it is available (FCFS)

            - If fairness is false, the thread which gets the lock would be random.

            - Default value for fairness is false

    - Important methods

        - All methods of Lock(I)

        - ```int getHoldCount()```

            - Get the hold count of that thread

        - ```boolean isHeldByCurrentThread()```

            - Checks if lock is held by the calling thread

        - ```int getQueueLength()```

            - Number of waiting threads

        - ```Collection getQueuedThreads()```
        
            - Get a list of the threads in the queue

        - ```boolean hasQueuedThreads()```

            - Check presence of queued threads

        - ```boolean isLocked()```

            - Check if that object is locked by some thread

        - ```boolean isFair()```

            - Check if fair or not

        - ```Thread getOwner()```

            - Returns the owner of the thread

    - Thread pools (Executor Framework)

        - Creating new threads for every job can create performance problems. Instead, we use a pool of pre-created threads ready to do the job

        - Thread pool framework is also known as executor framework

        - To create thread pool, we use the following

            - ```ExecutorService service = Executors.newFixedThreadPool(3)```

            - ```service.submit(job)```

                - To submit a new job

            - ```service.shutdown()```

                - To shutdown service after task completion

            - While designing web servers and application servers, the underlying concept is of thread pool

### Collable and Future

- When using the run method, the thread won't return anything after completing the job

- If a thread is required to return a result, we use Callable(I)

- Callable(I) has only one method

    - ```public Object call() throws Exception```

- The thread returns sthe result in the form of a Future object

### ThreadLocal

- To define thread local variables. The class maintains value per thread basis. Each thread object maintains a separate value, like user id, transaction id for each thread that accesses the object

- Thread can access, manipulate and remove its value in any part of code executed in the thread

- E.g. servlet, which invokes some business methods. We require to generate a unique transaction id for every request, which is then passed to the business method. ThreadLocal can be used to maintain transaction id for every thread

- Introduced in 1.2v and enhanced in 1.5v

- It can be associated with thread scope. Once a thread goes into dead state, all its variables are eligible for garbage collection

- Methods

    - ```ThreadLocal l = new ThreadLocal()```

    - ```Object get()```

        - Returns value of thread local variable associated with current thread

    - ```Object initialValue()```

        - Returns value associated with variable by default. Default is null.

        - This method should be overridden to customize default value

    - ```void set(Object newValue)```

    - ```void remove()```

        - After removal, the variable will be initialized again with initialValue() method

- Parent thread's ThreadLocal variable is not available to child thread by default. For this, we should go for InheritableThreadLocal class.

- By default, child thread's value is same as parent thread, but can be customized by overriding ```public Object childValue(Object parentValue)```