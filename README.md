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

![myimage](intro_to_objects/images/class_Restaurant.png)

## Using a class
A programmer can create one or more objects of the same class. Creating an object consists of two steps: declaring a reference variable of the class type, and assigning the variable with an explicitly allocated instance of the class type. A reference variable can refer to an instance of a class. The new operator explicitly allocates an object of the specified class type. Ex: Restaurant favLunchPlace = new Restaurant(); creates a Restaurant object named favLunchPlace.

The "." operator, known as the member access operator, is used to invoke a method on an object. Ex: favLunchPlace.setRating(4) calls the setRating() method on the favLunchPlace object, which sets the object's rating to 4.

![myimage](intro_to_objects/images/class_RestaurantFavorites.png)

### Class example: String
Java's String object is a class that stores a character string in memory, along with variables indicating the length and other things, but a String's user need not know such details. Instead, the String's user just needs to know what public member methods can be used.

# Defining a class
## Private fields
In addition to public member methods, a class definition has private fields: variables that member methods can access but class users cannot. The private access modifier precedes each private field declaration.

![myimage](intro_to_objects/images/private_fields.png)

## Defining a class public member methods
A programmer defining a class first names the class, declares private fields, and defines public member methods. A class' fields and methods are collectively called class members.

The programmer defines the details of each member method, sometimes called the class' implementation. A method definition provides an access modifier, return type, name, parameters, and the method's statements. A member method can access all private fields.

![myimage](intro_to_objects/images/Restaurant.png)
![myimage](intro_to_objects/images/RestaurantFavorites.png)

### Example - Bicycle class
The following class gives an overview of how a class, constructor and methods are defined.
<details><summary>Click to get the code</summary>
<p>

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
</p>
</details>

### Example - PersonInfo class
<details><summary>Click to get the code</summary>
<p>
    
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
</p>
</details>

# Mutators, accessors, and private helpers

## Mutators and accessors
A class' public methods are commonly classified as either mutators or accessors.

A **mutator** method may modify ("mutate") a class' fields.
An **accessor** method accesses fields but may not modify a class' fields.
Commonly, a field has two associated methods: a mutator for setting the value, and an accessor for getting the value, known as a setter and getter method, respectively, and typically with names starting with set or get. Other mutators and accessors may exist that aren't associated with just one field, such as the print() method below.

### Example
<details><summary>Click to get the code</summary>
<p>

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

</p>
</details>

## Private helper methods
A programmer commonly creates private methods, known as private helper methods, to help public methods carry out tasks.

![myimage](intro_to_objects/images/private_fields.png)

# Initialization and constructors

> A good practice is to initialize all variables when declared. This section deals with initializing the fields of a class when a variable of the class type is allocated.

## Field initialization
A programmer can initialize fields in the field declaration. Any object created of that class type will initially have those values.

### Example: A class definition with initialized fields
<details><summary>Click to get the code</summary>
<p>
    
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
</p>
</details>

## Constructors
Java provides a special class member method, known as a constructor, that is called when an object of that class type is created, and which can be used to initialize all fields. The constructor has the same name as the class. The constructor method has no return type, not even void. Ex: public Restaurant() {...} defines a constructor for the Restaurant class.

A programmer specifies the constructor that should be called when creating an object. Ex: Restaurant favLunchPlace = new Restaurant(); creates a new Restaurant object and calls the constructor Restaurant().

If a class does not have a programmer-defined constructor, then the Java compiler implicitly defines a default constructor with no arguments. The Java compiler also initializes all fields to their default values.

### Example: Adding a constructor member method to the Restaurant class.
<details><summary>Click to get the code</summary>
<p>
    
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
</p>
</details>

Further details can be found at:  
    - [Constructors from Oracle's Java tutorials](https://docs.oracle.com/javase/tutorial/java/javaOO/constructors.html)  
    - [Initializing fields from Oracle's Java tutorials](https://docs.oracle.com/javase/tutorial/java/javaOO/initial.html)  

# Choosing classes to create
## Decomposing into classes
Creating a program may start by a programmer deciding what "things" exist, and what each thing contains and does.

Below, the programmer wants to maintain a soccer team. The programmer realizes the team will have people, so decides to sketch a Person class. Each Person class will have private (shown by "-") data like name and age, and public (shown by "+") methods like get/set name, get/set age, and print. The programmer then sketches a Team class, which uses Person objects.

![myimage](intro_to_objects/images/sketch_class_soccer.png)

### Example: SoccerTeam and TeamPerson classes
<details><summary>Click to get the TeamPerson class</summary>
<p>

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
</p>
</details>

<details><summary>Click to get the SoccerTeam class</summary>
<p>

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
</p>
</details>

<details><summary>Click to get the main method</summary>
<p>

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
</p>
</details>

# Defining main() in a programmer-defined class
The main() method can be defined within a programmer-defined class and create objects of that class type. The BasicCar class defined in the example below represents a car that keeps track of the number of miles driven. BasicCar has a field that maintains the miles driven and three methods that set, retrieve, and modify the object's field.

main() is a static method that is independent of class objects. main() can access other static methods and static fields of the class, but cannot directly access non-static methods or fields, like BasicCar's checkOdometer() method. So, a programmer must create objects within main() to call non-static methods on those objects. Ex: BasicCar's main() creates two objects of type BasicCar and performs operations on those objects.

Non-static fields and methods are also called instance variables and instance methods.

### Example: Class definition with main() method.
<details><summary>Click to get the TeamPerson class</summary>
<p>

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
</p>
</details>

