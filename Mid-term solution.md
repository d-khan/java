## **Design Overview**

- **Parent Class:** `Item`
- Derived Classes:
  - `Painkiller`
  - `Bandage`
  - `Equipment`
- Concepts Used:
  - **Inheritance**
  - **Method Overriding** → `display()`
  - **Method Overloading** → `updateItem(...)` with different parameters

## Inventory control system - version 1.0

```java
// Parent Class
class Item {
    protected String name;
    protected String company;

    public Item(String name, String company) {
        this.name = name;
        this.company = company;
    }

    // Method to display basic info
    public void display() {
        System.out.println("Item Name: " + name);
        System.out.println("Company: " + company);
    }

    // Overloaded update methods
    public void updateItem(String name) {
        this.name = name;
    }

    public void updateItem(String name, String company) {
        this.name = name;
        this.company = company;
    }
}
```

```java
class Painkiller extends Item {
    private String expiryDate;
    private String ageGroup;

    public Painkiller(String name, String company, String expiryDate, String ageGroup) {
        super(name, company);
        this.expiryDate = expiryDate;
        this.ageGroup = ageGroup;
    }

    // Override display()
    @Override
    public void display() {
        super.display();
        System.out.println("Expiry Date: " + expiryDate);
        System.out.println("Age Group: " + ageGroup);
        System.out.println("---------------------------");
    }

    // Overloaded update method
    public void updateItem(String name, String company, String expiryDate, String ageGroup) {
        super.updateItem(name, company);
        this.expiryDate = expiryDate;
        this.ageGroup = ageGroup;
    }
}
```

```java
class Bandage extends Item {
    private String expiryDate;
    private String ageGroup;
    private boolean waterproof;

    public Bandage(String name, String company, String expiryDate, String ageGroup, boolean waterproof) {
        super(name, company);
        this.expiryDate = expiryDate;
        this.ageGroup = ageGroup;
        this.waterproof = waterproof;
    }

    // Override display()
    @Override
    public void display() {
        super.display();
        System.out.println("Expiry Date: " + expiryDate);
        System.out.println("Age Group: " + ageGroup);
        System.out.println("Waterproof: " + (waterproof ? "Yes" : "No"));
        System.out.println("---------------------------");
    }

    // Overloaded update method
    public void updateItem(String name, String company, String expiryDate, String ageGroup, boolean waterproof) {
        super.updateItem(name, company);
        this.expiryDate = expiryDate;
        this.ageGroup = ageGroup;
        this.waterproof = waterproof;
    }
}
```

```java
class Equipment extends Item {
    private double weight;

    public Equipment(String name, String company, double weight) {
        super(name, company);
        this.weight = weight;
    }

    // Override display()
    @Override
    public void display() {
        super.display();
        System.out.println("Weight (lbs): " + weight);
        System.out.println("---------------------------");
    }

    // Overloaded update method
    public void updateItem(String name, String company, double weight) {
        super.updateItem(name, company);
        this.weight = weight;
    }
}
```

```java
public class InventorySystem {
    public static void main(String[] args) {

        // Create objects
        Painkiller p = new Painkiller("Tylenol", "Johnson & Johnson", "2027-05", "Adult");
        Bandage b = new Bandage("Band-Aid", "3M", "2026-08", "All", true);
        Equipment e = new Equipment("Thermometer", "Omron", 1.2);

        // Display initial data
        System.out.println("Initial Inventory:");
        p.display();
        b.display();
        e.display();

        // Update items
        p.updateItem("Advil", "Pfizer", "2028-01", "Adult");
        b.updateItem("Waterproof Bandage", "3M", "2027-12", "All", true);
        e.updateItem("Digital Thermometer", "Omron", 1.5);

        // Display updated data
        System.out.println("\nUpdated Inventory:");
        p.display();
        b.display();
        e.display();
    }
}
```

## Inventory control system - version 2.0

```java
import java.util.Scanner;
import java.util.InputMismatchException;

// Parent Class
class Item {
    protected String name;
    protected String company;

    public Item(String name, String company) {
        this.name = name;
        this.company = company;
    }

    public void display() {
        System.out.println("Item Name: " + name);
        System.out.println("Company: " + company);
    }
}

// Equipment Class
class Equipment extends Item {
    private double weight;

    public Equipment(String name, String company, double weight) {
        super(name, company);
        this.weight = weight;
    }

    @Override
    public void display() {
        super.display();
        System.out.println("Weight (lbs): " + weight);
        System.out.println("---------------------------");
    }

    public void setWeight(double weight) {
        if (weight <= 0) {
            throw new IllegalArgumentException("Weight must be positive.");
        }
        this.weight = weight;
    }
}

// Bandage Class
class Bandage extends Item {
    private String expiryDate;
    private String ageGroup;
    private boolean waterproof;

    public Bandage(String name, String company, String expiryDate, String ageGroup, boolean waterproof) {
        super(name, company);
        this.expiryDate = expiryDate;
        this.ageGroup = ageGroup;
        this.waterproof = waterproof;
    }

    @Override
    public void display() {
        super.display();
        System.out.println("Expiry Date: " + expiryDate);
        System.out.println("Age Group: " + ageGroup);
        System.out.println("Waterproof: " + (waterproof ? "Yes" : "No"));
        System.out.println("---------------------------");
    }

    public void setWaterproof(char input) {
        if (input == 'Y' || input == 'y') {
            waterproof = true;
        } else if (input == 'N' || input == 'n') {
            waterproof = false;
        } else {
            throw new IllegalArgumentException("Enter only Y or N.");
        }
    }
}

// Painkiller Class
class Painkiller extends Item {
    private String expiryDate;
    private String ageGroup;

    public Painkiller(String name, String company, String expiryDate, String ageGroup) {
        super(name, company);
        this.expiryDate = expiryDate;
        this.ageGroup = ageGroup;
    }

    @Override
    public void display() {
        super.display();
        System.out.println("Expiry Date: " + expiryDate);
        System.out.println("Age Group: " + ageGroup);
        System.out.println("---------------------------");
    }
}

// Main Class
public class InventorySystemInteractive {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        // ---------------- EQUIPMENT INPUT ----------------
        System.out.println("Enter Equipment Details:");
        System.out.print("Name: ");
        String eqName = sc.nextLine();

        System.out.print("Company: ");
        String eqCompany = sc.nextLine();

        double weight = 0;
        boolean validWeight = false;

        do {
            try {
                System.out.print("Weight (lbs): ");
                weight = sc.nextDouble(); // may throw InputMismatchException

                if (weight <= 0) {
                    throw new IllegalArgumentException("Weight must be positive.");
                }

                validWeight = true;

            } catch (InputMismatchException e) {
                System.out.println("Error: Enter a numeric value.");
                sc.nextLine(); // clear buffer

            } catch (IllegalArgumentException e) {
                System.out.println("Error: " + e.getMessage());
            }

        } while (!validWeight);

        sc.nextLine(); // clear newline

        Equipment eq = new Equipment(eqName, eqCompany, weight);


        // ---------------- BANDAGE INPUT ----------------
        System.out.println("\nEnter Bandage Details:");
        System.out.print("Name: ");
        String bName = sc.nextLine();

        System.out.print("Company: ");
        String bCompany = sc.nextLine();

        System.out.print("Expiry Date: ");
        String bExpiry = sc.nextLine();

        System.out.print("Age Group: ");
        String bAge = sc.nextLine();

        boolean waterproof = false;
        boolean validChoice = false;

        do {
            try {
                System.out.print("Waterproof (Y/N): ");
                char choice = sc.next().charAt(0);

                if (choice == 'Y' || choice == 'y') {
                    waterproof = true;
                } else if (choice == 'N' || choice == 'n') {
                    waterproof = false;
                } else {
                    throw new IllegalArgumentException("Enter only Y or N.");
                }

                validChoice = true;

            } catch (IllegalArgumentException e) {
                System.out.println("Error: " + e.getMessage());
            }

        } while (!validChoice);

        sc.nextLine(); // clear newline

        Bandage bd = new Bandage(bName, bCompany, bExpiry, bAge, waterproof);


        // ---------------- PAINKILLER INPUT ----------------
        System.out.println("\nEnter Painkiller Details:");
        System.out.print("Name: ");
        String pName = sc.nextLine();

        System.out.print("Company: ");
        String pCompany = sc.nextLine();

        System.out.print("Expiry Date: ");
        String pExpiry = sc.nextLine();

        System.out.print("Age Group: ");
        String pAge = sc.nextLine();

        Painkiller pk = new Painkiller(pName, pCompany, pExpiry, pAge);


        // ---------------- DISPLAY ALL ----------------
        System.out.println("\nInventory Summary:");
        eq.display();
        bd.display();
        pk.display();

        sc.close();
    }
}
```

## Inventory control system - version 3.0 

Use it to validate **one invalid input** (e.g., **negative or zero weight**)

```java
import java.util.Scanner;
import java.util.InputMismatchException;

// ----------- CUSTOM EXCEPTION -----------
class InvalidWeightException extends Exception {
    public InvalidWeightException(String message) {
        super(message);
    }
}

// ----------- PARENT CLASS -----------
class Item {
    protected String name;
    protected String company;

    public Item(String name, String company) {
        this.name = name;
        this.company = company;
    }

    public void display() {
        System.out.println("Item Name: " + name);
        System.out.println("Company: " + company);
    }
}

// ----------- DERIVED CLASS -----------
class Equipment extends Item {
    private double weight;

    public Equipment(String name, String company, double weight) {
        super(name, company);
        this.weight = weight;
    }

    // Method that may throw custom exception
    public void setWeight(double weight) throws InvalidWeightException {
        if (weight <= 0) {
            throw new InvalidWeightException("Weight must be greater than 0.");
        }
        this.weight = weight;
    }

    @Override
    public void display() {
        super.display();
        System.out.println("Weight (lbs): " + weight);
        System.out.println("---------------------------");
    }
}

// ----------- MAIN CLASS -----------
public class InventorySystemCustomException {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.print("Enter Equipment Name: ");
        String name = sc.nextLine();

        System.out.print("Enter Company Name: ");
        String company = sc.nextLine();

        Equipment eq = new Equipment(name, company, 1.0);

        boolean valid = false;

        // ----------- LOOP UNTIL VALID INPUT -----------
        do {
            try {
                System.out.print("Enter Weight (lbs): ");
                double weight = sc.nextDouble(); // may throw InputMismatchException

                eq.setWeight(weight); // may throw InvalidWeightException
                valid = true;

            } catch (InputMismatchException e) {
                System.out.println("Error: Please enter a numeric value.");
                sc.nextLine(); // clear buffer

            } catch (InvalidWeightException e) {
                System.out.println("Custom Error: " + e.getMessage());
            }

        } while (!valid);

        // Display final object
        System.out.println("\nUpdated Equipment:");
        eq.display();

        sc.close();
    }
}
```

