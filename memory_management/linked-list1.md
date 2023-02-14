# Practice linked lists (not graded)

## Objective
Practice linked lists. This exercise is not graded.

## Pre-requisite
Review "Memory management"

## Task
Two strings, name1 and name2, are read from input as two friends' names. headObj has the default value of "name". 
Create a new node firstFriend with string name1, and insert firstFriend after headObj. 
Then, create a second node secondFriend with string name2, and insert secondFriend after firstFriend.

### Solution
<details> <summary> FriendLinkedList.java </summary>
<p>

``` java
import java.util.Scanner;

public class FriendLinkedList {
    public static void main(String[] args) {
        Scanner scnr = new Scanner(System.in);
        FriendNode headObj;
        FriendNode firstFriend;
        FriendNode secondFriend;
        FriendNode currFriend;
        String name1;
        String name2;

        name1 = scnr.next();
        name2 = scnr.next();

        headObj = new FriendNode("name");

        /* Your code goes here */

        currFriend = headObj;
        while (currFriend != null) {
            currFriend.printNodeData();
            currFriend = currFriend.getNext();
        }
    }
}```

</p>
</details>

<details> <summary> Click to get the FriendNode.java </summary>
<p>

``` java
public class FriendNode {
    private String nameVal;
    private FriendNode nextNodeRef;

    public FriendNode(String nameInit) {
        this.nameVal = nameInit;
        this.nextNodeRef = null;
    }
    public void insertAfter(FriendNode nodeLoc) {
        FriendNode tmpNext;

        tmpNext = this.nextNodeRef;
        this.nextNodeRef = nodeLoc;
        nodeLoc.nextNodeRef = tmpNext;
    }

    public FriendNode getNext() {
        return this.nextNodeRef;
    }

    public void printNodeData() {
        System.out.println(this.nameVal);
    }
}
```
</p>
</details>




