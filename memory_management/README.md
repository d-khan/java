# Introduction to memory management
An ArrayList stores a list of items in contiguous memory locations, which enables immediate access to any element at index i of ArrayList v by using the get() and set() methods — the program just adds i to the starting address of the first element in v to arrive at the element. The methods add(objRef) and add(i, objRef) append and insert items into an ArrayList, respectively. Now recall that inserting an item at locations other than the end of the ArrayList requires making room by shifting higher-indexed items. Similarly, removing (via the remove(i) method) an item requires shifting higher-indexed items to fill the gap. Each shift of an item from one element to another element requires a few processor instructions. This issue exposes the ArrayList add/remove performance problem.

For ArrayLists with thousands of elements, a single call to add() or remove() can require thousands of instructions, so if a program does many insert or remove operations on large ArrayLists, the program may run very slowly. The following animation illustrates shifting during an insertion operation.

The shifting of elements done by add() and remove() requires several processor instructions per element. Doing many insertions/removes on large ArrayLists can take a significantly long time.

The following program can be used to demonstrate the issue. The user inputs an ArrayList size, and a number of elements to insert. The program then carries out several tasks. The program creates an ArrayList of size numElem, writes an arbitrary value to all elements, performs numOps appends, numOps inserts, and numOps removes.

<details><summary>Click to get the code</summary>
<p>

'''java
import java.util.ArrayList;
import java.util.Scanner;

public class ArrayListAddRemove {
    public static void main(String[] args) {
        Scanner scnr = new Scanner(System.in);
        ArrayList<Integer> myInts = new ArrayList<Integer>(); // Dummy array list to demo ops
        int numElem;                                          // User defined array size
        int numOps;                                           // User defined number of inserts
        int i;                                                // Loop index

        System.out.print("\nEnter initial ArrayList size: ");
        numElem = scnr.nextInt();

        System.out.print("Enter number of ArrayList adds: ");
        numOps = scnr.nextInt();

        System.out.print("  Adding elements to ArrayList...");

        myInts.clear();
        for (i = 0; i < numElem; ++i) {
            myInts.add(new Integer(0));
        }

        System.out.println("done.");
        System.out.print("  Writing to each element...");

        for (i = 0; i < numElem; ++i) {
            myInts.set(i, new Integer(777)); // Any value
        }

        System.out.println("done.");
        System.out.print("  Doing " + numOps + " additions at the end...");

        for (i = 0; i < numOps; ++i) {
            myInts.add(new Integer(888)); // Any value
        }

        System.out.println("done.");
        System.out.print("  Doing " + numOps + " additions at index 0...");

        for (i = 0; i < numOps; ++i) {
            myInts.add(0, new Integer(444));
        }
        System.out.println("done.");
        System.out.print("  Doing " + numOps + " removes...");

        for (i = 0; i < numOps; ++i) {
            myInts.remove(0);
        }

        System.out.println("done.");
    }
}
```
</p>
</details>
