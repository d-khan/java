# Practice object and classes (not graded)

## Objective
Practice objects and classes. This exercise is not graded.

## Pre-requisite
Review "Introduction to objects & classes"

## Task A (using classes)
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

### What to submit?
1. Draw a flowchart of your thought process. I found this [online flowchart website](http://www.draw.io) very useful. However, you can use any application of your choice. (2 marks).   
2. What were your challenges in performing the lab (from design to the implementation phases)? (2 mark).  
3. Create a video that explains the working of the code. Furthermore, the video should show your face on one side of the screen (preferably the top or bottom right of the screen). Also, submit the code in the .java extension. (6 marks)

## How to submit it?
- Upload your work in the .pdf format and clearly define your responses.  
- Use headings when possible. Upload the code in the .java extension.



