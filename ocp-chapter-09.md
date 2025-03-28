# OCP Chapter 09

_Status: Published_
_Created: 2024-07-30 16:39:48_
_Tags: ocp_

# Class Design

## Inheritance
- Overerving
- is proces by which subclass automatically includes any public or protected memebrs of the class
- including primitives, objects, methods
- Package private memebrs are available if the child is in the same package as the parent
- private memebrs are restricted to the class they are defined in and never available via inherintance.
- PREVENT inheritance with **final** keyword
- 

## Single vs Multiple Inheritance
- class may inherit from only one direct parent class
- class may also inherit from another class that inherits from another class

- by design java doesnt support multiple inheritance. Only one exception: Multiple **interfaces**




```Java
// Steeds 1 parent
class Animal {}
class VierFooter {}
class Dog extends VierFooter{}
class Puppy extends Dog{}

```

## Inheriting Object

- java.lang.Object is parent van alles java classes



## Creating Classes
public - default  

abstract - final  

```
public/default abstract/final class ClassName extends ANotherClass{}
```

## Class Access Modifiers

- **top-level-class** is a class that is not defined inside another class
- **inner-class** is a class defined inside of another class

## this.

```
private String color;
public void setColor(String color) {
    color = color; // gaat dan field zetten met zichzelf -> null...
}
```
Daarom **this.color**


## super.
- moet als eerste worden uitgevoerd.
- parent class func uitvoeren
- mag maar 1x worden gebruikt in constructor
- verwijst naar de dichtst bijzijnde.


## Declaring constructors

- geen return type!

  ```
  public class Bunny {
    public Bunny(){}
  }

  
  public class Bunny {
    public bunny() {} // DNC
    public void Bunny() {} // is geen constructor maar compiles
  }
  ```

## Overloading Constructors this()
- this() is de eerste lijn in de contructor, MOET als eerste worden uitgevoerd.
- geen this aanroep loop -> DNC

## Missing Default No-Argument Constructor

```
public class Mammal {}

public class Elephant extends Mammal {} // DNC

```











```Java
public class Rabbit {

    public Rabbit(){}
    private Rabbit(boolean b){}
}


Rabbit b = new Rabbit();


```


```Java
public class Mammal {
    public Mammal(int age){}
}

public class Elephant extends Mammal {
    public Elephant() {
        //super(); DNC
        super(2);
        
    }
}
Elephant e = new Elephant();
```

## Constructors and final fields
- let op volgorde {} blocks dan pas constructor
- final mag maar 1x

## Order of Initialization
- super class first
- process all static variables in order of appearancce
- process all static inits in order

```
public class Animal {
    static { System.out.println("A");}
}

public class Hippo extends Animal {
    static { System.out.println("B");}

    public static void main(String[] args){
        System.out.println("B");
        new Hippo();
        new Hippo();
        new Hippo();
    }
}

```

- constructor start met this(); of super();
- geen this or super dan no-arg super()
- this() of super als niet eerste -> DNC
- if parent hasnt no-arg constr dan child moet starten met super of this()
- if parent hasnt no-arg constr en child not define constr -> DNC
- private constructors cannot dooorgegeven aan child
- final only once...




## Inheriting Members

- super.method() gebruiken (anders recusive overflow duh)

- the method moet zelde signature hebben asl parent
- same accessible as the parent method
- geen nieuwe exception toevoegen
- same return value / subtype **covariant return types**

### A subclass is a subtype but not all subtypes are subclasses... (interfaces!)

## Overloading vs Overriding

## Overriding Generic Method
-  cannot overload methods changing the generic type. -> type erasure

## Generic Method Params
- kan! maar moeten kloppen
- bij kleiner class scope dan wordt t overload

## Generic Return Types
- the return types must be covariant

## Redeclaring private methods
- permits to redeclare the same method

## Hiding Static Methods
- hidden method when a child class defines a static method with the same name asn sign as an inherited static method in the parent
- similar as overriding but not the same... Is meer masking dezelfde parent method met eigen implentatie
- let op : niet kleiner maken access...

## final Methods
- final cannot be replaced
- KAN NOOIT

## Hiding Variables
- java doesnt allow variable to be overriden.




## Polymorphism

- object can be referenced with the same type as the object, a superclass or an interface that is implemented.

### Interface
- can define **abstract** methods
- a class can implement any number of interfaces
- a class implements an interface by overriding the onherited abstract methods
- an object that implements an interface can be assigned to a reference for that interface.

### Object vs Reference

- In java all object are accessed by reference.

```
Lemur l = new Lemur();
Object lAsObject = l; // is gecast naar super object Object
```
- the type of the objevt determines which properties exists in memory
- the type of reference to the obj determines which methods and vars are accessible to the Java program

## Casting 
- implicit
- explicit
-  kan van parent naar child
-  kan NIET impliciet van child naar parent alleen met explicit casting...


```
Primate primate = new Lemur();
Lemur lemur2 = primate; // DNC

Lemur lemur3 =  (Lemur) primate; // Nu wel
```

1. Casting a refenrece from subtype to supertype doesnt require explicit casst
2. Casting a reference from a supertype to a subtype require epliciti cast
3. compiler disallows casts to an unrelated class
4. at runtime an invalid cast results in ClassCastException

```
public class Rodent{}

public class Capybara extends Rodent {
    public static void main(String[] args) {
        Rodent rodent = new Rodent();

        Capybara capybara = (Capybara)rodent; //Compiles but ClassCastException at runtime...
    }

}
```

## Instanceof
Kan niet gebruikt worden op ongerelateerd type....




```Java
class Bird {}
class Fish {}
Fish fish = new Fish();
//if(fish instanceof Bird) { //DNC
//    Bird bird = (Bird) fish; //DNC
//}
```

## Implement vs extends
- Use extends for class-to-class inheritance. (1x!)
- Use implements for class-to-interface relationships, allowing a class to commit to performing certain actions as defined by one or more interfaces.




## Polymorphism and Method Overriding
- polymorphism states that when you override a method you replace all calls to even those defined in the parent class.
- parent func met super hergebruiken.

## Overriding vs Hiding Members
- static methods and static vars cannot be replaced by override!!
- 


[ocp 08](http://hjh.devsnips.nl/ocp08)
[ocp 10](http://hjh.devsnips.nl/ocp10)