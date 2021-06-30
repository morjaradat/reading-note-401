# Primitives vs. Objects

## Java Type System

- Java has a two-fold type system :

1. primitives such as int, boolean
2. reference types such as Integer, Boolean.

- there are two types of process :

1. autoboxing
2. unboxing

** autoboxing that converts a primitive type to a reference one .

** unboxing that converts reference one type to a primitive .

## Pros and Cons

- The decision what object is to be used is based on what is the applicatoin performance we want and how much memory we have and what default value we handle .

## Single Item Memory Footprint

- The primitive type variables have the following impact on the memory :

1. boolean – 1 bit
2. byte – 8 bits
3. short, char – 16 bits
4. int, float – 32 bits
5. long, double – 64 bits

- This type of Variables are living in stack and hence are accessed fast.
- objects are living on the heap and are relatively slow to access.

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

# Exceptions in Java

## Exceptions

- The Java programming language uses exceptions to handle errors and other exceptional events.

## What Is an Exception?

- An exception is an event that occurs during the execution of a program that disrupts the normal flow of instructions. (it is an Error ) .

 **Processing :**

1. create an object and hands the error .
2. the system try to find something to handle the error.
3. the system call the method that handles the error .
4. the method chosen to catch the error and return it.

## The Catch or Specify Requirement

- Code that fails to honor the Catch or Specify Requirement will not compile.

**The Three Kinds of Exceptions :**

1. checked exception : like When the user miss writing the name file in import.
2. exception is the error : this exception is from out the code.
3. the runtime exception:  this exception is from internal the code, usually cannot anticipate(its usually from Bugs).

## Catching and Handling Exceptions

- we can use try-catch method or finally blocks method to write an exception handler.

# Using Scanner to read in a file in Java

- We use Scanner to get some input from the user in the execution time Scanner
- we need to close the scanner after we furnish using it
- the scanner would take a string or number value as input
