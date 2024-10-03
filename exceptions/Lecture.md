# Handling exceptions

- Exception handling is also known as error handling at run time.

## Unhandled exceptions

- An exception is an unexpected incident that stops the normal execution of a program.
- Dividing by zero or getting invalid input results in an exception. A program that does not handle an exception ends execution.

> __Note that the exceptions are handled at run time, not at compile time. Compile time exceptions would not compile the program.__

### Example - without exception handling

``` java
// Run this code and provide valid and invalid inputs.
import java.util.Scanner;

public class LightTravelTime {
    public static void main(String[] args) {
        Scanner scnr = new Scanner(System.in);
        double distMiles;
        double lightTravelTimeSec;

        System.out.print("Enter distance in miles: ");

        distMiles = scnr.nextDouble();

        lightTravelTimeSec = distMiles / 186282.0;
        System.out.println(lightTravelTimeSec);
    }
}
```

The following output displays when the user inputs an invalid input.

<img width="763" alt="image" src="https://user-images.githubusercontent.com/11669149/224497620-860e2581-266d-49c4-b130-700495e60df6.png">

1. Scanner's nextDouble() method expects the user to enter a floating-point number.
2. The input "twenty" is a word instead of a floating-point number. So, scnr.nextDouble() throws an InputMismatchException exception, and program execution stops.
3. Because the exception is not handled, the program outputs the exception type and method call stack, and the program execution ends.

## Catching exceptions

- To avoid having a program end when an exception occurs, a program can use try-and-catch blocks to handle the exception during program execution.
- A **try block** surrounds normal code, which is exited immediately if a statement within the try block throws an exception.
- A **catch block** catches an exception thrown in a preceding try block. If the thrown exception's type matches the catch block's parameter type, the code within the catch block executes. A catch block is called an **exception handler**.

### Example code - with exception handling

``` java
import java.util.Scanner;
import java.util.InputMismatchException;

public class LightTravelTime {
    public static void main(String[] args) {
        Scanner scnr = new Scanner(System.in);
        double distMiles = 0.0;
        double lightTravelTimeSec = 0.0;

        System.out.print("Enter distance in miles: ");

        try {
            distMiles = scnr.nextDouble();
            lightTravelTimeSec = distMiles / 186282.0;
        }
        catch (InputMismatchException e) {
            System.out.println("Must enter a number!");
        }

        System.out.println(lightTravelTimeSec);
    }
}
```

A program may be able to resolve some exceptions. The previous example only printed the caught exception. Instead, a program can discard the current input line and get the distance from the user again, as shown in the below example.

### Example code - with exception handling (modified)

``` java
import java.util.Scanner;
import java.util.InputMismatchException;

public class LightTravelTime {
   public static void main(String[] args) {
      Scanner scnr = new Scanner(System.in);
      double distMiles = 0.0;
      double lightTravelTime = 0.0;
      boolean needInput = true;

      while (needInput) {
         System.out.print("Enter a distance in miles: ");
         
         try {
            distMiles = scnr.nextDouble();
            lightTravelTime = distMiles / 186282.0;
            needInput = false;
         }
         catch (InputMismatchException e) {
            scnr.nextLine(); // Throw away incorrect input
         }
      }

      System.out.println("Light travels " + distMiles + 
                         " miles in " + lightTravelTime +
                         " seconds");
   }
}
```
Some common exception types are:

| Type                                                         | Reason exception is throw                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [EOFException](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/io/EOFException.html) | End of file or end of the stream has been reached unexpectedly during input |
| [InputMismatchException](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/InputMismatchException.html) | Received input does not match the expected type, or the input is out of range for the expected type (thrown by Scanner) |
| [ArrayIndexOutOfBoundsException](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/ArrayIndexOutOfBoundsException.html) | An array has been accessed with an illegal index (negative or greater than array size) |
| [FileNotFoundException](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/io/FileNotFoundException.html) | Attempt to open a file denoted by a filename failed          |
| [ArithmeticException](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/ArithmeticException.html) | Arithmetic condition failed (Ex: Divide by zero error)       |

### Practice example

Write a code that generates ArrayIndexOutOfBoundsException in Java.

## Throwing exceptions

- A program can throw user-defined exceptions using a throw statement. 

- A **throw** statement throws a throwable object, like an exception, during program execution. For example, the statement `throw new ArithmeticException;` creates and throws an exception with the message ""Access denied - You must be at least 18 years old.".

### Example code - throwing new exception

``` java
public class Main {
    static void checkAge(int age) {
        if (age < 18) {
            throw new ArithmeticException("Access denied - You must be at least 18 years old.");
        }
        else {
            System.out.println("Access granted - You are old enough!");
        }
    }
    public static void main(String[] args) {
        checkAge(15); // Set age to 15 (which is below 18...)
    }
}
```

### Example code - try, throw and catch

``` java
import java.util.Scanner;
public class DensityCalculator {
    public static void main(String[] args) {
        Scanner scnr = new Scanner(System.in);
        double massVal = 0;   // Object mass (kg)
        double volumeVal = 0; // Object volume (m^3)
        double densityCalc;   // Resulting density
        try {
            System.out.print("Enter mass in Kg: ");
            massVal = scnr.nextDouble();
            // Error checking, non-negative mass
            if (massVal < 0.0) {
                throw new Exception("Invalid mass");
            }
            System.out.print("Enter volume in m^3: ");
            volumeVal = scnr.nextDouble();
            // Error checking, non-negative volume
            if (volumeVal <= 0.0) {
                throw new Exception("Invalid volume");
            }
            densityCalc = massVal / volumeVal;
            System.out.print("Density: " + densityCalc);
        }
        catch (Exception excpt) {
            // Prints the error message passed by the throw statement.
            System.out.print(excpt.getMessage());
        }
    }
}
```

### Example code - multiple catch

``` java
import java.util.Scanner;
import java.util.InputMismatchException;

public class CircleRadiusCalculator {
   public static void main(String[] args) {
      Scanner scnr = new Scanner(System.in);
      double circleArea;
      double circleRadius;

      System.out.print("Enter area: ");
 
      try {
         circleArea = scnr.nextDouble();
 
        //a negative number will trigger this exception
         if (circleArea < 0) {
            throw new Exception("Invalid area.");
         }
 
         circleRadius = Math.sqrt(circleArea / Math.PI);
         System.out.println(circleRadius);
      }
      catch (InputMismatchException excpt) {
         System.out.println("Invalid input."); //a char will trigger this exception
      }
      catch (Exception excpt) {
         System.out.println(excpt.getMessage()); //
      }
   }
}
```

Line 26: An exception handler that catches Exception types can catch any exception because Exception is the base type.

## Hierarchy of Exception (inheritance)

java.lang
		Object
				Throwable
						Error
								LinkageError
								VirtualMachineError
										OutofMemoryError
										StackOverflowError
						Exception
								RuntimeException
										ClassCastException
										IllegalArgumentException
												NumberFormatException
										ArithmeticException
										IndexOutOfBoundException
												ArrayIndexOutOfBoundException
												StringIndexOutOfBoundException
										NullPointerException
								IOException
										SocketException
										FileNotFoundException
										EOFException

> __**What is the difference between an Error and an Exception in Java?**__

A Java **Error** is a subclass of **Throwable** that represents a serious problem that a reasonable application should not try to catch. The method does not have to declare an **Error** or any of its subclasses in its **throws** clause for it to be thrown during the execution of a method. The most common subclasses of the **Error** class are **Java OutOfMemoryError** and **StackOverflowError** classes. The first represents JVM's inability to create a new object; we discussed potential causes in our article about the JVM garbage collector. The second error represents an issue when the application recurses too deeply.

On the other hand, the Java Exception and its subclasses represent situations that an application should catch and try to handle. There are lots of implementations of the Exception class that represent situations that your application can gracefully handle. The **FileNotFoundException**, **SocketException,** or **NullPointerException** are just a few examples you’ve probably encountered when writing Java applications.[^1]

[^1]: https://sematext.com/blog/java-exceptions/

## Exception with files

A program may try to open a file that does not exist. For example,  the file may have been deleted, renamed, or moved. The FileInputStream constructor throws FileNotFoundException if the specified file cannot be found or opened for reading.

### Example code - file not found

``` java
import java.util.Scanner;
import java.io.FileInputStream;
import java.io.FileNotFoundException;

public class FileDataAverage {
   public static void main(String[] args) {
      Scanner scnr = new Scanner(System.in);
      Scanner fileScanner;
      String fileName;
      FileInputStream fileInStream;
      double dataAvg = 0;

      System.out.print("Enter a file name: ");
      fileName = scnr.next();

      try {
         fileInStream = new FileInputStream(fileName);
         fileScanner = new Scanner(fileInStream);
         
         // Read file with fileScanner ...

         System.out.println("Average: " + dataAvg);
      }
      catch (FileNotFoundException e) {
         System.out.println("Cannot find " + fileName);
      }
   }
}
```

## finally block

- A **finally block** always executes when a try block exits. 

- A programmer can use a finally block to do additional processing, even if an exception is thrown in the try statement. 
- The program below uses a finally block to write partial results to the output file, even if an InputMismatchException exception occurs while reading the input file.

### Example code

``` java
//incomplete code.
try {
  int[] myNumbers = {1, 2, 3};
  System.out.println(myNumbers[10]);
} catch (Exception e) {
  System.out.println("Something went wrong.");
} finally {
  System.out.println("The 'try catch' is finished.");
}
```

## Exceptions with methods

### Example code

``` java
import java.util.Scanner;

public class CircleRadiusCalculator {
   public static double getArea(Scanner scnr) throws Exception {
      double circleArea;

      System.out.print("Enter area: ");

      circleArea = scnr.nextDouble();

      if (circleArea < 0) {
         throw new Exception("Invalid area"); //Exception
      }

      return circleArea;
   }

   public static void main(String[] args) {
      Scanner scnr = new Scanner(System.in);
      double circleArea;
      double circleRadius;

      try {
         circleArea = getArea(scnr);
         circleRadius = Math.sqrt(circleArea / Math.PI);
         System.out.println(circleRadius);
      }
      catch (Exception excpt) {
         System.out.println(excpt.getMessage());
      }
   }
}
```

- The getArea() method may throw an exception that is not handled within the method.

- The throws clause indicates the method may throw an exception that should be handled by the calling code.

- The main() method, which calls getArea(), uses a try/catch block to catch and handle the exception thrown by getArea().

### Practice code

> Modify the above code and add exceptions. For example, circle area cant be 0 and cant be negative. Modify the exception to create two seperate messages.

## Checked vs unchecked exceptions

Java has two types of exceptions:

- A **checked exception** is an exception that a programmer should be able to anticipate and handle. For example, a program that opens files should anticipate and handle a FileNotFoundException.
- An **unchecked exception** is caused by hardware or logic errors that a programmer usually cannot anticipate and handle. For example, a program should try to eliminate code that uses null references instead of catching and handling NullPointerException.

### Example code - checked vs unchecked exceptions

``` java
public static int sumFile(String file) throws FileNotFoundException, InputMismatchException {			//InputMismatchException is optional
   FileInputStream inStrm = new FileInputStream(fileName);
   Scanner fileScnr = new Scanner(inStrm);
   int numValues = fileScnr.nextInt();
   int sumVal = 0;

   for (int i = 0; i < numValues; ++i) {
      sumVal += fileScnr.nextInt();
   }

   return sumVal;
}

public static void main(String[] args) {
   Scanner scnr = new Scanner(System.in);
   String fileName;
   int sumVal;

   fileName = scnr.next();

   try {
      sumVal = sumFile(fileName);
      System.out.println(sumVal);
   }
   catch (FileNotFoundException excpt) {
      System.out.println(excpt.getMessage());
   }
}
```

- The FileInputStream constructor may throw FileNotFoundException, which is a checked exception. sumFile() must either catch or specify FileNotFoundException in a throws clause.

- Scanner's nextInt() method may throw an InputMismatchException, which is an unchecked exception. Catching or specifying an unchecked exception in a throws clause is optional.

- Code that calls sumFile() must catch or specify FileNotFoundException. Catching or specifying InputMismatchException is optional.

**Common unchecked exceptions**

| Unchecked exception                                          | Notes                                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [NullPointerException](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/lang/NullPointerException.html) | Indicates a null reference.                                  |
| [IndexOutOfBoundsException](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/lang/IndexOutOfBoundsException.html) | Indicates that an index (e.g., an index for an array) is outside the appropriate range. |
| [ArithmeticException](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/lang/ArithmeticException.html) | Indicates the occurrence of an exceptional arithmetic condition (e.g., integer division by zero). |
| [IOError](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/io/IOError.html) | Indicates the failure of an I/O operation.                   |
| [ClassCastException](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/lang/ClassCastException.html) | Indicates an invalid attempt to cast an object to type of which the object is not an instance (e.g., casting a Double to a String). |
| [IllegalArgumentException](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/lang/IllegalArgumentException.html) | Indicates an illegal or inappropriate method argument.       |

## User-defined exceptions

- A catch block that catches the Exception type can catch exceptions of any type. Thus, a program that uses the Exception type may not be able to differentiate between caught exceptions or may catch unintended exception types.

```java
import java.util.Scanner;

public class DensityCalculator {
   public static double getDensity(Scanner scnr) throws Exception {
      double massVal = scnr.nextDouble();
      double volumeVal = scnr.nextDouble();
      double densityCalc = massVal / volumeVal;

      if (Double.isNaN(densityCalc)) {
         throw new Exception("densityCalc is NaN");
      }

      return densityCalc;
   }

   public static void main(String[] args) {
      Scanner scnr = new Scanner(System.in);
      double densityCalc = 0.0;

      try {
         densityCalc = getDensity(scnr);
         System.out.println("Density: " + densityCalc);
      }
      catch (Exception excpt) {
         // Programmer only intended to handle NaN Exception.
         // Catch block catches ALL exceptions.
      }
   }
}
```

- The programmer intended for the catch block to only catch the exception explicitly thrown if the calculation resulting in NaN.
- Because the catch block catches all exception types, an unintended InputMismatchException will also be caught.
- Catching the Exception type catches all exceptions, which may not be the programmer's intention.

A programmer can define a custom exception type by extending the Exception class. The example below extends Exception to create a custom checked exception that is initialized with a fixed message.

```java
public class NaNException extends Exception {
   public NaNException() {
      super("NaN Exception");
   }
}
```

- A user-defined exception type extends the Exception class.

- The constructor passes a fixed exception message string to the Exception class' constructor.

### Example code - multiple user-defined exceptions

The program below throws exceptions of type InvalidNegativeInputException for negative inputs and throws NaNException when dividing 0.0 by 0.0. By using separate exception handlers for each exception type, the program can handle each exception separately.

**InvalidNegativeInputException.java**

```
public class InvalidNegativeInputException extends Exception {
   public InvalidNegativeInputException(String varName) {
      super("Variable " + varName + " is negative");
   }
}
```

**NaNException.java**

``` java
public class NaNException extends Exception {
   public NaNException(String varName) {
      super("Variable " + varName + " is NaN");
   }
}
```

**DensityCalculator.java**

```java
import java.util.Scanner;

public class DensityCalculator {
   public static double getPositiveValue(Scanner scnr, String valName)
                        throws InvalidNegativeInputException {

      System.out.print("Enter " + valName + ": ");

      double inputVal = scnr.nextDouble();

      if (inputVal < 0.0) {
          throw new InvalidNegativeInputException(valName);
      }

      return inputVal;
   }

   public static double getDensity(Scanner scnr)
                        throws InvalidNegativeInputException, NaNException {

      double massVal = getPositiveValue(scnr, "massVal");
      double volumeVal = getPositiveValue(scnr, "volumeVal");
      double densityCalc = massVal / volumeVal;

      if (Double.isNaN(densityCalc)) {
         throw new NaNException("densityCalc");
      }

      return densityCalc;
   }

   public static void main(String[] args) {
      Scanner scnr = new Scanner(System.in);

      try {
         System.out.println("Density: " + getDensity(scnr));
      }
      catch (InvalidNegativeInputException excpt) {
         System.out.println(excpt.getMessage());

         // Handle ...
      }
      catch (NaNException excpt) {
         System.out.println(excpt.getMessage());

         // Handle ...
      }
   }
}
```

## Reflection

Exceptions are important to control errors at compile time. A programmer must include exceptions, especially when a program deals with inputs, to take defined data and prepare the code for unexpected events.

## Further reading

[Oracle docs](https://docs.oracle.com/en/java/javase/12/docs/api/index.html)
