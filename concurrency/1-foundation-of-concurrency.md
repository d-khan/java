# Module 1: Foundations of Concurrency
## Learning Outcomes

By the end of this module, students should be able to:

- Distinguish between processes and threads
- Explain concurrency vs parallelism
- Understand why concurrency is important in modern systems
- Create tasks using Runnable and Callable
- Understand the basic use of the Thread class

## What is Concurrency?

Concurrency refers to the ability of a system to handle multiple tasks that overlap in time.

> It does not necessarily mean tasks run at the exact same time — they may interleave execution.

**Key Idea**
- Concurrency = structure of program
- Parallelism = actual simultaneous execution

## Process vs Thread
**Process**
- Independent program in execution
- Has its own memory space
- Heavyweight

**Thread**
- Lightweight unit of execution within a process
- Shares memory with other threads in the same process
- Faster communication

**Example**
- Process: Web browser
- Threads:
  - UI rendering
  - Network requests
  - JavaScript execution

<img width="768" height="497" alt="image" src="https://github.com/user-attachments/assets/777ecc24-125f-4316-848b-0c966dc07d06" />


## **Concurrency vs Parallelism**

| Concept     | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Concurrency | Multiple tasks making progress (not necessarily simultaneously) |
| Parallelism | Multiple tasks executing **at the same time** on multiple cores |

### Simple Analogy

- Concurrency → One chef cooking multiple dishes (switching tasks)
- Parallelism → Multiple chefs cooking different dishes simultaneously

A clearer example of concurrency is this:
	•	You are cooking pasta
	•	At the same time, you are watching the stove
	•	While the water is boiling, you chop vegetables
	•	Then you stir the pasta
	•	Then you go back to cutting vegetables
  
### Key Insight

- A system can be **concurrent without being parallel**
- Parallelism requires **multiple cores/processors**

<img width="1070" height="708" alt="image" src="https://github.com/user-attachments/assets/a92956bd-19d8-4e37-a3bb-52945dd9fedd" />

## **Why Concurrency?**

### **Responsiveness**

- Applications remain interactive
- Example: UI does not freeze during file download

### **Throughput**

- More work completed in less time
- Example: Handling multiple web requests

### **Resource Utilization**

- CPU stays busy while waiting for I/O

## What is Runnable?

In Java, Runnable is a functional interface used to define a task that can be executed by a thread.

👉 In simple terms:

> Runnable represents “a piece of work (task) that a thread can run.”

Instead of telling a thread how to behave, you give it a task.

- Runnable = What to do
- Thread = Who executes it

### How It Works (Conceptual Flow)
1. You create a class (or lambda) that implements Runnable
2. Put your task inside run()
3. Pass it to a Thread
4. Call start() → thread executes run()

### Example 1: Simple Counter Task
```java
class CounterTask implements Runnable {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Count: " + i);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        new Thread(new CounterTask()).start();
    }
}
```

``` class CounterTask implements Runnable { ```
- This defines a class named CounterTask.
- The keyword implements Runnable means that this class agrees to provide the run() method required by the Runnable interface.
- In other words, CounterTask represents a task that can be executed by a thread.

``` public void run() { ```
- This is the run() method.
- Since Runnable has one method called run(), this class must define it.
- The code inside this method is the task that will be performed when the thread runs.

``` new Thread(new CounterTask()).start(); ```
This line does several things.

``` new CounterTask() ```
- This creates an object of the CounterTask class.
- Since CounterTask implements Runnable, this object is a task.

``` new Thread(new CounterTask()) ```
- This creates a new Thread object.
- The CounterTask object is passed to the thread.
- So the thread knows which task it should execute.

``` .start(); ```
- This starts the new thread.
- When the thread starts, it automatically calls the run() method of the CounterTask object.
- That means the loop begins running in a separate thread.

**Overall flow of the program**

Here is what happens step by step:

1. The program starts in main().
2. A CounterTask object is created.
3. A Thread object is created and given that task.
4. start() is called on the thread.
5. The thread begins execution and calls run().
6. The for loop prints the numbers 1 to 5.

### Example 2: Printing Thread Name
```java
class NameTask implements Runnable {
    public void run() {
        System.out.println("Running in: " + Thread.currentThread().getName());
    }
}

public class Main {
    public static void main(String[] args) {
        Thread t1 = new Thread(new NameTask(), "Worker-1");
        t1.start();
    }
}
```
### Example 3:  Multiple Threads Using Same Runnable
```java
class Task implements Runnable {
    public void run() {
        System.out.println(Thread.currentThread().getName() + " is working");
    }
}

public class Main {
    public static void main(String[] args) {
        Runnable task = new Task();
        // Note how the task and thread instructions are broken into double lines
        new Thread(task, "Thread-A").start();
        new Thread(task, "Thread-B").start();
    }
}
```

### Example 4:  Sequential vs Concurrent Execution
- One task sleeps (slow)
- One task runs fast
- Compare sequential vs concurrent

**Sequential version**

```java
class SleepTask {
    void run() {
        try {
            Thread.sleep(5000); // 5 seconds
            System.out.println("SleepTask done");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

class PrintTask {
    void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Print: " + i);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        SleepTask t1 = new SleepTask();
        PrintTask t2 = new PrintTask();

        t1.run(); // runs first
        t2.run(); // runs after 5 seconds
    }
}
```
**Concurrent version**
```java
class SleepTask implements Runnable {
    public void run() {
        try {
            Thread.sleep(5000);
            System.out.println("SleepTask done");
        } catch (InterruptedException e) {
            System.out.println("Thread was interrupted!");
        }
    }
}

class PrintTask implements Runnable {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Print: " + i);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        new Thread(new SleepTask()).start();
        new Thread(new PrintTask()).start();
    }
}
```

In Java, InterruptedException is thrown when a thread is:
> interrupted while it is sleeping, waiting, or blocked

**Why not just one thread?**

- You can use one thread.
- But then everything runs sequentially, not concurrently.

**Difference between a process, a task and a thread**
| **Concept** | **Meaning**      |
| ----------- | ---------------- |
| Process     | A full kitchen 🍳 |
| Thread      | A chef 👨‍🍳        |
| Task        | A recipe 📄       |

- You need a chef (thread) to execute a recipe (task)
- The kitchen (process) provides the environment

> The term "thread" in computing is derived from its everyday meaning as a thin strand, such as a thread of fabric, which runs through and connects parts of a material. In the context of computer science, a thread represents a single, continuous path of execution within a program, much like a strand running through a larger structure. A program (or process) can be thought of as the complete fabric, while threads are the individual lines of execution that pass through it. This analogy emphasizes that multiple threads can exist within the same process, each performing its own sequence of instructions while sharing the same underlying resources. The term gained prominence in operating systems research to describe these lightweight units of execution, distinguishing them from heavier processes, and highlighting their ability to enable concurrent activity within a single program.

**Can one thread perform two tasks?**
Short answer: No—one thread cannot execute two tasks at the exact same time.
But it can handle multiple tasks one after another.

A thread represents:

👉 One single sequence of execution

So at any given instant:
- It is executing only one instruction
- Therefore, only one task at a time

```java
Runnable task1 = () -> System.out.println("Task 1");
Runnable task2 = () -> System.out.println("Task 2");

Thread t = new Thread(() -> {
    task1.run();  // runs first
    task2.run();  // runs after
});

t.start();
```
**Output**
```txt
Task 1
Task 2
```

- A thread can handle multiple tasks, but only by executing them one at a time
- To run tasks at the same time, you need:
```java
new Thread(task1).start();
new Thread(task2).start();
```

> “A thread is like a single worker.
It can do many jobs, but only one job at a time.”

### "Using Lambda (Modern Java Style)"?

A lambda expression in Java is:

- A short, concise way to write a function (or task) without creating a separate class

It was introduced in Java 8 to simplify code, especially when working with functional interfaces like Runnable.

**Traditional Way (Before Lambdas)**
```java
class MyTask implements Runnable {
    public void run() {
        System.out.println("Task running");
    }
}

public class Main {
    public static void main(String[] args) {
        new Thread(new MyTask()).start();
    }
}
```

**Problems**
- Too much boilerplate
- Separate class just for one method

**Lambda Version (Modern Style)**
```java
public class Main {
    public static void main(String[] args) {

        new Thread(() -> {
            System.out.println("Task running");
        }).start();

    }
}
```

**Concurrent example using Lambda version**
```java
public class Main {
    public static void main(String[] args) {

        // SleepTask using lambda
        new Thread(() -> {
            try {
                Thread.sleep(5000);
                System.out.println("SleepTask done");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }).start();

        // PrintTask using lambda
        new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                System.out.println("Print: " + i);
            }
        }).start();
    }
}
```

Even though both threads use the same Runnable object:
- Each thread has its own execution path (stack)
- But they may share the same data (heap) if the task has fields

## What is Callable

## Thread class

Do NOT overuse Thread class directly in modern Java.

Why?
- Less flexible
- Cannot return results
- Harder to manage at scale

Prefer:
- Runnable
- Callable
- (Later modules → Thread Pools / Executors)
