# OutputStream and System.out
Programs need a way to output data to a screen, file, or elsewhere. An OutputStream is a class that supports output. OutputStream provides several overloaded methods for writing a sequence of bytes to a destination. That sequence is normally placed into a buffer, and the system then outputs the buffer at various times.

The print() and println() methods are overloaded in order to support the various standard data types, such as int, boolean, float, etc., each method converting that data type to a sequence of characters. These methods also provide support for reference types. When a programmer invokes either method with a reference type argument the method prints a string representation of the object consisting of the object's class name followed by the "@" character and the hexadecimal value of the object's hash code. A hash code typically represents the object's address in memory, although this is not guaranteed by the Java specification.

System.out is a predefined OutputStream object reference that is associated with a system's standard output, usually a computer screen. The System class' out variable is a reference derived from OutputStream called a PrintStream (declared as PrintStream out; in the System class). The PrintStream class extends the base functionality of the OutputStream class and provides the print() and println() methods for converting different types of data into a sequence of characters. Note that because the System class is predefined, a programmer is not required to import the System class in order to use the output stream System.out.

Basic use of these methods and System.out was discussed in an earlier section.

# InputStream and System.in

Programs need to receive input data, whether from a keyboard, touchscreen, or elsewhere. An InputStream is a class for achieving such input. InputStream provides several overloaded read() methods that allow a programmer to extract bytes from a particular source.

System.in is a predefined input stream object reference that is associated with a system's standard input, which is usually a keyboard. A programmer is not required to import the System class in order to use System.in because the System class is a predefined class.

The System.in input stream automatically reads the standard input from a memory region, known as a buffer, that the operating system fills with the input data.
