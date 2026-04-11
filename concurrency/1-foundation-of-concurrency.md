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
