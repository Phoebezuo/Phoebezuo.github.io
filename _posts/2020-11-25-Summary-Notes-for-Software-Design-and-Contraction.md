---
layout:     post
title:      Summary Notes for Software Design and Construction
date:       2020-11-25
summary:    Summary Notes for Software Design and Construction
categories: Java Software Development
---

- [OO Theory](#oo-theory)
  - [Class Methods](#class-methods)
  - [Access Modifier](#access-modifier)
  - [Compile-time vs Runtime Type](#compile-time-vs-runtime-type)
  - [Virtual Dispatch](#virtual-dispatch)
  - [Abstract Class](#abstract-class)
  - [Interface](#interface)
- [UML](#uml)
  - [Use Case Diagram](#use-case-diagram)
  - [Class Diagram](#class-diagram)
  - [Interaction Diagram](#interaction-diagram)
- [Design Smells](#design-smells)
  - [Common Design Smells](#common-design-smells)
  - [Symptoms Design Smells](#symptoms-design-smells)
- [SOLID](#solid)
  - [Single Responsibility Principle](#single-responsibility-principle)
  - [Open-closed Principle](#open-closed-principle)
  - [Liskov Substitution Principle](#liskov-substitution-principle)
  - [Interface Segregation Principle](#interface-segregation-principle)
  - [Dependency Inversion Principle](#dependency-inversion-principle)
- [GRASP](#grasp)
  - [Creator](#creator)
  - [Information Expert](#information-expert)
  - [High Cohesion](#high-cohesion)
  - [Low Coupling](#low-coupling)
  - [Coupling vs Cohesion](#coupling-vs-cohesion)
  - [Controller](#controller)
- [Design Patterns](#design-patterns)
  - [Creational Patterns](#creational-patterns)
    - [Factory Method](#factory-method)
    - [Builder](#builder)
    - [Singleton](#singleton)
    - [Prototype](#prototype)
  - [Structural Patterns](#structural-patterns)
    - [Adapter](#adapter)
    - [Facade](#facade)
    - [Decorator](#decorator)
  - [Behavioral Patterns](#behavioral-patterns)
    - [Strategy](#strategy)
    - [State](#state)
    - [Observer](#observer)
    - [Memento](#memento)
- [Exam Questions](#exam-questions)

# OO Theory

## Class Methods

- Mutator / setter - Methods that change the state of a class object
- Accessor / getter - Methods that read the state of a class object

## Access Modifier

- Public - Accessible for clients, class and sub-class
- Protected - Accessible for class, and sub-classes
- Private - Accessible for class itself only
- Default - Accessible within package
- **Notes:** There is no need for import statement if a public class is used in the same package

## Compile-time vs Runtime Type

```java
Number x;

if (userInput.equals("integer")) {
    x = new Integer(5);
} else {
    x = new Float(3.14);
}
```

- The type of the name `x` is `Number`. This is determined at compile-time and can never change, hence it's the static type
- The type of the value `x` refers to `Integer` or `Float`. This is determined at runtime (hence dynamic type), and may change multiple times, as long as it's a subclass of the static type.

## Virtual Dispatch

```java
public class Shape {
  double area() {}
}

public class Rectangle extends Shape {
  double area() {}
}

Shape X = new Shape();
double a1 = X.area() // invokes area of Shape

Shape Y = new Rectangle();
double a2 = Y.area() // invokes area of Rectangle
```

- The type of reference variable and class instance may differ
- Class variables may override methods of super classes
- The method invoked is determined by the type of the class instance

## Abstract Class

- Method implementations are deferred to sub-classes
- No instance of an abstract class can be generated

```java
abstract class Shape extends Object {
  public abstract double area();
}

public class Rectangle extends Shape {
  double width;
  double length;
  double area() {
    return width * length;
  }
}
```

## Interface

- Interfaces are specified so that they form a directed acyclic graph
- Methods declared in an interface are always public and abstract
- Variables are permitted if they are static and final only

```java
public interface A {
  int foo(int x);
}

public interface B extends A{
  int hoo(int x);
}
```
- Interface B has methods `foo()` and `hoo()`

# UML

## Use Case Diagram

<img src='https://i.loli.net/2020/11/25/OaFSUjJrQLqfYAu.png' alt='OaFSUjJrQLqfYAu'/>

- Role: interact with subject / system
- Use case: describe functionality of the system

<img src='https://i.loli.net/2020/11/25/uXWxYfg59BJMcZD.png' alt='uXWxYfg59BJMcZD'/>

## Class Diagram

<img src='https://i.loli.net/2020/11/25/EzspN17GiXqyJBv.png' alt='EzspN17GiXqyJBv'/>

**Notes:** Dependency exists between two elements if changes to the definition of one element (the supplier) may cause changes to the other (the client).
- Class send messages to another
- One class has another as its data
- One class mention another as a parameter to an operations
- One class is a superclass or interface of another

Aggression vs Composition

<img src='https://i.loli.net/2020/11/25/xbDTdUW7tqlJ6aZ.png' alt='xbDTdUW7tqlJ6aZ'/>

Multiplicity
- `*`: any number
- `0..1`: zero or one
- `1..*`: 1 or more
- `n..m`: n through m

<img src='https://i.loli.net/2020/11/25/trld2HfSeEwFKcI.png' alt='trld2HfSeEwFKcI'/>

## Interaction Diagram

<img src='https://i.loli.net/2020/11/25/X7de6GbrghRWJTs.png' alt='X7de6GbrghRWJTs'/>

Common frame operators
- `Alt`: Alternative fragment for mutual exclusion conditional logic expressed in the guards
- `Loop`: Loop fragment while guard is true
- `Opt`: Optional fragment that executes if guard is true
- `Par`: Parallel fragments that execute in parallel
- `Region`: Critical region within which only one thread can run

<img src='https://i.loli.net/2020/11/25/H4odLmgKw9yGI6B.png' alt='H4odLmgKw9yGI6B'/>

<img src='https://i.loli.net/2020/11/25/oIyzPO1Gpg9S7qY.png' alt='oIyzPO1Gpg9S7qY'/>

# Design Smells

## Common Design Smells

- **Missing abstraction:** bunches of data or encoded strings are used instead of creating an abstraction
- **Multifaceted abstraction:** an abstraction has multiple responsibilities assigned to it
- **Insufficient modularization:** an abstraction has not been completely decomposed, and a further decomposition could reduce its size, implementation complexity, or both
- **Cyclically-dependent modularization:** two or more abstractions depend on each other directly or indirectly (creating tightly-coupling abstractions)
- **Cyclic hierarchy:** a super-type in a hierarchy depends on any of its subtypes

## Symptoms Design Smells

- **Rigidity (difficult to change):** the system is hard to change because every change forces many other changes to other parts of the system
  - A design is rigid if a single change causes a cascade of subsequent changes in dependent modules
- **Fragility (easy to break):** Changes cause the system to break in places that have no conceptual relationship to the part that was changed
  - Fixing those problems leads to even more problems
  - As fragility of a module increases, the likelihood that a change will introduce unexpected problems approaches certainty
- **Immobility (difficult to reuse):** It is hard to detangle the system into components that can be reused in other systems
- **Viscosity (difficult to do the right thing):** Doing things right is harder than doing things wrong
  - Software: when design-preserving methods are more difficult to use than the others (hacks), the design viscosity is high (easy to do the wrong thing but difficult to do the right thing)
  - Environment: when development environment is slow and inefficient.
- **Needless Complexity (overdesign):** when design contains elements that are not useful.
  - When developers anticipate changes to the requirements and put facilities in software to deal with those potential changes.
- **Needless Repetition (mouse abuse):**
  - Developers tend to find what they think relevant code, copy and paste and change it in their module
  - Code appears over and over again in slightly different forms, developers are missing an abstraction
  - Bugs found in repeating modules have to be fixed in every repetition
- **Opacity (disorganized expression):** tendency of a module to be difficult to understand
  - Code written in unclear and non-expressive way
  - Code that evolves over time tends to become more and more opaque with age
  - Developers need to put themselves in the reader’s shoes and make appropriate effort to refactor their code so that their readers can understand it

# SOLID

<img src='https://i.loli.net/2020/11/25/1w2Vv6HPecKEgWJ.png' alt='1w2Vv6HPecKEgWJ'/>

## Single Responsibility Principle

A class should be **assigned a single responsibility, avoiding a class performing more roles than it should**. If you ﬁnd that you are assigning multiple roles to a class you can break the these roles into separate classes.

## Open-closed Principle

Open-Closed principle outlines that **an element is open for extension but closed for modiﬁcation**. Extension can be typically inferred as class inheritance but it is also possible to extend a class through composition or traits (interface with default method).

## Liskov Substitution Principle

This principle infers that **types should be replacable with instances of their subtypes**. It asserts that a class should utilise an interface and allow for an instance of that interface to be substituted. For example, if `S` is a subtype of `T`, then a `T` object can be replaced with an `S` object and no harm done.

## Interface Segregation Principle

Interface segregation asks to **break up large interface types**. Designing the application to use many client-speciﬁc interfaces over large general purpose interface. Each interface should focus on the functionality required instead of a large interface providing methods that some objects may never implement.

## Dependency Inversion Principle

Dependency inversion principle places the constraint that **an abstraction should never depend on the details of classes** (i.e. high level, complex modules should not depend on low-level, simple models). Allow your types to depend on abstractions, the type binding can be updated and substituted when refactoring.

# GRASP

## Creator

<img src='https://i.loli.net/2020/11/25/Zcbe9n2sd5CPzAL.png' alt='Zcbe9n2sd5CPzAL' width="30%"/>

- Problem - Who creates an A object
- Solution - Assign class B the responsibility to create an instance of class A if one of these is true
  - B “contains” A
  - B “records” A
  - B “closely uses” A
  - B “has the Initializing data for” A

## Information Expert

<img src='https://i.loli.net/2020/11/25/KPJYwkE96fvcxd8.png' alt='KPJYwkE96fvcxd8' width="50%"/>

- Problem - What is a general principle of assigning responsibilities to objects
- Solution - Assign a responsibility to the class that has the information needed to fulfill it

## High Cohesion

- Problem - How to keep objects focused, understandable, and manageable, and as a side effect, support Low Coupling?
- Solution - Assign responsibilities so that cohesion remains high

**Notes:** Cohesion - How strongly related and focused the responsibilities of an element are

## Low Coupling

<img src='https://i.loli.net/2020/11/25/wKU6fZzdYSjVXBC.png' alt='wKU6fZzdYSjVXBC'/>

- Problem - How to reduce the impact of change, to support low dependency, and increase reuse?
- Solution - Assign a responsibility so that coupling remains low

**Notes:** Coupling - How strongly one element is connected to, has knowledge of, or depends on other elements

## Coupling vs Cohesion

- Coupling describes the inter-objects relationship
- Cohesion describes the intra-object relationship
- Extreme case of “coupling”
  - Only one class for the whole system
  - No coupling at all
  - Extremely low cohesion
- Extreme case of cohesion
  - Separate even a single concept into several classes
  - Very high cohesion
  - Extremely high coupling

## Controller

- Problem - What first object beyond the UI layer receives and coordinates (“controls”) a system operation
- Solution - Assign the responsibility to an object representing one of these choices
  - Represents the overall system, root object, device or subsystem (a façade controller)
  - Represents a use case scenario within which the system operations occurs (a use case controller)

# Design Patterns

<img src='https://i.loli.net/2020/11/25/E5JK1p3olfed6uO.png' alt='E5JK1p3olfed6uO'/>

## Creational Patterns
- Abstract the instantiation process
- Make a system independent of how its objects are created, composed and represented
  - Class creational pattern uses inheritance to vary the class that's instantiated
  - Object creational pattern delegates instantiation to another object
- Provides flexibility in what gets created, who creates it, how it gets created and when

### Factory Method

Define an interface for creating an object, but let sub-class decide which class to instantiate (class instantiation deferred to subclasses)

<img src='https://i.loli.net/2020/11/25/uSV1KGrzfDhylTM.png' alt='uSV1KGrzfDhylTM'/>

Participates
- Product - Defines the interface of objects the factory method creates
  ```java
  public interface OfficeDocument {}
  ```
- ConcreteProduct - Implements the Product interface
  ```java
  public class ExcelDocument {}
  ```
  ```java
  public class WordDocument {}
  ```
- Creator - Declares the factory method, which returns an object of type Product.
  ```java
  public interface OfficeFactory {
    OfficeFactory createDocument();
  }
  ```
- ConcreteCreator - Overrides the factory method to return an instance of the ConcreteProduct
  ```java
  public class ExcelFactory {
    @Override
    ExcelDocument createDocument() {}
  }
  ```
  ```java
  public class WordFactory {
    @Override
    WordDocument createDocument() {}
  }
  ```

Benefits
Drawbacks

### Builder

Separate the construction of a complex object from its representation so that the same construction process can create different representations

### Singleton

Ensure a class only has one instance, and provide global point of access to it

### Prototype

Specify the kinds of objects to create using a prototype instance, and create new objects by copying this prototype

## Structural Patterns
- How classes and objects are composed to form larger structures

### Adapter

Allow classes of incompatible interfaces to work together. Convert the interface of a class into another interface that clients expect.

### Facade

Provides a unified interface to a set of interfaces in a subsystem. Defines a higher-level interface that makes the subsystem easier to use.

### Decorator

Attach additional responsibilities to an object dynamically (flexible alternative to subclassing for extending functionality)

## Behavioral Patterns
- Concerns with algorithms and the assignment of responsibilities between objects

### Strategy

Define a family of algorithms, encapsulate each one, and make them interchangeable (let algorithm vary independently from clients that use it)

### State

Allow an object to alter its behaviour when its internal state changes. The object will appear to change to its class

### Observer

Define a one-to-many dependency between objects so that when one object changes, all its dependents are notified and updated automatically

### Memento

Without violating encapsulation, capture and externalise an object's internal state so that the state can later be restored to this state

# Exam Questions

- Describe pattern / principle X and compare it to Y.
  ```
  – X is a design pattern that ...
  – X is generally useful because ..., although it has the drawbacks ...
  – Y is a design pattern that ...
  – Y is generally useful because ..., although it has the drawbacks ...
  – X differs from Y because ...
  ```

- Apply a design pattern to solve problem Y.
  ```
  – I will use X
  – X is a design pattern that ...
  – X is generally useful because ..., although it has the drawbacks ...
  – X is specifically applicable to Y because ...
  – ... implementation ... (if asked for)
  ```

- Given the following code, state the pattern has been used on it. Map the classes in the code to the roles/participants in the pattern.
  ```
  – The pattern has been used in the code is ...
  – Class X is ... (refer to participant name) of pattern ...
  – Class X is used for/to ... (specific roles) in pattern ... in the given code
  ```
- List all classifier names together with attributes and operations of the UML class diagram of system S. Identify the relationships among these classifiers.
  ```
  – Class X
    - Attributes: + variableName : String
    - Operations: + methodName (parm: float): double
  - Interface Y
    - Operations: + methodName (parm: float): double
  - Relationship:
    - Class X implements interface Y
  ```
