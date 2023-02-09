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
```
Nutritional information per serving of M&M's:
  Fat: 10.00 g
  Carbohydrates: 34.00 g
  Protein: 2.00 g
Number of calories for 1.00 serving(s): 234.00
Number of calories for 3.00 serving(s): 702.00
```
Note: The program outputs the number of calories for one serving of a food and for the input number of servings as well. The program only outputs the calories for one serving of water.

### Solution
<details> <summary> Click to get the NutritionalInfo.java </summary>
<p>

``` java
import java.util.Scanner;

public class NutritionalInfo {
   public static void main(String[] args) {
      Scanner scnr = new Scanner(System.in);
      FoodItem foodItem;
      
      String itemName = scnr.next();
      
      if(itemName.equals("Water") || itemName.equals("water")) {
         foodItem = new FoodItem();
         
         foodItem.printInfo();
         System.out.printf("Number of calories for %.2f serving(s): %.2f\n", 1.0, 
                          foodItem.getCalories(1.0));
      }
      
      else {
         double amountFat = scnr.nextDouble();
         double amountCarbs = scnr.nextDouble();
         double amountProtein = scnr.nextDouble();
      
         foodItem = new FoodItem(itemName, amountFat, amountCarbs, amountProtein);
      
         double numServings = scnr.nextDouble();
                                                      
         foodItem.printInfo();
         System.out.printf("Number of calories for %.2f serving(s): %.2f\n", 1.0,
                             foodItem.getCalories(1.0));
                             
         System.out.printf("Number of calories for %.2f serving(s): %.2f\n", numServings,
                             foodItem.getCalories(numServings));
      }
   }
}
```

</p>
</details>

<details> <summary> Click to get the FoodItem.java </summary>
<p>

``` java
public class FoodItem {
   private String name;
   private double fat;
   private double carbs;
   private double protein;
   
   // Define default constructor
   public FoodItem() {
      name = "Water";
      fat = 0.0;
      carbs = 0.0;
      protein = 0.0;
   }
   
   // Define second constructor with parameters to initialize private fields
   public FoodItem(String userName, double userFatAmt, double userCarbAmt, 
                   double userProteinAmt) {
      name = userName;
      fat = userFatAmt;
      carbs = userCarbAmt;
      protein = userProteinAmt;
   }
   
   public String getName() {
      return name;
   }
   
   public double getFat() {
      return fat;
   }
   
   public double getCarbs() {
      return carbs;
   }
   
   public double getProtein() {
      return protein;
   }
   
   public double getCalories(double numServings) {
      // Calorie formula
      double calories = ((fat * 9) + (carbs * 4) + (protein * 4)) * numServings;
      return calories;
   }
   
   public void printInfo() {
      System.out.println("Nutritional information per serving of " + name + ":");
      System.out.printf("  Fat: %.2f g\n", fat);
      System.out.printf("  Carbohydrates: %.2f g\n", carbs);
      System.out.printf("  Protein: %.2f g\n", protein);
   }
}
  
```
</p>
</details>




