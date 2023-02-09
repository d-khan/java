# Practice object and classes (not graded)

## Objective
Practice objects and classes. This exercise is not graded.

## Pre-requisite
Review "Introduction to objects & classes"

## Task
Given ```main()```, complete the Car class (in file Car.java) with methods to set and get the purchase price of a car (setPurchasePrice(), getPurchasePrice()), and to output the car's information (printInfo()).

### Expected input
2011  
18000   
2018   
where 2011 is the car's model year, 18000 is the purchase price, and 2018 is the current year, the output is:

### Expected output
Car's information:
  Model year: 2011
  Purchase price: $18000
  Current value: $5770

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




