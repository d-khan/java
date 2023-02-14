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


## Heap and Stacks

A program's memory usage typically includes four different regions:

__Code__ — The region where the program instructions are stored.
__Static memory__ — The region where static fields are allocated. The name "static" comes from these variables not changing (static means not changing); they are allocated once and last for the duration of a program's execution, their addresses staying the same.  
__The stack__ — The region where a method's local variables are allocated during a method call. A method call adds local variables to the stack, and a return removes them, like adding and removing dishes from a pile; hence the term "stack." Because this memory is automatically allocated and deallocated, it is also called automatic memory.
The heap — The region where the "new" operator allocates memory for objects. The region is also called free store.
In Java, the code and static memory regions are actually integrated into a region of memory called the method area , which also stores information for every class type used in the program.

<img width="703" alt="Screen Shot 2023-02-13 at 6 16 21 PM" src="https://user-images.githubusercontent.com/11669149/218621626-334502d8-6966-4a80-8b37-913536d210d4.png">

## Basic garbage collection
Because the amount of memory available to a program is finite, objects allocated to the heap must eventually be deallocated when no longer needed by the program. The Java programming language uses a mechanism called garbage collection wherein a program's executable includes automatic behavior that at various intervals finds all unreachable — i.e., unused — allocated memory locations, and automatically frees such memory locations in order to enable memory reuse. Garbage collection can present the programmer with the illusion of a nearly unlimited memory supply at the expense of runtime overhead.

In order to determine which allocated objects the program is currently using at runtime, the Java virtual machine keeps a count, known as a reference count, of all reference variables that are currently referring to an object. If the reference count is zero, then the object is considered an unreachable object and is eligible for garbage collection, as no variables in the program refer to the object. The Java virtual machine marks unreachable objects, and deallocation occurs the next time the Java virtual machine invokes the garbage collector. The following animation illustrates.

<img width="485" alt="image" src="https://user-images.githubusercontent.com/11669149/218622524-d49a73c9-7e21-4882-9461-bec5437ac29c.png">
<img width="572" alt="image" src="https://user-images.githubusercontent.com/11669149/218622659-ecd462b2-4835-41c8-a339-77820ebdd422.png">
<img width="579" alt="image" src="https://user-images.githubusercontent.com/11669149/218622716-49df2db2-1baf-4080-b6f4-96d92017b905.png">
<img width="575" alt="image" src="https://user-images.githubusercontent.com/11669149/218622783-d8a8f0e7-b377-4653-8ec4-f548759f6915.png">
<img width="576" alt="image" src="https://user-images.githubusercontent.com/11669149/218622838-30e4dc20-2752-4b9b-9f42-cd9a16ee2d14.png">
<img width="576" alt="image" src="https://user-images.githubusercontent.com/11669149/218622875-c6a1a6dc-a643-4909-91ab-dabc185f4184.png">

A programmer does not explicitly have to set a reference variable to null in order to indicate that the variable no longer refers to an object. The Java virtual machine can automatically infer a null reference once the variable goes out of scope — i.e., the reference variable is no longer visible to the program. For example, local reference variables that are declared within a method go out of scope as soon as the method returns. The Java virtual machine decrements the reference counts associated with the objects referred to by any local variables within the method.

<img width="661" alt="image" src="https://user-images.githubusercontent.com/11669149/218629353-92d38d40-605b-431e-82c3-bf1eb6d01132.png">
<img width="662" alt="image" src="https://user-images.githubusercontent.com/11669149/218633526-53d80896-a290-4209-bc1f-2978bea220c7.png">
<img width="659" alt="image" src="https://user-images.githubusercontent.com/11669149/218633966-ffaf1f74-55fa-4b08-a47b-362bc959f187.png">

Every time CountBits() is invoked, the method declares a local reference variable called binaryStr, which refers to a newly allocated String object used to store the binary representation of the integer num. The assignment of binaryStr increments the object's reference count. When the method returns, the reference variable binaryStr goes out of scope, and the Java virtual machine will decrement the reference count for the String object. The reference count for that String object becomes zero and the object is marked for deallocation, which occurs whenever the Java virtual machine invokes the garbage collector.

Although CountBits() happens to allocate binaryStr in the same memory location whenever CountBits() is called, note that Java makes no such guarantee. Also, recall that main() is itself a method. Thus, the Java virtual machine will decrement the reference count of any objects associated with reference variables declared in main() upon returning from main().

    
    
