# Java OO Tutorial (only the Object and Class ones)

## Object

### What Is an Object?

- Objects are key to understanding object-oriented technology.

- objects share two characteristics :

1. state  : like container (keys)
2. behavior : the data in side the container (values)

- number of benefits that provides using objects in the software:

1. reuseable code
2. Information-hiding
3. Pluggability and debugging ease
4. Modularity

## Classes

### What Is a Class?

- Class is like a blueprint that contains all the objects that belong to him

- example :

class Bicycle {

    int cadence = 0;

    int speed = 0;

    int gear = 1;

    void changeCadence(int newValue) {

         cadence = newValue;

    }
}

- Classes can contains fields(like int number), one constructor ,methods

- Classes may contain subclasses and look like :
public class MountainBike extends Bicycle (Bicycle in subClass from MountainBike)

- if subclass have a constructor or method the main Class can inherits  all the methods and the constructor from subclass.

# Binary, Decimal and Hexadecimal Numbers

## Decimals

- Based on 0, 1, 2, 3, 4, 5, 6, 7, 8 and 9
- we need to convert Decimal number to Binary number(0,1) to make the machine to read it .

## Binary Numbers

- based on 0,1 which is the language of machine that can read

## Hexadecimal Numbers

- based on 0 to 15 but after 9 its take string like 10 is A ,11 is B etc ..
