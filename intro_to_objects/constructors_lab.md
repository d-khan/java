# Practice constructors (not graded)

## Objective
Practice constructors in objects and classes. This exercise is not graded.

## Pre-requisite
Review "Introduction to objects & classes"

## Task A (using classes)
Given ```main()```, complete the FoodItem class (in file FoodItem.java) with constructors to initialize each food item. The default constructor should initialize the name to "Water" and all other fields to 0.0. The second constructor should have four parameters (food name, grams of fat, grams of carbohydrates, and grams of protein) and should assign each private field with the appropriate parameter value.

### Expected input
Water 

### Expected output
Nutritional information per serving of Water:
  Fat: 0.00 g
  Carbohydrates: 0.00 g
  Protein: 0.00 g
Number of calories for 1.00 serving(s): 0.00

Note: printInfo() should use two spaces for indentation.

### Solution
<details> <summary> Click to get the Car.java </summary>
<p>

``` java
public class Car {
   private int modelYear;
   // Declare purchasePrice data member (int)
   private int purchasePrice;
   private int currentValue;
   
   public void setModelYear(int userYear){
      modelYear = userYear;
   }
   
   public int getModelYear() {
      return modelYear;
   }
   
   // Define setPurchasePrice() method
   public void setPurchasePrice(int userPrice){
      purchasePrice = userPrice;
   }
   
   // Define getPurchasePrice() method
   public int getPurchasePrice() {
      return purchasePrice;
   }
   
   public void calcCurrentValue(int currentYear) {
      double depreciationRate = 0.15;
      int carAge = currentYear - modelYear;
      
      // Car depreciation formula
      currentValue = (int) 
         Math.round(purchasePrice * Math.pow((1 - depreciationRate), carAge));
   }
   
   // Define printInfo() method to output modelYear, purchasePrice, and currentValue
   public void printInfo() {
      System.out.println("Car's information:");
      System.out.println("  Model year: " + modelYear);
      System.out.println("  Purchase price: $" + purchasePrice);
      System.out.println("  Current value: $" + currentValue);
   }
}
```

</p>
</details>

<details> <summary> Click to get the CarValuemain.java </summary>
<p>

``` java
import java.util.Scanner;
import java.lang.Math;

public class CarValue {
   public static void main(String[] args) {
      Scanner scnr = new Scanner(System.in);
      
      Car myCar = new Car();
      
      int userYear = scnr.nextInt();
      int userPrice = scnr.nextInt();
      int userCurrentYear = scnr.nextInt();
      
      myCar.setModelYear(userYear);
      myCar.setPurchasePrice(userPrice);
      myCar.calcCurrentValue(userCurrentYear);
      
      myCar.printInfo();
   }
}

```
</p>
</details>




