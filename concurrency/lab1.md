# Lab: Parallel Counter using Runnable (Race Condition Exploration)

## Objective

- Understand how multiple threads run in parallel  
- Observe race conditions  
- Learn why synchronization is needed  

---

## Problem Statement

Create multiple threads using `Runnable` where each thread increments a shared counter. Analyze whether the final result is correct.

---

## Starter Code

```java
class Counter {
    int value = 0;
}

public class Main {
    public static void main(String[] args) throws Exception {

        Counter counter = new Counter();

        // Runnable task
        Runnable task = () -> {
            for (int i = 0; i < 1000; i++) {
                counter.value++;   // critical section
            }
        };

        Thread t1 = new Thread(task);
        Thread t2 = new Thread(task);

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Final Counter: " + counter.value);
    }
}
```

---

## Expected Outcome

- Expected value = **2000**
- Actual value → often **less than 2000**

---

## Task 1: Run Multiple Times

- Run program 5 times  
- Record outputs  

---

## Task 2: Fix Using synchronized

```java
class Counter {
    int value = 0;

    synchronized void increment() {
        value++;
    }
}
```

Modify task:

```java
Runnable task = () -> {
    for (int i = 0; i < 1000; i++) {
        counter.increment();
    }
};
```

---

## Expected Result After Fix

- Final Counter = **2000 (consistent)**

---

## Task 3: Increase Threads

- Change to 5 threads  
- Each increments 1000 times  

---

## Task 4: Add Sleep (Visualizing Parallelism)

```java
Runnable task = () -> {
    for (int i = 1; i <= 5; i++) {
        System.out.println(Thread.currentThread().getName() + " : " + i);
        try {
            Thread.sleep(500);
        } catch (InterruptedException e) {}
    }
};
```

---

## Reflection Questions

- Why does the incorrect result occur?  
- What is a race condition?  
- Why does `synchronized` fix the issue?  
- Does more threads always mean faster execution?  

---

## Summary

Multiple threads running the same task can lead to incorrect results if shared data is not properly synchronized.
