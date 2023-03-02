[TOC]

# Inheritance

Inheritance is one of the core concepts of object-oriented programming (OOP) languages. It is a mechanism where you can to derive a class from another class for a hierarchy of classes that share a set of attributes and methods.

## Derived classes

### Concepts

- The main idea is to speed up the code. Reuse the base code, modify, and use it.
- Inheritance works like building blocks.
- One class is similar to another class but with some additions or variations.

![inheritance_i1](https://raw.githubusercontent.com/d-khan/java/main/images/inheritance-i1.png)

### Inheritance

- A **derived class** (or **subclass**) is a class that is derived from another class, called a **base class** (or **superclass**).
- The derived class is said to inherit the properties of the base class, a concept called **inheritance**.
- A derived class is declared by placing the keyword **extends** after the derived class name, followed by the base class name. 

#### Example code - base & derived classes

__GenericItem.java - base class__

```{java .numberLines}
public class GenericItem {
   private String itemName;
   private int itemQuantity;

   public void setName(String newName) {
      itemName = newName;
   }

   public void setQuantity(int newQty) {
      itemQuantity = newQty;
   }

   public void printItem() {
      System.out.println(itemName + " " + itemQuantity);
   }
}

```

__ProduceItem.java - derived class__

```{java .numberLines}
public class ProduceItem extends GenericItem { 
   private String expirationDate;

   public void setExpiration(String newDate) {
      expirationDate = newDate;
   }

   public String getExpiration() {
      return expirationDate;
   }  
}
```

__Main ClassDerivationEx.java - main__

```{java .numberLines}
public class ClassDerivationEx {
   public static void main(String[] args) {
      GenericItem miscItem = new GenericItem();
      ProduceItem perishItem = new ProduceItem();

      miscItem.setName("Crunchy Cereal");
      miscItem.setQuantity(9);
      miscItem.printItem();

      perishItem.setName("Apples");
      perishItem.setQuantity(40);
      perishItem.setExpiration("Dec 5, 2019");
      perishItem.printItem();

      System.out.println("  (Expires: "
         + perishItem.getExpiration() + ")");
   }
}
```

### Inheritance scenarios

- A derived class can serve as a base class for another class.
- A class can serve as a base class for multiple derived classes.
- A class can only be derived from __one base class directly___.

![inheritance_i1](https://raw.githubusercontent.com/d-khan/java/main/images/inheritance-i2.png)

```public class TextbookItem extends BookItem```

```public class AudiobookItem extends BookItem```

```public class BookItem extends GenericItem```

```public class GenericItem```

The other left half works similarly, as shown in the example above.

#### Example code - base & multiple derived classes

__Business.java - base class__

```{java .numberLines}
public class Business {
   private String name;
   private String address;
   
   public void setName(String busName) { 
      name = busName; 
   }
   
   public void setAddress(String busAddress) {
      address = busAddress; 
   }
   
   public String getDescription() {
      return name + " -- " + address;
   }
}
```

__Business.java - derived class__

```{java .numberLines}
public class Restaurant extends Business {
   private int rating;
   
   public void setRating(int userRating) {
      rating = userRating;
   }
   
   public int getRating() {
      return rating;
   }
}
```

__InheritanceExample.java - main__

```{java .numberLines}
public class InheritanceExample {
   public static void main(String[] args) {
      Business someBusiness = new Business();
      Restaurant favoritePlace = new Restaurant();

      someBusiness.setName("ACME");
      someBusiness.setAddress("4 Main St");

      favoritePlace.setName("Friends Cafe");
      favoritePlace.setAddress("500 W 2nd Ave");
      favoritePlace.setRating(5);

      System.out.println(someBusiness.getDescription());
      System.out.println(favoritePlace.getDescription());
      System.out.println("  Rating: " + favoritePlace.getRating());
   }
}
```

##  Access by members of derived classes

### Member access

- Member methods of a derived class cannot access private members of the base class.
- Private is private. It defeats the purpose of a private variable if the private variable is accessible outside of the class.

![inheritance_i1](https://raw.githubusercontent.com/d-khan/java/main/images/inheritance-i3.png)

### Protected member access

-  Provides access to derived classes and all classes in the same **package** but not by anyone else.

![inheritance_i1](https://raw.githubusercontent.com/d-khan/java/main/images/inheritance-i4.png)

![inheritance_i1](https://raw.githubusercontent.com/d-khan/java/main/images/inheritance-i5.png)

Access specifiers for class members

| Specifier    | Description                                                  |
| ------------ | ------------------------------------------------------------ |
| private      | Accessible by self                                           |
| protected    | Accessible by self, derived classes, and other classes in the same package |
| public       | Accessible by self, derived classes, and everyone else       |
| no specifier | Accessible by self and other classes in the same package     |

### Class definitions

Separately, the keyword "public" in a class definition like public class DerivedClass {...} specifies a class's visibility in other classes in the program:

- *public* : A class can be used by every class in the program regardless of the package in which either is defined.

- no specifier* : A class can be used only in other classes within the same package, known as **package- private**.

## Overriding member methods

### Overriding

- When a derived class defines a member method that has the same name and parameters as a base class's method, the member method is said to **override** the base class's method.

- The **@Override** annotation is placed above a method that overrides a base class method so the compiler verifies that an identical base class method exists.

- An **annotation** is an optional command beginning with the "@" symbol that can provide the compiler with information that helps the compiler detect errors better.

#### Example code - overriding member method

__Business.java - base class__

```{java .numberLines}
public class Business {
    protected String name;
    protected String address;
    public void setName(String busName) {
        name = busName;
		}
    public void setAddress(String busAddress) {
        address = busAddress;
		}
    public String getDescription() {
        return name + " -- " + address;
		} 
}
//Same method as in Restaurant class
```

__Restaurant.java - derived class__

```{java .numberLines}
public class Restaurant extends Business {
    private int rating;
    public void setRating(int userRating) {
        rating = userRating;
		}
    public int getRating() {
        return rating;
		}
@Override
    public String getDescription() {
        return name + " -- " + address + " 96422";
		} 
}
```
__OverridingExample.java - main__

```{java .numberLines}
public class InheritanceExample {
    public static void main(String[] args) {
				Business someBusiness = new Business();
        Restaurant favoritePlace = new Restaurant();
 
      	someBusiness.setName("ACME");
        someBusiness.setAddress("4 Main St");
        
      	favoritePlace.setName("Friends Cafe");
        favoritePlace.setAddress("500 W 2nd Ave");
        favoritePlace.setRating(5);
        
      	System.out.println(someBusiness.getDescription());
        System.out.println(favoritePlace.getDescription());
        System.out.println("  Rating: " + favoritePlace.getRating());
    }
}
```

> **Overriding vs. Overloading**
>
> Overriding differs from overloading. In overloading, methods with the same name must have different parameter types, number of parameters, or return values. In overriding, a derived class member method must have the same parameter types, number of parameters, and return value as the base class member method with the same name. Overloading is performed if derived and base member methods have different parameter types; the member method of the derived class does not hide the member method of the base class.

### Calling a base class method
An overriding method can call the overridden method by using the super keyword ```super.getDescription()``` . The __super__ keyword is a reference variable used to call the parent class's methods or constructors.

__Restaurant.java - base class__
```{java .numberLines}
public class Restaurant extends Business {
    private int rating;
    public void setRating(int userRating) {
        rating = userRating;
		}
    public int getRating() {
        return rating;
    }
  	
  	@Override
    public String getDescription() { //same method as in Business class
        return super.getDescription();
        //return name + " -- " + address + " 96422";  //Zip code added
		} 
}
  
```

## The Object class

### Using Object class
- The built-in Object class serves as the base class for all other classes and does not have a base class.
- __It is a hidden base/parent class__
- All classes, including user-defined classes, are derived from Object and implement Object's methods.
- Two common methods defined within the Object class are toString() and equals().
  - The **toString()** method returns a String representation of the Object. By default, toString() returns a String containing the object's class name followed by the object's hash code in hexadecimal form. Ex: java.lang.Object@372f7a8d.
  - The **equals(otherObject)** method compares an Object to otherObject and returns true if both variables reference the same object. Otherwise, equals() returns false. By default, equals() tests the equality of the two Object references, not the equality of the Objects' contents.


> __"Object class" and the generic term "object", are two different terms. Object refers to the instance of any class.__

#### Example code - Behavior of ```toString()``` method

__Business.java__
```{java .numberLines}
public class Business {
    protected String name;
    protected String address;

    void setName(String busName) {
        name = busName;
    }

    void setAddress(String busAddress) {
        address = busAddress;
    }

    String getDescription() {
        return name + " -- " + address;
    }
}
```

__ObjectPrinter - main__
```{java .numberLines}
public class ObjectPrinter {
    public static void main(String[] args) {
        Object myObj = new Object();
        Integer num = new Integer(100);
        Business someBusiness = new Business();

        // Call toString() on each object and print result
        System.out.println("myObj = " + myObj.toString());
        System.out.println("num = " + num.toString());
        System.out.println("someBusiness = " + someBusiness.toString());
    }
}
```

- The Object class is the base class for all other classes.
- Java's Integer class overrides the Object's toString() method, but the user-defined Business class does not.
- Object's toString() returns a string consisting of the object's class name (java.lang.Object), the '@' character, and an unsigned hexadecimal representation of the object's hash code (1148ab5c).
- Integer's toString() method returns the object's associated integer value.
- Business does not override toString() so Object's toString() method is called and outputs the object's class name (Business), the '@' character, and an unsigned hexadecimal representation of the object's hash code (19469ea2).

### Overriding toString() in the base class
- The code below shows a Business class that overrides Object's toString() method and returns a String containing the business name and address.
- The Restaurant class derives from Business but does not override toString().
- When a Restaurant object's toString() method is called, the Business class's toString() method executes.

#### Example code - Base class Business overrides ```toString()```
__Business.java base class__
```{java .numberLines}
public class Business {
    protected String name;
    protected String address;

    void setName(String busName) {
        name = busName;
    }

    void setAddress(String busAddress) {
        address = busAddress;
    }

    @Override
    public String toString() {
        return name + " -- " + address;
    }
}
```

__Restaurant.java sub class__
```{java .numberLines}
public class Restaurant extends Business {
    private int rating;

    public void setRating(int userRating) {
        rating = userRating;
    }

    public int getRating() {
        return rating;
    }
}
```
__ObjectPrinter.java - main__
```{java .numberLines}
public class ObjectPrinter {
    public static void main(String[] args) {
        Business aaaBus = new Business();
        Restaurant tacoRest = new Restaurant();

        aaaBus.setName("AAA Business");
        aaaBus.setAddress("5 Race St");

        tacoRest.setName("Tom's Tacos");
        tacoRest.setAddress("600 Pleasure Ave");
        tacoRest.setRating(5);

        System.out.println(aaaBus.toString());
    }
}
```
> __The ```toString()``` method is called automatically by the compiler when an object is concatenated to a string or when ```print()``` or ```println()``` is called. Ex: ```System.out.println(someObj)``` calls ```someObj.toString()``` automatically.__

#### Practice task
__Objective:__ Overriding ```toString()``` in the derived class
Re-use the business, restaurant, objectprinter classes. Display user rating when ```tacoRest.toString()``` is called.



