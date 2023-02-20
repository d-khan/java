# Learning objectives

Last week, we discussed how to use memory effectively. The linked-list data structure is recommended over conventional arrays when data is inserted or deleted frequently in an array. Furthermore, we discussed how stacks and heaps are used when a class or data type is defined.

In this lecture, we will discuss various input and output streams. As a programmer, you may need to provide input from a user (using a keyboard), memory, or a file. Similarly, the output can be displayed on the console (screen), passed on to a variable, or saved in a file. 

# Output and input streams

## OutputStream
An OutputStream is a class that supports output. OutputStream provides several overloaded methods for writing a sequence of bytes to a destination.

## ```System.out```
```System.out``` is a predefined OutputStream object reference that is associated with a system's standard output, usually a computer screen.

## PrintStream
PrintStream (declared as PrintStream out; in the System class).

<img width="980" alt="image" src="https://user-images.githubusercontent.com/11669149/219922565-944b0e4c-30f4-4efd-ad34-2bf627d001d6.png">

## InputStream
An InputStream is a class for achieving such input. InputStream provides several overloaded ```read()``` methods that allow a programmer to extract bytes from a particular source.

<img width="721" alt="image" src="https://user-images.githubusercontent.com/11669149/219961583-6cdc5246-72f9-489f-9538-32df0ba40115.png">

## byte stream
A byte stream is used by programs to input or output 8-bits (a byte).

## throws clause / exception
A throws clause tells the Java virtual machine that the corresponding method may exit unexpectedly due to an exception, which is an event that disrupts a program's execution.

# Output formatting

## ```printf() / format()```
The standard output stream ```System.out``` provides the methods printf() and format() for output formatting.

## format string
The first argument of the ```printf()``` method, the format string, specifies the format of the text to print along with any number of placeholders for printing numeric values.

## format specifier
A format specifier specifies the type of value to print in its place.

<img width="1056" alt="image" src="https://user-images.githubusercontent.com/11669149/219933140-d54e98c1-0aad-4232-8eda-c879a22708b6.png">

<img width="661" alt="image" src="https://user-images.githubusercontent.com/11669149/219933257-a82b0bf0-daa1-4d95-aa0b-84f13f581a95.png">

## sub-specifier
A sub-specifier provides formatting options for a format specifier and are included between the % and format specifier character.

__%(flags)(width)(.precision)specifier__

<img width="969" alt="image" src="https://user-images.githubusercontent.com/11669149/219933421-943130d7-bb14-4635-8039-cee218fd82b2.png">

## Flushing output
- The PrintStream method ```flush()``` flushes the stream's buffer contents.
- To preserve resources, the system may wait until the buffer is full, or at least has a certain number of characters before moving them to the output device. 
- The PrintStream method flush() flushes the stream's buffer contents. Ex: The statement ```System.out.flush()```; writes the contents of the buffer for System.out to the computer screen. Most Java implementations make System.out flush when a newline character is output or println() method is called.

__Indicate if the line of output is immediately flushed from the System.out buffer.__
```Java
System.out.print("My life has been the poem ");  // A
System.out.println("I would have writ");         // B
System.out.print("But I could not ");            // C
System.out.flush();
System.out.print("both live and utter it.\n");   // D
```

# Streams using Strings
Sometimes a programmer wishes to read input data from a string rather than from the keyboard (standard input).

## input string stream

```java
import java.util.Scanner;

public class StringInputStream {
   public static void main(String[] args) {
      Scanner inSS = null;              // Input string stream
      String userInfo;                  // Input string
      String firstName;                 // First name
      String lastName;                  // Last name
      int userAge;                      // Age

      userInfo = "Amy Smith 19";

      // Init scanner object with string
      inSS = new Scanner(userInfo);

      // Parse name and age values from string
      firstName = inSS.next();
      lastName = inSS.next();
      userAge = inSS.nextInt();

      // Output parsed values
      System.out.println("First name: " + firstName);
      System.out.println("Last name: " + lastName);
      System.out.println("Age: " + userAge);
   }
}
```

## output string stream

- Created that it is associated with a string rather than the screen (standard output). 
- An output string stream is created using both the StringWriter and PrintWriter classes, which are available by including: ```import java.io.StringWriter;``` and ```import java.io.PrintWriter;```
- The __StringWriter__ class provides a character stream that allows a programmer to output characters. 
- The __PrintWriter__ class is a wrapper class that augments character streams, such as StringWriter, with print() and println() methods that allow a programmer to output various data types (e.g., int, double, String, etc.) to the underlying character stream like System.out.

### Example of output string streams

```java
import java.util.Scanner;
import java.io.PrintWriter;
import java.io.StringWriter;

public class StringOutputStream {
    public static void main(String[] args) {
        Scanner scnr = new Scanner(System.in);

        // Basic character stream for fullname
        StringWriter fullnameCharStream = new StringWriter();
        // Augments character stream (fullname) with print()
        PrintWriter fullnameOSS = new PrintWriter(fullnameCharStream);
        // Basic character stream for age
        StringWriter ageCharStream = new StringWriter();
        // Augments character stream (age) with print()
        PrintWriter ageOSS = new PrintWriter(ageCharStream);

        String firstName;      // First name
        String lastName;       // Last name
        String fullName;       // Full name (first and last)
        String ageStr;         // Age (string)
        int userAge;           // Age

        // Prompt user for input
        System.out.print("Enter \"firstname lastname age\": \n   ");
        firstName = scnr.next();
        lastName = scnr.next();
        userAge = scnr.nextInt();

        // Writes formatted string to buffer, copies from underlying char buffer
        fullnameOSS.print(lastName + ", " + firstName);
        fullName = fullnameCharStream.toString();

        // Output parsed input
        System.out.println("\n   Full name: " + fullName);

        // Writes int age as characters to buffer
        ageOSS.print(userAge);

        // Appends (minor) to object if less than 21, then
        // copies buffer into string
        if (userAge < 21) {
            ageOSS.print(" (minor)");
        }

        ageStr = ageCharStream.toString();

        // Output string
        System.out.println("   Age: " + ageStr);
    }
}
```

# File input

## Opening and reading from a file

- Get input from a file rather than from a user typing on a keyboard. 

- To read file input, a programmer can create a new input stream that comes from a file, rather than the predefined input stream System.in that comes from the standard input (keyboard). 

  #### __```fileByteStream = new FileInputStream("numFile.txt");```__ 

### Example - input from a file

  ```java
  import java.util.Scanner;
  import java.io.FileInputStream;
  import java.io.IOException;
  
  public class FileReadNums {
     public static void main (String[] args) throws IOException {
        FileInputStream fileByteStream = null; // File input stream
        Scanner inFS = null;                   // Scanner object
        int fileNum1;                       // Data value from file
        int fileNum2;                       // Data value from file
  
        // Try to open file
        System.out.println("Opening file numFile.txt.");
        fileByteStream = new FileInputStream("numFile.txt");
        inFS = new Scanner(fileByteStream);
        
        // File is open and valid if we got this far 
        // (otherwise exception thrown)
        // numFile.txt should contain two integers, else problems
        System.out.println("Reading two integers.");
        fileNum1 = inFS.nextInt();
        fileNum2 = inFS.nextInt();
  
        // Output values read from file
        System.out.println("num1: " + fileNum1);
        System.out.println("num2: " + fileNum2);
        System.out.println("num1+num2: " + (fileNum1 + fileNum2));
  
        // Done with file, so try to close it
        System.out.println("Closing file numFile.txt.");
        // close() may throw IOException if fails
        fileByteStream.close(); 
     }
  }
  ```
## Reading until the end of the file
- A program can read varying amounts of data in a file by using a loop that reads until valid data is unavailable or the end of the file has been reached. 
- The **```hasNextInt()```** method returns true if an integer is available for reading. If the next item in the file is not an integer or if the previous stream operation reached the end of the file, the method returns false.
  
### Example - Reading a varying amount of data from a file
```java
//Before you start, create a text file "myfile.txt" with some contents on it.
import java.util.Scanner;
import java.io.FileInputStream;
import java.io.IOException;

public class FileReadVaryingAmount {
   public static void main(String[] args) throws IOException {
      FileInputStream fileByteStream = null; // File input stream
      Scanner inFS = null;                   // Scanner object
      int fileNum;                           // Data value from file

      // Try to open file
      System.out.println("Opening file myfile.txt.");
      fileByteStream = new FileInputStream("myfile.txt");
      inFS = new Scanner(fileByteStream);
 
      // File is open and valid if we got this far (otherwise exception thrown)
      System.out.println("Reading and printing numbers.");

      while (inFS.hasNextInt()) {
         fileNum = inFS.nextInt();
         System.out.println("num: " + fileNum);
      }

      // Done with file, so try to close it
      System.out.println("Closing file myfile.txt.");
      fileByteStream.close(); // close() may throw IOException if fails
   }
}
```
# File output

- A FileOutputStream is a class that supports writing to a file. The FileOutputStream class inherits from OutputStream.

<img width="935" alt="image" src="https://user-images.githubusercontent.com/11669149/219969053-983cb263-ad68-44d7-af15-d994dea2e861.png">

### Example - Writing a text file
```java
import java.io.PrintWriter;
import java.io.FileOutputStream;
import java.io.IOException;

public class TextFileWriteSample {
  public static void main(String[] args) throws IOException {
     FileOutputStream fileStream = null;
     PrintWriter outFS = null;

     // Try to open file
     fileStream = new FileOutputStream("myoutfile.txt");
     outFS = new PrintWriter(fileStream);

     // Arriving here implies that the file can now be written
     // to, otherwise an exception would have been thrown.
     outFS.println("Hello");
     outFS.println("1 2 3");

     // Done with file, so try to close
     // Note that close() may throw an IOException on failure
     outFS.close();
  }
}
```

# Takeaway points

- You can provide user input to the code using a keyboard, string, or file.
- Similarly, you can display output to the screen, string, or a file.

------

End of document

