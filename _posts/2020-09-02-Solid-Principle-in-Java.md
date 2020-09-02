---
layout:     post
title:      Solid Principle in Java
date:       2020-09-02
summary:    Summary of SOLID principle in Java 
categories: Java SOLID 
---


SOLID is a software design acronym that incorporates ﬁve principles to assist with designing ﬂexible, maintainable and robust software. These typically push for application structure to be contain types which can act independently, depend on abstractions and can be easily refactored.

![83jvHpV2cgn6xX5](https://i.loli.net/2020/09/02/83jvHpV2cgn6xX5.png)

## Single Responsibility Principle 单一职责

A class should be **assigned a single responsibility, avoiding a class performing more roles than it should**. If you ﬁnd that you are assigning multiple roles to a class you can break the these roles into separate classes.

如果你把多个功能放在同一个类中，功能之间就形成了关联，改变其中一个功能，有可能中止另一个功能，这时就需要新一轮的测试来避免可能出现的问题，非常耗时耗力。

![ONGDZiREK65sUxH](https://i.loli.net/2020/09/02/ONGDZiREK65sUxH.png)

例子中， `Rectangle` class 违反了SRP原则。`Rectangle` class具有两个职责，如果其中一个改变，会影响到两个应用程序的变化。

## Open-closed Principle 开闭原则

Open-Closed principle outlines that **an element is open for extension but closed for modiﬁcation**. Extension can be typically inferred as class inheritance but it is also possible to extend a class through composition or traits (interface with default method).

通过增加代码来扩展功能，而不是修改已经存在的代码。我们应该以插件式的方式来编写类和模块。如果我们需要额外的功能，我们不应该修改类，而是能够嵌入一个提供这个额外功能的不同类。

比如，代码修改前为

```java
public boolean sendByEmail(String addr, String title, String content);
Public boolean sendByFax(String addr, String content);
```

当我们需要在其他地方调用上面的信息

```java
sendByEmail(addr, title, content);
sendByFax(addr, content);
```

但是当我们想增加一种方式发送，比如`sendByWechat`, 那我们还得在调用它的地方进行修改。更好的办法就是同一`send`的方法，但是分成不同的`class`.

```java
public interface Send {
    void send(String addr, String title, String content);
}
public class SendByEmail implements Send {
    public void send(String addr, String title, String content) {
        System.out.println("SendByEmail");
    }
}

public class SendByWeChat implements Send {
    public void send(String addr, String title, String content) {
        System.out.println("SendByWeChat");
    }
}
```

## Liskov Substitution Principle 里氏替换原则

This principle infers that **types should be replacable with instances of their subtypes**. It asserts that a class should utilise an interface and allow for an instance of that interface to be substituted.

子类可以扩展父类的功能，但不能改变父类原有的功能。

比如一个interface `Bike`， 他有`pedal(), handBrake()`的方法。假如山地自行车和古董自行车同时`implements Bike`， 那么古董自行车就会出现问题，因为古董自行车没有手刹。

```java
interface Bike {
    void pedal()
    void handBrake()
}

// 山地自行车有手刹功能
class MountainBike implements Bike {
    void pedal() { /* pedal implementation */ }
    void handBrake() { /* hand brake implementation */ }
    void changeGear() { /* change gear implementation */ }
}

// 古董自行车有手刹功能
class ClassicalBike implements Bike {
    void pedal() { /* pedal implementation */ }
    void handBrake() { /* no implementation */ }
}
```

那么我们修改一个interface，让它只包含子类共同的功能就可以了

```java
interface Bike {
    void pedal()
}

class MountainBike implements Bike {
    void pedal() { /* pedal implementation */ }
    void handBrake() { /* hand brake implementation */ }
    void changeGear() { /* change gear implementation */ }
}

class ClassicalBike implements Bike {
    void pedal() { /* pedal implementation */ }
}
```

## Interface Segregation Principle 接口隔离原则

Interface segregation asks to **break up large interface types**. Designing the application to use many client-speciﬁc interfaces over large general purpose interface. Each interface should focus on the functionality required instead of a large interface providing methods that some objects may never implement.

一旦interface变得太大，我们需要将其拆分为更具体的小接口, 否则一旦某个大的interface更新，所有的subclass都需要被迫更新。

比如一辆砖头，它可以用来盖房子，也可以用来打人。

```java
public interface BrickInterface {
    void buildHouse();
    void defense();
}
```

但是不是每个人都是工人，需要用砖头盖房子。我们可以把这个大的interface拆成两个小的interface，让他们有各自的功能。

```java
public interface BuildHouse { void build(); }
public interface StrickCompetence { void defense(); }
public class Brick implement BuildHouse, StrickCompetence { /* some codes */ }
```

那么普通大众和建筑工人可以用自己特有的interface。

```java
// in Worker.java
brick.build();

// in Person.java
brick.defense();
```

## Dependency Inversion Principle 依赖倒置原则

Dependency inversion principle places the **constraint that a type should never depend on another concrete type**. Allow your types to depend on abstractions, the type binding can be updated and substituted when refactoring.

依赖关系应该是自上而下，也就是上层模块依赖于下层模块，而下层模块不依赖于上层。因为越底层的模块相对就越稳定，改动也相对越少，而越上层的改动会很频繁，所以当上层发生变更时，不会影响到下层，降低变更带来的风险。

例如，John最开始只开Toyota。。

```java
class Driver {
    private String name;
    public Driver(String name) { this.name = name; }
    public void drive(Toyota toyota) { /* some code */ }
}

class Toyota {
    public void run() { /* some code */ }
}

// in main method 
Driver John = new Driver("John");
John.drive(new Toyota());
```

但是John之后想换一辆宝马，我们只能更改第四行的`Toyota` class，需要使两个操作的class都依赖于抽象，而不是互相依赖。

```java
interface AbstractCar { public void run(); }
class Toyota implements AbstractCar { public void run(); }
class BMW implements AbstractCar { public void run(); }

interface AbstractDriver { public void driver(); }
class Driver implements AbstractDriver { /* some code */ }

// in main method 
Driver John = new Driver("John");
John.drive(new Toyota());
John.drive(new BMW());
```

