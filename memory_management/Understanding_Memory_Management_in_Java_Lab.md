# 🧪 Lab: Understanding Memory Management in Java

## 🎯 Learning Objectives

By the end of this lab, students will be able to:

1.  Distinguish between **stack memory** and **heap memory**
2.  Understand how **object references** work in Java
3.  Observe **garbage collection behavior**
4.  Identify potential **memory leaks**
5.  Explain how Java manages memory automatically

------------------------------------------------------------------------

# 📘 Part 1 --- Stack vs Heap

## 🔹 Concept Review

-   **Primitive variables** → stored in stack\
-   **Object references** → stored in stack\
-   **Objects themselves** → stored in heap

------------------------------------------------------------------------

## 📝 Task 1: Trace the Memory

``` java
public class MemoryTest1 {
    public static void main(String[] args) {
        int x = 10;
        String name = "Danish";
        Student s1 = new Student("Ali", 20);

        modify(x, s1);

        System.out.println("x = " + x);
        System.out.println("Student age = " + s1.age);
    }

    static void modify(int x, Student s) {
        x = 50;
        s.age = 99;
    }
}

class Student {
    String name;
    int age;

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

### 🔎 Questions

1.  Where is `x` stored?
2.  Where is `s1` stored?
3.  Where is the `Student` object stored?
4.  Why does `x` remain 10 after `modify()`?
5.  Why does `s1.age` change?

### 🎯 Deliverable

Draw a **memory diagram** showing: - Stack frame of `main` - Stack frame
of `modify` - Heap object(s)

------------------------------------------------------------------------

# 📘 Part 2 --- Object References and Aliasing

## 📝 Task 2: Reference Copying

``` java
public class MemoryTest2 {
    public static void main(String[] args) {
        Student s1 = new Student("Sara", 22);
        Student s2 = s1;

        s2.age = 30;

        System.out.println(s1.age);
    }
}
```

### 🔎 Questions

1.  How many objects are created?
2.  How many references exist?
3.  Why does modifying `s2` affect `s1`?

### 🎯 Deliverable

Explain in 5--7 sentences how reference copying works in Java.

------------------------------------------------------------------------

# 📘 Part 3 --- Garbage Collection

## 🔹 Concept Review

Java automatically reclaims memory for objects that: - Are no longer
referenced - Become unreachable

## 📝 Task 3: Eligible for Garbage Collection

``` java
public class MemoryTest3 {
    public static void main(String[] args) {
        Student s1 = new Student("John", 18);
        Student s2 = new Student("Emma", 19);

        s1 = s2;
    }
}
```

### 🔎 Questions

1.  How many objects are created?
2.  Which object becomes eligible for garbage collection?
3.  At what line does that happen?
4.  Does Java immediately delete it?

### 🎯 Experiment

Add:

``` java
@Override
protected void finalize() throws Throwable {
    System.out.println("Object is being garbage collected");
}
```

Run multiple times.

Do you always see the message? Why or why not?

------------------------------------------------------------------------

# 📘 Part 4 --- Memory Leak Simulation

## 📝 Task 4: Static Reference Leak

``` java
import java.util.ArrayList;

public class MemoryLeakExample {

    static ArrayList<Student> students = new ArrayList<>();

    public static void main(String[] args) {

        for(int i = 0; i < 100000; i++) {
            students.add(new Student("Student" + i, i));
        }

        System.out.println("Done creating students");
    }
}
```

### 🔎 Questions

1.  Why are these objects NOT garbage collected?
2.  What would you change to fix this?
3.  Modify the code to prevent the leak.

------------------------------------------------------------------------

# 📘 Part 5 --- Forcing Memory Pressure

## 📝 Task 5: OutOfMemoryError

``` java
import java.util.ArrayList;

public class MemoryPressure {
    public static void main(String[] args) {

        ArrayList<int[]> list = new ArrayList<>();

        while(true) {
            list.add(new int[1000000]);
        }
    }
}
```

### 🔎 Questions

1.  What exception occurs?
2.  Why does it happen?
3.  What JVM argument can limit heap size?

Try running with:

    -Xmx128m

------------------------------------------------------------------------

# 📘 Part 6 --- Reflection / Conceptual Questions

1.  Why doesn't Java allow manual memory deallocation?
2.  What is the advantage of garbage collection?
3.  What is the trade-off compared to C++?
4.  What is a "strong reference"?

------------------------------------------------------------------------

# 🧠 Advanced Challenge (Optional)

-   Use `Runtime.getRuntime().totalMemory()`\
-   Use `Runtime.getRuntime().freeMemory()`\
-   Track memory before and after object creation\
-   Print memory usage statistics

------------------------------------------------------------------------
