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
- created that is associated with a string rather than with the screen (standard output). 
- An output string stream is created using both the StringWriter and PrintWriter classes, which are available by including: ```import java.io.StringWriter;``` and ```import java.io.PrintWriter;```

>The StringWriter class provides a character stream that allows a programmer to output characters. The PrintWriter class is a wrapper class that augments character streams, such as StringWriter, with print() and println() methods that allow a programmer to output various data types (e.g., int, double, String, etc.) to the underlying character stream in a manner similar to System.out.



