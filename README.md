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
