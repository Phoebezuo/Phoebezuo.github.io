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

优点
- 一个调用者想创建一个对象，只要知道其名称就可以了。
- 扩展性高，如果想增加一个产品，只要扩展一个工厂类就可以。
- 屏蔽产品的具体实现，调用者只关心产品的接口。
- Flexibility: subclasses get a hook for providing an extension to an object
- Connects parallel class hierarchies

缺点
- 每次增加一个产品时，都需要增加一个具体类和对象实现工厂，使得系统中类的个数成倍增加，在一定程度上增加了系统的复杂度，同时也增加了系统具体类的依赖。
- Can require subclassing just to get an implementation

### Builder

Separate the construction of a complex object from its representation so that the same construction process can create different representations

<img src='https://i.loli.net/2020/11/25/Ot4SxHN96LP5uXU.png' alt='Ot4SxHN96LP5uXU'/>

Participates
- Builder
  - Specifies an abstract interface for creating parts of a Product object
- Concrete Builder
  - Constructs and assembles parts of the product by implementing the Builder interface
  - defines and keeps track of the representation it creates.
  - provides an interface (GetResult) for retrieving the product
- Director
  - Constructs an object using the Builder interface
- Product
  - Represents the complex object under construction.
  - ConcreteBuilder builds the product's internal representation and defines the process by which it's assembled
  - Includes classes that define the constituent parts, including interfaces for assembling the parts into the final result

Example

<img src='https://i.loli.net/2020/11/26/TgYycKSxUCVOb6R.png' alt='TgYycKSxUCVOb6R'/>

优点
- 建造者独立，易扩展。
- 便于控制细节风险。
- Gives flexibility that can be extended by implementing new subclasses of the Builder
- Isolates code of construction from implementation

缺点
- 产品必须有共同点，范围有限制。
- 如内部变化复杂，会有很多的建造类。
- Not completely generic, less useful in situations where variety of implementations is not high

### Singleton

Ensure a class only has one instance, and provide global point of access to it

<img src='https://i.loli.net/2020/11/26/6TcI1GsQUVEgmbA.png' alt='6TcI1GsQUVEgmbA'/>

Participate
- Defines an `instance()` operation that lets clients access its unique instance. `instance()` is a class operation
- May be responsible for creating its own unique instance

Example

<img src='https://i.loli.net/2020/11/26/KzSgEQOmwNYrlXn.png' alt='KzSgEQOmwNYrlXn'/>

优点
- 在内存里只有一个实例，减少了内存的开销，尤其是频繁的创建和销毁实例(比如管理学院首页页面缓存)
- 避免对资源的多重占用(比如写文件操作)

缺点
- 没有接口，不能继承，与单一职责原则冲突，一个类应该只关心内部逻辑，而不关心外面怎么样来实例化。

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

优点
- 性能提高。
- 逃避构造函数的约束。
- It hides the concrete product classes from the client, thereby reducing the number of names clients know about
- These patterns let a client work with application-specific classes without modification

缺点
- 配备克隆方法需要对类的功能进行通盘考虑，这对于全新的类不是很难，但对于已有的类不一定很容易，特别当一个类引用不支持串行化的间接对象，或者引用含有循环结构的时候。
- 必须实现 Cloneable 接口。
- Each subclass of prototype must implement the clone operation

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

Object adapter
- Relies on object composition to achieve adapter
- Can be used in multiple abstract classes
<img src='https://i.loli.net/2020/11/26/PkHVlGMw1cOTrFN.png' alt='PkHVlGMw1cOTrFN'/>

Participates
- Target
  - Defines the domain-specific interface that Client uses
- Client
  - Collaborates with objects conforming to the Target interface.
- Adaptee
  - Defines an existing interface that needs adapting.
- Adapter
  - Adapts the interface of Adaptee to the Target interface

Example - class adaptor

<img src='https://i.loli.net/2020/11/26/dcktTpL9VSwoyjD.png' alt='dcktTpL9VSwoyjD'/>

Example - Object adaptor

<img src='https://i.loli.net/2020/11/26/WPjx6Q9FbKV1CGg.png' alt='WPjx6Q9FbKV1CGg'/>

优点
- 可以让任何两个没有关联的类一起运行。
- 提高了类的复用。
- 增加了类的透明度。
- 灵活性好。

缺点
- 过多地使用适配器，会让系统非常零乱，不易整体进行把握。比如，明明看到调用的是 A 接口，其实内部被适配成了 B 接口的实现，一个系统如果太多出现这种情况，无异于一场灾难。因此如果不是很有必要，可以不使用适配器，而是直接对系统进行重构。
- 由于 JAVA 至多继承一个类，所以至多只能适配一个适配者类，而且目标类必须是抽象类。

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

优点
- 减少系统相互依赖。
- 提高灵活性。
- 提高了安全性。
- Simplify the usage of an existing subsystem by defining your own interface
- Shields clients from subsystem components, reduce the number of objects that clients deal with and make the subsystem easier to use.
- Promote weak coupling between the subsystem and the clients
  - Vary the components of the subsystem without affecting its clients
  - Reduce compilation dependencies (esp. large systems) – when subsystem classes change

缺点
- 不符合开闭原则，如果要改东西很麻烦，继承重写都不合适。
- Does not prevent applications from using subsystem classes if they need to. Choice between ease of use and flexibility.

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

<img src='https://i.loli.net/2020/11/26/bpDIPENykK7zZRV.png' alt='bpDIPENykK7zZRV'/>

优点
- 装饰类和被装饰类可以独立发展，不会相互耦合，装饰模式是继承的一个替代模式，装饰模式可以动态扩展一个实现类的功能。
- More flexibility and less complexity than static inheritance
  - Can add and remove responsibilities to objects at run-time
  - Inheritance requires adding new class for each responsibility (increase complexity)
- Avoids feature-laden (heavily loaded) classes high up in the hierarchy
  - Defines a simple class and add functionality incrementally with Decorator objects – applications do not need to have un-needed features
  - You can define new kinds of Decorators independently from the classes of objects they extend, even for unforeseen extensions

缺点
- 多层装饰比较复杂。
- Decorator and its component are not identical
  - Decorated component is not identical to the component itself - you shouldn’t rely on object identity when you use decorator
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

<img src='https://i.loli.net/2020/11/26/DxfPBcUAW2C5sT1.png' alt='DxfPBcUAW2C5sT1'/>

```java
Composition composition = new Composition(new SimpleCompositor());
composition.repair();
```

优点
- 算法可以自由切换。
- 避免使用多重条件判断。
- 扩展性良好。
- Family of related algorithms (behaviors) for context to reuse
- Alternative to sub-classing
- Strategies eliminate conditional statements
- Provide choice of different implementation of the same behavior

缺点
- 策略类会增多。
- 所有策略类都需要对外暴露。
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

优点
- 封装了转换规则。
- 枚举可能的状态，在枚举状态之前需要确定状态种类。
- 将所有与某个状态有关的行为放到一个类中，并且可以方便地增加新的状态，只需要改变对象状态即可改变对象的行为。
- 允许状态转换逻辑与状态对象合成一体，而不是某一个巨大的条件语句块。
- 可以让多个环境对象共享一个状态对象，从而减少系统中对象的个数。
- Removes case or if/else statements depending on state, and replaces them with function calls
- Makes the state transitions explicit
- Permits states to be shared

缺点
- 状态模式的使用必然会增加系统类和对象的个数。
- 状态模式的结构与实现都较为复杂，如果使用不当将导致程序结构和代码的混乱。
- 状态模式对"开闭原则"的支持并不太好，对于可以切换状态的状态模式，增加新的状态类需要修改那些负责状态转换的源代码，否则无法切换到新增状态，而且修改某个状态类的行为也需修改对应类的源代码。
- Does require that all the states have to have their own objects

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

优点
- 观察者和被观察者是抽象耦合的。
- 建立一套触发机制。
- Abstract coupling between Subject and Observer
  - Subject only knows its Observers through the abstract Observer class (it doesn’t know the concrete class of any observer)
- Support for broadcast communication
  - Notifications are broadcast automatically to all interested objects that subscribe to the Subject
  - Add/remove Observers anytime

缺点
- 如果一个被观察者对象有很多的直接和间接的观察者的话，将所有的观察者都通知到会花费很多时间。
- 如果在观察者和观察目标之间有循环依赖的话，观察目标会触发它们之间进行循环调用，可能导致系统崩溃。
- 观察者模式没有相应的机制让观察者知道所观察的目标对象是怎么发生变化的，而仅仅只是知道观察目标发生了变化。
- Unexpected updates
  - Observers have no knowledge of each other’s presence, so they can be blind to the cost of changing the subject
  - An innocent operation on the subject may cause a cascade of updates to Observers and their dependents

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

<img src='https://i.loli.net/2020/11/26/IAyErQfczBkT2KS.png' alt='IAyErQfczBkT2KS'/>

优点
- 给用户提供了一种可以恢复状态的机制，可以使用户能够比较方便地回到某个历史的状态。
- 实现了信息的封装，使得用户不需要关心状态的保存细节。
- Preserve encapsulation boundaries
  - By protecting other objects from potentially complex originator internals
- Simplifies Originator
  - Originator keeps the versions of internal state that clients have requested

缺点
- 消耗资源。如果类的成员变量过多，势必会占用比较大的资源，而且每一次保存都会消耗一定的内存。
- Might be expensive
  - If the originator must copy large amounts of information to store in the memento or,
  - If clients often create and return mementos to the originator

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
