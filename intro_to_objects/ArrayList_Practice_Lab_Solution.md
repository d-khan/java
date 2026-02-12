# ArrayList Practice Lab -- Solution Version

------------------------------------------------------------------------

# Part 1 -- Creating and Using an ArrayList

``` java
import java.util.ArrayList;

public class Part1 {
    public static void main(String[] args) {
        ArrayList<Integer> scores = new ArrayList<>();

        scores.add(85);
        scores.add(92);
        scores.add(78);
        scores.add(90);
        scores.add(88);

        System.out.print("Scores: ");
        for (int score : scores) {
            System.out.print(score + " ");
        }

        System.out.println("\nSize: " + scores.size());
    }
}
```

### Concept Check Answers

-   Arrays have fixed size; ArrayList is dynamic.
-   ArrayList cannot store primitive types directly (uses wrapper
    classes like Integer).

------------------------------------------------------------------------

# Part 2 -- Traversing the ArrayList

``` java
for (int i = 0; i < scores.size(); i++) {
    System.out.println(scores.get(i));
}

for (int score : scores) {
    System.out.println(score);
}

scores.forEach(score -> System.out.println(score));
```

-   Only the traditional for-loop gives index access.

------------------------------------------------------------------------

# Part 3 -- Modifying Elements

``` java
scores.set(scores.indexOf(78), 80);
scores.remove(Integer.valueOf(92));

System.out.println(scores);
```

Answers:

-   Elements shift left after removal.
-   Removing from middle: O(n)

------------------------------------------------------------------------

# Part 4 -- Linear Search Implementation

``` java
public static int linearSearch(ArrayList<Integer> list, int target) {
    for (int i = 0; i < list.size(); i++) {
        if (list.get(i) == target) {
            return i;
        }
    }
    return -1;
}
```

-   Time complexity: O(n)

------------------------------------------------------------------------

# Part 5 -- Insertions

``` java
scores.add(0, 95);     // Beginning
scores.add(2, 70);     // Index 2
scores.add(100);       // End

System.out.println(scores);
```

### Time Complexity Table

  Operation             Time Complexity
--------------------- ------------------
  Add at end            O(1)\* amortized
  Add at beginning      O(n)
  Remove at end         O(1)
  Remove at beginning   O(n)
  Access by index       O(1)

------------------------------------------------------------------------

# Part 6 -- Mini Project Solution

``` java
import java.util.ArrayList;
import java.util.Scanner;

public class StudentManager {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ArrayList<String> students = new ArrayList<>();
        int choice;

        do {
            System.out.println("\n1. Add Student");
            System.out.println("2. Remove Student");
            System.out.println("3. Search Student");
            System.out.println("4. Display All");
            System.out.println("5. Exit");
            System.out.print("Choice: ");
            choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
                case 1:
                    System.out.print("Enter name: ");
                    students.add(scanner.nextLine());
                    break;

                case 2:
                    System.out.print("Enter name to remove: ");
                    students.remove(scanner.nextLine());
                    break;

                case 3:
                    System.out.print("Enter name to search: ");
                    String name = scanner.nextLine();
                    if (students.contains(name))
                        System.out.println("Student found.");
                    else
                        System.out.println("Student not found.");
                    break;

                case 4:
                    System.out.println("Students: " + students);
                    break;

            }

        } while (choice != 5);

        scanner.close();
    }
}
```

------------------------------------------------------------------------

# Reflection Answers

1.  ArrayList is dynamic because it resizes automatically.
2.  Internally backed by a dynamic array.
3.  Size = number of elements stored. Capacity = internal array size.
4.  Prefer arrays when fixed size and performance predictability are
    required.

------------------------------------------------------------------------

# Bonus Solution

``` java
ArrayList<Double> numbers = new ArrayList<>();
numbers.add(10.5);
numbers.add(5.2);
numbers.add(8.3);

double sum = 0;
double max = numbers.get(0);
double min = numbers.get(0);

for (double num : numbers) {
    sum += num;
    if (num > max) max = num;
    if (num < min) min = num;
}

double average = sum / numbers.size();

System.out.println("Average: " + average);
System.out.println("Max: " + max);
System.out.println("Min: " + min);
```
