# Collections in Java

The **Collection in Java** is a framework that provides an architecture to store and manipulate a group of objects.

> **Java Collections can achieve all the operations you perform on data, such as searching, sorting, insertion, manipulation, and deletion.**

Java Collection means a single unit of objects. Java Collection framework provides many interfaces (Set, List, Queue, Deque) and classes ArrayList, Vector, LinkedList, PriorityQueue, HashSet, LinkedHashSet, and TreeSet).

### Example

### Conventional way of printing elements of an array

```Java
import java.util.ArrayList;
public class conventional {
    public static void main(String[] args) {
        ArrayList<String> teamRoster = new ArrayList<String>();
        String playerName;

// Adding player names
        teamRoster.add("Mike");
        teamRoster.add("Scottie");
        teamRoster.add("Toni");

        System.out.println("Current roster: ");

        for (int i = 0; i < teamRoster.size(); ++i) {
            playerName = teamRoster.get(i);
            System.out.println(playerName);
        }
    }
}
```

### Enhanced way of printing elements of an array

```java
import java.util.ArrayList;
public class enhanced {
    public static void main(String[] args) {
        ArrayList<String> teamRoster = new ArrayList<String>();

// Adding player names
        teamRoster.add("Mike");
        teamRoster.add("Scottie");
        teamRoster.add("Toni");

        System.out.println("Current roster:");

        for (String playerName : teamRoster) {
            System.out.println(playerName);
        }
    }
}
```
## List: LinkedList

A LinkedList is one of several types that implement the List interface. The LinkedList type is an ADT implemented as a generic class that supports different types of elements. A LinkedList can be declared and created as `LinkedList<T> linkedList = new LinkedList<T>();` where T represents the LinkedList's type, such as Integer or String. The statement `import java.util.LinkedList;` enables use of a LinkedList within a program.

- A LinkedList supports insertion of elements either at the end of the list or at a specified index.
- If an index is not provided, as in `authorList.add("Martin");`, the add() method adds the element at the end of the list. 
- If an index is specified, as in `authorList.add(0, "Butler");`, the element is inserted at the specified index, with the list element previously located at the specified index appearing after the inserted element.

### Example - Linked list

```java
import java.util.LinkedList;
public class linkedlist {
    public static void main(String[] args) {
        LinkedList<String> authorsList = new LinkedList<String>();
        authorsList.add("Gamow");
        authorsList.add("Penrose");
        authorsList.add("Hawking");

        authorsList.add(1, "Greene");
        System.out.println(authorsList);
    }
}
```

authorsList = Gamow --> Greene --> Penrose --> Hawking

- The add() method adds an element, such as a String, to the end of the list.

- Using the add() method with an index inserts an element at the specified index.

### Common LinkedList methods

| Method name  | Description                                                  | Example                                                      |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **get()**    | `get(index)`  Returns element at specified index.            | `// Assume List is: 5, 10, 11 exList.get(2);  // Returns 11 ` |
| **set()**    | `set(index, newElement)`  Replaces element at specified index with newElement. Returns element previously at specified index. | `// Assume List is: 5, 8, 11 exList.set(0, new Integer(3)); // Returns 5 // List is now: 3, 8, 11 ` |
| **add()**    | `add(newElement)`  Adds newElement to the end of the List. List's size is increased by one.  `add(index, newElement)`  Adds newElement to the List at the specified index. Indices of the elements previously at that specified index and higher are increased by one. List's size is increased by one. | `// Assume List is empty exList.add(new Integer(7));      // List is: 7  exList.add(14);                  // List is: 7, 14 exList.add(0, new Integer(21));  // List is: 21, 7, 14 exList.add(2, 9);                // List is: 21, 7, 9, 14 ` |
| **size()**   | `size()`  Returns the number of elements in the List.        | `// Assume List is empty exList.size(); // Returns 0 exList.add(8); exList.add(22); // List is now: 8, 22 exList.size(); // Returns 2 ` |
| **remove()** | `remove(index)`  Removes element at specified index. Indices for elements from higher positions are decreased by one. List size is decreased by one. Returns reference to element removed from List.  `remove(existingElement)`  Removes the first occurrence of an element which is equal to existingElement. Indices for elements from higher positions are decreased by one. List size is decreased by one. Returns true if specified element was found and removed. | `// Assume List is: 22, 8, 4, 4 exList.remove(1); // Returns 8 // List is now: 22, 4, 4                  exList.remove(5); // Throws exception // List is still: 22, 4, 4   exList.remove(2); // Returns 4 // List is now: 22, 4` |

### Iterating through a list

LinkedList methods with index parameters, such as get() or set(), cause the list to be traversed from the first element to the specified element each time the method is called. Thus, using the LinkedLists' `get()` or `set()` methods within a loop that iterates through all list elements is inefficient.

#### Example - inefficient iteration

```java
import java.util.LinkedList;
public class linkedlist {
    public static void main(String[] args) {
        LinkedList<String> authorsList = new LinkedList<String>();
        String authorName;
        authorsList.add("Gamow");
        authorsList.add("Penrose");
        authorsList.add("Hawking");
        authorsList.add(1, "Greene");

        for (int i = 0; i < authorsList.size(); i++) {
            authorName = authorsList.get(i);
            System.out.println(authorName);
        }
    }
}
```

#### Example - efficient iteration

``` java
import java.util.LinkedList;
import java.util.ListIterator;
public class linkedlist {
    public static void main(String[] args) {
        LinkedList<String> authorsList = new LinkedList<String>();
        String authorName;
        ListIterator<String> listIterator;

        authorsList.add("Gamow");
        authorsList.add("Penrose");
        authorsList.add("Hawking");
        authorsList.add(1, "Greene");

        listIterator = authorsList.listIterator();

        while (listIterator.hasNext()) {
            authorName = listIterator.next();
            System.out.println(authorName);
        }
    }
}
```

> **Same output but a different code**

## Map: HashMap

**What is a Map?**

A programmer may wish to look up values or elements based on another value, such as looking up an employee's record based on an employee ID. The **Map** interface within the Java Collections Framework defines a Collection that associates (or maps) keys to values. The statement `import java.util.HashMap;`enables the use of a HashMap.

### Example

``` java
import java.util.HashMap;

public class hashmap {
    public static void main (String[] args) {
        HashMap<String, Integer> statePopulation = new HashMap();

        // 2013 population data from census.gov
        statePopulation.put("CA", 38332521);
        statePopulation.put("AZ", 6626624);
        statePopulation.put("MA", 6692824);

        System.out.print("Population of Arizona in 2013 is ");
        System.out.print(statePopulation.get("AZ"));
        System.out.println(".");

        // 2014 estimated population
        statePopulation.put("AZ", 6871809);

        System.out.print("Population of Arizona in 2014 is ");
        System.out.print(statePopulation.get("AZ"));
        System.out.println(".");
    }
}
```

### Common HashMap methods

| Method name         | Description                                                  | Example                                                      |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **put()**           | `put(key, value)` Associates key with specified value. If the key already exists, replace the previous value with the specified value. | `// Map originally empty exMap.put("Tom", 14);  // Map now: Tom->14,   exMap.put("John", 86);  // Map now: Tom->14, John->86 ` |
| **putIfAbsent()**   | `putIfAbsent(key, value) ` Associates key with specified value if the key does not already exist or is mapped to null. | `// Assume Map is: Tom->14, John->86 exMap.putIfAbsent("Tom", 20);  // Key "Tom" already exists. Map is unchanged. exMap.putIfAbsent("Mary", 13);  // Map is now: Tom->14, John->86, Mary->13 ` |
| **get()**           | `get(key)` Returns the value associated with key. If key does not exist, return null. | `// Assume Map is: Tom->14, John->86, Mary->13 exMap.get("Tom")  // returns 14  exMap.get("Bob")  // returns null ` |
| **containsKey()**   | `containsKey(key) ` Returns true if key exists, otherwise returns false. | `// Assume Map is: Tom->14, John->86, Mary->13 exMap.containsKey("Tom")  // returns true  exMap.containsKey("Bob")  // returns false ` |
| **containsValue()** | `containsValue(value) ` Returns true if at least one key is associated with the specified value, otherwise returns false. | `// Assume Map is: Tom->14, John->86, Mary->13 exMap.containsValue(86)  // returns true (key "John" associated with value 86) exMap.containsValue(17)  // returns false (no key associated with value 17) ` |
| **remove()**        | `remove(key) ` Removes the map entry for the specified key if the key exists. | `// Assume Map is: Tom->14, John->86, Mary->13 exMap.remove("John");   // Map is now: Tom->14, Mary->13 ` |
| **clear()**         | `clear() ` Removes all map entries.                          | `// Assume Map is: Tom->14, John->86, Mary->13 exMap.clear();   // Map is now empty ` |
| **keySet()**        | `keySet() ` Returns a Set containing all keys within the map. | `// Assume Map is: Tom->14, John->86, Mary->13 keys = exMap.keySet(); // keys contains: "Tom", "John", "Mary" ` |
| **values()**        | `values() ` Returns a Collection containing all values within the map. | `// Assume Map is: Tom->14, John->86, Mary->13 values = exMap.values(); // values contains: 14, 86, 13` |

## Set: HashSet

- The uniqueness of elements in a list. Duplication of elements is not permitted.
- The **Set** interface defined within the Java Collections Framework defines a Collection of unique elements. 
- The Set interface supports methods for adding and removing elements and querying if a set contains an element. For example, a programmer may use a set to store employee names and use that set to determine which customers are eligible for employee discounts.
- The HashSet type is an ADT implemented as a generic class that supports different types of elements. A HashSet can be declared and created as `HashSet<T> hashSet = new HashSet<T>();` where T represents the HashSet's type, such as Integer or String. The statement `import java.util.HashSet;` enables use of a HashSet within a program.

### Example
```java
import java.util.HashSet;
public class Hashset {
    public static void main(String[] args) {
        HashSet<String> ownedBooks = new HashSet<String>();

        ownedBooks.add("A Tale of Two Cities");
        ownedBooks.add("The Lord of the Rings");

        System.out.println("Contains \"A Tale of Two Cities\": " +
                ownedBooks.contains("A Tale of Two Cities"));

        ownedBooks.remove("The Lord of the Rings");

        System.out.println("Contains \"The Lord of the Rings\": " +
                ownedBooks.contains("The Lord of the Rings"));
    }
}
```

### Common HashSet methods

| Method name    | Description                                                  | Example                                                      |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **add()**      | `add(element) ` If element does not exist, adds element to the set and returns true. If element already exists, returns false. | `// Set originally empty exSet.add("Kasparov"); // returns true (element "Kasparov" does not exist) // Set is now: Kasparov   exSet.add("Kasparov"); // returns false (element "Kasparov" already exists) // Set is unchanged ` |
| **remove()**   | `remove(element) ` If element exists, removes element from the set and returns true. If the element does not exist, returns false. | `// Assume Set is: Kasparov, Fisher exSet.remove("Fisher");  // returns true (element "Fisher" exists) // Set is now: Kasparov exSet.remove("Carlsen"); // returns false (element "Carlsen" does not exist) // Set is unchanged ` |
| **contains()** | `contains(element)` Returns true if element exists, otherwise returns false. | `// Assume Set is: Kasparov, Fisher, Carlsen exSet.contains("Carlsen")  // returns true  exSet.contains("Anand")  // returns false ` |
| **size()**     | `size() ` Returns the number of elements in the set.         | `// Set originally empty exSet.size(); // returns 0 exSet.add("Nakamura");  exSet.add("Carlsen"); // Set is now: Nakamura, Carlsen exSet.size(); // returns 2 ` |

## Queue interface

- The **Queue** interface defined within the Java Collections Framework defines a Collection of ordered elements that supports element insertion at the tail and element retrieval from the head.
- A LinkedList is one of several types that implements the Queue interface. A LinkedList implementation of a Queue can be declared and created as `Queue<T> queue = new LinkedList<T>();` where T represents the element's type, such as Integer or String. Java supports the automatic conversion of an object, e.g., LinkedList, to a reference variable of an interface type, e.g., Queue, as long as the object implements the interface.
- The statements `import java.util.LinkedList;` and `import java.util.Queue;` enable the use of a LinkedList and Queue within a program.
- Remember: adding an element to the tail of the queue, and removing the element at the head of the queue.

### Example
``` java
import java.util.LinkedList;
import java.util.Queue;
public class queue {
    public static void main(String[] args) {
        Queue<String> waitList = new LinkedList<String>();

        waitList.add("Neumann party of 1");
        waitList.add("Amdahl party of 2");
        waitList.add("Flynn party of 4");

        System.out.println("Serving: " + waitList.remove());
        System.out.println("Serving: " + waitList.remove());
        System.out.println("Serving: " + waitList.remove());

    }
}
```

### Common Queue methods

| Method name   | Description                                                  | Example                                                      |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **add()**     | `add(newElement)`  Adds newElement element to the tail of the queue. The queue's size increases by one. | `// Assume exQueue is: "down" "right" "A" exQueue.add("B"); // exQueue is now:    "down" "right" "A" "B" ` |
| **remove()**  | `remove()`  Removes and returns the element at the head of the queue. Throws an exception if the queue is empty. | `// Assume exQueue is: "down" "right" "A" exQueue.remove(); // Returns "down" // exQueue is now:    "right" "A" ` |
| **poll()**    | `poll()`  Removes and returns the element at the head of the queue if the queue is not empty. Otherwise, returns null. | `// Assume exQueue is: "down" exQueue.poll(); // Returns "down" // exQueue is now empty exQueue.poll(); // Returns null ` |
| **element()** | `element()`  Returns, but does not remove, the element at the head of the queue. Throws an exception if the queue is empty. | `// Assume exQueue is: "down" "right" "A" exQueue.element(); // Returns "down" // exQueue is still:  "down" "right" "A" ` |
| **peek()**    | `peek()`  Returns, but does not remove, the element at the head of the queue if the queue is not empty. Otherwise, returns null. | `// Assume exQueue is: "down" exQueue.peek(); // Returns "down" // exQueue is still:  "down" ` |

## Deque interface

- The **Deque** (pronounced "deck") interface defined within the Java Collections Framework defines a Collection of ordered elements that supports element insertion and removal at both ends (i.e., at the head and tail of the deque).
- A LinkedList is one of several types that implements the Deque interface. A LinkedList implementation of a Deque can be declared and created as `Deque<T> deque = new LinkedList<T>();` where T represents the element's type, such as Integer or String. 
- The statements `import java.util.LinkedList;` and `import java.util.Deque;` enable use of a LinkedList and Deque within a program.
- Deque's addFirst() and removeFirst() methods allow a Deque to be used as a stack. A **stack** is an ADT in which elements are only added or removed from the top of a stack. Deque's addFirst() method adds an element at the head of the deque and increases the deque's size by one. The addFirst() method shifts elements in the deque to make room for the new element. The removeFirst() method removes and returns the element at the head of the deque. If the deque is empty, removeFirst() throws an exception.

### Example

```java
import java.util.LinkedList;
import java.util.Deque;
public class deque {
    public static void main(String[] args) {
        Deque<String> tripRoute = new LinkedList<String>();

        System.out.println("Depart Tokyo");
        tripRoute.addFirst("Tokyo");

        System.out.println("Transfer at Osaka");
        tripRoute.addFirst("Osaka");

        System.out.println("Arrive in Nara");
        tripRoute.addFirst("Nara");

        System.out.println("\nReturn trip: ");
        System.out.println("Depart " + tripRoute.removeFirst());
        System.out.println("Transfer at " + tripRoute.removeFirst());
        System.out.println("Arrive in " + tripRoute.removeFirst());
    }
}
```

### Common Deque methods

| Method name       | Description                                                  | Example                                                      |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **addFirst()**    | `addFirst(newElement)`  Adds newElement element at the head of the deque. The deque's size increases by one. | `// Assume exDeque is: 3 5 6 exDeque.addFirst(1); // exDeque is now:    1 3 5 6 ` |
| **addLast()**     | `addLast(newElement)`  Adds newElement element at the tail of the deque. The deque's size increases by one. | `// Assume exDeque is: 3 5 6 exDeque.addLast(7); // exDeque is now:    3 5 6 7 ` |
| **removeFirst()** | `removeFirst()`  Removes and returns the element at the head of the deque. Throws an exception if the deque is empty. | `// Assume exDeque is: 3 5 6 exDeque.removeFirst(); // Returns 3 // exDeque is now:    5 6 ` |
| **removeLast()**  | `removeLast()`  Removes and returns the element at the tail of the deque. Throws an exception if the deque is empty. | `// Assume exDeque is: 3 5 6 exDeque.removeLast(); // Returns 6 // exDeque is now:    3 5 ` |
| **pollFirst()**   | `pollFirst()`  Removes and returns the element at the head of the deque if the deque is not empty. Otherwise, returns null. | `// Assume exDeque is: 3 5 6 exDeque.pollFirst(); // Returns 3 // exDeque is now:    5 6 exDeque.pollFirst(); // Returns 5 exDeque.pollFirst(); // Returns 6 // exDeque is now empty exDeque.pollFirst(); // Returns null ` |
| **pollLast()**    | `pollLast()`  Removes and returns the element at the tail of the deque if the deque is not empty. Otherwise, returns null. | `// Assume exDeque is: 3 5 6 exDeque.pollLast(); // Returns 6 // exDeque is now:    3 5 exDeque.pollLast(); // Returns 5 exDeque.pollLast(); // Returns 3 // exDeque is now empty exDeque.pollLast(); // Returns null ` |
| **getFirst()**    | `getFirst()`  Returns, but does not remove, the element at the head of the deque. Throws an exception if the deque is empty. | `// Assume exDeque is: 3 5 6 exDeque.getFirst(); // Returns 3 // exDeque is still:  3 5 6 ` |
| **getLast()**     | `getLast()`  Returns, but does not remove, the element at the tail of the deque. Throws an exception if the deque is empty. | `// Assume exDeque is: 3 5 6 exDeque.getLast(); // Returns 6 // exDeque is still:  3 5 6 ` |
| **peekFirst()**   | `peekFirst()`  Returns, but does not remove, the element at the head of the deque if the deque is not empty. Otherwise, returns null. | `// Assume exDeque is: 3 5 6 exDeque.peekFirst(); // Returns 3 // exDeque is still:  3 5 6 ` |
| **peekLast()**    | `peekLast()`  Returns, but does not remove, the element at the tail of the deque if the deque is not empty. Otherwise, returns null. | `// Assume exDeque is: 3 5 6 exDeque.peekLast(); // Returns 6 // exDeque is still:  3 5 6` |

### Practice exercise (not graded)

Use the above methods to create a deque. Add at least 5 elements (at head and tail) and practice several methods.

## Summary

- Collections in Java is a very useful tool, specially when a programmer is dealing with list-type data structures and manipulating elements in a list.
