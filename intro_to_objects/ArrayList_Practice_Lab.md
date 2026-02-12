# Practice Lab: Mastering ArrayList in Java

------------------------------------------------------------------------

## Learning Objectives

After completing this lab, you will be able to:

-   Create and manipulate an `ArrayList`
-   Add, remove, and update elements dynamically
-   Traverse an `ArrayList` using different techniques
-   Analyze time complexity of common `ArrayList` operations
-   Compare `ArrayList` behavior with fixed-size arrays
-   Implement simple search and data-processing logic using `ArrayList`

------------------------------------------------------------------------

# Part 1 -- Creating and Using an ArrayList

## Task 1: Create an ArrayList of Integers

Create an `ArrayList<Integer>` named `scores`.

-   Add the following values: `85, 92, 78, 90, 88`
-   Print all elements
-   Print the size of the list

### Expected Output Format:

    Scores: 85 92 78 90 88
    Size: 5

### Concept Check

1.  What is the difference between:

    ``` java
    int[] arr = new int[5];
    ```

    and

    ``` java
    ArrayList<Integer> list = new ArrayList<>();
    ```

2.  Can `ArrayList` store primitive types directly?

------------------------------------------------------------------------

# Part 2 -- Traversing the ArrayList

## Task 2: Traverse in Three Ways

Using the same `scores` list:

1.  Traverse using a traditional `for` loop (index-based)
2.  Traverse using an enhanced `for-each` loop
3.  Traverse using `.forEach()` with a lambda expression

### Discussion Question

-   Which traversal method gives you access to the index?
-   Why might that matter?

------------------------------------------------------------------------

# Part 3 -- Modifying Elements

## Task 3: Update and Remove

1.  Change the score `78` to `80`
2.  Remove the score `92`
3.  Print the updated list

Then answer:

-   What happens to the indexes after removal?
-   What is the time complexity of removing from the middle?

------------------------------------------------------------------------

# Part 4 -- Searching the List

## Task 4: Implement Manual Search

Write a method:

``` java
public static int linearSearch(ArrayList<Integer> list, int target)
```

Return: - The index if found - `-1` if not found

Test with: - Search for `90` - Search for `100`

### Theoretical Question

-   What is the time complexity of searching in an `ArrayList`?
-   Why?

------------------------------------------------------------------------

# Part 5 -- Insertions at Different Positions

## Task 5

1.  Insert `95` at the beginning
2.  Insert `70` at index 2
3.  Insert `100` at the end

Print the list after each insertion.

### Complexity Analysis Table

For a list of size `n`, determine the time complexity of:

  Operation             Time Complexity
--------------------- -----------------
  Add at end            
  Add at beginning      
  Remove at end         
  Remove at beginning   
  Access by index       

Fill this table in your submission.

------------------------------------------------------------------------

# Part 6 -- Mini Project

## Student Management System (Mini Version)

Create an `ArrayList<String>` that stores student names.

Implement:

1.  Add student
2.  Remove student
3.  Display all students
4.  Search student
5.  Display total count

Use a simple menu-driven program:

    1. Add Student
    2. Remove Student
    3. Search Student
    4. Display All
    5. Exit

------------------------------------------------------------------------

# Reflection Questions

1.  Why is `ArrayList` considered dynamic?
2.  How does it grow internally?
3.  What is capacity vs size?
4.  When would you prefer an array over an `ArrayList`?

------------------------------------------------------------------------

# Bonus Challenge (Advanced)

1.  Create an `ArrayList<Double>` and compute:

    -   Average
    -   Maximum
    -   Minimum

2.  Convert an `ArrayList` to an array.

3.  Compare `ArrayList` vs `LinkedList` in terms of:

    -   Insertions
    -   Memory
    -   Random access

------------------------------------------------------------------------

# Submission Requirements

-   Include properly formatted Java code blocks:

    ``` java
    // your code here
    ```

-   Include answers to all theoretical questions

-   Include time complexity analysis
