```java
public class Permutations {

    public static void main(String[] args) {
        int[] arr = {0, 1, 2, 3};   // You can change this
        permute(arr, 0);
    }

    public static void permute(int[] arr, int index) {
        // Base case
        if (index == arr.length) {
            printArray(arr);
            return;
        }

        // Recursive case
        for (int i = index; i < arr.length; i++) {
            swap(arr, index, i);              // Fix current position
            permute(arr, index + 1);          // Recurse
            swap(arr, index, i);              // Backtrack
        }
    }

    // Utility method to swap elements
    public static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // Utility method to print array
    public static void printArray(int[] arr) {
        for (int num : arr) {
            System.out.print(num);
        }
        System.out.println(); // new line after each permutation
    }
}
```
