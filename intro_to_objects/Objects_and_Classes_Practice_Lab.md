# Practice Lab: Objects and Classes in Java

------------------------------------------------------------------------

# Learning Objectives

After completing this lab, you will be able to:

-   Define classes with attributes and methods
-   Create and use objects
-   Understand constructors
-   Apply encapsulation using getters and setters
-   Override toString() method
-   Understand object references and memory concepts

------------------------------------------------------------------------

# Part 1 -- Creating a Simple Class

## Task 1: Create a Student Class

Create a class named `Student` with:

### Attributes:

-   String name
-   int age
-   double gpa

### Requirements:

1.  Create a constructor to initialize all attributes.
2.  Create getter and setter methods.
3.  Create a method `displayInfo()` that prints student details.
4.  Override `toString()`.

------------------------------------------------------------------------

## Example Usage (Main Method)

``` java
public class Main {
    public static void main(String[] args) {

        Student s1 = new Student("Alice", 20, 3.8);
        s1.displayInfo();

        s1.setGpa(3.9);
        System.out.println(s1);

    }
}
```

------------------------------------------------------------------------

# Part 2 -- Understanding Object References

## Task 2: Reference Behavior

1.  Create a second reference variable:

``` java
Student s2 = s1;
```

2.  Change the name using `s2.setName("Bob");`
3.  Print `s1` and `s2`.

### Reflection:

-   Why did both objects change?
-   Are s1 and s2 two separate objects?

------------------------------------------------------------------------

# Part 3 -- Multiple Objects

## Task 3

Create three different Student objects.

Store them inside an `ArrayList<Student>`.

Print all students using:

-   Traditional loop
-   Enhanced for-loop

------------------------------------------------------------------------

# Part 4 -- Class with Behavior

## Task 4: Create a BankAccount Class

Attributes: - String accountHolder - double balance

Methods: - deposit(double amount) - withdraw(double amount) -
getBalance() - toString()

Rules: - Prevent withdrawal if balance is insufficient. - Print
appropriate messages.

------------------------------------------------------------------------

## Example Usage

``` java
BankAccount account = new BankAccount("John", 1000);
account.deposit(500);
account.withdraw(200);
System.out.println(account);
```

------------------------------------------------------------------------

# Part 5 -- Static vs Instance Members

Modify `BankAccount`:

1.  Add a static variable `totalAccounts`.
2.  Increment it inside the constructor.
3.  Create a static method `getTotalAccounts()`.

Test by creating multiple accounts.

------------------------------------------------------------------------

# Part 6 -- Theoretical Questions

1.  What is the difference between a class and an object?
2.  Where are objects stored in memory?
3.  What does the `new` keyword do?
4.  Why is encapsulation important?
5.  What is the purpose of overriding `toString()`?

------------------------------------------------------------------------

# Bonus Challenge (Advanced)

1.  Create a `Rectangle` class with:

    -   length
    -   width
    -   area()
    -   perimeter()

2.  Add constructor overloading.

3.  Create UML diagram of Student and BankAccount classes.

------------------------------------------------------------------------

# Submission Requirements

-   All classes must be properly structured.
-   Include properly formatted Java code blocks:

``` java
// Your code here
```

-   Answer all theoretical questions.
