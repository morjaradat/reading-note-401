# Primitives vs. Objects

## Java Type System

- Java has a two-fold type system :

1. consisting of primitives such as int, boolean
2. reference types such as Integer, Boolean.

- The wrapper classes are immutable.
- there are two types of process :

`` 
Integer j = 1;          // autoboxing
int i = new Integer(1); // unboxing
``

1. autoboxing that converts a primitive type to a reference one
2. unboxing that converts reference one type to a primitive .

## Pros and Cons

- The decision what object is to be used is based on :

1. what application performance we try to achieve
2. how much available memory we have
3. the amount of available memory director
4. what default values we should handle.

## Single Item Memory Footprint

the primitive type variables have the following impact on the memory:

1. boolean – 1 bit
2. byte – 8 bits
3. short, char – 16 bits
4. int, float – 32 bits
5. long, double – 64 bits

- Variables of these types live in the stack and hence are accessed fast.
- The reference types are objects, they live on the heap and are relatively slow to access.
- To get an object's internal structure, we may use the Java Object Layout tool
- It turns out that a single instance of a reference type on this JVM occupies 128 bits except for Long and Double which occupy 192 bits

## Memory Footprint for Arrays

- Arrays are consume  memory depend on the type of primitive like :

1. long, double: m(s) = 128 + 64 s
2. short, char: m(s) = 128 + 64 [s/4]
3. byte, boolean: m(s) = 128 + 64 [s/8]
4. the rest: m(s) = 128 + 64 [s/2]

- arrays of the primitive types long and double consume more memory than their wrapper classes Long and Double.

## Performance

- The performance of a Java code is quite a subtle issue
- its depend on the hardware that runs on

## Default Values

- Default values of the primitive types are :

1. 0 for numeric type
2. false for boolean type
3. u0000 for the char type

- For the wrapper classes, the default value is null.

## Usage

- Java language specification doesn't allow usage of primitive types in the parametrized types (generics),  in the Java collections or the Reflection API.
- When our application needs collections with a big number of elements, we should consider using arrays with as more “economical” type as possible.

# Exceptions in Java

## Exceptions

- The Java programming language uses exceptions to handle errors and other exceptional events.

## What Is an Exception?

- An exception is an event that occurs during the execution of a program that disrupts the normal flow of instructions. (it is an Error ) .

 **Processing :**

- When an error occurs within a method, the method creates an object and hands it.
- After a method throws an exception, the runtime system attempts to find something to handle it ( The list of methods is known as the call stack).
- The runtime system searches the call stack for a method that contains a block of code that can handle the exception(This block of code is called an exception handler)
- The exception handler chosen is said to catch the exception. If the runtime system exhaustively searches all the methods on the call stack without finding an appropriate exception handler.

## The Catch or Specify Requirement

- Code that fails to honor the Catch or Specify Requirement will not compile.

**The Three Kinds of Exceptions :**

1. checked exception : These are exceptional conditions that a well-written application should anticipate and recover from, like When the user miss writing the name file in import.
2. exception is the error : These exceptional are external to the application, and that the application usually cannot anticipate or recover from.
3. the runtime exception: These are exceptional conditions that are internal to the application, and that the application usually cannot anticipate or recover from (its usually from Bugs).

## Catching and Handling Exceptions

- we can use try-catch method or finally blocks method to write an exception handler.

# Using Scanner to read in a file in Java

- We use Scanner to get some input from the user in the execution time Scanner
- we need to close the scanner after we furnish using it
- the scanner would take a string or number value as input
