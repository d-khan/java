# Introduction to objects
## Grouping things into objects
The physical world comprises material items like wood, metal, plastic, fabric, etc. To keep the world understandable, people deal with higher-level objects, like chairs, tables, and TV's. Those objects are groupings of lower-level items.

Likewise, a program is made up of items like variables and methods. To keep programs understandable, programmers often deal with higher-level groupings of those items known as objects. In programming, an object is a grouping of data (variables) and operations that can be performed on that data (methods).

## Abstraction
Abstraction means to have a user interact with an item at a high-level, with lower-level internal details hidden from the user (aka information hiding or encapsulation). Ex: An oven supports an abstraction of a food compartment and a knob to control heat. An oven's user need not interact with the internal parts of an oven.

Objects strongly support abstraction, hiding entire groups of methods and variables and exposing only certain methods to a user.

An abstract data type (ADT) is a data type whose creation and update are constrained to specific well-defined operations. A class can be used to implement an ADT.

# Using a class
## Classes intro: Public member methods
The class construct defines a new type that can group data and methods to form an object. A class' public member methods indicate all operations a class user can perform on the object. The power of classes is that a class user need not know how the class' data and methods are implemented but need only understand how each public member method behaves.

<img width="634" alt="class_Restaurant" src="https://user-images.githubusercontent.com/11669149/214719429-4dbbb7a7-1033-467a-a232-530e43ae5964.png">

## Using a class
A programmer can create one or more objects of the same class. Creating an object consists of two steps: declaring a reference variable of the class type, and assigning the variable with an explicitly allocated instance of the class type. A reference variable can refer to an instance of a class. The new operator explicitly allocates an object of the specified class type. Ex: Restaurant favLunchPlace = new Restaurant(); creates a Restaurant object named favLunchPlace.

The "." operator, known as the member access operator, is used to invoke a method on an object. Ex: favLunchPlace.setRating(4) calls the setRating() method on the favLunchPlace object, which sets the object's rating to 4.

<img width="640" alt="class_RestaurantFavorites" src="https://user-images.githubusercontent.com/11669149/214719560-cdd1e47a-0559-44f9-934a-64e882e0e604.png">

### Class example: String
Java's String object is a class that stores a character string in memory, along with variables indicating the length and other things, but a String's user need not know such details. Instead, the String's user just needs to know what public member methods can be used.

# Defining a class
## Private fields
In addition to public member methods, a class definition has private fields: variables that member methods can access but class users cannot. The private access modifier precedes each private field declaration.

<img width="640" alt="private_fields" src="https://user-images.githubusercontent.com/11669149/214719619-917d46ec-9c3d-47b7-85a3-2c0db619cb42.png">

## Defining a class public member methods
A programmer defining a class first names the class, declares private fields, and defines public member methods. A class' fields and methods are collectively called class members.

The programmer defines the details of each member method, sometimes called the class' implementation. A method definition provides an access modifier, return type, name, parameters, and the method's statements. A member method can access all private fields.

<img width="637" alt="Restaurant" src="https://user-images.githubusercontent.com/11669149/214719673-e719b4cb-1cab-4bdf-95d8-f62a7e290eb3.png">
<img width="638" alt="RestaurantFavorites" src="https://user-images.githubusercontent.com/11669149/214719687-bfbf7983-69c3-4a66-8d49-23f23c46bc85.png">

### Example - Bicycle class
The following class gives an overview of how a class, constructor and methods are defined.

``` java
public class Bicycle { 
    // the Bicycle class has three fields
    public int cadence;
    public int gear;
    public int speed;
       

    // the Bicycle class has one constructor
    public Bicycle(int startCadence, int startSpeed, int startGear) {
        gear = startGear;
        cadence = startCadence;
        speed = startSpeed;
    }
    // the Bicycle class has four methods
    public void setCadence(int newValue) {
        cadence = newValue;
    }  
    public void setGear(int newValue) {
        gear = newValue;
    }   
    public void applyBrake(int decrement) {
        speed -= decrement;
    }   
    public void speedUp(int increment) {
        speed += increment;
    }   
}
```

### Example - PersonInfo class
    
```java
import java.util.Scanner;
public class CallPersonInfo {

    public static void main(String [] args) {
        Scanner scnr = new Scanner(System.in);
        PersonInfo person1 = new PersonInfo();
        int personsKid;

        System.out.println("Enter number of kids: ");
        personsKid = scnr.nextInt();

        person1.setNumKids(personsKid);

        System.out.println("Kids: " + person1.getNumKids());
        person1.incNumKids();
        System.out.println("New baby, kids now: " + person1.getNumKids());

    }

}

class PersonInfo {
    private int numKids;

    public void setNumKids(int setPersonsKids) {
        numKids = setPersonsKids;
    }

    public void incNumKids() {
        numKids = numKids + 1;
    }

    public int getNumKids() {
        return numKids;
    }
}
```


# Mutators, accessors, and private helpers

## Mutators and accessors
A class' public methods are commonly classified as either mutators or accessors.

A **mutator** method may modify ("mutate") a class' fields.
An **accessor** method accesses fields but may not modify a class' fields.
Commonly, a field has two associated methods: a mutator for setting the value, and an accessor for getting the value, known as a setter and getter method, respectively, and typically with names starting with set or get. Other mutators and accessors may exist that aren't associated with just one field, such as the print() method below.

### Example

``` java
public class MyRestaurant {
    public static void main(String[] args) {
        Restaurant myPlace = new Restaurant();
        myPlace.setName("Maria's Diner");
        myPlace.setRating(5);
        System.out.print(myPlace.getName() + " is rated ");
        System.out.println(myPlace.getRating());
    }
}
class Restaurant {
    private String name;
    private int rating;

    public void setName(String restaurantName) {  // Mutator
        name = restaurantName;
    }

    public void setRating(int userRating) {       // Mutator
        rating = userRating;
    }

    public String getName() {  // Accessor
        return name;
    }

    public int getRating() {  // Accessor
        return rating;
    }

    public void print() {      // Accessor
        System.out.println(name + " -- " + rating);
    }
}
```


## Private helper methods
A programmer commonly creates private methods, known as private helper methods, to help public methods carry out tasks.

<img width="640" alt="private_fields" src="https://user-images.githubusercontent.com/11669149/214719756-a43d59a9-180d-4370-977b-3b858b8f5101.png">

# Initialization and constructors

> A good practice is to initialize all variables when declared. This section deals with initializing the fields of a class when a variable of the class type is allocated.

## Field initialization
A programmer can initialize fields in the field declaration. Any object created of that class type will initially have those values.

### Example: A class definition with initialized fields

    
``` java
public class RestaurantFavorites {
    public static void main(String[] args) {
        Restaurant_f favLunchPlace = new Restaurant_f(); // Initializes fields with values in class definition

        favLunchPlace.print();

        favLunchPlace.setName("Central Deli");
        favLunchPlace.setRating(4);

        favLunchPlace.print();
    }
}

class Restaurant_f {
    private String name = "NoName";
    private int rating = -1;

    public void setName(String restaurantName) {
        name = restaurantName;
    }

    public void setRating(int userRating) {
        rating = userRating;
    }

    public void print() {
        System.out.println(name + " -- " + rating);
    }
}
```


## Constructors
Java provides a special class member method, known as a constructor, that is called when an object of that class type is created, and which can be used to initialize all fields. The constructor has the same name as the class. The constructor method has no return type, not even void. Ex: public Restaurant() {...} defines a constructor for the Restaurant class.

A programmer specifies the constructor that should be called when creating an object. Ex: Restaurant favLunchPlace = new Restaurant(); creates a new Restaurant object and calls the constructor Restaurant().

If a class does not have a programmer-defined constructor, then the Java compiler implicitly defines a default constructor with no arguments. The Java compiler also initializes all fields to their default values.

### Example: Adding a constructor member method to the Restaurant class.

    
``` java
public class RestaurantFavorites {
    public static void main(String[] args) {
        Restaurant_f favLunchPlace = new Restaurant_f(); // Calls the constructor
        favLunchPlace.print();
        favLunchPlace.setName("Central Deli");
        favLunchPlace.setRating(4);
        favLunchPlace.print();
    }
}

class Restaurant_f {
    private String name;
    private int rating;

    public Restaurant_f() {  // Constructor with no arguments
        name = "NoName";    // Default name: NoName indicates name was not set
        rating = -1;        // Default rating: -1 indicates rating was not set
    }

    public void setName(String restaurantName) {
        name = restaurantName;
    }

    public void setRating(int userRating) {
        rating = userRating;
    }

    public void print() {
        System.out.println(name + " -- " + rating);
    }
}
```


Further details can be found at:  
    - [Constructors from Oracle's Java tutorials](https://docs.oracle.com/javase/tutorial/java/javaOO/constructors.html)  
    - [Initializing fields from Oracle's Java tutorials](https://docs.oracle.com/javase/tutorial/java/javaOO/initial.html)  

# Choosing classes to create
## Decomposing into classes
Creating a program may start by a programmer deciding what "things" exist, and what each thing contains and does.

Below, the programmer wants to maintain a soccer team. The programmer realizes the team will have people, so decides to sketch a Person class. Each Person class will have private (shown by "-") data like name and age, and public (shown by "+") methods like get/set name, get/set age, and print. The programmer then sketches a Team class, which uses Person objects.

<img width="619" alt="sketch_class_soccer" src="https://user-images.githubusercontent.com/11669149/214720619-566f685f-1efd-4b1b-9aa4-95681d99de1b.png">


### Example: SoccerTeam and TeamPerson classes

``` java
\\ TeamPerson.java
public class TeamPerson {
    private String fullName;
    private int ageYears;

    public void setFullName(String firstAndLastName) {
        fullName = firstAndLastName;
    }

    public void setAgeYears(int ageInYears) {
        ageYears = ageInYears;
    }

    public String getFullName() {
        return fullName;
    }

    public int getAgeYears() {
        return ageYears;
    }

    public void print() {
        System.out.println("Full name: " + fullName);
        System.out.println("Age (years): " + ageYears);
    }
}

```


``` java
\\ SoccerTeam.java
public class SoccerTeam {
    private TeamPerson headCoach;
    private TeamPerson assistantCoach;
    // Players omitted for brevity

    public void setHeadCoach(TeamPerson teamPerson) {
        headCoach = teamPerson;
    }

    public void setAssistantCoach(TeamPerson teamPerson) {
        assistantCoach = teamPerson;
    }

    public TeamPerson getHeadCoach() {
        return headCoach;
    }

    public TeamPerson getAssistantCoach() {
        return assistantCoach;
    }

    public void print() {
        System.out.println("HEAD COACH: ");
        headCoach.print();
        System.out.println();

        System.out.println("ASSISTANT COACH: ");
        assistantCoach.print();
        System.out.println();
    }
}
```


``` java
// main method
public class SoccerTeamPrinter {
    public static void main(String[] args) {
        SoccerTeam teamCalifornia = new SoccerTeam();
        TeamPerson headCoach = new TeamPerson();
        TeamPerson asstCoach = new TeamPerson();

        headCoach.setFullName("Mark Miwerds");
        headCoach.setAgeYears(42);
        teamCalifornia.setHeadCoach(headCoach);

        asstCoach.setFullName("Stanley Lee");
        asstCoach.setAgeYears(30);
        teamCalifornia.setAssistantCoach(asstCoach);

        teamCalifornia.print();
    }
}
```


# Defining main() in a programmer-defined class
The main() method can be defined within a programmer-defined class and create objects of that class type. The BasicCar class defined in the example below represents a car that keeps track of the number of miles driven. BasicCar has a field that maintains the miles driven and three methods that set, retrieve, and modify the object's field.

main() is a static method that is independent of class objects. main() can access other static methods and static fields of the class, but cannot directly access non-static methods or fields, like BasicCar's checkOdometer() method. So, a programmer must create objects within main() to call non-static methods on those objects. Ex: BasicCar's main() creates two objects of type BasicCar and performs operations on those objects.

Non-static fields and methods are also called instance variables and instance methods.

### Example: Class definition with main() method.

``` java
public class BasicCar {

    // Total miles driven by the car
    private int milesDriven;

    // Constructor assigns initial values to instance variables
    public BasicCar() {
        milesDriven = 0;
    }

    // Drive the requested miles
    public void drive(int tripMiles) {
        milesDriven = milesDriven + tripMiles;
    }

    // Return total number of miles driven
    public int checkOdometer() {
        return milesDriven;
    }

    // Main() creates objects of type BasicCar and
    // calls methods to operate on the objects
    public static void main(String [] args) {
        BasicCar redCorvette = new BasicCar();
        BasicCar fordMustang = new BasicCar();

        redCorvette.drive(100);
        fordMustang.drive(75);
        fordMustang.drive(300);
        fordMustang.drive(50);
    }
}
```


# Unit testing (classes)
## Testbenches
Like a chef who tastes food before serving, a class creator should test a class before allowing use. A testbench is a program whose job is to thoroughly test another program (or portion) via a series of input/output checks known as test cases. Unit testing means to create and run a testbench for a specific item (or "unit") like a method or a class.

### Example: Unit testing of a class

``` java
public class StatsInfoTest {
    public static void main(String[] args) {
        StatsInfo testData = new StatsInfo();

        // Typical testbench tests more thoroughly

        System.out.println("Beginning tests.");

        // Check set/get num1
        testData.setNum1(100);
        if (testData.getNum1() != 100) {
            System.out.println("   FAILED set/get num1");
        }

        // Check set/get num2
        testData.setNum2(50);
        if (testData.getNum2() != 50) {
            System.out.println("   FAILED set/get num2");
        }

        // Check getAverage()
        testData.setNum1(10);
        testData.setNum2(20);
        if (testData.getAverage() != 15) {
            System.out.println("   FAILED GetAverage for 10, 20");
        }

        testData.setNum1(-10);
        testData.setNum2(0);
        if (testData.getAverage() != -5) {
            System.out.println("   FAILED GetAverage for -10, 0");
        }

        System.out.println("Tests complete.");
    }
}

class StatsInfo {

    // Note: This class intentionally has errors

    private int num1;
    private int num2;

    public void setNum1(int numVal) {
        num1 = numVal;
    }

    public void setNum2(int numVal) {
        num2 = numVal;
    }

    public int getNum1() {
        return num1;
    }

    public int getNum2() {
        return num1;
    }

    public int getAverage() {
        return num1 + num2 / 2;
    }
}
```


Features of a good testbench include:
- Automatic checks. Ex: Values are compared, as in testData.GetNum1() != 100. For conciseness, only fails are printed.
- Independent test cases. Ex: The test case for GetAverage() assigns new values, vs. relying on earlier values.
- 100% code coverage: Every line of code is executed. A good testbench would have more test cases than below.
- Includes not just typical values but also border cases: Unusual or extreme test case values like 0, negative numbers, or large numbers.

# Constructors overloading
Programmers often want to provide different initialization values when creating a new object. A class creator can overload a constructor by defining multiple constructors differing in parameter types. When an object is created with the new operator, arguments can be passed to the constructor. The constructor with matching parameters will be called.

<img width="664" alt="Overload_constructors" src="https://user-images.githubusercontent.com/11669149/214720691-039dc6eb-ba35-48d6-ac2d-347c2e283613.png">

Creating a new object with no constructor arguments calls the default constructor. In this case, the object gets initialized with NoName and -1.
Passing a String and int argument to the constructor causes the constructor with matching parameters to be called instead. The object gets initialized with those argument values.

> If a programmer defines any constructor, the compiler does not implicitly define a default constructor, so good practice is for the programmer to also explicitly define a default constructor so that an object creation like new MyClass() remains supported.

<img width="903" alt="default_constructor" src="https://user-images.githubusercontent.com/11669149/214720732-2ab981b0-2654-4554-a5ad-0f2ddc00b8f8.png">

# Objects and references
## References
A reference is a variable type that refers to an object. A reference may be thought of as storing the memory address of an object. Variables of a class data type (and array types, discussed elsewhere) are reference variables.

<img width="606" alt="Reference_var" src="https://user-images.githubusercontent.com/11669149/214720778-697ba768-10c9-4412-8aee-03c1e5425695.png">

A statement like TimeHrMin travelTime; declares a reference to an object of type TimeHrMin, while String firstName; declares a reference to an object of type String. The reference variables do not store data for those class types. Instead, the programmer must assign each reference to an object, which can be created using the new operator.

The statement TimeHrMin travelTime; declares a reference variable with an unknown value. A common error is to attempt to use a reference variable that does not yet refer to a valid object.

The new operator allocates memory for an object, then returns a reference to the object's location in memory. Thus, travelTime = new TimeHrMin(); sets travelTime to refer to a new TimeHrMin object in memory. travelTime now refers to a valid object and the programmer may use travelTime to access the object's methods. The reference variable declaration and object creation may be combined into a single statement: TimeHrMin travelTime = new TimeHrMin();

Java does not provide a direct way to determine the memory location of an object, or to determine the exact address to which a reference variable refers. The "value" of a reference variable is unknown to the programmer. 

# The 'this' implicit parameter
## Implicit parameter
An object's member method is called using the syntax objectReference.method(). The object reference before the method name is known as an implicit parameter of the member method because the compiler converts the call syntax objectReference.method(...) into a method call with the object reference implicitly passed as a parameter. Ex: method(objectReference, ...).

Within a member method, the implicitly-passed object reference is accessible via the keyword this. In particular, a class member can be accessed as this.classMember. The "." is the member access operator.

Using this makes clear that a class member is being accessed and is essential if a field member and parameter have the same identifier. In the example below, this is necessary to differentiate between the field member sideLength and the parameter sideLength.

### Example: Using 'this' to refer to an object's members

``` java
public class ShapeTest {
    public static void main(String[] args) {
        ShapeSquare square1 = new ShapeSquare();

        square1.setSideLength(1.2);
        System.out.println("Square's area: " + square1.getArea());
    }
}

class ShapeSquare {
    // Private fields
    private double sideLength;

    // Public methods
    public void setSideLength(double sideLength) {
        this.sideLength = sideLength;
        // Field member    Parameter
    }

    public double getArea() {
        return sideLength * sideLength; // Both refer to field
    }
}
```


### Using 'this' in class member methods and constructors
The figure below illustrates how member methods work. When an object's member method is called, the object's reference, which can be thought of as the object's memory address, is passed to the method via the implicit "this" parameter. An access in setTime() to this.hours first goes to the object's address, then to the hours field.

<img width="725" alt="class_member_method" src="https://user-images.githubusercontent.com/11669149/214720921-8c79cd99-6597-4113-9e3a-1043191ca7bb.png">

1. travTime is an object of class type ElapsedTime.  
2. When travTime's SetTime() member method is called, travTime's object reference, which can be thought of as the object's memory address, is passed to the method via the implicit 'this' parameter.  
3. The implicitly-passed object reference is accessible within the member method via the keyword 'this'. Ex: this.hours first goes to travTime's memory address, then to the hours data member.  

The "this" keyword can also be used in a constructor to invoke a different (overloaded) constructor. In the default constructor below, this(0, 0); invokes the other constructor to initialize both fields to zero. For this example, a programmer could have just set both fields to zero within the default constructor. However, invoking other constructors is useful when a class' initialization routine is lengthy and avoids rewriting the same code.

Further details can be found at:  
- [Using the 'this' keyword from Oracle's Java tutorials](https://docs.oracle.com/javase/tutorial/java/javaOO/thiskey.html)

# Primitive and reference types
## Wrapper classes

Java variables are one of two types.

- A primitive type variable directly stores the data for that variable type, such as int, double, or char. Ex: int numStudents = 20; declares an int that directly stores the data 20.  
- A reference type variable can refer to an instance of a class, also known as an object.  

Java provides several wrapper classes that are built-in reference types that augment the primitive types. The Integer data type is a built-in class in Java that augments the int primitive type. Ex: Integer maxPlayers = 10; declares an Integer reference variable named maxPlayers that refers to an instance of the Integer class, also known as an Integer object. That Integer object stores the integer value 10.

Many of Java's built-in classes, such as Java's Collection library, only work with objects. For example, a programmer can create an ArrayList containing Integer elements, e.g., ArrayList\<Integer\> frameScores; but not an ArrayList of int elements. Wrapper classes allow the program to create objects that store a single primitive type value, such as an integer or floating-point value. The wrapper classes also provide methods for converting between primitive types (e.g., int to double), between number systems (e.g., decimal to binary), and between a primitive type and a String representation. 
    
| Reference type | Associated primitive type |
| -------------- | --------------------------|
| Character      | char                      |
| Integer        | int                       |
| Double         | double                    |
| Boolean        | boolean                   |
| Long           | long                      |
    
## Memory allocation for wrapper class objects

A programmer may use a wrapper class variable in expressions in the same manner as the primitive type int. An expression may even combine Integers, ints, and integer literals.

A wrapper class object (as well as a String object) is immutable, meaning a programmer cannot change the object via methods or variable assignments after object creation. When the result of an expression is assigned to an Integer reference variable, memory for a new Integer object with the computed value is allocated, and the reference (or address) of this new object is assigned to the reference variable. A new memory allocation occurs every time a new value is assigned to an Integer variable, and the previous memory location to which the variable referred, remains unmodified.

<img width="758" alt="Screen Shot 2023-01-23 at 10 27 40 PM" src="https://user-images.githubusercontent.com/11669149/214225857-bdbc81e7-52db-4cdc-aa4e-f357b7d64eef.png">

1. timeMins is a primitive type variable. A primitive type variable directly stores the data for that variable type.
2. Assigning the Integer variable timeHrs with the literal 0 assigns timeHrs with a reference to an Integer object with value 0. Note that Java maintains a cache of Integer objects for literal values -128 to 127 (inclusive).
3. timeMins is a primitive type and directly stores the value 400.
4. A new Integer object is created and assigned with 400 / 60, or 6, and timeHrs is updated to refer to that new Integer object.

### Example: Program using the Double class to calculate flight and driving times
    
``` java
import java.util.Scanner;

public class FlyDrive {
    public static void main(String [] args) {
        Scanner scnr = new Scanner(System.in);
        Double distMiles;
        Double hoursFly;
        Double hoursDrive;

        System.out.print("Enter a distance in miles: ");
        distMiles = scnr.nextDouble();

        hoursFly = distMiles / 500.0;
        hoursDrive = distMiles / 60.0;

        System.out.println(distMiles + " miles would take:");
        System.out.println(hoursFly + " hours to fly");
        System.out.println(hoursDrive + " hours to drive");
    }
}
```


**Note**
> When using a literal for initialization, the programmer must ensure that the literal's value falls within the appropriate numeric range, e.g., -2,147,483,648 to 2,147,483,647 for an integer. The wrapper classes (except for Character and Boolean) declare the MAX_VALUE and MIN_VALUE fields, which are static fields initialized with the maximum and minimum values a type may represent, respectively. A programmer may access these fields to check the supported numeric range by typing the wrapper class' name followed by a dot and the field name, as in Integer.MIN_VALUE, which returns -2,147,483,648.

## Comparing wrapper class objects
For reference variables of wrapper classes (e.g., Integer, Double, Boolean), a common error is to use the equality operators == and != when comparing values, which does not work as expected. Using the equality operators on any two reference variables evaluates to either true or false depending on each operand's referenced object. For example, given two Integers num1 and num2, the expression num1 == num2 compares if both num1 and num2 reference the same Integer object, but does not compare the Integers' contents. Because those references will (usually) be different, num1 == num2 will evaluate to false. This is not a syntax error, but clearly a logic error.

Although a programmer should never compare two reference variables of wrapper classes using the equality operators, a programmer may use the equality operators when comparing a wrapper class object with a primitive variable or a literal constant. The relational operators <, <=, >, and >= may be used to compare wrapper class objects. However, note that relational operators are not typically valid for other reference types. The following table summarizes allowable comparisons.

### Comparing wrapper class objects using relational operators
<img width="823" alt="Screen Shot 2023-01-23 at 10 52 11 PM" src="https://user-images.githubusercontent.com/11669149/214229448-70a349cd-928e-4e94-8b34-e90c62f670d4.png">

Reference variables of wrapper classes can also be compared using the equals() and compareTo() methods. These method descriptions are presented for the Integer class, but apply equally well to the other wrapper classes. Although the use of comparison methods is slightly cumbersome in comparison to relational operators, these comparison methods may be preferred by programmers who do not wish to memorize exactly which comparison operators work as expected.

### equals() and compareTo() methods for wrapper class types
<img width="963" alt="Screen Shot 2023-01-23 at 10 52 57 PM" src="https://user-images.githubusercontent.com/11669149/214229574-987edfbd-83bc-4ffc-85e3-81e6de6714a0.png">

# Wrapper class conversions
## Autoboxing and unboxing

Java allows statements to combine primitive and wrapper class variables by automatically converting between primitive types and wrapper classes. **Autoboxing** is the automatic conversion of primitive types to the corresponding wrapper classes. **Unboxing** is the automatic conversion of wrapper class objects to the corresponding primitive types.

### Common autoboxing scenarios
<img width="959" alt="Screen Shot 2023-01-24 at 8 13 23 AM" src="https://user-images.githubusercontent.com/11669149/214346849-8c9b8bcc-c120-41f4-a2ac-5416a7b283ce.png">

### Common unboxing scenarios
<img width="966" alt="Screen Shot 2023-01-24 at 8 15 17 AM" src="https://user-images.githubusercontent.com/11669149/214347223-97ab534f-eaca-4854-aa68-3437956d94cc.png">

### Converting to primitive types
The Integer, Double, and Long wrapper classes provide methods for converting objects to primitive types.

<img width="836" alt="Screen Shot 2023-01-24 at 8 19 02 AM" src="https://user-images.githubusercontent.com/11669149/214348096-c3c2ae9d-a08f-43b8-a8f9-93f1ecb4ca26.png">

The Character and Boolean classes support the charValue() and booleanValue() methods, respectively, which perform similar functions.

### Converting to and from Strings
Wrapper classes feature methods that are useful for converting to and from Strings. Several of these methods are static methods, meaning they can be called by a program without creating an object. To call a static method, the name of the class and a '.' must precede the static method name, as in  Integer.toString(16);.

<img width="957" alt="Screen Shot 2023-01-24 at 2 02 00 PM" src="https://user-images.githubusercontent.com/11669149/214430859-f1455687-7cfe-4b7a-afc9-7309399fcbb0.png">
<img width="955" alt="Screen Shot 2023-01-24 at 2 02 23 PM" src="https://user-images.githubusercontent.com/11669149/214430921-f8143d7e-cfc9-4e67-a3eb-2da399a461e8.png">

### Example: A program to convert a decimal number to binary

    
``` java
import java.util.Scanner;

public class DecimalToBinary {
   public static void main(String [] args) {
      Scanner scnr = new Scanner(System.in);
      int decimalInput;
      String binaryOutput;
      
      System.out.print("Enter a decimal number: ");
      decimalInput = scnr.nextInt();
      
      binaryOutput = Integer.toBinaryString(decimalInput);
      
      System.out.println("The binary representation of " + decimalInput +
                         " is " + binaryOutput);
   }
}

```


# ArraysList
## Introduction

Sometimes a programmer wishes to maintain a list of items, like a grocery list, or a course roster. An ArrayList is an ordered list of reference type items that comes with Java. Each item in an ArrayList is known as an element. The statement import java.util.ArrayList; enables use of an ArrayList.

The declaration ArrayList\<Integer\> vals = new ArrayList\<Integer\>() creates reference variable vals that refers to a new ArrayList object consisting of Integer objects. The ArrayList list size can grow to contain the desired elements. ArrayList does not support primitive types like int, but rather reference types like Integer. A common error among beginners is to declare an ArrayList of a primitive type like int, as in ArrayList\<int\> myVals, yielding a compilation error: "unexpected type, found : int, required: reference."

<img width="665" alt="Screen Shot 2023-01-24 at 9 31 04 PM" src="https://user-images.githubusercontent.com/11669149/214487464-b4e41fcf-628b-4fea-85d8-a80a1949ce37.png">

1. valsList is a reference variable that refers to an ArrayList object consisting of Integer objects.   
2. Java automatically creates an Integer object from the integer literal passed to the add() method. The add() method then adds the Integer object to the end of the ArrayList.   
3. The get() method returns the element at the specified list location.   
4. The set() method replaces the element at the specified list position with the new Integer object. Again, Java automatically converts the integer literal 119 to an Integer object with that value.   

**Common ArrayList methods**

<img width="957" alt="Screen Shot 2023-01-24 at 9 34 07 PM" src="https://user-images.githubusercontent.com/11669149/214487828-5d3c855a-2fab-4e4b-b04d-e982720c2af7.png">

## Accessing ArrayList elements
The ArrayList's get() method returns the element at the specified list location, and can be used to lookup the Nth item in a list. The program below allows a user to print the name of the Nth most popular operating system. The program accesses the Nth most popular operating system using operatingSystems.get(nthOS - 1);. Note that the index is nthOS - 1 rather than just nthOS because an ArrayList's indices start at 0, so the 1st operating system is at index 0, the 2nd at index 1, etc.

An ArrayList's index must be an integer type. The index cannot be a floating-point type, even if the value is 0.0, 1.0, etc.

### Example: ArrayList's ith element can be directly accessed using .get(i)
    
``` java
import java.util.ArrayList;
import java.util.Scanner;

public class ArrayListAverage {
    public static void main(String[] args) {
        final int NUM_ELEMENTS = 8;
        Scanner scnr = new Scanner(System.in);
        ArrayList<Double> userNums = new ArrayList<Double>(); // User numbers
        Double sumVal;
        Double averageVal;
        int i;

        // Get user numbers and add to userNums
        System.out.println("Enter " + NUM_ELEMENTS + " numbers...");
        for (i = 0; i < NUM_ELEMENTS; ++i) {
            System.out.print("Number " + (i + 1) + ": ");
            userNums.add(scnr.nextDouble());
        }

        // Determine average value
        sumVal = 0.0;
        for (i = 0; i < userNums.size(); ++i) {
            sumVal = sumVal + userNums.get(i); // Calculate sum of all numbers
        }
        averageVal = sumVal / userNums.size(); // Calculate average

        System.out.println("Average: " + averageVal);
    }
}

```


## Iterating through ArrayLists
The program below allows a user to enter 8 numbers, then prints the average of those 8 numbers. The first loop uses the add() method to add each user-specified number to the ArrayList userNums. After adding the numbers to userNums, the size() method can be used to determine the number of elements in userNums. Thus, size() is used in the second for loop to calculate the sum, and in the statement that computes the average.

With an ArrayList and loops, the program could easily be changed to support say 100 numbers; the code would be the same, and only the value of NUM_ELEMENTS would be changed to 100.

### Example - ArrayLists with loops
    
``` java
import java.util.ArrayList;
import java.util.Scanner;

public class ArrayListAverage {
    public static void main(String[] args) {
        final int NUM_ELEMENTS = 8;
        Scanner scnr = new Scanner(System.in);
        ArrayList<Double> userNums = new ArrayList<Double>(); // User numbers
        Double sumVal;
        Double averageVal;
        int i;

        // Get user numbers and add to userNums
        System.out.println("Enter " + NUM_ELEMENTS + " numbers...");
        for (i = 0; i < NUM_ELEMENTS; ++i) {
            System.out.print("Number " + (i + 1) + ": ");
            userNums.add(scnr.nextDouble());
        }

        // Determine average value
        sumVal = 0.0;
        for (i = 0; i < userNums.size(); ++i) {
            sumVal = sumVal + userNums.get(i); // Calculate sum of all numbers
        }
        averageVal = sumVal / userNums.size(); // Calculate average

        System.out.println("Average: " + averageVal);
    }
}

```


**Note**
> An ArrayList is one of several Collections supported by Java for keeping groups of items. Other collections include LinkedList, Set, Queue, Map, and many more. A programmer selects the collection whose features best suit the desired task. For example, an ArrayList can efficiently access elements at any valid index but inserts are expensive, whereas a LinkedList supports efficient inserts but access requires iterating through elements. So a program that will do many accesses and few inserts might use an ArrayList.
    
# Classes and ArrayLists
## ArrayList of objects: A reviews program
A programmer commonly uses classes and ArrayLists together. The program below creates a Review class (reviews might be for a restaurant, movie, etc.), then manages an ArrayList of Review objects.

# Java documentation for classes
The Javadoc tool parses source code along with specially formatted comments to generate documentation. The documentation generated by Javadoc is known as an API for classes and class members. API is short for application programming interface.

The specially formatted comments for Javadoc are called Doc comments, which are multi-line comments consisting of all text enclosed between the /** and \*/ characters. Importantly, Doc comments are distinguished by the opening characters /\**, which include two asterisks. The following illustrates.

### Example - Using Javadoc comments to document the ElapsedTime and TimeDifference classes
    
``` java
//ElapsedTime.java
/**
 * A class representing an elapsed time measurement 
 * in hours and minutes. 
 * @author Mary Adams
 * @version 1.0
 */
public class ElapsedTime {
   /**
    * The hours portion of the time
    */
   private int hours;
   
   /**
    * The minutes portion of the time
    */
   private int minutes;

   /**
    * Constructor initializing hours to timeHours and 
    * minutes to timeMins. 
    * @param timeHours hours portion of time
    * @param timeMins minutes portion of time
    */   
   public ElapsedTime(int timeHours, int timeMins) {
      hours   = timeHours;
      minutes = timeMins;
   }
   
   /**
    * Default constructor initializing all fields to 0. 
    */   
   public ElapsedTime() {
      hours = 0;
      minutes = 0;
   }
   
   /**
    * Prints the time represented by an ElapsedTime 
    * object in hours and minutes.
    */
   public void printTime() {
      System.out.print(hours + " hour(s) " + minutes + " minute(s)");
   }
   
   /**
    * Sets the time to timeHours:timeMins.
    * @param timeHours hours portion of time
    * @param timeMins minutes portion of time
   */
   public void setTime(int timeHours, int timeMins) {
      hours = timeHours;
      minutes = timeMins;
   }

   /**
    * Returns the total time in minutes.
    * @return an int value representing the elapsed time in minutes.
    */
   public int getTimeMinutes() {
      return ((hours * 60) + minutes);
   }
}

```

    
``` java
//TimeDifference.java
    import java.util.Scanner;

/**
 * This program calculates the difference between two 
 * user-entered times. This class contains the 
 * program's main() method and is not meant to be instantiated.
 * @author Mary Adams
 * @version 1.0
 */
public class TimeDifference {
   /**
    * Asks for two times, creating an ElapsedTime object for each, 
    * and uses ElapsedTime's getTimeMinutes() method to properly 
    * calculate the difference between both times.
    * @param args command-line arguments
    * @see ElapsedTime#getTimeMinutes()
    */
   public static void main(String[] args) {
      Scanner scnr = new Scanner(System.in);
      int timeDiff;     // Stores time difference
      int userHours;
      int userMins;
      ElapsedTime startTime = new ElapsedTime(); // Starting time
      ElapsedTime endTime = new ElapsedTime(); // Ending time

      // Read starting time in hours and minutes
      System.out.print("Enter starting time (hrs mins): ");
      userHours = scnr.nextInt();
      userMins = scnr.nextInt();
      startTime.setTime(userHours, userMins);
              
      // Read ending time in hours and minutes
      System.out.print("Enter ending time (hrs mins): ");
      userHours = scnr.nextInt();
      userMins = scnr.nextInt();
      endTime.setTime(userHours, userMins);

      // Calculate time difference by converting both times to minutes
      timeDiff = endTime.getTimeMinutes() - startTime.getTimeMinutes(); 
      
      System.out.println("Time difference is " + timeDiff + " minutes");
   }
}
```


A Doc comment associated with a class is written immediately before the class definition. The main description typically describes the class' purpose. The tag section of the Doc comment may include block tags such as @author and @version to specify the class' author and version number respectively. For the classes above, the Doc comments specify "Mary Adams" as the author of the first version of both classes.

Each class also contains Doc comments describing member methods. Programmers can use the @param and @return block tags to specify a method parameter and method return value respectively.

Doc comments may be used to describe a class's fields as well. Unlike classes or methods, a field's Doc comment is not typically associated with specific block tags. However, generic block tags, such as @see and others described by the Javadoc specification, may be used to provide more information. For example, the main() method's Doc comment uses the @see block tag to refer to ElapsedTime's getTimeMinutes() method, as in @see ElapsedTime#getTimeMinutes(). Note that when referring to a method, the @see block tag requires the programmer to precede the method name with the class name followed by the # character. The following table summarizes commonly used block tags.

<img width="721" alt="Screen Shot 2023-01-25 at 12 15 03 AM" src="https://user-images.githubusercontent.com/11669149/214512141-946bd5aa-460f-4b0c-82d5-61b788c7dd6f.png">

Private class members are not included by default in the API documentation generated by the Javadoc tool. API documentation is meant to provide a summary of all functionality available to external applications interfacing with the described classes. Thus, private class members, which cannot be accessed by other classes, are not typically included in the documentation. The Java Scanner class specification, for example, only describes the public class members available to programmers using the class.

Similarly, the resulting API documentation for the above classes need only include information that enables their use by other programmers. However, if a programmer needs to document a class's complete structure, the Javadoc tool can be executed with the -private flag, as in javadoc -private -d destination class1.java class2.java, to enable the documentation of private class members.


# Parameters of reference types
## Methods with reference variables as parameters

A reference variable is a variable that points to, or refers to, an object or array. Internally, a reference variable stores a reference, or the memory location, of the object to which it refers. A programmer can only access the data or functionality provided by objects through the use of reference variables. Because reference variables store object locations and not the object data itself, passing a reference variable as a method argument assigns the argument's stored reference to the corresponding method parameter. Similarly, returning a reference variable returns an object reference.

<img width="811" alt="Screen Shot 2023-01-25 at 12 19 25 AM" src="https://user-images.githubusercontent.com/11669149/214512934-b77306f1-4636-4a37-a433-b021c5bf9ad8.png">

## Methods with wrapper class parameters
Instances of wrapper classes, such as Integer and Double, and the String class are defined as immutable, meaning that a programmer cannot modify the object's contents after initialization; new objects must be created instead. The statement Integer travelTime = 10; initializes the variable travelTime with a reference to a new Integer object. Assigning the variable travelTime later with another value, such as travelTime = 11;, creates a completely new object and assigns travelTime to refer to the new object's reference. Note that for convenience, a programmer can assign a literal to reference variables of type String, Integer, Double, or other wrapper classes, and the Java compiler will automatically convert the assigned literal to a new object of the correct type.

# Static fields and methods
## Static fields
The keyword **static** indicates a variable is allocated in memory only once during a program's execution. Static variables reside in the program's static memory region and have a global scope. Thus, static variables can be accessed from anywhere in a program.

In a class, a **static** field is a field of the class instead of a field of each class object. Thus, static fields are independent of any class object, and can be accessed without creating a class object. Static fields are declared and initialized in the class definition. Within a class method, a static field is accessed using the field name. A public static field can be accessed outside the class using dot notation: ClassName.fieldName.

> Static fields are also called class variables, and non-static fields are also called instance variables.

<img width="698" alt="Screen Shot 2023-01-25 at 7 37 42 AM" src="https://user-images.githubusercontent.com/11669149/214606881-90ed6250-e618-4941-8421-c759bde79b04.png">

1. The Store class' static field nextId is declared and initialized in the Store class definition. Only one instance of the field nextId will exist in memory.   
2. When a Store object is created, memory is allocated for the object's name, type, and id fields, but not the static field nextId.   
3. The constructor assigns an object's id with nextId, and then increments nextId. Each time an object is created, nextId is incremented. Thus, each object will have a unique id.   
4. Any class method can access or mutate a static field. Because nextId is public, nextId can also be accessed outside the class using the member access operator (.)

## Static member methods
A static member method is a class method that is independent of class objects. Static member methods are typically used to access and mutate private static fields from outside the class. Since static methods are independent of class objects, the this parameter is not passed to a static member method. So, a static member method can only access a class' static fields.

### Example - Static member method used to access a private static field

    
``` java
public class Store {   
   // Declare and initialize private static field
   private static int nextId = 101;   

   // Define private fields 
   private String name;
   private String type;
   private int id;

   public Store(String storeName, String storeType) {
      name = storeName;
      type = storeType;
      id = nextId;

      ++nextId;   // Increment each time a Store object is created
   }

   public int getId() {
      return id;
   }
   
   public static int getNextId() {
      return nextId;
   }
}


```

    
``` java
public class NewStores {
   public static void main(String[] args) {
      Store store1 = new Store("Macy's", "Department");
      Store store2 = new Store("Albertsons", "Grocery");
      Store store3 = new Store("Ace", "Hardware");
    
      System.out.println("Store 1's ID: " + store1.getId());
      System.out.println("Store 2's ID: " + store2.getId());
      System.out.println("Store 3's ID: " + store3.getId());
      System.out.println("Next ID: " + Store.getNextId());
   }
}
```



# Using packages
## Built-in Java packages
Java provides a variety of built-in classes, such as Scanner, ArrayList, File, and many others, that programmers can use to write programs. Given the large number of built-in classes, Java organizes related classes into groupings called packages.

A package is a grouping of related types, classes, interfaces, and subpackage. The types, classes, and interfaces in a package are called package members. The following table lists several built-in Java packages and sample package members.

<img width="960" alt="Screen Shot 2023-01-25 at 7 46 50 AM" src="https://user-images.githubusercontent.com/11669149/214608820-51d8fd6a-5b85-4b50-8c67-55cb405d9ead.png">

## Using package members in a program
A programmer can use a package member using one of the following methods.

Using a package member's fully qualified name: A class' fully qualified name is the concatenation of the package name with the class name using a period. Ex: java.util.Scanner is the fully qualified name for the Scanner class in the java.util package.

- Using an import statement to import the package member: An import statement imports a package member into a file to enable use of the package member directly, without having to use the package member's fully qualified name. Ex: import java.util.Scanner; imports the Scanner class into a file and allows a programmer to use Scanner instead of java.util.Scanner.

- Using an import statement to import every member in a package: A programmer import all members of a package by using the wildcard character \* instead of a package member name. Ex: import java.util.\*; imports all classes in the java.util package and allows a programmer use package members such as Scanner and ArrayList directly.

<img width="709" alt="Screen Shot 2023-01-25 at 7 51 19 AM" src="https://user-images.githubusercontent.com/11669149/214610307-7d1c8fdb-a71d-4b54-852f-baf61dfa97cf.png">

1. A programmer can access a package member, such as Scanner, using the fully qualified name.   
2. The import statement allows a programmer to use a package member, such as ArrayList, directly.   
3. A programmer can also import all package members in a package by using a wildcard import. Importing java.io.* imports all package members in java.io, including FileInputStream

