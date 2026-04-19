# Lab: Parallel Task Processing with Callable (Advanced)

## Objective

- Use Callable for parallel computation  
- Compare first-result vs full aggregation  
- Understand completion order and performance  

---

## Problem Statement

Execute multiple tasks in parallel and:

1. Retrieve the first completed result  
2. Compute the sum of all results  

---

## Part A: Setup Tasks

```java
import java.util.concurrent.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {

        ExecutorService executor = Executors.newFixedThreadPool(3);

        List<Callable<Integer>> tasks = List.of(
            () -> { Thread.sleep(3000); return 10; },
            () -> { Thread.sleep(1000); return 20; },
            () -> { Thread.sleep(2000); return 30; }
        );
```

---

## Part B: First Result Wins (invokeAny)

```java
int fastestResult = executor.invokeAny(tasks);
System.out.println("Fastest Result: " + fastestResult);
```

Expected Output:

```
Fastest Result: 20
```

---

## Part C: Aggregate All Results (invokeAll)

```java
List<Future<Integer>> results = executor.invokeAll(tasks);

int sum = 0;
for (Future<Integer> f : results) {
    sum += f.get();
}

System.out.println("Sum of all results: " + sum);
```

Expected Output:

```
Sum of all results: 60
```

---

## Part D: Completion Order (CompletionService)

```java
CompletionService<Integer> service =
        new ExecutorCompletionService<>(executor);

for (Callable<Integer> task : tasks) {
    service.submit(task);
}

System.out.println("Results in completion order:");

for (int i = 0; i < tasks.size(); i++) {
    Future<Integer> result = service.take();
    System.out.println(result.get());
}
```

Expected Output:

```
20
30
10
```

---

## Part E: Performance Experiment

```java
long start = System.currentTimeMillis();

// run tasks

long end = System.currentTimeMillis();
System.out.println("Time: " + (end - start));
```

---

## Part F: Real-World Simulation

- Task 1: Database query (3s)  
- Task 2: Cache lookup (1s)  
- Task 3: API call (2s)  

---

## Reflection Questions

- Why does invokeAny return early?  
- When should you use invokeAll?  
- How does CompletionService improve performance?  
- Does more threads always mean faster execution?  

---

## Summary

Parallel programming involves deciding how and when to use results from concurrent tasks efficiently.
