# SOLID: The First 5 Principles of Object Oriented Design

SOLID stand for :

1. S - Single-responsiblity Principle
2. O - Open-closed Principle
3. L - Liskov Substitution Principle
4. I - Interface Segregation Principle
5. D - Dependency Inversion Principle

## Single-responsiblity Principle

- every class must have one job .
- like a class for calculate teh sum the class should only be concerned with the sum only .
- Example :

$shapes = [
  new Circle(2),
  new Square(5),
  new Square(6),
];

$areas = new AreaCalculator($shapes);

$output = new SumCalculatorOutputter($areas);

echo $output->JSON();

echo $output->HTML();

## Open-Closed Principle

- its mean the class can be expanded but not modified .
- like put the logic in the related class like sum of area of square we put the method in square class .
- The interface is very important because we don't know which class must have a specific method .

## Liskov Substitution Principle

- its mean very subClass or class must be substitutable  of their parent .
- the satisfied of liskov principle is multi type of primitive they can return.

## Interface Segregation Principle

- its mean the client mustn't forced to use any interface that doesn't use and the same on method they mustn't forced to use method that doesn't use .
- like when interface force class to implement a method and the class has no use to it .
- the better way is make very interface have one method only .

## Dependency Inversion Principle

**I dont understanding the state of it**

- its mean like the superClass should not care about the subclass.
- the solution for this problem we should create two interfaces one with high-level and another with low-level modules  .

# The SOLID Principles in Real Life

- the single responsibility principle doesn't applied on all classes like server classes.

- the open/closed principle is should be close for modified but open for extends by instance, inheriting from it and overriding.

- the liskov substitution principle its say every child of calss should be stand without the parent class.

- the dependency inversion principle encourages you to write code that depends upon abstractions rather than upon concrete details.
