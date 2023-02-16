# Introduction

JVM divides into memory and heap.
- declare new variables and objects, call a new method, declare a String, or perform similar operations
- JVM designates memory to these operations from either Stack Memory or Heap Space.

## Stacks
- Stack Memory in Java is used for static memory allocation and the execution of a thread. 
- It contains primitive values that are specific to a method and references to objects referred from the method that are in a heap.
-  Access to this memory is in Last-In-First-Out (LIFO) order. Whenever we call a new method, a new block is created on top of the stack which contains values specific to that method, like primitive variables and references to objects.
-  When the method finishes execution, its corresponding stack frame is flushed, the flow goes back to the calling method, and space becomes available for the next method.

### Features of stack memory
- It grows and shrinks as new methods are called and returned, respectively.
- Variables inside the stack exist only as long as the method that created them is running.
- It's automatically allocated and deallocated when the method finishes execution.
- If this memory is full, Java throws java.lang.StackOverFlowError.
- Access to this memory is fast when compared to heap memory.
- This memory is threadsafe, as each thread operates in its own stack.

## Heaps
Heap space is used for the dynamic memory allocation of Java objects and JRE classes at runtime. New objects are always created in heap space, and the references to these objects are stored in stack memory.
These objects have global access and we can access them from anywhere in the application.

We can break this memory model down into smaller parts, called generations, which are:

- __Young Generation__ – this is where all new objects are allocated and aged. A minor Garbage collection occurs when this fills up.
- __Old or Tenured Generation__ – this is where long surviving objects are stored. When objects are stored in the Young Generation, a threshold for the object's age is set, and when that threshold is reached, the object is moved to the old generation.
- __Permanent Generation__ – this consists of JVM metadata for the runtime classes and application methods.
