# Module 1: Foundations of Concurrency
## 1. Learning Outcomes

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

Runnable represents “a piece of work (task) that a thread can run.”
