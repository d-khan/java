# Calculate salary using classes

## Objective

## Pre-requisite
Review "Introduction to objects & classes"

## Task A (using classes)
The program below uses a class, TaxTableTools, which has a tax table built in. The main method prompts for a salary, then uses a TaxTableTools method to get the tax rate. The program then calculates the tax to pay and displays the results to the user. Run the program with annual salaries of 10000, 50000, 50001, 100001 and -1 (to end the program) and note the output tax rate and tax to pay.

1. Modify the TaxTableTools class to use a setter method that accepts a new salary and tax rate table.   
2. Modify the program to call the new method, and run the program again, noting the same output.   

### Example - Templates
<details> <summary> Click to get the TaxTableTools.java </summary>
<p>

``` java
public class TaxTableTools {

   /** This class searches the 'search' table with a search argument and
       returns the corresponding value in the 'value' table. Variable
       'nEntries' has the number of entries in each table.
   */
   private int [] search =   {   0,  20000, 50000, 100000, Integer.MAX_VALUE };
   private double [] value = { 0.0,   0.10,  0.20,   0.30,              0.40 };
   private int nEntries;

   // *********************************************************************** 

   // Default constructor 
   public TaxTableTools () {
      nEntries  = search.length;  // Set the length of the search table
   } 
   
   // *********************************************************************** 

   // FIXME: Write a void setter method that sets new values for the private
   //        search and value tables. Name the method: setTables
   //        The method receives as parameters tables from which to load the 
   //        search and value tables.
   
   // *********************************************************************** 

   // Method to get a value from one table based on a range in the other table

   public double getValue(int searchArgument) {
      double result;
      boolean keepLooking;
      int i;

      result = 0.0;
      keepLooking = true;
      i = 0;

      while ((i < nEntries) && keepLooking) {
         if (searchArgument <= search[i]) {
            result = value[i];
            keepLooking = false;
         }
         else {
            ++i;
         }
      } 

      return result;
   } 
} 
```

</p>
</details>

<details> <summary> Click to get the IncomeTaxMain.java </summary>
<p>

``` java
import java.util.Scanner;

public class IncomeTaxMain {    

   // Method to prompt for and input an integer
   public static int getInteger(Scanner input, String prompt) {
      int inputValue;
      
      System.out.println(prompt + ": ");
      inputValue = input.nextInt();
      
      return inputValue;
   } // 

   // *********************************************************************** 

   public static void main(String [] args) { 
      final String PROMPT_SALARY = "\nEnter annual salary (-1 to exit)";
      Scanner scnr = new Scanner(System.in);
      int annualSalary;
      double taxRate;
      int taxToPay;
      int i;

      int []    salary   = {   0,  20000, 50000, 100000, Integer.MAX_VALUE };
      double [] taxTable = { 0.0,   0.10,  0.20,   0.30,              0.40 };

      // Access the related class
      TaxTableTools table = new TaxTableTools();

      // FIXME: Call a setter method in the TaxTableClass that supplies new 
      //        tables for the class to work with. The method should be called
      //        with: table.setTables(salary, taxTable);

      // Get the first annual salary to process
      annualSalary = getInteger(scnr, PROMPT_SALARY);

      while (annualSalary >= 0) {
         taxRate = table.getValue(annualSalary);
         taxToPay= (int)(annualSalary * taxRate);     // Truncate tax to an integer amount
         System.out.println("Annual Salary: " + annualSalary + 
                            "\tTax rate: " + taxRate +
                            "\tTax to pay: " + taxToPay);

         // Get the next annual salary
         annualSalary = getInteger(scnr, PROMPT_SALARY);
      } 
   } 
} 
```
</p>
</details>

## Task B (using constructor overload)
The program below calculates a tax rate and tax to pay given an annual salary. The program uses a class, TaxTableTools, which has the tax table built in. Run the program with annual salaries of 10000, 50000, 50001, 100001 and -1 (to end the program) and note the output tax rate and tax to pay.

1. Overload the constructor.   
   - Add to the TaxTableTools class an overloaded constructor that accepts the base salary table and corresponding tax rate table as parameters.   
   - Modify the main method to call the overloaded constructor with the two tables (arrays) provided in the main method. Be sure to set the nEntries value, too.
   - Note that the tables in the main method are the same as the tables in the TaxTableTools class. This sameness facilitates testing the program with the same annual salary values listed above.
   - Test the program with the annual salary values listed above.
2. Modify the salary and tax tables
   - Modify the salary and tax tables in the main method to use different salary ranges and tax rates.
   - Use the just-created overloaded constructor to initialize the salary and tax tables.
   - Test the program with the annual salary values listed above.

### Example - Templates (constructor overload)
<details> <summary> Click to get the TaxTableTools.java </summary>
<p>

``` java
import java.util.Scanner;

public class TaxTableTools {

   /** This class searches the 'search' table with a search argument and
       returns the corresponding value in the 'value' table. Variable
       'nEntries' has the number of entries in each table.
   */
   private int [] search =   {   0, 20000, 50000, 100000,  Integer.MAX_VALUE };
   private double [] value = { 0.0,  0.10,  0.20,   0.30,               0.40 };
   private int nEntries;

   // *********************************************************************** 

   // Default constructor 
   
   public TaxTableTools () {
      nEntries  = search.length;  // Set the length of the search table
   } 
   
   // *********************************************************************** 

   // Overloaded constructor

   // FIXME: Add an overloaded constructor to load the search and value tables.
   // FIXME: Be sure to set the nEntries value, too.

   // *********************************************************************** 

   // Method to prompt for and input an integer
   
   public int getInteger(Scanner input, String prompt) {
      int inputValue = 0;
      
      System.out.println(prompt + ": ");
      inputValue = input.nextInt();
      
      return inputValue;
   } 

   // *********************************************************************** 

   // Method to get a value from one table based on a range in the other table

   public double getValue(int searchArgument) {
      double result;
      boolean keepLooking;
      int i;

      result = 0.0;
      keepLooking = true;
      i = 0;

      while ((i < nEntries) && keepLooking) {
         if (searchArgument <= search[i]) {
            result = value[i];
            keepLooking = false;
         }
         else {
            ++i;
         }
      } 

      return result;
   } 
} 
```
</p>
</details>

<details> <summary> Click to get the IncomeTaxMain.java </summary>
<p>

``` java
import java.util.Scanner;

public class IncomeTaxMain {    
   public static void main(String [] args) { 
      final String PROMPT_SALARY = "\nEnter annual salary (-1 to exit)";
      Scanner scnr = new Scanner(System.in);
      int annualSalary;
      double taxRate;
      int taxToPay;
      int i;

      // Tables to use in the exercise are the same as in the TaxTableTools class
      // int [] salaryRange = {   0,  20000, 50000, 100000,  Integer.MAX_VALUE };
      // double [] taxRates = { 0.0,   0.10,  0.20,   0.30,               0.40 };

      // 2(a) Modify the salary and tax tables in the main method to use 
      // different salary ranges and tax rates.
      int []    salaryRange  = {   0,  30000,  60000,  Integer.MAX_VALUE };
      double [] taxRates     = { 0.0,  0.25,   0.35,               0.45 };

      // Access the related class
      // TaxTableTools table = new TaxTableTools();

      // 2(b)Use the just-created overloaded constructor to initialize 
      // the salary and tax tables.
      TaxTableTools table = new TaxTableTools(salaryRange, taxRates);

      // Get the first annual salary to process
      annualSalary = table.getInteger(scnr, PROMPT_SALARY);

      while (annualSalary >= 0) {
         taxRate = table.getValue(annualSalary);
         taxToPay= (int)(annualSalary * taxRate);     // Truncate tax to an integer amount
         System.out.println("Annual Salary: " + annualSalary + 
                            "\tTax rate: " + taxRate +
                            "\tTax to pay: " + taxToPay);

         // Get the next annual salary
         annualSalary = table.getInteger(scnr, PROMPT_SALARY);
      } 
   } 
} 
```
</p>
</details>

## What to submit?
1. Draw a flowchart of your thought process. I found this [online flowchart website](http://www.draw.io) very useful. However, you can use any application of your choice. (2 marks). 
2. Explain why did you select a particular sorting algorithm. (1 mark).  
3. What were your challenges in performing the lab (from design to the implementation phases)? (1 mark).  
4. Create a video that explains the working of the code. Furthermore, the video should show your face on one side of the screen (preferably the top or bottom right of the screen). Also, submit the code in the .java extension. (6 marks)

## How to submit it?
- Upload your work in the .pdf format and clearly define your responses.  
- Use headings when possible. Upload the code in the .java extension.

## Deadline
The deadlines are posted on the Syllabus as well as on Canvas.

## Rubric
- The video describes the code in detail. The code is working as per instruction, and the explanation of the questions is submitted (10 marks).  
- The video is submitted, and the code is working, but a partial explanation of the questions is submitted. (6+ marks).  
- The code is uploaded but not working regardless the video is submitted or not. (0 marks)


