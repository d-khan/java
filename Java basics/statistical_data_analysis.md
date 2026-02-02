# Lab: Statistical Data Analysis Using Java (No Classes, No Objects)

## Course Context

Introductory Java / Programming Fundamentals

## Lab Title

**Basic Statistics and Data Analysis Using Java Arrays**

---

## Lab Overview

In this lab, you will use **basic Java programming constructs** to analyze a numerical dataset and compute **statistical measures** commonly used in data science.

You will simulate a real-world **data analysis workflow**:

- Data collection
- Data organization
- Statistical computation
- Interpretation of results

All code must be written inside the `main` method using **primitive types, arrays, loops, and conditionals** only.

---

## Learning Objectives

By the end of this lab, students will be able to:

- Store numeric data in arrays
- Use loops to process datasets
- Sort data manually using loops
- Compute statistical measures:
  - Mean
  - Median
  - Range
  - Variance
  - Standard deviation
- Interpret numerical results programmatically

---

## Rules & Constraints

### ✅ Allowed

- One Java file: `Main.java`
- Code inside `public static void main(String[] args)`
- Primitive types (`int`, `double`)
- `String`
- `Scanner`
- Arrays
- Loops (`for`, `while`)
- Conditionals (`if`, `else`)
- `Math.sqrt()`

### ❌ Not Allowed

- Creating additional classes
- Creating custom objects
- Writing methods outside `main`
- Using Java collections (`ArrayList`, `HashMap`, etc.)
- Using built-in sorting utilities (`Arrays.sort`)

---

## Problem Scenario: Daily Temperature Analysis

You are given daily temperature readings collected over multiple days.  
Your task is to analyze the data and compute **descriptive statistics**.

---

## Starter Code

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        // Your code starts here
    }
}
```

---

## Part 1: Data Collection

1. Ask the user how many days of temperature data will be entered.
2. Create a `double` array of that size.
3. Ask the user to enter the temperature for each day.
4. Store all values in the array.

---

## Part 2: Mean (Average)

Calculate and print the **mean temperature**.

Formula:

```
mean = (sum of all values) / number of values
```

---

## Part 3: Sorting the Data

Sort the temperature array in **ascending order** using **loops only**.

After sorting, print the sorted temperatures.

---

## Part 4: Median

Calculate the **median temperature**:

- If the number of values is **odd** → middle value
- If the number of values is **even** → average of the two middle values

---

## Part 5: Range

Calculate and print the **range** of the dataset:

```
range = maximum value − minimum value
```

---

## Part 6: Variance

Calculate the **variance** using the formula:

```
variance = Σ(x − mean)² / n
```

---

## Part 7: Standard Deviation

Calculate the **standard deviation**:

```
standard deviation = √variance
```

Use:

```java
Math.sqrt(variance)
```

---

## Part 8: Data Insight

Based on the standard deviation:

- If standard deviation < 2 → print `Temperatures are very consistent`
- If standard deviation < 5 → print `Temperatures show moderate variation`
- Otherwise → print `Temperatures vary significantly`

---

## Sample Output (Partial)

```
Enter number of days: 5
Enter temperature for day 1: 72.5
Enter temperature for day 2: 75.0
Enter temperature for day 3: 70.0
Enter temperature for day 4: 68.5
Enter temperature for day 5: 74.0

Sorted Temperatures:
68.5 70.0 72.5 74.0 75.0

Mean: 72.0
Median: 72.5
Range: 6.5
Variance: 5.7
Standard Deviation: 2.39

Temperatures show moderate variation
```

---

## Submission Requirements

- Submit **one Java file** named `Main.java`
- Program must compile and run
- All logic must be inside the `main` method
- Use proper indentation and comments

---

## Grading Rubric (100 Points)

| Category                 | Points |
| ------------------------ | ------ |
| Data Input & Storage     | 15     |
| Sorting Logic            | 20     |
| Statistical Calculations | 35     |
| Output & Formatting      | 15     |
| Code Quality & Comments  | 15     |

---

## Bonus (Optional)

- Format output to **2 decimal places**
- Validate temperature input
- Count how many days were above the mean
- Display the coldest and hottest day

---

**End of Lab**
