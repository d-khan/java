```java
public class LinkedListDemo {

    // Node class
    static class Node {
        int data;
        Node next;

        Node(int data) {
            this.data = data;
            this.next = null;
        }
    }

    // Head of the list
    private Node head;

    // Insert at front
    public void insertAtFront(int data) {
        Node newNode = new Node(data);
        newNode.next = head;
        head = newNode;
    }

    // Insert at end
    public void insertAtEnd(int data) {
        Node newNode = new Node(data);

        if (head == null) {
            head = newNode;
            return;
        }

        Node current = head;
        while (current.next != null) {
            current = current.next;
        }

        current.next = newNode;
    }

    // Delete by value
    public void delete(int key) {
        if (head == null) return;

        if (head.data == key) {
            head = head.next;
            return;
        }

        Node current = head;
        while (current.next != null && current.next.data != key) {
            current = current.next;
        }

        if (current.next != null) {
            current.next = current.next.next;
        }
    }

    // Display list
    public void display() {
        Node current = head;

        while (current != null) {
            System.out.print(current.data + " -> ");
            current = current.next;
        }

        System.out.println("null");
    }

    // Main method (entry point)
    public static void main(String[] args) {
        LinkedListDemo list = new LinkedListDemo();

        // Insert elements
        list.insertAtFront(10);
        list.insertAtFront(20);
        list.insertAtEnd(30);
        list.insertAtEnd(40);

        System.out.println("Initial list:");
        list.display();

        // Delete element
        list.delete(10);
        System.out.println("After deleting 10:");
        list.display();

        // Add more elements
        list.insertAtFront(5);
        System.out.println("After inserting 5 at front:");
        list.display();
    }
}
```
