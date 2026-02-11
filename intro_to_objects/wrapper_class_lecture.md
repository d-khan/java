# Lecture: Java Wrapper Classes --- Are They Really "Just Objects"?

------------------------------------------------------------------------

## Motivation: Why Wrapper Classes Exist

Java has two categories of types:

## 🔹 Primitive Types

`int, double, char, boolean, byte, short, long, float`

They: - Store raw values - Are not objects - Have no methods - Cannot be
used in generics

## 🔹 Reference Types

Classes, Interfaces, Arrays, Enums

They: - Are objects - Have methods - Live on the heap - Work with
generics and collections

Problem: Collections like `ArrayList` require objects --- not
primitives.

Wrapper classes solve this problem.

------------------------------------------------------------------------

## What Is a Wrapper Class?

A wrapper class encapsulates a primitive value inside an immutable
object.

  Primitive   Wrapper
----------- -----------
  int         Integer
  double      Double
  char        Character
  boolean     Boolean
  long        Long
  float       Float
  byte        Byte
  short       Short

Example:

``` java
Integer x = Integer.valueOf(10);
```

Conceptually:

``` java
public final class Integer {
    private final int value;
}
```

------------------------------------------------------------------------

## Are Wrapper Classes Objects?

## Yes --- Technically

Wrapper classes: - Are defined using `class` - Extend `Object` - Have
methods - Have fields - Live on the heap - Can be null

Example:

``` java
Integer a = 5;
System.out.println(a.getClass());
```

So yes --- they are objects.

------------------------------------------------------------------------

## ❗ But They Are Not "Just Objects"

Wrapper classes are specialized immutable objects with additional
behavior.

------------------------------------------------------------------------

## Special Behaviors of Wrapper Classes

## 🔹 Auto-Boxing

``` java
Integer obj = 10;
```

Behind the scenes:

``` java
Integer obj = Integer.valueOf(10);
```

------------------------------------------------------------------------

## 🔹 Auto-Unboxing

``` java
Integer obj = 20;
int num = obj;
```

Behind the scenes:

``` java
int num = obj.intValue();
```

------------------------------------------------------------------------

## 🔹 Immutability

``` java
Integer a = 10;
a = a + 5;
```

Steps: 1. Unboxing 2. Addition 3. New Integer object created 4.
Reference reassigned

------------------------------------------------------------------------

## 🔹 Caching Behavior

``` java
Integer a = 100;
Integer b = 100;
System.out.println(a == b); // true
```

``` java
Integer x = 200;
Integer y = 200;
System.out.println(x == y); // false
```

Java caches values from -128 to 127.

------------------------------------------------------------------------

## Why Wrapper Classes Are Necessary

## 🔹 Generics Require Objects

Illegal:

``` java
ArrayList<int> list = new ArrayList<>();
```

Legal:

``` java
ArrayList<Integer> list = new ArrayList<>();
```

------------------------------------------------------------------------

## 🔹 Nullability

Primitive:

``` java
int x = null; // error
```

Wrapper:

``` java
Integer x = null; // allowed
```

------------------------------------------------------------------------

## Memory Model Discussion

Primitive:

``` java
int x = 5;
```

Wrapper:

``` java
Integer x = 5;
```

Stack stores reference → Heap stores object → Object stores primitive
value.

------------------------------------------------------------------------

## Performance Considerations

Wrappers introduce: - Object allocation - Garbage collection -
Boxing/unboxing overhead

Use primitives in performance-critical code.

------------------------------------------------------------------------

## When to Use Wrapper Classes

Use wrappers when: - Working with collections - Using generics - Needing
null values - Using utility methods

Use primitives when performance matters.

------------------------------------------------------------------------

## Summary

Instead of saying:

"Wrapper classes are just objects."

Say:

"Wrapper classes are immutable objects that encapsulate primitive values
and enable primitives to interact with object-based APIs."

------------------------------------------------------------------------

# 🔬 Advanced Section --- Deep Dive

------------------------------------------------------------------------

## Integer Caching

``` java
Integer a = 127;
Integer b = 127;
System.out.println(a == b); // true

Integer x = 128;
Integer y = 128;
System.out.println(x == y); // false
```

Java caches Integer values between -128 and 127.

Always use:

``` java
a.equals(b)
```
## What Is the Purpose of Caching in Wrapper Classes?
When we say:

> Java caches Integer objects from -128 to 127

The natural question is:

> Why would the JVM do that?

### Primary Purpose: Performance

Creating objects is expensive compared to using primitives.

Without caching:

```java
Integer a = 10;
Integer b = 10;
```

Java would create:

- Object #1 for 10
- Object #2 for 10

That’s unnecessary duplication.

With caching:

- Only one object is created for 10.

- Both references point to the same object.

This reduces:

- Object allocation

- Heap usage

- Garbage collection pressure

### Why Cache -128 to 127?

Because this range:

- Covers common small numbers
- Includes ASCII values
- Covers loop counters
- Covers most frequently used numeric literals

```java
for (int i = 0; i < 100; i++)
```

These values are used constantly.

So caching this range optimizes the most common cases.

This is an engineering tradeoff.

### Memory Efficiency

If Java didn’t cache:

In a program using millions of small integers (like 0, 1, 2, 10, etc.),

You would create millions of identical objects.

Caching:

- Reduces memory duplication
- Reduces GC overhead
- Improves runtime performance

### Why Not Cache All Integers?

Because:

- There are $2^{31}$ possible `int` values.
- Caching all would require enormous memory.
- Most large integers are rarely reused.

So JVM designers chose a practical compromise:

- Cache the common range
- Create new objects outside it

# Important Design Insight:

## Why Immutability Enables Caching

The key statement is:

> Caching works **because wrapper classes are immutable**.

Let’s unpack that carefully.

------

## What Caching Really Means

When Java caches:

```
Integer a = 100;
Integer b = 100;
```

Both `a` and `b` may refer to the **same object in memory**.

Conceptually:

```
a ──┐
    │
    └──> [ Integer object: value = 100 ]
    │
b ──┘
```

Two references → one shared object.

That’s object reuse.

------

## Why This Is Safe

It is safe **only because the object cannot change**.

Wrapper classes are:

```
public final class Integer {
    private final int value;
}
```

Notice:

- `final class` → cannot be subclassed
- `private final int value` → cannot change after construction

So once created:

```
value = 100
```

It will *always* be 100.

That guarantees safety.

------

## What If Integer Were Mutable?

Imagine (hypothetically) that `Integer` allowed mutation:

```
Integer x = 10;
Integer y = x;
```

Both point to same cached object.

Now suppose:

```
x.setValue(20);
```

Then:

```
y would now also see 20
```

Because both references share the same object.

That would:

- Corrupt cached values
- Break program correctness
- Cause unpredictable behavior
- Destroy referential consistency

Caching would become impossible.

------

## Why Immutability Is the Foundation

Caching depends on three guarantees:

1. The object’s value never changes.
2. Sharing the object does not change program behavior.
3. The object has no mutable state.

Wrapper classes satisfy all three.

Therefore:

> Immutability makes object sharing safe.

------------------------------------------------------------------------

## Autoboxing Performance Cost

``` java
for (Integer i = 0; i < 1_000_000; i++) {
}
```

Creates repeated boxing/unboxing.

Better:

``` java
for (int i = 0; i < 1_000_000; i++) {
}
```

------------------------------------------------------------------------

## NullPointerException Risk

``` java
Integer x = null;
int y = x;  // throws NullPointerException
```

Auto-unboxing calls `x.intValue()`.

------------------------------------------------------------------------

##Memory Footprint Comparison

  Type      Approx Memory
--------- ---------------
  int       4 bytes
  Integer   16+ bytes

Wrapper objects consume significantly more memory.

------------------------------------------------------------------------

## Immutability and Thread Safety

Wrapper classes are: - final - immutable

This ensures safe caching and predictable behavior.

------------------------------------------------------------------------

## equals() vs ==

  Operator    Meaning
----------- ----------------------
  ==          reference comparison
  .equals()   logical equality

------------------------------------------------------------------------

# 🎓 Concept Check Questions

1.  Why does `ArrayList<int>` not compile?
2.  Why can `Integer` be null but `int` cannot?
3.  Why does `Integer x = null; int y = x;` throw an exception?
4.  Why can `==` behave unexpectedly with Integer?
5.  Why are wrapper classes immutable and final?

------------------------------------------------------------------------

End of Lecture

