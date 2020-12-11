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
- [Testing](#testing)
  - [Type of testing](#type-of-testing)
  - [Black box testing](#black-box-testing)
  - [White box testing](#white-box-testing)
  - [JUnit](#junit)
    - [Constructs](#constructs)
    - [Annotation](#annotation)
    - [Assertion](#assertion)
- [Design Smells](#design-smells)
  - [Common Design Smells](#common-design-smells)
  - [Symptoms Design Smells](#symptoms-design-smells)
- [Code Reviews](#code-reviews)
  - [Formal Review (Fagan Inspection)](#formal-review-fagan-inspection)
  - [Informal Review](#informal-review)
  - [Semi-formal Review (Design by Contract DbC)](#semi-formal-review-design-by-contract-dbc)

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

public interface B implements A{
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

- Aggression
  - When whole is removed, part may not removed.
  - A **uses** B
  - e.g. whole is car, part is wheel.
- Composition
  - When whole is removed, part also removed.
  - A **owns** B
  - e.g. whole is head, part is head.

<img src='https://i.loli.net/2020/11/25/xbDTdUW7tqlJ6aZ.png' alt='xbDTdUW7tqlJ6aZ'/>
<img src='https://i.loli.net/2020/11/29/TGnHDcXFbhJC3NE.png' alt='TGnHDcXFbhJC3NE'/>

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
- Product
  - Defines the interface of objects the factory method creates
- Concrete Product
  - Implements the Product interface
- Creator
  - Declares the factory method, which returns an object of type Product.
- Concrete Creator
  - Overrides the factory method to return an instance of the ConcreteProduct

Example

<img src='https://i.loli.net/2020/11/26/Don6aPdX3ABwHQ7.png' alt='Don6aPdX3ABwHQ7'/>

```java
OfficeFactory factory = new WordFactory();
OfficeDocument document = factory.createDocument();
```

Positive
- Improve extensibility when add a new class, if can simply create a new class and implements *Creator*. This also deploys the *Open-closed Principle*
- If client needs to create an object, the only thing to know is its name, instead of the algorithm about how to create this object. It allows to hide implementation of a product.
- It eliminate the need to bind application-specific classes into your code. The code only deals with the *Product* interfaces. Therefore, it can work with any user-defined *Concrete Product* classes.
- It connect parallel class hierarchies in such a way that it localizes the knowledge of which classes belong together.

Negative
- Whenever a new product needs, it requires to implement its *Concrete Creator* and *Concrete Product*. This increases the complexity of whole system, as well as its louping between.
- Because every application object that intends to use the services offered by the class hierarchy needs to implement the class selection criteria, it results in a high degree of coupling between an application object and the service provider class hierarchy.

### Builder

Separate the construction of a complex object from its representation so that the same construction process can create different representations

<img src='https://i.loli.net/2020/11/25/Ot4SxHN96LP5uXU.png' alt='Ot4SxHN96LP5uXU'/>

Participates
- Builder
  - Specifies an abstract interface for creating parts of a Product object
- Concrete Builder
  - Constructs and assembles parts of the product by implementing the Builder interface
  - defines and keeps track of the representation it creates.
  - provides an interface (`GetResult`) for retrieving the product
- Director
  - Constructs an object using the Builder interface
- Product
  - Represents the complex object under construction.
  - ConcreteBuilder builds the product's internal representation and defines the process by which it's assembled
  - Includes classes that define the constituent parts, including interfaces for assembling the parts into the final result

Example

<img src='https://i.loli.net/2020/11/29/O4jKg7aPCFi6nIo.png' alt='O4jKg7aPCFi6nIo'/>

Positive
- Extensibility - gives flexibility that can be extended by implementing new subclasses of the Builder
- Isolates code of construction from implementation. Each *Concrete Builder* contains all the code to create and assemble a particular kind of product. Different *Directors* can reuse it to build Product variants from the same set of parts.
- Varying product's internal representation. Because the *Product* is constructed through an abstract interface, all you have to do to change the product's internal representation is define a new kind of builder
- Finer control over the construction process, since the builder pattern constructs the product step by step under the *Director* control. Only when the product finished, *Director* retrieve it from the builder

Negative
- Not completely generic, less useful in situations where variety of implementations is not high.
- It will have additional code in order to implement this design pattern.
- There should be some similarity among its *Concrete Builder*, so it restricts the scope of product.

### Singleton

Ensure a class only has one instance, and provide global point of access to it

<img src='https://i.loli.net/2020/11/26/6TcI1GsQUVEgmbA.png' alt='6TcI1GsQUVEgmbA'/>

Participate
- Defines an `instance()` operation that lets clients access its unique instance. `instance()` is a class operation
- May be responsible for creating its own unique instance

Example

<img src='https://i.loli.net/2020/11/26/KzSgEQOmwNYrlXn.png' alt='KzSgEQOmwNYrlXn'/>

Positive
- It prevents other objects from instantiating their own copies of the Singleton object, ensuring that all objects access the single instance. This reduce the memory usage, especially initialize or destroy regular like database, etc.
- Since the class controls the instantiation process, the class has the flexibility to change the instantiation process.
- It encapsulates a unique resource and makes it readily available throughout the application.

Negative
- They deviate from the *Single Responsibility Principle*. A singleton class has the responsibility to create an instance of itself along with other business responsibilities. However, this issue can be solved by delegating the creation part to a factory object.
- Singleton classes cannot be sub classed, thus should not be easily extensible.

### Prototype

Specify the kinds of objects to create using a prototype instance, and create new objects by copying this prototype

<img src='https://i.loli.net/2020/11/26/tIgvwK9VeZNR2mh.png' alt='tIgvwK9VeZNR2mh'/>

Participate
- Prototype
  - Declares an interface for cloning itself
- ConcretePrototype
  - Implements an operation for cloning itself.
- Client
  - Creates a new object by asking a prototype to clone itself

Example

<img src='https://i.loli.net/2020/11/26/dv6hfXRimGUtuAK.png' alt='dv6hfXRimGUtuAK'/>

Positive
- It hides the *concrete product* classes from the client, thereby reducing the number of names clients know about.
- It let you incorporate a new *concrete product* class into a system simply by registering a prototypical instance with the client. This increase flexibility, because a client can install and remove prototypes at run-time.
- It reduced subclassing as *Factory Method* often produces a hierarchy of *Creator* classes that parallels the *Product* class hierarchy. The Prototype pattern lets you clone a prototype instead of asking a factory method to make a new object. Hence you don’t need a *Creator* class hierarchy at all.

Negative
- It mush have an interface that has `cloneable()` method, and each subclass of prototype must implement the clone operation
- It hides concrete product classes from the client
- Each subclass of Prototype must implement the `clone()` operation which may be difficult, when the classes under consideration already exist.

## Structural Patterns

- How classes and objects are composed to form larger structures
- Structural class patterns use inheritance to compose interfaces or implementations
- Structural object patterns describe ways to compose objects to realise new functionality - The flexibility of object composition comes from the ability to change the composition at run-time

### Adapter

Allow classes of incompatible interfaces to work together. Convert the interface of a class into another interface that clients expect.

Class adapter
- Relies on class inheritance to achieve adapter
- Can only be used in one abstract class

<img src='https://i.loli.net/2020/11/26/8RGfE3JryCYwtvk.png' alt='8RGfE3JryCYwtvk'/>

<img src='https://i.loli.net/2020/11/26/dcktTpL9VSwoyjD.png' alt='dcktTpL9VSwoyjD'/>

Object adapter
- Relies on object composition to achieve adapter
- Can be used in multiple abstract classes

<img src='https://i.loli.net/2020/11/26/PkHVlGMw1cOTrFN.png' alt='PkHVlGMw1cOTrFN'/>

<img src='https://i.loli.net/2020/11/29/Cit7Lzo1gEN6TJe.png' alt='Cit7Lzo1gEN6TJe'/>

Participates
- Target
  - Defines the domain-specific interface that Client uses
- Client
  - Collaborates with objects conforming to the Target interface.
- Adaptee
  - Defines an existing interface that needs adapting.
- Adapter
  - Adapts the interface of Adaptee to the Target interface

Positive
- By introducing a new class, which acts as an adapter between the interface and the class, you avoid any changes to the existing code. That limits the scope of your changes to your software component and avoids any changes and side-effects in other components or applications.
- It increase the reusability and flexibility of code as it makes two incompatible interfaces compatible without changing their existing code.
- It deploys *Dependency Inversion Principle*, as *Adaptor* can be used to adapt the lower level implementation (*Adaptee*) details to make it comply with the *Target* interface. The higher-level layer (*Client*), however, remains unaware of the use of adapter pattern as the reference point for the higher layer still remains the *Target* interface which is left untouched.

Negative
- Sometimes if there are too many adaptations, the system is too complicated. For example, if client is call a class, but it adopts to another class inside, it will hard to debug.
- Since java can only extends one class, so it can extend only one *Adaptee* abstract class in *Class Adaptor Design Pattern*.
- The overall complexity of the code increases because you need to introduce a set of new interfaces and classes. Sometimes it’s simpler just to change the service class so that it matches the rest of your code.

### Facade

Provides a unified interface to a set of interfaces in a subsystem. Defines a higher-level interface that makes the subsystem easier to use.

<img src='https://i.loli.net/2020/11/26/JLkMc6YEawrH1gD.png' alt='JLkMc6YEawrH1gD'/>

Participates
- Facade
  - Knows which subsystem classes are responsible for a request.
  - Delegates client requests to appropriate subsystem objects.
- Subsystem classes
  - Implement subsystem functionality.
  - Handle work assigned by the Façade object
  - Have no knowledge of the facade; they keep no references to it.

Example

<img src='https://i.loli.net/2020/11/26/V6hupIsTtMkR54o.png' alt='V6hupIsTtMkR54o'/>

```java
Facade = facade = new Facade();
facade.drawCircle();
facade.drawSquare();
```

Positive
- Simplify the usage of an existing subsystem by defining your own interface
- Shields clients from subsystem components, reduce the number of objects that clients deal with, as well as reduce louping within system. So that it will make the subsystem easier to use.
- Promote weak coupling between the subsystem and the clients
  - Vary the components of the subsystem without affecting its clients
  - Reduce compilation dependencies (especially for large systems) – when subsystem classes change
- It provides an entry point to each subsystem level if you want to layer your subsystem.

Negative
- Does not prevent applications from using subsystem classes if they need to. Choice between ease of use and flexibility.
- In future development, if structure of the subsystem changes then it will require subsequent change to the *Facade* and client methods. This violates *Open-closed Principle*.

### Decorator

Attach additional responsibilities to an object dynamically (flexible alternative to subclassing for extending functionality)

<img src='https://i.loli.net/2020/11/26/pTH56an9VGFR38v.png' alt='pTH56an9VGFR38v'/>

Participates
- Component
  - Defines the interface for objects that can have responsibilities added to them dynamically
- Concrete Component
  - Defines an object to which additional responsibilities can be attached
- Decorator
  - Maintains a reference to a Component object and defines an interface that conforms to Component's interface.
- Concrete Decorator
  - Adds responsibilities to the component

Example

<img src='https://i.loli.net/2020/11/29/YDuvaZ2q4wRXUFL.png' alt='YDuvaZ2q4wRXUFL'/>

Positive
- More flexibility and less complexity than static inheritance
  - Can add and remove responsibilities to objects at run-time
  - Inheritance requires adding new class for each responsibility (increase complexity)
- Avoids feature-laden (heavily loaded) classes high up in the hierarchy
  - Defines a simple class and add functionality incrementally with Decorator objects – applications do not need to have un-needed features
  - You can define new kinds of Decorators independently from the classes of objects they extend, even for unforeseen extensions

Negative
- Decorator and its component are not identical, thus shouldn’t rely on object identity when you use decorator and test for object types will fail.
- Many little objects
  - Can become hard to learn and debug when lots of little objects that look alike
  - Still not difficult to customize by those who understand them

## Behavioral Patterns

- Concerns with algorithms and the assignment of responsibilities between objects

### Strategy

Define a family of algorithms, encapsulate each one, and make them interchangeable (let algorithm vary independently from clients that use it)

<img src='https://i.loli.net/2020/11/25/ptD37YaFVbev2df.png' alt='ptD37YaFVbev2df'/>

Participates
- Strategy
  - Declares an interface common to all supported algorithms Used by context to call the algorithm defined by Concrete Strategy
- Concrete Strategy
  - Implements the algorithm using the Strategy interface
- Context
  - Is configured with a ConcereteStrategy object Maintains a reference to a Strategy object May define an interface that lets Strategy access its data

Example

<img src='https://i.loli.net/2020/11/29/HJGtwCTjZiY79o5.png' alt='HJGtwCTjZiY79o5'/>

```java
Composition composition = new Composition(new SimpleCompositor());
composition.repair();
```

Positive
- Family of related algorithms (behaviors) for context to reuse
- Alternative to sub-classing, enhance extensibility
- Strategies eliminate conditional statements
- Provide choice of different implementation of the same behavior

Negative
- Clients must be aware of different strategies - Understand how strategies differ
- Communicate overhead between Strategy and Context - Strategy interface is shared by all Concrete Strategy classes whether the algorithms they implement are trivial or complex
- Increased number of objects in an application - Can be reduced by implementing strategies as stateless objects that context can share

### State

Allow an object to alter its behaviors when its internal state changes. The object will appear to change to its class

<img src='https://i.loli.net/2020/11/25/LM2eJGjr8oVlbv7.png' alt='LM2eJGjr8oVlbv7'/>

Participates
- State
  - Defines an interface for encapsulating the behavior associated with a certain state of the Context
- Concrete State
  - Each subclass implements a behavior associated with a state of the Context
- Context
  - Defines the interface of interest to clients
  - Maintains an instance of a ConcreteState subclass that defines the current state

Example

<img src='https://i.loli.net/2020/11/26/GFjwL8hrvzQxgbS.png' alt='GFjwL8hrvzQxgbS'/>

Positive
- Encapsulate the transition rules. The client does not need to know details about implementation to transit between different states.
- It minimizes conditional complexity, eliminating the need for `if` and `switch` statements in objects that have different behavior requirements unique to different state transitions.
- Permits states to be shared, so that it enhance reusability of code
- It improves Cohesion since state-specific behaviors are aggregated into *Concrete State* classes, which are placed in one location in the code.

Negative
- Does require that all the states have to have their own objects
- Applying the pattern can be overkill if a state machine has only a few states or rarely changes.
- It requires a lot of code to be written. Depending on how many different state transition methods are defined, and how many possible states an object can be in, there can quickly be dozens or more different methods that must be written.
- It violates *Open-closed Principle*, since it require modification of existing code if need to add a new *Concrete State*.

### Observer

Define a one-to-many dependency between objects so that when one object changes, all its dependents are notified and updated automatically

<img src='https://i.loli.net/2020/11/26/cTsjVDAJpt6RlQ8.png' alt='cTsjVDAJpt6RlQ8'/>

Participates
- Subject
  - Knows its observers. Any number of observer objects may observe a subject.
  - Provides an interface for attaching and detaching observer objects
- Observer
  - Defines an updating interface for objects that should be notified of changes in a subject
- Concrete Subject
  - Stores state of interest to ConcreteObserver objects Sends notifications to its observers when its state changes
- Concrete Observer
  - Maintains a reference to a ConcreteSubject object Stores state that should stay consistent with the subject’s.
  - Implements the observer’s updating interface to keep its state consistent

Example

<img src='https://i.loli.net/2020/11/26/PjMiHbpWZz4c8kY.png' alt='PjMiHbpWZz4c8kY'/>

Positive
- It supports the principle of *low coupling* between objects that interact with each other, as *Subject* only knows its *Observers* through the *abstract Observer* class (it doesn’t know any *concrete observer*)
- It allows sending data to other objects effectively and automatically without any change in the *Subject* or *Observer* classes
- *Observers* can be added/removed at any point in time

Negative
- *Observers* have no knowledge of each other’s presence, so they can be blind to the cost of changing the subject
- An innocent operation on the subject may cause a cascade of updates to *Observers* and their dependents. This invokes cyclically-dependent modularization, which may break the system.
- If the number of registered observers is very high, it would be a huge amount of computing time can be wasted by the observer system

### Memento

Without violating encapsulation, capture and externalise an object's internal state so that the state can later be restored to this state

<img src='https://i.loli.net/2020/11/26/W26iYETtR7ZgOyd.png' alt='W26iYETtR7ZgOyd'/>

Participate
- Memento
  - Stores internal state of the Originator object. The memento may store as much or as little of the originator's internal state as necessary at its originator’s discretion
  - Protects against access by objects other than the originator. Mementos have effectively two interfaces
    - Caretaker: sees a narrow interface to the Memento — it can only pass the memento to other objects
    - Originator: sees a wide interface, one that lets it access all the data necessary to restore itself to its previous state
- Originator
  - Creates a memento containing a snapshot of its current internal state
  - Uses the memento restore its internal state
- Caretaker
  - Responsible for the memento’s safekeeping
  - Never operates on or examines the contents of a memento

Example

<img src='https://i.loli.net/2020/11/29/4JXIRe7xbNAZEw1.png' alt='4JXIRe7xbNAZEw1'/>

Positive
- Providing a way of recording the internal state of an object in a separate object without violating rule of design pattern
- Preserve data encapsulation by protecting other objects from potentially complex *Originator* internals, so that client no need to care algorithm.
- Simplifies *Originator* by giving responsibility of *Memento* storage among the *Caretakers*.
- Helps to restore back an object to its previous stat or maintain a history of states of an object.

Negative
- Saving and restoring state may be time consuming.
- It might be expensive is the *Originator* must copy large amounts of information to store in the *Memento*
- When managing a multiple number of *Originators*, need to maintain which *Memento* is for which *Originator*

# Testing

## Type of testing

- Unit testing
  - Verify functionality of software components independent of the whole system
- Integration testing
  - Verify interactions between software components
- System Testing
  - Verify functionality and behavior of the entire software system
  - Includes security, performance, reliability, and external interfaces
- Acceptance testing
  - Verify desired acceptance criteria are met from the users point of view

## Black box testing

- The internals of the software system is unknown
- Only inputs to the system are controlled, and outputs from the system are measured
- Specification-based testing
- May be the only choice to test libraries without access to internal

## White box testing

- The internals of the software system are known
- The internal structure is tested directly
- Unit, integration, system testing

## JUnit

### Constructs

- JUnit test
  - A method only used for testing
- Test suite
  - A set of test classes to be executed together
- Test annotations
  - Define test methods (e.g. `@Test`, `@Before`)
  - JUnit uses the annotations to build the tests
- Assertion methods
  - Check expected result is the actual result
  - e.g. `assertEquals`, `assertTrue`, `assertSame`

### Annotation

- `@Test` - Identifies a test method
- `@Before` - Execute before each test
- `@After` - Execute after each test
- `@BeforeClass` - Execute once, before all tests in this class
- `@AfterClass` - Execute once, after all tests in this class

### Assertion

```java
import static org.junit.Assert.assertEquals;
import org.junit.Test;
import mypackage.Calculator;

class CalculatorTest {
    Calculator calculator

    @Before
    void setup() {
        calculator = new Calculator();
    }

    @Test
    void addition() {
        int expected = 2;
        int actual = calculator.add(1, 1);
        assertEquals(“Expected value != actual”, expected, actual);
        assertTrue("Cannot do 1+1", expected == actual);
    }
}
```

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

# Code Reviews

## Formal Review (Fagan Inspection)

- Describe program development process in terms of operations
- Define `entry` and `exit` criteria for all operation
- Specify objectives for the inspection process to keep the team focused on one objective at a time
  - Operation: Overview, Preparation, Inspection, Rework, Follow-up
  - Objective: Communications, Education, Find errors, Fix errors, Ensure all fixes are applied correctly
- Classify errors by type, rank by frequency, identify which types to spend most time looking for
- Analyse results and use for constant process improvement

Operations
- Planning
  - Preparation of materials
  - Arranging of participants
  - Arranging of meeting place
- Overview
  - Group education of participants on review materials
  - Assignment of roles
- Preparation
  - Participants review item to be inspected and supporting material to prepare for the meeting, noting any questions or possible defects
  - Participants prepare their roles
- Inspection meeting
  - Actual finding of defect
- Rework
  - Rework is the step in software inspection in which the defects found during the inspection meeting are resolved by the author, designer or programmer. On the basis of the list of defects the low-level document is corrected until the requirements in the high-level document are met.
- Follow-up
  - In the follow-up phase of software inspections all defects found in the inspection meeting should be corrected. The moderator is responsible for verifying that this is indeed the case. They should verify that all defects are fixed and no new defects are inserted while trying to fix the initial defects.

## Informal Review

- Formal reviews are far more effective than informal reviews
- Informal reviews are far more convenient than formal reviews
- e.g. Pair-programming, “Over the shoulder”, Walkthroughs, Presentations, Self-guided reviews, Checklists

## Semi-formal Review (Design by Contract DbC)

Purpose
- Have a clear purpose for the review
- Identify all relevant project specifications
- Identify how the specifications can be verified
- Identify who the relevant stakeholders are

Change List Review Challenges
- Size
  - The more there is to read, the more scope there is to miss problems
  - Many small code reviews are more manageable (somewhat like unit tests vs blackbox system tests)
  - A large code review can take so much time that special planning is needed
  - May need to place limits on acceptable sizes for review
- Scope
  - Changes that affect many processes may need more reviewers for the required technical knowledge
  - May sometimes be helped by multiple, smaller change lists
  - May bring specifications from different processes into conflict, requiring management review
    - May also be triggered by small changes with big impacts, such as changing JDK version
- Complexity
  - Fast, efficient, code may be hard to read and hard to understand
  - Is the code complexity, thus review complexity and maintenance complexity, worth the improvement?
  - Does the complexity affect maintainability and testability?
- Confusion
  - What is the change meant to be for?
  - May be doing too many unrelated things
  - May be making unnecessary changes
  - May even be about a disagreement between colleagues
  
  
  # Propositional Logic

1.  The truth value of $(F \land G)$ under assignment  $\alpha$ is equal to the **maximum** of the truth value of F under $\alpha$ and the truth value of G under $\alpha$.

    False, $tv((F \land G), \alpha) = \min\{tv(F,\alpha), tv(G, \alpha)\}$

2.  Let F be the propositional formula $(p \rightarrow q)$, and let G be the propositional formula $(q \rightarrow p)$. Why is F not a logical consequence of G (i.e. $G \vDash F$)?

    when p = 1, q = 0, $F (1 \rightarrow 0) = 0, G = (0 \rightarrow 1) = 1$

3.  If $(F \land \neg G)$ is statisfiable,  then G is not a logical consequence of F.

    True, if $(F \land \neg G)$ is statisfiable, it means there exist an assignment to make $tv(F \land \neg G) = 1$, i.e. F = 1 and G = 0. However, for $G$ to be a logical consequence of $F$, every assignment that makes $F$ true should make $G$ true. So $G$ is not a logical consequence of $F$.

4.  Compute $tv((F \rightarrow G), \alpha)$ and $tv((F \leftrightarrow G), \alpha)$
    $$
    \begin{align}
    tv((F \rightarrow G), \alpha) &= tv((\neg F \lor G), \alpha) \\
    &= max\{\textcolor{red}{tv(\neg F, \alpha)}, \textcolor{blue}{tv(G, \alpha)}\} \\
    &= max\{\textcolor{red}{1 - tv(F, \alpha)}, \textcolor{blue}{tv(G, \alpha)}\} \\
    tv((F \leftrightarrow G), \alpha) &= tv((\textcolor{red}{(F \rightarrow G)} \land \textcolor{blue}{(G \rightarrow F)}), \alpha) \\
    &= min\{\textcolor{red}{tv((F \rightarrow G), \alpha)}, \textcolor{blue}{tv((G \rightarrow F), \alpha)}\} \\
    &= min\{\textcolor{red}{max\{1 - tv(F, \alpha), tv(G, \alpha)\}}, \textcolor{blue}{max\{1 - tv(G, \alpha), tv(F, \alpha)\}}\} \\
    &= 1 - |tv(F, \alpha) - tv(G, \alpha)|
    \end{align}
    $$

5.  How to show that F is not a logical consequence of $\{E_1, ..., E_k\}$? 

    F is not a logical consequence if it is in the following sitution 

    -   For propositional logcial formulas, there is an assignment $\alpha$ such that $\alpha(E_i) = 1$ and $\alpha(F) = 0$
    -   For predicate logical formula, there is a structure $\mathbb{A}$ and an assignment $\alpha$ such that truth-value of E under $\mathbb{A}$ and $\alpha$ is 1 while the truth-value of F under $\mathbb{A}$ and $\alpha$ is 0.

    In both case, you should find specific concrete formula E, F with these properties.
