# Introduction to memory management
An ArrayList stores a list of items in contiguous memory locations, which enables immediate access to any element at index i of ArrayList v by using the get() and set() methods — the program just adds i to the starting address of the first element in v to arrive at the element. The methods add(objRef) and add(i, objRef) append and insert items into an ArrayList, respectively. Now recall that inserting an item at locations other than the end of the ArrayList requires making room by shifting higher-indexed items. Similarly, removing (via the remove(i) method) an item requires shifting higher-indexed items to fill the gap. Each shift of an item from one element to another element requires a few processor instructions. This issue exposes the ArrayList add/remove performance problem.

For ArrayLists with thousands of elements, a single call to add() or remove() can require thousands of instructions, so if a program does many insert or remove operations on large ArrayLists, the program may run very slowly. The following animation illustrates shifting during an insertion operation.



