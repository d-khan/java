# Lab: Java Programming Fundamentals (Without Classes & Objects)

## Course Context

Introductory Java / Programming Fundamentals

## Lab Title

**Java Basics Using a Single `main` Method (No Objects, No Custom Classes)**

---

## Lab Overview

In this lab, you will practice **core Java programming concepts** using only:

- Primitive data types  
- Variables  
- Operators  
- Control structures  
- Arrays  
- Code written inside the `main` method  

You will **not** create custom classes or objects. Everything will be written inside a **single Java file** using the `main` method.

This lab focuses on **problem solving and program flow**, not object-oriented programming.

---

## Learning Objectives

By the end of this lab, students will be able to:

- Write and execute a Java program using `main`
- Declare and use primitive variables
- Perform arithmetic and logical operations
- Use conditional statements (`if`, `if-else`, `switch`)
- Use loops (`for`, `while`)
- Work with arrays
- Read user input using `Scanner`
- Display formatted output

---

## Rules & Constraints

### ✅ Allowed

- `public class Main`
- `public static void main(String[] args)`
- Primitive data types (`int`, `double`, `char`, `boolean`)
- `String`
- `Scanner`
- Control structures (`if`, `else`, `switch`)
- Loops (`for`, `while`)
- Arrays

### ❌ Not Allowed

- Creating additional classes
- Creating custom objects
- Instance variables
- Methods outside `main`
- Any object-oriented concepts (constructors, inheritance, polymorphism)

---

## Starter Code

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        // Your code starts here
    }
}
```

---

## Part 1: Variables & Arithmetic

### Task 1.1 – Variable Declaration

Declare and initialize the following variables:

- Two integers  
- One double  
- One character  
- One boolean  

Print each variable on a separate line.

---

### Task 1.2 – Arithmetic Operations

Using the two integers declared above, calculate and print:

- Sum  
- Difference  
- Product  
- Quotient (as a double)  
- Remainder  

---

## Part 2: User Input

### Task 2.1 – Basic Input

Ask the user to enter:

- Their name  
- Their age  

Print a message in the following format:

```
Hello Danish, you will be 25 next year.
```

---

### Task 2.2 – Comparing Numbers

Ask the user to enter **two integers**.

Print the **larger number**.

---

## Part 3: Decision Making

### Task 3.1 – `if / else`

Ask the user to enter an integer.

- Print `Positive` if the number is greater than zero
- Print `Negative` if the number is less than zero
- Print `Zero` otherwise

---

### Task 3.2 – `switch`

Ask the user to enter a number between **1 and 7**.

Use a `switch` statement to print the corresponding day of the week.

---

## Part 4: Loops

### Task 4.1 – `for` Loop

Use a `for` loop to print numbers from **1 to 20** on one line.

---

### Task 4.2 – `while` Loop

Repeatedly ask the user to enter integers until they enter `-1`.

After the loop ends, print the **sum of all numbers entered** (excluding `-1`).

---

### Task 4.3 – Nested Loops

Use nested loops to print the following pattern:

```
*
**
***
****
*****
```

---

## Part 5: Arrays

### Task 5.1 – Array Input

Create an integer array of size **5**.

- Ask the user to enter 5 numbers
- Store the values in the array
- Print all elements
- Calculate and print:
  - Sum
  - Average

---

### Task 5.2 – Min & Max

Using the same array, determine and print:

- The maximum value
- The minimum value

---

## Part 6: Mini Program (Integrated Practice)

Write a program that:

1. Asks how many students are in a class
2. Creates an array to store their exam scores
3. Calculates and prints:
   - Average score
   - Highest score
   - Number of students who passed (score ≥ 60)

---

## Submission Requirements

- Submit **one Java file** named `Main.java`
- Code must compile and run without errors
- Follow proper indentation and commenting
- All work must be inside the `main` method

---

## Grading Rubric (100 Points)

| Section                | Points |
| ---------------------- | ------ |
| Variables & Arithmetic | 15     |
| User Input             | 15     |
| Conditionals           | 20     |
| Loops                  | 20     |
| Arrays                 | 20     |
| Code Quality           | 10     |

---

## Bonus (Optional)

- Use `printf` for formatted output
- Validate user input
- Add comments explaining your logic

---

**End of Lab**
