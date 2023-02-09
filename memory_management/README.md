# Introduction to memory management
An ArrayList stores a list of items in contiguous memory locations, which enables immediate access to any element at index i of ArrayList v by using the get() and set() methods — the program just adds i to the starting address of the first element in v to arrive at the element. The methods add(objRef) and add(i, objRef) append and insert items into an ArrayList, respectively. Now recall that inserting an item at locations other than the end of the ArrayList requires making room by shifting higher-indexed items. Similarly, removing (via the remove(i) method) an item requires shifting higher-indexed items to fill the gap. Each shift of an item from one element to another element requires a few processor instructions. This issue exposes the ArrayList add/remove performance problem.

For ArrayLists with thousands of elements, a single call to add() or remove() can require thousands of instructions, so if a program does many insert or remove operations on large ArrayLists, the program may run very slowly. 

The shifting of elements done by add() and remove() requires several processor instructions per element. Doing many insertions/removes on large ArrayLists can take a significantly long time.

The following program can be used to demonstrate the issue. The user inputs an ArrayList size, and a number of elements to insert. The program then carries out several tasks. The program creates an ArrayList of size numElem, writes an arbitrary value to all elements, performs numOps appends, numOps inserts, and numOps removes.


<details><summary>Click to get the code</summary>
<p>
    
```java

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

The appends are fast because they do not involve any shifting of elements, whereas each insert requires 500,000 elements to be shifted — one at a time. 7,500 inserts thus requires 3,750,000,000 (over 3 billion) shifts.

## Linked-lists
 
One way to make inserts or removes faster is to use a different approach for storing a list of items. The approach does not use contiguous memory locations. Instead, each item contains a "pointer" to the next item's location in memory, as well as, the data being stored. Thus, inserting a new item B between existing items A and C just requires changing A to refer to B's memory location, and B to refer to C's location.

> There is a very interactive website that shows graphically [how linked-list works](https://visualgo.net/en/list).

A linked list is a list wherein each item contains not just data but also a reference — a link — to the next item in the list. Comparing ArrayLists and linked lists:

__ArrayList:__ Stores items in contiguous memory locations. Supports quick access to i'th element via the set() and get() methods, but may be slow for inserts or removes on large ArrayLists due to necessary shifting of elements.  

__Linked list:__ Stores each item anywhere in memory, with each item referring to the next item in the list. Supports fast inserts or removes, but access to i'th element may be slow as the list must be traversed from the first item to the i'th item. Also uses more memory due to storing a link for each item.
    
A common use of objects and references is to create a list of items such that an item can be efficiently inserted somewhere in the middle of the list, without the shifting of later items as required for an ArrayList. The following program illustrates how such a list can be created. A class is defined to represent each list item, known as a list node. A node is comprised of the data to be stored in each list item, in this case just one int, and a reference to the next node in the list. A special node named head is created to represent the front of the list, after which regular items can be inserted.
    
<details><summary>Click to get the code IntNode.java</summary>
<p>

```java
public class IntNode {
   private int dataVal;         // Node data
   private IntNode nextNodeRef; // Reference to the next node

   public IntNode() {
      dataVal = 0;
      nextNodeRef = null;
   }

   // Constructor
   public IntNode(int dataInit) {
      this.dataVal = dataInit;
      this.nextNodeRef = null;
   }

   /* Insert node after this node.
    Before: this -- next
    After:  this -- node -- next
    */
   public void insertAfter(IntNode nodeLoc) {
      IntNode tmpNext;

      tmpNext = this.nextNodeRef;
      this.nextNodeRef = nodeLoc;
      nodeLoc.nextNodeRef = tmpNext;
   }

   // Get location of nextNodeRef
   public IntNode getNext() {
      return this.nextNodeRef;
   }

   public void printNodeData() {
      System.out.println(this.dataVal);
   }
}
```
    
</p>
</details>

<details><summary>Click to get the code CustomLinkedList.java</summary>
<p>

```java
    
public class CustomLinkedList {
   public static void main(String[] args) {
      IntNode headObj; // Create IntNode reference variables
      IntNode currObj;
      IntNode lastObj;
      int i;           // Loop index
      
      headObj = new IntNode(-1); // Front of nodes list
      lastObj = headObj;
      
      for (i = 0; i < 20; ++i) { // Append 20 rand nums
         int rand = (int)(Math.random() * 100000); // random int (0-99999)
         currObj = new IntNode(rand);
         
         lastObj.insertAfter(currObj); // Append curr
         lastObj = currObj;
      }
      
      currObj = headObj; // Print the list
      while (currObj != null) {
         currObj.printNodeData();
         currObj = currObj.getNext();
      }
   }
}
                         
```
</p>
</details>
