---
layout:     post
title:      Summary Note for Java 
date:       2020-08-21
summary:    Summary notes for Object-Oriented Programming 
categories: Java Programming Object-Oriented
---

## Compilation

- a byte is made up of 8 bits 
- your code is compiled to form bytecode(.class file), then JVM then convert this Bytecode into machine code in order to communicate with the underlying system. 
- python source code is interpreted by a python interpreter and code is **compiled and executed at runtime** 
- C is **compiled into a set of machine instructions** and can be executed by the machine. 

## Printing 

``` java
int a = 2;
String b = "hello";
float c = 3.45;
System.out.printf("%d %s %f", a, b, c);
```

- %d --> integer (base 10)
- %o --> octal (base 8)
- %x --> hexadecimal (base 16)
- %f -->  float 
- %s --> string
- %%, \% --> print a percent sign 

``` java
int x = 2;
System.out.println(++x); // 3
System.out.println(++x); // 4

int i = 0;
while(i < 10) {
	int j = i++; // j = 0, i = 1;
  	System.out.println(i + " " + j); // 1 0; 2 1; ...; 10 9
}
```

## Converting

``` java
// String to integer
int x = Integer.parseInt("1");

// int to String 
String s = String.valueOf(1);

// char to string 
String s = Character.toString(c);

// array to string 
String s = Arrays.toString(array);
```

### Type Casting

Although we cannot change the type of the variable after declaring it, we can use it in operations with certain types 

``` java
int x = 5;
float z = 2.0;
z = z + x; // implicit casting, compiler recognnises the type of z as a float 
```

## Data Type

| Name    | Memory   | Type      | Default  |
| ------- | -------- | --------- | -------- |
| boolean | 1 byte   | primitive | False    |
| Byte    | 1 byte   | primitive | 0        |
| short   | 2 byte   | primitive | 0        |
| Char    | 2 byte   | primitive | '\u0000' |
| Int     | 4 byte   | primitive | 0        |
| float   | 4 byte   | primitive | 0.0f     |
| Long    | 8 byte   | primitive | 0L       |
| double  | 8 byte   | primitive | 0.0d     |
| string  | variable | object    | null     |

Reference types hold an address pointing to the area of memory containing the data. It is not storing the value directly but rather a **REFERENCE** to it. That is why comparison between Strings as shown above need a speciﬁc .equals operation rather than ==, since == compares direct contents of the **address** whereas .equals compares that **content** within the address

``` java
String s1 = "Meow";
String s2 = new String("Meow");
System.out.println(s1 == s2); // false
System.out.println(s1.equals(s2)); // true
```

## Scanner

``` java
import java.util.Scanner;
import java.util.ArrayList;

public class UsingScanner {
    public static void main(String[] args) {
        ArrayList<String> lines = new ArrayList<String>();
        Scanner scan = new Scanner(System.in);
        // the new keyword on instatiation creates an instant 
        // of the object using the called constructor.
        // which defines a blueprint of how to make and use a scanner
        while (scan.hasNextLine()) {
            String line = scan.nextLine();
            lines.add(line);
        }

        for (String s: lines) {
            System.out.println(s);
        }
    }
}
```

## Defensive Programming

``` java
// 1D array: check for null and empty array
// 2D array: also check for null array of array 
public static void printSum(int[][] numbers) {
    if (numbers == null || numbers.length == 0) {
        return;
    } else if (numbers[0] == null) {
        return;
    } else {
        int sum = 0
            // for loop has 3 parts: variable, condition, updates 
            for (int i = 0; i < numbers.length; i++) {
                for (int j = 0; j < numbers[i].length; j++) {
                    sum += numbers[i][j];
                }
            }
        System.out.println("The total sum is: " + sum);
    }
}
```

## Array

An array is a contiguous block of memory that holds a fixed number of values of the same type. 

``` java
String[] strArray = new String[10]; // define the size in 2nd bracket
// new keyword is used to tell the compiler to create space for a new string array.
// reference type arrays DO NOT contain a string, but a reference to a string.

// initialisation
type[]<name> = new type[size];
// method 1
int[] numbers = new int[] {1,2,3,4};
// method 2
int[] numbers = new int[4]; // initialising 4 references 
numbers = {1,2,3,4};
```

a memory address is the size of the cpu address size. E.g. X86-64 CPU (Intel, AMD) has an address size of 8 bytes. (64 / 8 = 8)

### Multi Dimensional Array

``` java
int[] arr = {
  				{1,2,3,4,4,4,4,4,4},
  				{1,2,3,4,4,4,4,4,4}
						}; 

// method 1
for (int i = 0; i < arr.length; i++) { 
	for (int j = 0; j < arr[i].length; j++) {
    	System.out.println(arr[i][j]);
  	}
}

// method 2 
String[] strings = new String[] {"a","b","c"};
for (String s: strings) {
    System.out.println(s);
}

int[][] arr = new arr[2][2]; // matrix type
int[][] arr = new arr[2][]; // vector type
```

## String

- Each time we use += with the String type we are creating a new string. 

- The String class is immutable

``` java
String cat = "Meow";
cat += " , says the cat"
```

### String Builder

- it can resize and append very efficiently 

``` java
StringBuilder sb = new StringBuilder();
append(Stirng str): StringBuilder
charAt(int index): char
indexOf(String str): int 
length(): int
toString(): String 
```

## Classes

- reference type, the type of an object variable is its class 
- Objects are instance of a particular class. 
- a class is a **Blueprint** of an object
- it defines the **attributes** and **behaviours** of the object. 
- the main objective of a class is to able to reuse the data we store in an efficient and easy manner

### Constuctor 

- what is the difference between constructor and a normal method? 
  - The return type of a constructor is defined as the object of the class being created, hence there is no need to specify the return type
- every class in java has a constructor even if it is not explicity defined. 
- extending the class, we can write our own constructor 

``` java
public class Coffee {
    private String name;
    private String type;
    private boolean isUsed;

    public Coffee(String name; String type) {
        this.name = name;
        this.type = type;
        this.isUsed = false;
    }
}
```

### Static Methods

- a method is a set of instructions bound to an object 
- for static method, the object is the class itself 
- The **this** keyword allows the programmer to refer to the object while **within an instance method** context. It refers to the current calling object 
- We **cannot** use the keyword **within a static context**. It is unable to refer to the calling object.

``` java 
public static double getArea(r) {
    return r * r * math.pi;
}

public static void main(String[] args) {
    double area = getArea(3);
}
```

### Non-static Methods (instance)

- static methods belong to the class 
- Non-static methods belong to the instance of the class object 
- a way to know when to use static methods, is to check whether this method will be called regardless of any object being created 

``` java
public class Circle {
    public double r;

    public Circle(double r) {
        this.r = r;
    }

    public double getArea() {
        return r * r * math.pi;
    }

    public static void main(String[] args) {
        Circle c = new Circle(3);
        double area = c.getArea();
    }
}
```

example 1 

``` java
public class Postcard {
    String sender;
    String receiver;
    boolean received;

  // this static method is attempting to utillise an instance variable. what is the issue? 
  // because it isn't referring to an object
  // instance methods are not allowed in this context 
  public static boolean inTransit() {
      return !received;
  }
}
```

example 2 

``` java
public class Postcard {
    String sender;
    String receiver;
    boolean received;
  
    public boolean inTransit() {
        return !received;
    }

    // this static method is attempting to utillise an instance method 
    // attached to an object. is there an issue?
    // nope! there is an object instantiated and we are able to utilise method 
    public static boolean hasArrived(Postcard p) {
        if (!p.inTransit()) {
            return true;
        } else {
            return false;
        }
    }
}
```

example 3 

``` java
public class Postcard {
    String sender;
    String receiver;
    boolean received;
  
      // we have an instance method invoking a static method 
      // while also using this keyword. is this correct? 
      // yes! we are just passing the instance to a static function. 
      // this is no difference from what we have done before but we are using this keyword
      public boolean alreadyArrived() {
          return hasArrived(this);
      }

      public static boolean hasArrived(Postcard p) {
          if (!p.inTransit()) {
              return true;
          } else {
              return false;
          }
      }
}
```

### Getters and Setters

- why we make variable private (aka, only allows access within the same class)? 
  - customisation, safety and more control

## Unified Modelling Language

UML offers a the ability to purely design a system in how objects will interact with each other as well as describing interaction a user may have with the system.

### Abstract Class 

- italicised font shows that it is an abstract class  <<abstract>>
- we also show polymorphic method as italicised (abstract class & interface)

### Interface

- specify the stereotype in UML to be interface   <<interface>>
- the relationship link is dashed line 

## File IO

- reader and writer classes are character stream classes 
- difference between a file and a stream 
    - no finite size or beginning 
    - no concept of beginning or end in a stream 
    - Recall System.out is a stream 

### Reading from Files

``` java
import java.util.Scanner;
import java.io.File;
import java.io.FileNotFoundException;

public class ReadingFile {
	public static void main(String[] args) {
		File f = new File("numbers.txt");
        
		try {
			Scanner reader = new Scanner(f);
            
			while(reader.hasNextInt()) {
				int n = reader.nextInt();
				System.out.println(n);
			}
            
		} catch (FileNotFoundException e) {
            System.err.println("File not found");
            // we can also print the error
            e.printStackTrace();
            // it shows the trace or history before the error occured
		}
	}
}

```

### Writing to Files

``` java
import java.io.PrintWriter;
import java.io.File;
import java.io.FileNotFoundException;

public class WritingFile {
	public static void main(String[] args) {
		try {
			File f = new File("new_numbers.txt");
			PrintWriter writer = new PrintWriter(f);
			for(int i = 0; i < 10; i++) {
				writer.println(i);
			}
			writer.flush(); // save from 0 - 9
			for(int i = 10; i < 20; i++) {
				writer.println(i);
            }
			writer.close(); // save from 10 to 19
		} catch (FileNotFoundException e) {
			e.printStackTrace();	
		}		
	}
}
```

## Binary IO

- Input stream and output stream classes are byte stream classes 

### Reading

``` java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class BinaryWriter {
  
    public static int convert(byte[] b) {
        return (b[3] & 0xFF) |
            ((b[2] & 0xFF) << 8) |
            ((b[1] & 0xFF) << 16) |
            ((b[0] & 0xFF) << 24);
    }
    
    public static void main(String[] args) {
        try {
            FileInputStream f = new FileInputStream("file.bin");
            byte[] buffer = new byte[4];
            f.read(buffer);
            int v = convert(buffer);
            System.out.println(v);
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### Writing 

``` java
import java.io.FileOutputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class BinaryWriter {
  
    public static byte[] convert(int v) {
        byte[] b = new byte[4];
        b[0] = (byte) (v >> 24);
        b[1] = (byte) (v >> 16);
        b[2] = (byte) (v >> 8);
        b[3] = (byte) v;
        return b;
    }

    public static void main(String[] args) {
        try {
            FileOutputStream f = new FileOutputStream("file.bin");
            int v = 50;
            byte[] buffer = convert(v);
            f.write(buffer);
            f.close();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## Abstract Data Type (ADT)

- primitive type --> not an ADT
- reference type --> is an ADT

### ArrayList

``` java
ArrayList<T> name = new ArrayList<T>();
add(E e): boolean
add(int index, E element): void
contains(Object o): boolean
get(int index): E
indexOf(Object o): int 
remove(int index): E
set(int index, E element): E
size(): int 
toArray(): Object[]
```

### Map

``` java
Map<K, V> name = new Map<K, V>();
containsKey(Object key): boolean
containsValue(Object value): boolean
get(Object key): V
put(K key, V value): V
remove(Object key): V
for (Type each: name.keySet()) {
      K key = each.toString();
      V value = name.get(each).toString();
      System.out.println(key + " " + value);
}
```

### Set

``` java
Set<T> name = new Set<T>;
```

## Checked Operation VS Unchecked Operation 

### Checked Operation 

- compiler checks for errors in the code and ensures that the types we are using are valid and not being muddled
- e.g. FileNotFoundException

### Unchecked Operation 

- assumption of the compiler that the user knows to a degree what they are doing in areas of code where exceptions can occur
- e.g. RuntimeException 

## Inheritance 

- What does inheritance offer? 
  - attribute and method reusability 
  - defining sub-type methods 
  - overriding inherited methods 
  - type information 
- what does protected mean? (Encapsulation)
  - Is only accessible within the class 
  - attributes and methods will be accessible by all subtypes 
  - allows single definition of an attribute instead of multiple 
- some factors to consider 
  - superclass does not know about its subclass 
  - private is not inherited, only protected and public 
  - only inherit from 1 class 
- Polymorphism 
    - idea of having the same interface/design to represent diﬀerent types of objects and being able to manipulate this to represent them under a branch

### Abstract Class

- cannot be instantiated, but can specify methods subtypes must define 
- the main case for abstract is that we have some type that we do not want instantiate but is a generalisation of many other types 

### Abstract methods 

- only declare an abstract method in only abstract classes 
- When declearing an abstract method, we do not define a method body

### Interface 

- Cannot use instances variables, only static and constant (have the final modifier applied to them) in interface  
- do not (typically) provide a method definition 
- cannot instantiate them 
- can be implemented multiple times 

``` java
public interface move {
  	public void move(double hours);
  // an interface is not a class, it defines a group of methods for implementers to define 
}

// sinve they both implement Move interface, we can treat them as a Move type
public class Dog implements Move {
  ...
}

public class Dophin implements Move {
  ... 
}

public class MovingAnimals {
    public static void main(String[] args) {
        Dog dog = new Dog();
        Dolphine dolphine = new Dolphin();
        Move[] movingAnimals = {dog, dolphine};

        // if they of type Move we are guaranteed to be able to use move() method 
        for (Move m: movingAnimals) {
            m.move(1.0);
        }
    }
}
```

### Default Method in Interface

``` java
interface Container {

    public void pour(double litres);

    public default pourInto(Container container, double litres) {
        if (container != null) {
            pour(liters);
            container.fill(litres);
        } else {
            pour(litres);
        }
    }

    public void fill(double litres);
}

public class CoffeeShot implements Container {
  ...
}

public class CoffeeCup implements Container {
  ...
}
```

## Overloading 

- use the same method name but with different method signature 

- We are unable to apply overloading if we have a different return type between the methods. the return type is **not** part of method signature

- e.g.

    ``` java
    int[] x = add(null, null);
    float[] y = add(null, null);
    // the compiler would be unable to determine exactly 
    // what method is trying to be called and will throw an error 
    
    int[] x = add((int[])null, (int[])null);
    float[] y = add((float[])null, (float[])null);
    // if we want to deal with ambiguous statement, we will need to cast. 
    ```

### Constructor Overloading 

``` java
public class Person {
  
    private static int DEFAULT_AGE = 21;

    private String name;
    private int age;

    public Person() {
        this("Jeff", DEFAULT_AGE);
    }

    public Person(String name) {
        this(name, DEFAULT_AGE);
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    // by using this keyword, we are able to eliminate 2 lines 
    // from the other constructors by usinte last one
}

public class Employee extends Person {
  
    private long employeeID;
    private long departmentID;

    public Employee(String name, int age, long departmentID, long employeeID) {
        super(name, age);
        // we are able to specify the constructor we want to invoke 
        // and set attributes for the object 
        this.departmentID = departmentID;
        this.employeeID = employeeID;
    }
}
```

## Overriding 

-   applies for classes, abstract classes and interface 

-   able to override inherited methods and replace them with a subtype specific definition 

-   without the use of the '@Override', java automatically overrides 

-   cannot override final class 

    ``` java 
    public final class Person {
        ... 
    }
    ```


example 

``` java 
@Override
public boolean equals(Object o) {
    // Defensive checking 
    if (!(o instanceof Plant)) {
        return false;
    }
    
    // type casting 
    Plant p = (Plant) o;
    
    ... 
}
```

## Exception

-   checked exception (handled at compile time)

    -   These exceptions are checked during compilation and the code will compile only if these conditions are met. 
    -   Examples of these include Type exceptions etc.

-   runtime exception (unchecked exception)

    -   It is something that can occur but the compiler will allow you to compile. This can cause an exception if not handled correctly. 
    -   e.g. list of objects. Adding elements that are not expected
    -   e.g. an Integer to an Object list of Strings. Then casting to Strings.

-   Error (state that cannot be handled)

    -   Cannot be handled by a try/catch block and these include irrecoverable errors, such as StackOverﬂowError and the program will crash. 

    -   Both Errors and Exception are subclasses of java.lang.Throwable class. 

    -   All errors are also unchecked. 

    -   ``` java
        // StackOverFlowError 
        public int recursion(int n) {
            return recursion(n-1) + recursion(n-2);
        }
        // occur then a recursive function does not have base case that 
        // properly exits it out of the recursive case 
        ```

example 1

``` java
public static void imGonnaCrash() throws Exception {
  	throw new Exception("Definitely crashing!");
}

// we are forced to catch it by the compiler 
public static void main(String[] args) {
    try {
        imGonnaCrash();
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```

example 2

``` java
class InvalidRateException extends Exception {
    public InvalidRateException() {
        super("Invalid");
    }
}

public class Monitor {
    
    private double rate;
    public final double MAX_RATE;

    public Monitor(double defaultRate, double max) {
        MAX_RATE = max;
        rate = defaultRate;
    }

    public double setRate(double hz) throws InvalidRateException {
        if (hz < 0 || hz > MAX_RATE) {
            throw new InvalidRateException();
        } else {
            rate = hz;
        }
        return rate;
    }
}
```

## Enums 

-   a set of defined instances of the same type 
-   Cannot use the "new" keywoard of an enum type 

``` java
// method 1
enum Colour {
    Red, Green, Yellow;
    
    public Colour change() {
        if (this == Red) {
            return Green;
        } else if (this == Green) {
            return Yellow;
        } else if (this == Yellow) {
            return Red;
        }
    }
}

// method 2
enum Colour {
    Red { public Colour change() { return Green; }},
    Green { public Colour change() { return Yellow; }},
    Yellow { public Colour change() { return Red; }};
    
    public abstract Colour change();
}

public class TrafficLight {
    private Colour colour;
    
    public TrafficLight() {
        colour = Colour.Red; // by default it is red 
    }
    
    public Colour change() {
        colour = colour.change();
        return colour;
    }
}
```

## Iterators

``` java
ArrayList<String> list = new ArrayList<String>();
for (String s: list) {
    System.out.println(s);
}
```

``` java
Iterator<String> iterator = list.iterator();
while (iterator.hasNext()) {
    String s = iterator.next(); // returns element and move it
    System.out.println(s);
}
```

``` java
hasNext(): boolean;
next(): E;
remove(): void;
```

## Generics

-   advantages 

    -   Stronger type checks at compile time 
    -   elimination of casts 
    -   enabling programmers to implement generic algorithms (handle multiple different types without needing to rewrite the same code)

-   Generic Static Method 

    ``` java
    // Example 
    public class GenericFind {
    	
    	public static <T> T find(T needle, T[] haystack) {
    		T element = null;
    		for(T e : haystack) {
    			if(needle.equals(e)) {
    				element = e;
    				break;
    			}
    		}
    		return element;
    	}
        
    	// usage
    	public static void main(String[] args) {
    		String s = GenericFind.<String>find("Hello", new String[] {
    			"One",
    			"two",
    			"Hello",
    			"World"
    		});
    		
    		System.out.println(s);
    	}
    }
    
    ```

-   Extends with type parameters 

    ``` java
    import java.util.List;
    import java.util.ArrayList;
    
    abstract class Liquid {
    	public Liquid(double litres) {
    		this.litres = litres;
    	}
    	
    	protected double litres;
    	public abstract double getLitres();
    }
    
    class Water extends Liquid {
    	
    	public Water(double l) {
    		super(l);
    	}
    	
    	public double getLitres() {
    		return litres;
    	}
    	
    	public String toString() { return "Water"; }
    }
    
    class Oil extends Liquid {
    	
    	public Oil(double l) {
    		super(l);
    	}
    	
    	public double getLitres() {
    		return litres;
    	}
    	
    	public String toString() { return "Oil"; }
    }
    
    
    public class Barrel<T extends Liquid> {
    	
    	List<T> contents;
    	
    	public Barrel() {
    		contents = new ArrayList<T>();
    	}
    	
    	public void add(T item) {
    		contents.add(item);
    	}
    	
        // since we have a bounded type we are able to infer that all types 
        // have a super type Liquid, therefore we are able to utilise 
        // the methods defined in liquids 
    	public void outputContents() {
    		for(T e : contents) {
    			System.out.println(e + " " + e.getLitres());
    			
    		}
    	}
    }
    ```

-   Array are covariant, Generics are **NOT**

    ``` java
    List<String> strings = new ArrayList<String>();
    List<Object> objects = strings;
    // because generics are invariant, we are unable to perform a similar operation 
    // to arrays, this will result in a compilation error 
    ```

### DynamicArray

``` java
package collections;

public class DynamicArray<T> {
	private int size;
	private T[] elements;
	
	@SuppressWarnings("unchecked")
	public DynamicArray() {
		size = 0;
        // we will need to instantiate an Object[] to use with array and cast 
        // cannot instantiate with generic type 
		elements = (T[]) new Object[16];
	}
	
	public int size() {
		return size;
	}
	
	@SuppressWarnings("unchecked")
	public void add(T v) {
		if(size >= elements.length) {
			T[] temp = (T[]) new Object[elements.length*2];
			for(int i = 0; i < elements.length; i++) {
				temp[i] = elements[i];
			}
			elements = temp;
		}
		elements[size] = v;
		size++;
	}
	
	public T remove(int idx) {
		if(idx >= 0 && idx < size) {
			T v = elements[idx];
			for(int i = idx; i < size-1; i++) {
				elements[i] = elements[i+1];
			}
			size--;
			return v;
		} else {
			return null;
		}
	}
	
	public T get(int idx) {
		if(idx >= 0 && idx < size) {
			T v = elements[idx];
			return v;
		} else {
			return null;
		}
	}
}
```

### LinkedList

``` java
import java.util.Iterator;

public class LinkedList<T> implements Iterable<T> {

    private Node<T> root;
    private int size;

    public LinkedList() {
        size = 0;
        root = null;
    }

    public Iterator<T> iterator() {
    	return new LinkedListIterator<T>(root);
    }

    public int size() { return size; }

    public void add(T value) {
        Node<T> cursor = root;
        if(root == null) {
            root = new Node<T>(value, null);
        } else {
            while(cursor.next() != null) {
                cursor = cursor.next();
            }
            cursor.setNext(new Node<T>(value, null));
        }
        size++;
    }

    public T get(int index) {
        Node<T> cursor = root;
        int counter = 0;

        if(index < 0) { return null; }

        while(cursor != null && counter < index) {
            cursor = cursor.next();
            counter++;
        }
        return cursor.value();
    }

    public void set(int index, T value) {
        Node<T> cursor = root;
        int counter = 0;

        if(index < 0) { return; }

        while(cursor != null && counter < index) {
            cursor = cursor.next();
            counter++;
        }
        cursor.setNext(new Node<T>(value, cursor.next()));
        size++;
	}

	public void remove(int index) {
        Node<T> cursor = root;
        int counter = 0;
        if(index <= 0) {
            root = root.next();
        } else {
            while(cursor.next() != null && counter < index) {
                cursor = cursor.next();
                counter++;
            }
            if (cursor.next() != null) {
                cursor.setNext(cursor.next().next());
            }
        }
        size--;
	}
}

class LinkedListIterator<T> implements Iterator<T> {

	private Node<T> cursor;

	public LinkedListIterator(Node<T> node) {
		cursor = node;
	}

	public boolean hasNext() {
		return cursor != null;
	}

	public T next() {
		T val = cursor.value();
		cursor = cursor.next();
		return val;
	}

}

class Node<T> {

    private T value;
    private Node<T> next;

    public Node(T value, Node<T> next) {
        this.value = value;
        this.next = next;
    }

    public Node<T> next() {
        return next;
    }

    public void setNext(Node<T> n) {
        next = n;
    }

    public T value() {
        return value;
    }
}
```

### Generic Array

``` java
import java.util.Arrays;

public class JArray<T> {

	private Object[] array;
	private int size;

	public JArray(int size) {
		array = new Object[size];
		this.size = size;
	}

	public int length() {
		return size;
	}

	public T set(int index, T element) {
		if (index < 0 || index >= size) {
			throw new ArrayIndexOutOfBoundsException();
		}
		for (int i = 0; i < array.length; i++) {
			if (i == index) {
				array[i] = element;
			}
		}
		return element;
	}

	@SuppressWarnings("unchecked")
	public T get(int index) {
		if (index >= 0 && index < size) {
			T value = (T) array[index];
			return value;
		} else {
			throw new ArrayIndexOutOfBoundsException();
		}
	}

    @SuppressWarnings("unchecked")
    public Object[] setSlice(int start, T[] slice, int sliceEnd) {
        array = Arrays.copyOf(array, array.length +  slice.length -1);
        int count = 0;
        // duplicate the data backwards 
		for (int i = array.length - 1; i >= sliceEnd; i--) {
			if (i >= start + sliceEnd) {
				array[i] = array[i-slice.length+1];
			}
		}
        // apply from the start 
        for (int i = 0; i < slice.length; i++) {
            array[start] = slice[i];
			start++;
        }
        return array;
    }
    
    public void clear() {
        array = new Object[array.length];
    }
    
	@Override
	public String toString() {
		return Arrays.toString(array);
	}

	public static void main(String[] args) {
		JArray<Integer> arr = new JArray<Integer>(20);
		for (int i = 0; i < arr.length(); i++) {
			arr.set(i, i+1);
		}
		Integer[] slice = new Integer[] {100,101,102,103};
		arr.setSlice(3,slice,4);
		System.out.println(arr);
	}
}
```

## Testing

-   white box testing --> typically where we employ some unit testing software, to help analyse the internals of the system and test them independently 
-   black box testing --> user centric testing, without knowledge of the internals, input is given and compared to match the output of the program 
-   regression testing --> when the system has been modified and the changes may result in a failure of a previous successful test case 
-   integration testing --> when developing individual components, we want to integrate it into the whole system and check to see if it works. 

``` java
@Test 
public void checkForNull() {
    Container a = new Container(null);
    assertNull(a.get());
}

// examples 
assertTrue(boolean expression);
assertFalse(boolean expression);
assertEquals(expected, actual);
assertNull(object);
assertSame(object1, object2);
```

## Recursion 

-   a base case, where the function terminates 
-   recursive case, which will converge to a base case 

### Advantages 

-   can be simpler to read and write 
-   immediately writing an iterative method where there is an established recursive method can be considered a premature optimisation 

### Drawbacks 

-   the java programming model does not allow for infinite recursion 
-   inefficient with memory 
-   potentially more computationally demanding due to the overhead caused by method calls 

### Caching

``` java
// constructing it with an interger as a key(the nth fibonacci sequence) 
// and int[] as the value 
public static HashMap<Integer, int[]> results = new HashMap<>();

public static int[] generateSequence(int n) {
    // we have added a check to see if we have already computed this answer before 
    if(results.containsKey(n)) {
        System.out.println("We have retrieved a result!");
        return results.get(n);
    } else {
        if(n < 0) {
            return new int[0];
        } else if(n == 0) {
            return new int[] { 0 };
        } else if(n == 1) {
            return new int[] { 0, 1 };
        } else {
            int[] f1 = generateSequence(n-1);
            int[] f2 = generateSequence(n-2);
            int[] newsequence = new int[f1.length+1];
            newsequence[f1.length] =
                f1[f1.length-1] + f2[f2.length-1];
            for(int i = 0; i < f1.length; i++) {
                newsequence[i] = f1[i];
            }
            results.put(n, newsequence);
            return newsequence;
        }
    }
}
```

## Inner classes 

-   a common case to use is where we have a similar concept but its definition may differ for each class 
-   Non-static inner class will utilise instance variables from the outer class 
-   Static inner class operate similarly to regular classes by their existence within another class is for grouping reasons 

``` java
public class Book implements Iterable<Book.Page> {
	List<Page> pages = new ArrayList<>();

	public static class Page {
		String contents;
		public Page(String c) { contents = c; }
		public String toString() { return contents; }
	}
    
	// change the access modifier to public and access it outside 
	public class BookReader implements Iterator<Page> {
		int index;
		public BookReader(int i) {
			index = i;
		}
		
		public boolean hasNext() { return index < pages.size(); }
		public Page next() {
			Page p = pages.get(index);
			index++;
			return p;
		}
	}
	
	public void addPage(Page p) { pages.add(p); }
	
	public void addContent(String s) { pages.add(new Page(s)); }
	
	public Iterator<Page> iterator() { return new BookReader(0); }
}

public static void main(String[] args) {
    Book b = new Book();
    b.addContent("Line 1");
    b.addContent("Line 2");
    b.addContent("Line 3");
    // since changing it to public we can access the class 
    // but only through an instance of the outer class
    // the declaration type does not require an instance 
    Book.BookReader reader = b.new BookReader(0);
    while(reader.hasNext()) {
        Book.Page p = reader.next();
        System.out.println(p); 
    }
}
```

## Optionals 

``` java
// since the method could return no element, our method will return an optional, 
// notifying the programmer that it could return null and they should handle it 
public static Optional<Integer> retrieveElement(List<Integer> list, int i) {
    // we will initialise the result to an empty optional type
    // if the element can be retrieved, we can set it to contain an element from the list
    Optional<Integer> result = Optional.empty();
    if (i >= 0 && i < list.size()) {
        result = Optional.of(list.get(i));
    }
    return result;
}
```

## Anonymous class VS Lambdas 

-   anonymous class can do more

    -   create instance variables 

        ```java 
        interface Greeting {
            public void hello();
            public void goodbye();
        }
        public class Hello {
            public static void main(String[] args) {
                Greetings Sam = new Greetings() {
                    String to = "Sam";
                    public void hello() { System.out.println("Hello" + to); }
                    public void goodbye() { System.out.println("Goodbye" + to); }
                }
                Sam.hello();
                Sam.goodbye();
            }
        }
        ```
        
-   multiple methods 
    
-   encapsulation of fields 

### Anonymouse Class

An anonymous class is immediately constructed and an instance returned to the caller 

-   only one instance of an anonymous class exists 
-   interface can have multiple methods 
-   it is typically declared within a method 

``` java
SayHello hi = new SayHello() { public void hello() { System.out.println("Hello!")} }
// within the braces, we are defining the anonymous type
// simly just overriding the method that is required by SayHello
```

### Lambdas

-   Lambda methods require an interface that declares only **one** method

-   lambda can have multiple lines 

    ``` java
    SayHello hi = () -> {
        System.out.println("Hello!");
        System.out.println("Yo!");
    }
    ```

-   we can use lambda expression within our default methods 

### Comparator 

``` java
Collections.sort(people, new Comparator<Person>() {
    public int compare(Person p1, Person p2) {
        return p1.getAge() - p2.getAge();
    }
});
```

``` java
Collections.sort(people, new SortByAge());
class SortByAge implements Comparator<Person> {
    public int compare(Person a, Person b) {
        return a.getAge() - b.getAge();
    }
}
```

## Method References

``` java
<ClassOrInstance>::MethodIdentifier
```

``` java
SayHi h = System.out::println;
SayHi h = (arg) -> System.out.println(arg);
```

``` java
interface MyReference {
    public int ref(int x, int y);
}

public class MethodReference {
    public static int add(int a, int b) {
        return a + b;
    }
    public static void main(String[] args) {
        MyReference m1 = MethodReferences::add;
        System.out.pritnln(m1.ref(1,1)); // 2
    }
}
```

## Functional Interfaces 

### Predicate<T>

-   ipt: String, opt: true/false

``` java
Predicate<String> p = (String s) -> s.length() > 5;
System.out.pritnln(p.test("This is a string longer than 5"));
```

-   e.g. filter 

### Consumer<T>

-   ipt: String, opt: n/a 

``` java
Consumer<String> i = (String s) -> System.out.pritnln(s);
i.accept("I'm printing this!");
```

-   e.g. forEach 

### Supplier<T>

ipt: n/a, opt: Integer

``` java
Random random = new Random();
Supplier<Integer> s = () -> Integer.valueOf(random.nextInt() % 10);
System.out.println("This is a randomly outputted integer: " + s.get());
```

### Function<T, R>

ipt: String, opt: Integer

``` java
Function<String, Integer> f = (String s) -> Integer.valueOf(s.length());
System.out.pritnln(f.apply("Give me the length"));
```

-   e.g. map

Example

``` java 
List<Person> over25 = people.stream().filter((Person p) -> p.getAge() > 25).collect(Collectors.toList());
// aka
List<Person> over25 = new ArrayList<Person>();
for (Person p : people) {
    if (p.getAge() > 25) {
        over25.add(p);
    }
}
```

## Builder Pattern 

``` java 
public class ComputerBuilder {
    private Part cpu;
    private Part motherboard;
    private ArrayList<Part> ram;
    public ComputerBuilder() {
        cpu = null;
        motherboard = null;
        ram = new ArrayList<Part>();
    }
    public ComputerBuilder setCPU(Part p) {
        cpu = p;
        return this;
    }
    public ComputerBuilder setMotherboard(Part p) {
        motherboard = p;
        return this;
    }
    public ComputerBuilder addRAM(Part p) {
        ram.add(p);
        return this;
    }
    public Computer build() {
        return new Computer (cpu, Motherboard, ram);
    }
}

Computer c = new ComputerBuilder().setCPU(new CPU()).setMotherboard(new Motherboard()).addRAM(new Part()).build();
```

## State Pattern

``` java
abstract class TelephoneState {
	public abstract TelephoneState dial(String number);
	public abstract TelephoneState hangup();
}

class LineBusy extends TelephoneState {
	public TelephoneState dial(String number) {
		throw new RuntimeException("Line is already busy");
	}
	
	public TelephoneState hangup() {
		System.out.println("Shutting down");
		return new LineWaiting();
	}
}

class LineWaiting extends TelephoneState {
	public TelephoneState dial(String number) {
		System.out.println("Dialing... " + number);
		return new LineBusy();
	}
	
	public TelephoneState hangup() {
		throw new RuntimeException("Line is already waiting");
	}
}

public class Telephone {
	private TelephoneState state;
	
	public Telephone() {
		state = new LineWaiting();
	}
	
	public void dial(String number) {
		state = state.dial(number);
	}
	
	public void hangup() {
		state = state.hangup();
	}
}
```

## Wildcards

Producer extends, Consumer super (PECS)

### Super

-   Add to the list 

``` java
Type<? super LowerBound> variable;
```

### Extends

-   read object from list 

``` java
Type<? extends UpperBound> variable;
```

### Wildcards VS Generic 

-   type parameters support multiple bounds, wildcards don't 
-   Wildcards support both upper and lower bounds unlike generic which support only extends 

