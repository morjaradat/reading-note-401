# Java Imports (ignore the parts about NetBeans)

## Package declaration

- We can import any package from any source

## Package declaration syntax

- the import syntax is : import javax.libraryName

## there are three types of imports :

1.make all classes visible by using *
2.a single class  can be specified explicitly by passing the class Name after the libraryName in import.
3.we can use the classes directory in the syntax by write javax.libraryName .

## Common imports

- most common packages 

1. import java.awt.*;    	Common GUI elements.
2. import java.awt.event.*;	The most common GUI event listeners.
3. import javax.swing.*;	More common GUI elements. Note "javax".
4. import java.util.*;	Data structures (Collections), time, Scanner, etc classes.
5. import java.io.*;	Input-output classes.
6. import java.text.*;	Some formatting classes.
7. import java.util.regex.*;	Regular expression classes.

## import FAQ

1- import is doesn't make the file larger
2- its no need to remember the library's name
3- its bad to use (*) in import
4- "*" only makes the classes in this package visible, not any of the subpackages.
5- there is no specific order to import

- If you forgot to write import statements, or don't remember which package a class is it NetBeans  will automatically create it.

## Static imports

- Java 5 added an import static option that allows static variables (typically constants) to be referenced without qualifying them with a class name.
- For example, after

import static java.awt.Color;
It would then be possible to write

   Color background = RED;
instead of

   Color background = Color.RED;

- this is bad idea because it leads to name pollution and confusion about which class constants come from.

# Different types of loops in Java

- types of loops :

1. Simple for loop : control structure that allows us to repeat certain operations by incrementing and evaluating a loop counter.
2. Enhanced for-each loop : same simple for loop but with different write
3. While loop : It repeats a statement or a block of statements while its controlling Boolean-expression is true.
4. Do-While loop : the first iteration of the loop happened once before we check the condition .
