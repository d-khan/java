# Searching algorithms

This lecture is an introductory level about searching and sorting algorithms.

## Linear search

- An **algorithm** is a sequence of steps for accomplishing a task. 
- **Linear search** is a search algorithm that starts from the beginning of a list, and checks each element until the search key is found or the end of the list is reached.

### Example - Linear search algorithm

```java
import java.util.Scanner;
public class LinearSearch {
    public static int linearSearch(int [] numbers, int key) {
        int i;

        for (i = 0; i < numbers.length; ++i) {
            if (numbers[i] == key) {
                return i;
            }
        }

        return -1; /* not found */
    }

    public static void main(String [] args) {
        Scanner scnr = new Scanner(System.in);
        int [] numbers = {2, 4, 7, 10, 11, 32, 45, 87};
        int i;
        int key;
        int keyIndex;

        System.out.print("NUMBERS: ");
        for (i = 0; i < numbers.length; ++i) {
            System.out.print(numbers[i] + " ");
        }
        System.out.println();

        System.out.print("Enter a value: ");
        key = scnr.nextInt();

        keyIndex = linearSearch(numbers, key);

        if (keyIndex == -1) {
            System.out.println(key + " was not found.");
        }
        else {
            System.out.println("Found " + key + " at index " + keyIndex + ".");
        }
    }
}
```

An algorithm's **runtime** is the time the algorithm takes to execute. If each comparison takes 1 µs (1 microsecond), a linear search algorithm's runtime is up to 1 s to search a list with 1,000,000 elements, 10 s for 10,000,000 elements, and so on. Ex: Searching Amazon's online store, which has more than 200 million items, could require more than 3 minutes.

An algorithm typically uses a number of steps proportional to the size of the input. For a list with 32 elements, linear search requires at most 32 comparisons: 1 comparison if the search key is found at index 0, 2 if found at index 1, and so on, up to 32 comparisons if the search key is not found. For a list with N elements, linear search thus requires at most N comparisons. The algorithm requires "on the order" of N comparisons.

## Binary search

The linear search may require searching all list elements, which can lead to long runtimes. For example, searching for a contact on a smartphone one by one from first to last can be time consuming. Because a contact list is sorted, a faster search, known as binary search, checks the middle contact first. If the desired contact comes alphabetically before the middle contact, binary search will then search the first half and otherwise the last half. Each step reduces the contacts that need to be searched by half.

[Animation of binary search](https://www.youtube.com/watch?v=DRsJ8sA9xzc&ab_channel=FreeCodeClass)

1. Elements with indices between low and high remain to be searched.
2. Search starts by checking the middle element.
3. If search key is greater than element, then only elements in right sublist need to be searched.
4. Each iteration reduces search space by half. Search continues until key found or search space is empty.

### Example - binary search algorithm

```java
import java.util.Scanner;

public class BinarySearch {
    public static int binarySearch(int [] numbers, int key) {
        int mid;
        int low;
        int high;

        low = 0;
        high = numbers.length - 1;

        while (high >= low) {
            mid = (high + low) / 2;
            if (numbers[mid] < key) {
                low = mid + 1;
            }
            else if (numbers[mid] > key) {
                high = mid - 1;
            }
            else {
                return mid;
            }
        }

        return -1; // not found
    }

    public static void main(String [] args) {
        Scanner scnr = new Scanner(System.in);
        int [] numbers = {2, 4, 7, 10, 11, 32, 45, 87};
        int i;
        int key;
        int keyIndex;

        System.out.print("NUMBERS: ");
        for (i = 0; i < numbers.length; ++i) {
            System.out.print(numbers[i] + " ");
        }
        System.out.println();

        System.out.print("Enter a value: ");
        key = scnr.nextInt();

        keyIndex = binarySearch(numbers, key);

        if (keyIndex == -1) {
            System.out.println(key + " was not found.");
        }
        else {
            System.out.println("Found " + key + " at index " + keyIndex + ".");
        }
    }
}
```

Binary search is incredibly efficient in finding an element within a sorted list. During each iteration or step of the algorithm, binary search reduces the search space (i.e., the remaining elements to search within) by half. The search terminates when the element is found, or the search space is empty (element not found). For a 32-element list, if the search key is not found, the search space is halved to have 16 elements, then 8, 4, 2, 1, and finally none, requiring only 6 steps. For an N-element list, the maximum number of steps required to reduce the search space to an empty sublist is $log_2 N$ steps.

### Comparison of linear and binary search algorithms

<img width="518" alt="image" src="https://user-images.githubusercontent.com/11669149/229294764-a7184330-be92-4ba1-b15e-07b707570e97.png">

## O notation

**Big O notation** is a mathematical way of describing how a function (running time of an algorithm) generally behaves in relation to the input size. In Big O notation, all functions that have the same growth rate (as determined by the highest order term of the function) are characterized using the same Big O notation. In essence, all functions that have the same growth rate are considered equivalent in Big O notation.

Given a function that describes the running time of an algorithm, the Big O notation for that function can be determined using the following rules:

1. If f(x) is a sum of several terms, the highest order term (the one with the fastest growth rate) is kept and others are discarded.
2. If f(x) has a term that is a product of several factors, all constants (those that are not in terms of x) are omitted.

<img width="549" alt="image" src="https://user-images.githubusercontent.com/11669149/229295038-153c502f-4f08-4fff-94c1-ee63c7662562.png">

> **Which of the following Big O notations is equivalent to $O(12N +6N^3 + 1000)$?**

One consideration in evaluating algorithms is that the efficiency of the algorithm is most critical for large input sizes. Small inputs are likely to result in fast running times because N is small, so efficiency is less of a concern. The table below shows the runtime to perform f(N) instructions for different functions f and different values of N. For large N, the difference in computation time varies greatly with the rate of growth of the function f. The data assumes that a single instruction takes 1 μs to execute.

**Growth rates for different input sizes.**

| Function | N = 10 | N = 50     | N = 100 | N = 1000 | N = 10000  | N = 100000 |
| -------- | ------ | ---------- | ------- | -------- | ---------- | ---------- |
| log N    | 3.3 μs | 5.65 μs    | 6.6 μs  | 9.9 μs   | 13.3 μs    | 16.6 μs    |
| N        | 10 μs  | 50 μs      | 100 μs  | 1000 μs  | 10 ms      | 0.1 s      |
| N log N  | .03 ms | .28 ms     | .66 ms  | .099 s   | .132 s     | 1.66 s     |
| $N^2^$       | .1 ms  | 2.5 ms     | 10 ms   | 1 s      | 100 s      | 2.7 hours  |
| $N^3^$       | 1 ms   | .125 s     | 1 s     | 16.7 min | 11.57 days | 31.7 years |
| $2^N^$       | .001 s | 35.7 years | *       | *        | *          | *          |

Many commonly used algorithms have running time functions that belong to one of a handful of growth functions. These common Big O notations are summarized in the following table. The table shows the Big O notation, the common word used to describe algorithms that belong to that notation, and an example with source code. Clearly, the best algorithm is one that has constant time complexity. Unfortunately, not all problems can be solved using constant complexity algorithms. In fact, in many cases, computer scientists have proven that certain types of problems can only be solved using quadratic or exponential algorithms.

<img width="708" alt="image" src="https://user-images.githubusercontent.com/11669149/229295323-18215b90-54b4-4239-a4bb-db44f2355ee1.png">

Many commonly used algorithms have running time functions that belong to one of a handful of growth functions. These common Big O notations are summarized in the following table. The table shows the Big O notation, the common word used to describe algorithms that belong to that notation, and an example with source code. Clearly, the best algorithm is one that has constant time complexity. Unfortunately, not all problems can be solved using constant complexity algorithms. In fact, in many cases, computer scientists have proven that certain types of problems can only be solved using quadratic or exponential algorithms.

### Runtime complexities for various pseudocode examples.

***Notation: $O(1)$ - Constant***

**Pseudocode**

```
FindMin(x, y) {
   if (x < y) {
      return x
   }
   else {
      return y
   }
}
```

***Notation: $O(log N)$ - Log***

**Pseudocode**

```
BinarySearch(numbers, N, key) {
    mid = 0;
   low = 0;
   high = 0;
   
   high = N - 1;
   
   while (high >= low) {
      mid = (high + low) / 2
      if (numbers[mid] < key) {
         low = mid + 1
      }
      else if (numbers[mid] > key) {
         high = mid - 1
      }
      else {
         return mid
      }
   }
   
   return -1   // not found
}
```

***Notation: $O(N)$ - Linear***

**Pseudocode**

```
LinearSearch(numbers, N, key) {
  for (i = 0; i < N; ++i) {
      if (numbers[i] == key) {
         return i
      }
   }
   
   return -1 // not found
}
```

***Notation: $O(N Log N)$ - Log-linear***

**Pseudocode**

```
MergeSort(numbers, i, k) {
   j = 0
   if (i < k) {
      j = (i + k) / 2              // Find midpoint 
      
      MergeSort(numbers, i, j)     // Sort left part
      MergeSort(numbers, j + 1, k) // Sort right part
      Merge(numbers, i, j, k)      // Merge parts
   }
}
```

***Notation: $O(N^2)$ - Quadratic***

**Pseudocode**

```
SelectionSort(numbers, N) { 
   for (i = 0; i < N; ++i) {
      indexSmallest = i
      for (j = i + 1; j < N; ++j) {
         if (numbers[j] < numbers[indexSmallest]) {
            indexSmallest = j
         }
      }
      
      temp = numbers[i]
      numbers[i] = numbers[indexSmallest]
      numbers[indexSmallest] = temp
   }
}
```

***Notation: $O(c^N)$ - Exponential***

**Pseudocode**

```
Fibonacci(N) {
  if ((1 == N) || (2 == N)) {
    return 1
  }
  return Fibonacci(N-1) + Fibonacci(N-2)
}
```

## Algorithm analysis

### Worst-case scenario

To analyze how runtime of an algorithm scales as the input size increases, we first determine how many operations the algorithm executes for a specific input size, N. Then, the big-O notation for that function is determined. Algorithm runtime analysis often focuses on the worst-case runtime complexity. The **worst-case runtime** of an algorithm is the runtime complexity for an input that results in the longest execution. Other runtime analyses include best-case runtime and average-case runtime. Determining the average-case runtime requires knowledge of the statistical properties of the expected data inputs.

### Constant-time operations

For algorithm analysis, the definition of a single operation does not need to be precise. An operation can be any statement (or constant number of statements) that has a constant runtime complexity, O(1). Since constants are omitted in big-O notation, any constant number of constant time operations is O(1). So, precisely counting the number of constant time operations in a finite sequence is not needed. Ex: An algorithm with a single loop that execute 5 operations before the loop, 3 operations each loop iteration, and 6 operations after the loop would have a runtime of f(N) = 5 + 3N + 6, which can be written as O(1) + O(N) + O(1) = O(N). If the number of operations before the loop was 100, the big-O notation for those operation is still O(1).

### Runtime analysis of nested loops

Runtime analysis for nested loops requires summing the runtime of the inner loop over each outer loop iteration. The resulting summation can be simplified to determine the big-O notation.

<img width="660" alt="image" src="https://user-images.githubusercontent.com/11669149/229296276-8a9ecfef-7f41-4c70-afa8-86ee5edaf662.png">

1. For each iteration of the outer loop, the runtime of the inner loop is determined and added together to form a summation. For iteration i = 0, the inner loop executes N - 1 iterations.
2. For i = 1, the inner loop iterates N - 2 times: iterating from j = 2 to N - 1.
3. For i = N - 2, the inner loop iterates once: iterating from j = N - 1 to N - 1.
4. The summation is the sum of a consecutive sequence of numbers, and can be simplified.
5. Each iteration of the loops requires a constant number of operations, which is defined as the constant c.
6. Additionally, each iteration of the outer loop requires a constant number of operations, which is defined as the constant d.
7. Big-O notation omits the constant values, and the runtime is equal to the summation of the total inner loop iterations.

# Sorting algorithms

**Sorting** is the process of converting a list of elements into ascending (or descending) order. For example, given a list of numbers {17 3 44 6 9}, the list after sorting is {3 6 9 17 44}. You may have carried out sorting when arranging papers in alphabetical order, or arranging envelopes to have ascending zip codes (as required for bulk mailings).

The challenge of sorting is that a program can't "see" the entire list to know where to move an element. Instead, a program is limited to simpler steps, typically observing or swapping just two elements at a time. So sorting just by swapping values is an important part of sorting algorithms.

## Selection sort

**Selection sort** is a sorting algorithm that treats the input as two parts, a sorted part and an unsorted part, and repeatedly selects the proper next value to move from the unsorted part to the end of the sorted part.

[Selection sort animation](https://www.youtube.com/watch?v=xWBP4lzkoyM&ab_channel=GeeksforGeeks)

1. Selection sort treats the input as two parts, a sorted and unsorted part. Variables i and j keep track of the two parts.
2. The selection sort algorithm searches the unsorted part of the array for the smallest element; indexSmallest stores the index of the smallest element found.
3. Elements at i and indexSmallest are swapped.
4. Indices for the sorted and unsorted parts are updated.
5. The unsorted part is searched again, swapping the smallest element with the element at i.
6. The process repeats until all elements are sorted.

The index variable i denotes the dividing point. Elements to the left of i are sorted, and elements including and to the right of i are unsorted. All elements in the unsorted part are searched to find the index of the element with the smallest value. The variable indexSmallest stores the index of the smallest element in the unsorted part. Once the element with the smallest value is found, that element is swapped with the element at location i. Then, the index i is advanced one place to the right, and the process repeats.

The term "selection" comes from the fact that for each iteration of the outer loop, a value is selected for position i.

### Example - Selection sort

```java
public class SelectionSort {
    public static void selectionSort(int [] numbers) {
        int i;
        int j;
        int indexSmallest;
        int temp;      // Temporary variable for swap

        for (i = 0; i < numbers.length - 1; ++i) {

            // Find index of smallest remaining element
            indexSmallest = i;
            for (j = i + 1; j < numbers.length; ++j) {

                if (numbers[j] < numbers[indexSmallest]) {
                    indexSmallest = j;
                }
            }

            // Swap numbers[i] and numbers[indexSmallest]
            temp = numbers[i];
            numbers[i] = numbers[indexSmallest];
            numbers[indexSmallest] = temp;
        }
    }

    public static void main(String [] args) {
        int numbers [] = {10, 2, 78, 4, 45, 32, 7, 11};
        int i;

        System.out.print("UNSORTED: ");
        for (i = 0; i < numbers.length; ++i) {
            System.out.print(numbers[i] + " ");
        }
        System.out.println();

        /* initial call to selection sort with index */
        selectionSort(numbers);

        System.out.print("SORTED: ");
        for (i = 0; i < numbers.length; ++i) {
            System.out.print(numbers[i] + " ");
        }
        System.out.println();
    }
}
```

Selection sort may require a large number of comparisons. The selection sort algorithm runtime is $O(N^2)$.

## Insertion sort

**Insertion sort** is a sorting algorithm that treats the input as two parts, a sorted part and an unsorted part, and repeatedly inserts the next value from the unsorted part into the correct location in the sorted part.

[Insertion sort animation](https://www.youtube.com/watch?v=OGzPmgsI-pQ&ab_channel=GeeksforGeeks)

### Example - Insertion sort

``` java
public class InsertionSort {
    public static void insertionSort(int [] numbers) {
        int i;
        int j;
        int temp;      // Temporary variable for swap

        for (i = 1; i < numbers.length; ++i) {
            j = i;
            // Insert numbers[i] into sorted part
            // stopping once numbers[i] in correct position
            while (j > 0 && numbers[j] < numbers[j - 1]) {

                // Swap numbers[j] and numbers[j - 1]
                temp = numbers[j];
                numbers[j] = numbers[j - 1];
                numbers[j - 1] = temp;
                --j;
            }
        }
    }

    public static void main(String [] args) {
        int [] numbers = {10, 2, 78, 4, 45, 32, 7, 11};
        int i;

        System.out.print("UNSORTED: ");
        for (i = 0; i < numbers.length; ++i) {
            System.out.print(numbers[i] + " ");
        }
        System.out.println();

        insertionSort(numbers);

        System.out.print("SORTED: ");
        for (i = 0; i < numbers.length; ++i) {
            System.out.print(numbers[i] + " ");
        }
        System.out.println();
    }
}
```

The index variable i denotes the starting position of the current element in the unsorted part. Initially, the first element (i.e., element at index 0) is assumed to be sorted, so the outer for loop initializes i to 1. The inner while loop inserts the current element into the sorted part by repeatedly swapping the current element with the elements in the sorted part that are larger. Once a smaller or equal element is found in sorted part, the current element has been inserted in the correct location and the while loop terminates.

Insertion sort's typical runtime is $O(N^2)$.

## Quick sort

**Quicksort** is a sorting algorithm that repeatedly partitions the input into low and high parts (each part unsorted), and then recursively sorts each of those parts. To partition the input, quicksort chooses a pivot to divide the data into low and high parts. The **pivot** can be any value within the array being sorted, commonly the value of the middle array element. Ex: For the list {4 34 10 25 1}, the middle element is located at index 2 (the middle of indices 0..4) and has a value of 10.

To partition the input, the quicksort algorithm divides the array into two parts, referred to as the low partition and the high partition. All values in the low partition are less than or equal to the pivot value. All values in the high partition are greater than or equal to the pivot value. The values in each partition are not necessarily sorted. Ex: Partitioning {4 34 10 25 1} with a pivot value of 10 results in a low partition of {4 10 1} and a high partition of {34 25}. Values equal to the pivot may appear in either or both of the partitions.

[Quick sort animation](https://www.youtube.com/watch?v=PgBzjlCcFvc&ab_channel=GeeksforGeeks)

The partitioning algorithm uses two index variables l and h (low and high), initialized to the left and right sides of the current elements being sorted. As long as the value at index l is less than the pivot value, the algorithm increments l, because the element should remain in the low partition. Likewise, as long as the value at index h is greater than the pivot value, the algorithm decrements h, because the element should remain in the high partition. Then, if l >= h, all elements have been partitioned, and the partitioning algorithm returns h, which is the index of the last element in the low partition. Otherwise, the elements at indices l and h are swapped to move those elements to the correct partitions. The algorithm then increments l, decrements h, and repeats.

### Example - Quick sort

```java
public class QuickSort {
    public static int partition(int [] numbers, int i, int k) {
        int l;
        int h;
        int midpoint;
        int pivot;
        int temp;
        boolean done;

        /* Pick middle element as pivot */
        midpoint = i + (k - i) / 2;
        pivot = numbers[midpoint];

        done = false;
        l = i;
        h = k;

        while (!done) {
            /* Increment l while numbers[l] < pivot */
            while (numbers[l] < pivot) {
                ++l;
            }

            /* Decrement h while pivot < numbers[h] */
            while (pivot < numbers[h]) {
                --h;
            }

         /* If there are zero or one items remaining,
            all numbers are partitioned. Return h */
            if (l >= h) {
                done = true;
            }
            else {
            /* Swap numbers[l] and numbers[h],
               update l and h */
                temp = numbers[l];
                numbers[l] = numbers[h];
                numbers[h] = temp;

                ++l;
                --h;
            }
        }

        return h;
    }

    public static void quicksort(int [] numbers, int i, int k) {
        int j;

      /* Base case: If there are 1 or zero entries to sort,
       partition is already sorted */
        if (i >= k) {
            return;
        }

      /* Partition the data within the array. Value j returned
         from partitioning is location of last item in low partition. */
        j = partition(numbers, i, k);

      /* Recursively sort low partition (i to j) and
         high partition (j + 1 to k) */
        quicksort(numbers, i, j);
        quicksort(numbers, j + 1, k);
    }

    public static void main(String [] args) {
        int [] numbers = {10, 2, 78, 4, 45, 32, 7, 11};
        int i;

        System.out.print("UNSORTED: ");
        for (i = 0; i < numbers.length; ++i) {
            System.out.print(numbers[i] + " ");
        }
        System.out.println();

        /* Initial call to quicksort */
        quicksort(numbers, 0, numbers.length - 1);

        System.out.print("SORTED: ");
        for (i = 0; i < numbers.length; ++i) {
            System.out.print(numbers[i] + " ");
        }
        System.out.println();
    }
}
```

The quicksort algorithm's runtime is typically $O(N log N)$. The worst case runtime for the quicksort algorithm is $O(N^2)$.

## Merge sort

**Merge sort** is a sorting algorithm that divides a list into two halves, recursively sorts each half, and then merges the sorted halves to produce a sorted list. The recursive partitioning continues until a list of 1 element is reached, as a list of 1 element is already sorted.

[Merge sort animation](https://www.youtube.com/watch?v=JSceec-wEyw&ab_channel=GeeksforGeeks)

### Example - Merge sort

```java
public class MergeSort {
    public static void merge(int [] numbers, int i, int j, int k) {
        int mergedSize = k - i + 1;       // Size of merged partition
        int mergedNumbers [] = new int[mergedSize]; // Temporary array for merged numbers
        int mergePos;                     // Position to insert merged number
        int leftPos;                      // Position of elements in left partition
        int rightPos;                     // Position of elements in right partition

        mergePos = 0;
        leftPos = i;                      // Initialize left partition position
        rightPos = j + 1;                 // Initialize right partition position

        // Add smallest element from left or right partition to merged numbers
        while (leftPos <= j && rightPos <= k) {
            if (numbers[leftPos] < numbers[rightPos]) {
                mergedNumbers[mergePos] = numbers[leftPos];
                ++leftPos;
            }
            else {
                mergedNumbers[mergePos] = numbers[rightPos];
                ++rightPos;
            }
            ++mergePos;
        }

        // If left partition is not empty, add remaining elements to merged numbers
        while (leftPos <= j) {
            mergedNumbers[mergePos] = numbers[leftPos];
            ++leftPos;
            ++mergePos;
        }

        // If right partition is not empty, add remaining elements to merged numbers
        while (rightPos <= k) {
            mergedNumbers[mergePos] = numbers[rightPos];
            ++rightPos;
            ++mergePos;
        }

        // Copy merge number back to numbers
        for (mergePos = 0; mergePos < mergedSize; ++mergePos) {
            numbers[i + mergePos] = mergedNumbers[mergePos];
        }
    }

    public static void mergeSort(int [] numbers, int i, int k) {
        int j;

        if (i < k) {
            j = (i + k) / 2;  // Find the midpoint in the partition

            // Recursively sort left and right partitions
            mergeSort(numbers, i, j);
            mergeSort(numbers, j + 1, k);

            // Merge left and right partition in sorted order
            merge(numbers, i, j, k);
        }
    }

    public static void main(String [] args) {
        int [] numbers = {10, 2, 78, 4, 45, 32, 7, 11};
        int i;

        System.out.print("UNSORTED: ");
        for (i = 0; i < numbers.length; ++i) {
            System.out.print(numbers[i] + " ");
        }
        System.out.println();

        /* initial call to merge sort with index */
        mergeSort(numbers, 0, numbers.length - 1);

        System.out.print("SORTED: ");
        for (i = 0; i < numbers.length; ++i) {
            System.out.print(numbers[i] + " ");
        }
        System.out.println();
    }
}
```

The merge sort algorithm's runtime is $O(N log N)$. Merge sort requires $O(N)$ additional memory elements for the temporary array of merged elements.

## Conclusion

There are many more searching and sorting algorithms; some are simple, and some are complex, requiring parallel processing. I have covered basic searching and sorting algorithms. Big O notation helps compare algorithms and is a very useful method for programmers and data analysis.





