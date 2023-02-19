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

<img width="731" alt="image" src="https://user-images.githubusercontent.com/11669149/219932878-e97ad981-89b9-4e06-8e3b-fc68587e85ee.png">

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

Multiple choice problems allow learners to select only one option. Learners can see all the options along with the problem text.
       When you add the problem, be sure to select Settings to specify a Display Name and other values that apply.
       You can use the following example problem as a model.
       >>Which of the following countries has the largest population?<<
       ( ) Brazil {{ timely feedback -- explain why an almost correct answer is wrong }}
       ( ) Germany
       (x) Indonesia
       ( ) Russia




