# 🧪 Lab: Understanding and Using Wrapper Classes in Java

## 🎯 Objectives

By the end of this lab, students will: - Understand Java Wrapper
Classes - Perform boxing and unboxing - Use wrapper utility methods -
Store wrapper objects inside ArrayList - Apply Character class utility
methods

------------------------------------------------------------------------

## 📘 Background

Java primitive types: `int`, `double`, `char`, `boolean`

Wrapper classes: `Integer`, `Double`, `Character`, `Boolean`

Collections like `ArrayList` require objects --- not primitives.

------------------------------------------------------------------------

# 🔬 Part 1 --- Boxing and Unboxing

### Task 1.1 --- Manual Boxing

1.  Create an `int` variable.
2.  Convert it to an `Integer` using `Integer.valueOf()`.
3.  Print both values.

### Task 1.2 --- Auto Boxing and Unboxing

1.  Assign an int directly to an Integer.
2.  Assign an Integer back to an int.
3.  Print both values.

### Reflection Questions

1.  What is the difference between primitive and wrapper types?
2.  When does auto-boxing occur?

------------------------------------------------------------------------

# 🔬 Part 2 --- Wrapper Utility Methods

### Task 2.1 --- Convert String to Integer

1.  Create a string `"123"`.
2.  Convert it using `Integer.parseInt()`.
3.  Add 10 and print result.

### Task 2.2 --- Print Limits

Print: - `Integer.MAX_VALUE` - `Integer.MIN_VALUE`

### Reflection

Why are these constants useful in programming?

------------------------------------------------------------------------

# 🔬 Part 3 --- Wrapper Classes with ArrayList

1.  Create an `ArrayList<Integer>`.
2.  Add at least 3 numbers.
3.  Compute and print their sum.

### Question

Why can't we use `ArrayList<int>`?

------------------------------------------------------------------------

# 🔬 Part 4 --- Character Wrapper

1.  Declare a character.
2.  Use:
    -   `Character.isUpperCase()`
    -   `Character.isDigit()`
    -   `Character.isLetter()`
3.  Print results.

------------------------------------------------------------------------

# 🚀 Bonus Challenge

1.  Ask user for 5 numbers (as strings).
2.  Convert them to Integer objects.
3.  Store in ArrayList.
4.  Compute:
    -   Sum
    -   Average
    -   Maximum (without using Collections.max)

------------------------------------------------------------------------

# 📊 Submission

Submit: - All `.java` files - Reflection answers - Clean formatting -
Proper comments

