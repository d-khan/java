# Objects and Classes Practice Lab -- Full Solution Version

------------------------------------------------------------------------

# Part 1 -- Student Class Implementation

``` java
public class Student {

    private String name;
    private int age;
    private double gpa;

    public Student(String name, int age, double gpa) {
        this.name = name;
        this.age = age;
        this.gpa = gpa;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public double getGpa() {
        return gpa;
    }

    public void setGpa(double gpa) {
        this.gpa = gpa;
    }

    public void displayInfo() {
        System.out.println("Name: " + name + ", Age: " + age + ", GPA: " + gpa);
    }

    @Override
    public String toString() {
        return "Student{name='" + name + "', age=" + age + ", gpa=" + gpa + "}";
    }
}
```

------------------------------------------------------------------------

# Main Class Example

``` java
public class Main {
    public static void main(String[] args) {

        Student s1 = new Student("Alice", 20, 3.8);
        s1.displayInfo();

        s1.setGpa(3.9);
        System.out.println(s1);

        Student s2 = s1;
        s2.setName("Bob");

        System.out.println("s1: " + s1);
        System.out.println("s2: " + s2);
    }
}
```

------------------------------------------------------------------------

# Part 3 -- Multiple Objects with ArrayList

``` java
import java.util.ArrayList;

public class StudentListDemo {

    public static void main(String[] args) {

        ArrayList<Student> students = new ArrayList<>();

        students.add(new Student("Alice", 20, 3.8));
        students.add(new Student("Bob", 21, 3.5));
        students.add(new Student("Charlie", 19, 3.9));

        for (int i = 0; i < students.size(); i++) {
            System.out.println(students.get(i));
        }

        for (Student s : students) {
            System.out.println(s);
        }
    }
}
```

------------------------------------------------------------------------

# Part 4 -- BankAccount Class

``` java
public class BankAccount {

    private String accountHolder;
    private double balance;
    private static int totalAccounts = 0;

    public BankAccount(String accountHolder, double balance) {
        this.accountHolder = accountHolder;
        this.balance = balance;
        totalAccounts++;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposit successful.");
        }
    }

    public void withdraw(double amount) {
        if (amount > balance) {
            System.out.println("Insufficient funds.");
        } else {
            balance -= amount;
            System.out.println("Withdrawal successful.");
        }
    }

    public double getBalance() {
        return balance;
    }

    public static int getTotalAccounts() {
        return totalAccounts;
    }

    @Override
    public String toString() {
        return "BankAccount{holder='" + accountHolder + "', balance=" + balance + "}";
    }
}
```

------------------------------------------------------------------------

# BankAccount Usage

``` java
public class BankDemo {
    public static void main(String[] args) {

        BankAccount acc1 = new BankAccount("John", 1000);
        BankAccount acc2 = new BankAccount("Sara", 2000);

        acc1.deposit(500);
        acc1.withdraw(200);
        acc1.withdraw(2000);

        System.out.println(acc1);
        System.out.println("Total Accounts: " + BankAccount.getTotalAccounts());
    }
}
```

------------------------------------------------------------------------

# Theoretical Answers

1.  A class is a blueprint; an object is an instance of that blueprint.
2.  Objects are stored in heap memory.
3.  The `new` keyword allocates memory and returns a reference.
4.  Encapsulation protects internal state and ensures controlled access.
5.  `toString()` provides meaningful object representation when printed.

------------------------------------------------------------------------

# Bonus -- Rectangle Class

``` java
public class Rectangle {

    private double length;
    private double width;

    public Rectangle() {
        this.length = 1;
        this.width = 1;
    }

    public Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }

    public double area() {
        return length * width;
    }

    public double perimeter() {
        return 2 * (length + width);
    }

    @Override
    public String toString() {
        return "Rectangle{length=" + length + ", width=" + width + "}";
    }
}
```
