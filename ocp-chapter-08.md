# OCP Chapter 08

_Status: Published_
_Created: 2024-07-30 16:38:25_
_Tags: ocp_

# Class Design

**Inheritance** is the process by which a subclass automatically includes any public or protected members of the class, including primitives, objects, or methods, defined in the parent class.

For illustrative purposes, we refer to any class that inherits from another class as a **subclass** or **child** class, as it is considered a descendant of that class. Alternatively, we refer to the class that the child inherits from as the **superclass** or **parent** class, as it is considered an ancestor of the class.

access levels: 
- public
- protected
- package-private
- private

When one class inherits from a parent class, all public and protected members are automatically available as part of the child class. 

Package-private members are available if the child class is in the same package as the parent class. 

Last but not least, private members are restricted to the class they are defined in and are never available via inheritance.


## SINGLE VS. MULTIPLE INHERITANCE

Java supports single inheritance, by which a class may inherit from only one direct parent class. Java also supports multiple levels of inheritance, by which one class may extend another class, which in turn extends another class. You can have any number of levels of inheritance, allowing each descendant to gain access to its ancestor’s members.

multiple inheritance: by which a class may have multiple direct parents. By design, Java doesn’t support multiple inheritance in the language

## PREVENT FROM BEING EXTENDED

It is possible in Java to prevent a class from being extended by marking the class with the final modifier.


## INHERITING OBJECT

Object is the only class that doesn’t have a parent class.

The key is that when Java sees you define a class that doesn’t extend another class, it automatically adds the syntax extends java.lang.Object to the class definition.

**Primitive types** such as int and boolean **do not** inherit from **Object**, since they are not classes.



## Extending a Class

format of a class definition:
<public / protected/ private / nothing(package-provate) default> < abstract / final (optional) > class(required) {ClassName(required)} <extends / implements {Class}(optional)>

access modifier - class modifier - class declaration - inheritance

Remember that final means a class cannot be extended. 

### Access Modifier Summary

| Access Modifier               | Class | Package | Subclass | World |
|-------------------------------|-------|---------|----------|-------|
| `public`                      | Yes   | Yes     | Yes      | Yes   |
| `protected`                   | No    | Yes     | Yes      | No    |
| `package-private` (default)   | No    | Yes     | No       | No    |
| `private`                     | No    | No      | No       | No    |





## APPLYING CLASS ACCESS MODIFIERS

In Java, a top-level class is a class that is not defined inside another class.

Applying public access to a class indicates that it can be referenced and used in any class. Applying default (package-private) access, which you’ll remember is the lack of any access modifier, indicates the class can be accessed only by a class within the same package.

An inner class is a class defined inside of another class and is the opposite of a top-level class. In addition to public and package- private access, inner classes can also have protected and private access. 

## ACCESSING THE THIS REFERENCE
let op met **this.___**

```
public class Flamingo {

    private String color;
    private String color2;

    public void setColor(String color) {
        color = color; // zet NIET de color field van Flaming => die is nu nog null....
        this.color = color;
        color  = this.color; // werkt wel maar this.color blijft null....en color als inputvar is dat nu ook...
    }

    public void setColor2(String color) {
        color2 = color; // werkt nu WEL want andere naam....
    }

    public static void main(String[] args) {
        Flamingo flamingo = new Flamingo();
        flamingo.setColor("HJH");
        flamingo.setColor2("HJH");
        System.out.println(flamingo.color);
        System.out.println(flamingo.color2);
    }
}

```

## Declaring Constructors

```
public class Bunny {
   public bunny() { }     // DOES NOT COMPILE
   public void Bunny() { } // COMPILES maar is geen constructor
}

class Bonobo {
   public Bonobo(var food) { // DOES NOT COMPILE 
   }
}
```
Like method parameters, constructor parameters can be any valid class, array, or primitive type, including generics, but may not include **var**.

nog een keer: GEEN **var** in constructor!

A class can have multiple constructors, so long as each constructor has a unique signature. 

Like methods with the same name but different signatures, declaring multiple constructors with different signatures is referred to as constructor overloading.

Constructors are used when creating a new object. This process is called instantiation because it creates a new instance of the class. A constructor is called when we write new followed by the name of the class we want to instantiate.



## CALLING THE SUPER REFERENCE

```
class Mammal {
    String type = "mammal";
}

public class Bat extends Mammal {
    String type = "bat";

    public String getType() {
        return super.type + ":" + this.type;
    }

    public static void main(String... zoo) {
        System.out.print(new Bat().getType());
    }
}

```
The program prints mammal:bat


## DEFAULT CONSTRUCTOR

Every class in Java has a constructor whether you code one or not. If you don’t include any constructors in the class, Java will create one for you without any parameters. 

This Java-created constructor is called the default constructor and is added anytime a class is declared without any constructors. 


```
public class Rabbit1 {} => ENIGE die een default constructor krijgt: public Rabbit() {}


public class Rabbit2 {
   public Rabbit2() {}
}

public class Rabbit3 {
   public Rabbit3(boolean b) {}
}

public class Rabbit4 {
   private Rabbit4() {}
}
```



## CALLING OVERLOADED CONSTRUCTORS WITH THIS()

a single class can have multiple constructors. This is referred to as constructor overloading because all constructors have the same inherent name but a different signature.

```

public class Hamster {
    private String color;
    private int weight;

    public Hamster(int weight) { // FIRST
         this.weight = weight;
        color = "brown";
    }

    public Hamster(int weight, String color) { // SECOND
        this.weight = weight;
        this.color = color;
    }
}


// kan dus beter

public class Hamster {
    private String color;
    private int weight;

    public Hamster(int weight) { // FIRST
        this.weight = weight;
        this.color = "brown";
    }

    public Hamster(int weight, String color) { // SECOND
        this(weight);
        this.color = color;
    }

    public static void main(String[] args) {
        Hamster h =new Hamster(12, "green");
        System.out.println(h.color);
        System.out.println(h.weight);
    }
}

```


## INFINITE CONSTRUCTOR

Will not compile => infinite constructions....
```

public class Gopher {
    public Gopher() {
        this(5);  // DOES NOT COMPILE
    }

    public Gopher(int dugHoles) {
        this();   // DOES NOT COMPILE
    }
}
```

## this vs this()

this, refers to an instance of the class, while the second, this(), refers to a constructor call within the class.



## SUPER()

 super() can only be called once as the first statement of the constructor
 
```

public class Zoo {

    public Zoo() {
        System.out.println("Zoo created");
        super();     // DOES NOT COMPILE
    }
}
public class Zoo {
    public Zoo() {
        super();
        System.out.println("Zoo created");
        super();     // DOES NOT COMPILE
    }
}

```

### SUPER vs SUPER()

Like this and this(), super and super() are unrelated in Java. The first, super, is used to reference members of the parent class, while the second, super(), calls a parent constructor.



## ARE CLASSES WITH ONLY PRIVATE CONSTRUCTORS CONSIDERED FINAL?

Remember, a final class cannot be extended. What happens if you have a class that is not marked final but only contains private constructors—can you extend the class? The answer is “yes,” but only an inner class defined in the class itself can extend it. An inner class is the only one that would have access to a private constructor and be able to call super(). Other top-level classes cannot extend such a class. Don’t worry—knowing this fact is not required for the exam.



## Missing default No-Argument Constructor

```
public class Mammal {
   public Mammal(int age) {}
}
public class Elephant extends Mammal {  // DOES NOT COMPILE
}

```
Als er al een constructor is dan gaat de compiler er niet de standaard aan toevoegen.....


Since Elephant does not define any constructors, the Java compiler will attempt to insert a default no-argument constructor. As a second compile- time enhancement, it will also auto-insert a call to super() as the first line of the default no-argument constructor.

You should be wary of any exam question in which a class defines a constructor that takes arguments and doesn’t define a no-argument constructor. Be sure to check that the code compiles before answering a question about it, especially if any classes inherit it


## CONSTRUCTORS AND FINAL FIELDS

By the time the constructor completes, all final instance variables must be assigned a value. 

```
public class MouseHouse {
   private final int volume;
   private final String type;
   {
      this.volume = 10;
   }
   public MouseHouse(String type) {
      this.type = type;
   }
   public MouseHouse() {  // DOES NOT COMPILE
      this.volume = 2;    // DOES NOT COMPILE
   }
}
```

## ORDER OF INITIALIZATION

### Class Init

First, you need to initialize the class, which involves invoking all static members in the class hierarchy, starting with the highest superclass and working downward. This is often referred to as loading the class. The JVM controls when the class is initialized, although you can assume the class is loaded before it is used. The class may be initialized when the program first starts, when a static member of the class is referenced, or shortly before an instance of the class is created.

1. If there is a superclass Y of X,then initialize class Y first.
2. Process all static variable declarations in the order they appear in the class.
3. Process all static initializers in the order they appear in the class.


### Instance Init

1. If there is a superclass Y of X,then initialize the instance of Y first.
2. Process all instance variable declarations in the order they appear in the class.
3. Process all instance initializers in the order they appear in the class.
4. Initialize the constructor including any overloaded constructors referenced with this().


```
public class ZooTickets {
    private String name = "BestZoo";

    {
        System.out.print(name + "-");
    }

    private static int COUNT = 0;

    static {
        System.out.print(COUNT + "-");
    }

    static {
        COUNT += 10;
        System.out.print(COUNT + "-");
    }

    public ZooTickets() {
        System.out.print("z-");
    }

    public static void main(String... patrons) {
        new ZooTickets();
    }
}

```
0-10-BestZoo-z-

```

class Primate {
    public Primate() {
        System.out.print("Primate-");
    }
}

class Ape extends Primate {
    public Ape(int fur) {
        System.out.print("Ape1-");
    }

    public Ape() {
        System.out.print("Ape2-");
    }
}

public class Chimpanzee extends Ape {
    public Chimpanzee() {
        super(2);
        System.out.print("Chimpanzee-");
    }

    public static void main(String[] args) {
        new Chimpanzee();
    }
}


```
Primate-Ape1-Chimpanzee-




## REVIEWING CONSTRUCTOR RULES

1. The first statement of every constructor is a call to an overloaded constructor via this(), or a direct parent constructor via super().
2. If the first statement of a constructor is not a call to this() or super(), then the compiler will insert a no-argument super() as the first statement of the constructor.
3. Calling this() and super() after the first statement of a constructor results in a compiler error.
4. If the parent class doesn’t have a no-argument constructor,then every constructor in the child class must start with an explicit this() or super() constructor call.
5. If the parent class doesn’t have a no-argument constructor and the child doesn’t define any constructors, then the child class will not compile.
6. If a class only defines private constructors, then it cannot be extended by a top-level class.
7. All final instance variables must be assigned a value exactly once by the end of the constructor. Any final instance variables not assigned a value will be reported as a compiler error on the line the constructor is declared.

# Key Points about Constructors

- **Same Name as the Class**: The constructor's name must exactly match the class name.

- **No Return Type**: Constructors do not have a return type, not even `void`. This distinguishes them from other methods.

- **Automatic Invocation**: A constructor is automatically called when an object of the class is created.

- **Default Constructor**: If no constructor is explicitly defined in a class, the Java compiler automatically provides a default constructor, which is a no-argument constructor. This constructor initializes the object with default values (e.g., `0`, `null`, `false`).

- **Parameterized Constructors**: Constructors can take parameters, allowing you to create objects with custom initial values.

- **Overloading Constructors**: Like other methods in Java, constructors can be overloaded. This means you can have multiple constructors in the same class with different parameter lists.

- **Constructor Chaining**: Within a class, one constructor can call another constructor of the same class using the `this()` keyword. This is called constructor chaining. If you want to call the constructor of the superclass, you use the `super()` keyword.


## INHERITING METHODS

### Overriding a Method

To override a method, you must follow a number of rules. The compiler performs the following checks when you override a method:

1. The method in the child class must have the same signature as the method in the parent class.
2. The method in the child class must beat least as accessible as the method in the parent class.
3. The method in the child class may not declare a checked exception that is new or broader than the class of any exception declared in the parent class method.
4. If the method returns a value,it must be the same or a subtype of the method in the parent class, known as covariant return types.


#### DEFINING SUBTYPE AND SUPERTYPE

When discussing inheritance and polymorphism, we often use the word subtype rather than subclass, since Java includes interfaces. A subtype is the relationship between two types where one type inherits the other. If we define X to be a subtype of Y, then one of the following is true:
- X and Y are classes, and X is a subclass of Y.
- X and Y are interfaces, and X is a subinterface of Y.
- X is a class and Y is an interface, and X implements Y (either directly or through an inherited class).

Likewise, a supertype is the reciprocal relationship between two types where one type is the ancestor of the other. Remember, a subclass is a subtype, but not all subtypes are subclasses.





```

public class Bird {
    public void fly() {
        System.out.println("Bird is flying");
    }

    public void eat(int food) {
        System.out.println("Bird is eating " + food + " units of food");
    }
}

public class Eagle extends Bird {
    public int fly(int height) {
        System.out.println("Bird is flying at " + height + " meters");
        return height;
    }

    public int eat(int food) {  // DOES NOT COMPILE
        System.out.println("Bird is eating " + food + " units  of food");
        return food;
    }

}

```
the method is being overridden, the return type of the method in the Eagle class must be compatible with the return type for the method in the Bird class. In this example, the return type int is not a subtype of void; therefore, the compiler will throw an exception on this method definition.



```
public class Camel {
   public int getNumberOfHumps() {
return 1; }
}
public class BactrianCamel extends Camel {
   private int getNumberOfHumps() {  // DOES NOT COMPILE
return 2; }
}
public class Rider {
   public static void main(String[] args) {
      Camel c = new BactrianCamel();
      System.out.print(c.getNumberOfHumps());
   }
}

```
In this example, BactrianCamel attempts to override the getNumberOfHumps() method defined in the parent class but fails because the access modifier private is more restrictive than the one defined in the parent version of the method.


The third rule says that overriding a method cannot declare new checked exceptions or checked exceptions broader than the inherited method. This is done for similar polymorphic reasons as limiting access modifiers. In other words, you could end up with an object that is more restrictive than the reference type it is assigned to, resulting in a checked exception that is not handled or declared. 

```
public class Reptile {
   protected void sleepInShell() throws IOException {}
   protected void hideInShell() throws NumberFormatException{}
   protected void exitShell() throws FileNotFoundException {}
}

public class GalapagosTortoise extends Reptile {
   public void sleepInShell() throws FileNotFoundException {}
   public void hideInShell() throws IllegalArgumentException{}
   public void exitShell() throws IOException {} // DOES NOT COMPILE
}

```
The third overridden exitShell() method declares IOException, which is a superclass of the exception declared in the inherited method, FileNotFoundException. Since these are checked exceptions and IOException is broader, the overridden exitShell() method does not compile in the GalapagosTortoise class. 



The fourth and final rule around overriding a method is probably the most complicated, as it requires knowing the relationships between the return types. The overriding method must use a return type that is covariant with the return type of the inherited method.

```
public class Rhino {
   protected CharSequence getName() {
      return "rhino";
   }
   protected String getColor() {
      return "grey, black, or white";
    }
}
class JavanRhino extends Rhino {
   public String getName() {
      return "javan rhino";
   }
   public CharSequence getColor() {  // DOES NOT COMPILE
      return "grey";
    }
}
```
the overridden getColor() method does not compile because CharSequence is not a subtype of String. To put it another way, all String values are CharSequence values, but not all CharSequence values are String values....

A simple test for covariance is the following: Given an inherited return type A and an overriding return type B, can you assign an instance of B to a reference variable for A without a cast? If so, then they are covariant. This rule applies to primitive types and object types alike. If one of the return types is void, then they both must be void, as nothing is covariant with void except itself.


## Overriding a Generic Method
Overriding methods is complicated enough, but add generics to it and things only get more challenging.

### Review of Overloading a Generic Method

```
public class LongTailAnimal {
   protected void chew(List<Object> input) {}
   protected void chew(List<Double> input) {}  // DOES NOT COMPILE
}
```
only one of the two methods is allowed in a class because type erasure will reduce both sets of argumentsto(List input).

### Generic Method Parameters

```
public class LongTailAnimal {
   protected void chew(List<Object> input) {}
}

public class Anteater extends LongTailAnimal {
   protected void chew(List<Double> input) {}  // DOES NOT COMPILE
}
```
Both of these examples fail to compile because of type erasure. In the compiled form, the generic type is dropped, and it appears as an invalid overloaded method.

### Generics and Wildcards
```
void sing1(List<?> v) {}                 // unbounded wildcard
void sing2(List<? super String> v) {}    // lower bounded wildcard
void sing3(List<? extends String> v) {}  // upper bounded wildcard
```



### Generic Return Types

When you’re working with overridden methods that return generics, the return values must be covariant. In terms of generics, this means that the return type of the class or interface declared in the overriding method must be a subtype of the class defined in the parent class. The generic parameter type must match its parent’s type exactly.

```
public class Mammal {
   public List<CharSequence> play() { ... }
   public CharSequence sleep() { ... }
}
public class Monkey extends Mammal {
   public ArrayList<CharSequence> play() { ... }
}
public class Goat extends Mammal {
   public List<String> play() { ... }  // DOES NOT COMPILE
   public String sleep() { ... }
}
```

### Redeclaring private Methods

In Java, you can’t override private methods since they are not inherited. Just because a child class doesn’t have access to the parent method doesn’t mean the child class can’t define its own version of the method. It just means, strictly speaking, that the new method is not an overridden version of the parent class’s method.

Java permits you to redeclare a new method in the child class with the same or modified signature as the method in the parent class. This method in the child class is a separate and independent method, unrelated to the parent version’s method, so none of the rules for overriding methods is invoked.

```
public class Camel {
   private String getNumberOfHumps() {
      return "Undefined";
   }
}
public class DromedaryCamel extends Camel {
   private int getNumberOfHumps() {
return 1; }
}
```
Notice that the return type differs in the child method from String to int. In this example, the method getNumberOfHumps() in the parent class is redeclared, so the method in the child class is a new method and not an override of the method in the parent class. 



## Hiding Static Methods

A hidden method occurs when a child class defines a static method with the same name and signature as an inherited static method defined in a parent class. Method hiding is similar but not exactly the same as method overriding. The previous four rules for overriding a method must be followed when a method is hidden. In addition, a new rule is added for hiding a method:

5. The method defined in the child class must be marked as static if it is marked as static in a parent class.

```
public class Bear {
   public static void eat() {
      System.out.println("Bear is eating");
   }
}
public class Panda extends Bear {
   public static void eat() {
      System.out.println("Panda is chewing");
   }
   public static void main(String[] args) {
      eat();
    }
}
```
werkt! Allebei static methods en als je er bij Panda eat() weghaald dan wordt die van Bear gebruikt. Because they are both marked as static, this is not considered an overridden method. That said, there is still some inheritance going on. If you remove the eat() method in the Panda class, then the programprints"Bear is eating"atruntime.

```
public class Bear {
   public static void sneeze() {
      System.out.println("Bear is sneezing");
   }
   public void hibernate() {
      System.out.println("Bear is hibernating");
   }
   public static void laugh() {
      System.out.println("Bear is laughing");
   }
}
public class Panda extends Bear {
   public void sneeze() {           // DOES NOT COMPILE
      System.out.println("Panda sneezes quietly");
   }
   public static void hibernate() { // DOES NOT COMPILE
      System.out.println("Panda is going to sleep");
   }
   protected static void laugh() {  // DOES NOT COMPILE
      System.out.println("Panda is laughing");
   }
}
```
In this example, sneeze() is marked static in the parent class but not in the child class. The compiler detects that you’re trying to override using an instance method. However, sneeze() is a static method that should be hidden, causing the compiler to generate an error.

In the second method, hibernate() is an instance member in the parent class but a static method in the child class. In this scenario, the compiler thinks that you’re trying to hide a static method. Because hibernate() is an instance method that should be overridden, the compiler generates an error. 

Finally, the laugh() method does not compile. Even though both versions of method are marked static, the version in Panda has a more restrictive access modifier than the one it inherits, and it breaks the second
rule for overriding methods. Remember, the four rules for overriding methods must be followed when hiding static methods.








## Creating final Methods

We conclude our discussion of method inheritance with a somewhat self-
explanatory rule—final methods cannot be replaced.
By marking a method final, you forbid a child class from replacing this method. This rule is in place both when you override a method and when you hide a method. In other words, you cannot hide a static method in a child class if it is marked final in the parent class.

```
public class Bird {
   public final boolean hasFeathers() {
      return true;
   }
   public final static void flyAway() {}
}
public class Penguin extends Bird {
   public final boolean hasFeathers() {  // DOES NOT COMPILE
      return false;
   }
   public final static void flyAway() {}  // DOES NOT COMPILE
}
```
This rule applies only to inherited methods. For example, if the two methods were marked private in the parent Bird class, then the Penguin class, as defined, would compile. In that case, the private methods would be redeclared, not overridden or hidden.



## HIDING VARIABLES

Java doesn’t allow variables to be overridden. Variables can be hidden, though.

A hidden variable occurs when a child class defines a variable with the same name as an inherited variable defined in the parent class. This creates two distinct copies of the variable within an instance of the child class: one instance defined in the parent class and one defined in the child class.

```
class Carnivore {
   protected boolean hasFur = false;
}
public class Meerkat extends Carnivore {
   protected boolean hasFur = true;
   public static void main(String[] args) {
      Meerkat m = new Meerkat();
      Carnivore c = m;
      System.out.println(m.hasFur);
      System.out.println(c.hasFur);
    }
}
```
It prints true followed by false. Confused? Both of these classes define a hasFur variable, but with different values. Even though there is only one object created by the main() method, both variables exist independently of each other. The output changes depending on the reference variable used.

overriding a method replaces the parent method on all reference variables (other than super), whereas hiding a method or variable replaces the member only if a child reference type is used.



## Understanding Polymorphism

Java supports polymorphism, the property of an object to take on many different forms. To put this more precisely, a Java object may be accessed using a reference with the same type as the object, a reference that is a superclass of the object, or a reference that defines an interface the object implements, either directly or through a superclass. Furthermore,  a cast is not required if the object is being reassigned to a super type or interface of the object.


### Interfaces
- An interface can define abstract methods.
- A class can implement any number of interfaces.
- A class implements an interface by overriding the inherited abstract methods.
- An object that implements an interface can be assigned to a reference for that interface.


```
public class Primate {
   public boolean hasHair() {
      return true;
   }
}

public interface HasTail {
   public abstract boolean isTailStriped();
}

public class Lemur extends Primate implements HasTail {
   public boolean isTailStriped() {
      return false;
   }
   public int age = 10;
   public static void main(String[] args) {
      Lemur lemur = new Lemur();
      System.out.println(lemur.age);
      HasTail hasTail = lemur;
      System.out.println(hasTail.isTailStriped());
        => System.out.println(hasTail.age);             // DOES NOT COMPILE, kan nu aleen bij zn type blijven
      Primate primate = lemur;
      System.out.println(primate.hasHair());
   }
}

```
Polymorphism enables an instance of Lemur to be reassigned or passed to a method using one of its supertypes, such as Primate or HasTail.

## OBJECT VS. REFERENCE

In Java, all objects are accessed by reference, so as a developer you never have direct access to the object itself. Conceptually, though, you should consider the object as the entity that exists in memory, allocated by the Java runtime environment. Regardless of the type of the reference you have for the object in memory, the object itself doesn’t change.

```
Lemur lemur = new Lemur();
Object lemurAsObject = lemur;
```
Even though the Lemur object has been assigned to a reference with a different type, the object itself has not changed and still exists as a Lemur object in memory. What has changed, then, is our ability to access methods within the Lemur class with the lemurAsObject reference.

1. The type of the object determines which properties exist within the object in memory.
2. The type of the reference to the object determines which methods and variables are accessible to the Java program.

Denk aan Class van type Bla in memory. Daar referen als Bla of Object levert andere mogelijk funcs+fields op



## CASTING OBJECTS

```
Primate primate = new Lemur();  // Implicit Cast
Lemur lemur2 = primate;         // DOES NOT COMPILE
System.out.println(lemur2.age);
Lemur lemur3 = (Lemur)primate;  // Explicit Cast
System.out.println(lemur3.age);
```
When casting objects, you do not need a cast operator if the current reference is a subtype of the target type. This is referred to as an implicit cast or type conversion. Alternatively, if the current reference is not a subtype of the target type, then you need to perform an explicit cast with a compatible type. If the underlying object is not compatible with the type, then a ClassCastException will be thrown at runtime.

1. Casting a reference from a subtype to a supertype doesn’t require an explicit cast.
2. Casting a reference from a supertype to a subtype requires an explicitcast.
3. The compiler disallows casts to an unrelated class.
4. At runtime, an invalid cast of a reference to an unrelated type results in a ClassCastException being thrown.

```
public class Bird {}
public class Fish {
   public static void main(String[] args) {
      Fish fish = new Fish();
      Bird bird = (Bird)fish;  // DOES NOT COMPILE
   }
}
```
In this example, the classes Fish and Bird are not related through any class hierarchy that the compiler is aware of; therefore, the code will not compile. While they both extend Object implicitly, they are considered unrelated types since one cannot be a subtype of the other.


```
public class Rodent {}
public class Capybara extends Rodent {
   public static void main(String[] args) {
      Rodent rodent = new Rodent();
      Capybara capybara = (Capybara)rodent;  // ClassCastException
    }
}
```
This code creates an instance of Rodent and then tries to cast it to a subclass of Rodent, Capybara. Although this code will compile, it will throw a ClassCastException at runtime since the object being referenced is not an instance of the Capybara class. The thing to keep in mind in this example is the Rodent object created does not inherit the Capybara class in any way.


### THE INSTANCEOF OPERATOR

 the instanceof operator, which can be used to check whether an object belongs to a particular class or interface and to prevent ClassCastExceptions at runtime.

 ```
if(rodent instanceof Capybara) {
   Capybara capybara = (Capybara)rodent;
}
```
Just as the compiler does not allow casting an object to unrelated types, it also does not allow instanceof to be used with unrelated types.

```

public static void main(String[] args) {
   Fish fish = new Fish();
   if (fish instanceof Bird) {  // DOES NOT COMPILE
      Bird bird = (Bird) fish;  // DOES NOT COMPILE
    }
}
```

## POLYMORPHISM AND METHOD OVERRIDING

In Java, polymorphism states that when you override a method, you replace all calls to it, even those defined in the parent class.

```
class Penguin {
   public int getHeight() { return 3; }
   public void printInfo() {
      System.out.print(this.getHeight());
} }
public class EmperorPenguin extends Penguin {
   public int getHeight() { return 8; }
   public static void main(String []fish) {
      new EmperorPenguin().printInfo();
   }
}
```
Penguin3 en EmperorPenguin 8  

The facet of polymorphism that replaces methods via overriding is one of the most important properties in all of Java. It allows you to create complex inheritance models, with subclasses that have their own custom implementation of overridden methods. It also means the parent class does not need to be updated to use the custom or overridden method. If the method is properly overridden, then the overridden version will be used in all places that it is called.

Remember, you can choose to limit polymorphic behavior by marking methods final, which prevents them from being overridden by a subclass.

### CALLING THE PARENT VERSION OF AN OVERRIDDEN METHOD

there is one exception to overriding a method where the parent method can still be called, and that is when the super reference is used. How can you modify our EmperorPenguin example to print 3, as defined in the Penguin getHeight() method? You could try calling super.getHeight() in the printInfo() method of the Penguin class. Unfortunately, this does not compile, as super refers to the superclass of Penguin, in this case Object. The solution is to override printInfo() in the EmperorPenguin class and use super there.
```
public void printInfo() {
      System.out.print(super.getHeight());
}

```
This new version of EmperorPenguin uses the getHeight() method declared in the parent class and prints 3.




## OVERRIDING VS. HIDING MEMBERS

While method overriding replaces the method everywhere it is called, static method and variable hiding does not. Strictly speaking, hiding
members is not a form of polymorphism since the methods and variables maintain their individual properties. Unlike method overriding, hiding members is very sensitive to the reference type and location where the member is being used.

```
class Penguin {
   public static int getHeight() { return 3; }
   public void printInfo() {
        System.out.println(this.getHeight());
   }
}
public class CrestedPenguin extends Penguin {
   public static int getHeight() { return 8; }
   public static void main(String... fish) {
      new CrestedPenguin().printInfo();
   }
}
```
The CrestedPenguin example is nearly identical to our previous EmporerPenguin example, although as you probably already guessed, it prints 3 instead of 8. The getHeight() method is static and is therefore hidden, not overridden. The result is that calling getHeight() in CrestedPenguin returns a different value than calling it in the Penguin, even if the underlying object is the same. Contrast this with overriding a method, where it returns the same value for an object regardless of which class it is called in.

```
class Marsupial {
   protected int age = 2;

   public static boolean isBiped() {
     return false;
   }
}

public class Kangaroo extends Marsupial {
   protected int age = 6;

   public static boolean isBiped() {
      return true;
   }

   public static void main(String[] args) {
      Kangaroo joey = new Kangaroo();
      Marsupial moey = joey;
      System.out.println(joey.isBiped()); // true
      System.out.println(moey.isBiped()); //false
      System.out.println(joey.age); //6
      System.out.println(moey.age); // 2
    }
}
```
Remember, in this example, only one object, of type Kangaroo, is created and stored in memory. Since static methods can only be hidden, not overridden, Java uses the reference type to determine which version of isBiped() should be called, resulting in joey.isBiped() printing true and moey.isBiped() printing false.
Likewise, the age variable is hidden, not overridden, so the reference type is used to determine which value to output. This results in joey.age returning 6 and moey.age returning 2.

**DON’T HIDE MEMBERS IN PRACTICE**

When you’re defining a new variable or static method in a child class, it is considered good coding practice to select a name that is not already used by an inherited member. Redeclaring private methods and variables is considered less problematic, though, because the child class does not have access to the variable in the parent class to begin with.



[ocp 07](http://hjh.devsnips.nl/ocp07)
[ocp 09](http://hjh.devsnips.nl/ocp09)