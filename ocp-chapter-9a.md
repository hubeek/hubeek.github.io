# OCP Chapter 9a

_Status: Published_
_Created: 2024-07-30 16:43:25_
_Tags: ocp_

# Advanceed CLass Design

## Abstract classes
- Abstract class is a class that cannot be instantiated and may contain abstract methods.
- Abstract methods is a method that doesnot define an implementation when it is declared.
- Abstract class cannot instantiated
- Abstract methods alleen in Abstract Classess!!!
- abstract keyword VOOR class/return type keyword
- Geen final + abstract!!   //DNC
- Geen private + abstract!! //DNC
```
abstract class Asd {

    public static main(String[] args) {
        var a = new Asd(); //DNC
    }
}
public class abstract Zxc {    //DNC
    public int abstract ert(); //DNC
}

public abstract class Turtle {

    public abstract long eat()       //DNC
    public abstract void swim() {};  //DNC
    public abstract int getAge() { return 10;}   //DNC
    public void sleep;  //DNC
    public void goInShell(); //DNC
}

public abstract final class Turtle{ //DNC
    public anstract final void walk(); //DNC
}

```





```Java
public abstract class Asd {

    public void bla() {}
    
}
public class Qwe extends Asd {
    
}
var q = new Qwe();
q.bla();
```

## Abstract Class Rules
- abstract classes cannot be instanciated
- all top-level types including abstract classes cannot be marked **protected** or **private**.
- Abstract classes cannot be marked **final**
- abstract classes may include zero or more abstract and nonabstract methods
- abstract class that extends another abstract class inherits all of its abstract methods
- the first concrete class that extends an abstract class must provide an implementation for all of the inherited abstract methods
- abstract class constructors follow the same rules for initialization as regular constructors except they can be called only as part of the initilization of a subclass

## Abstract Method Definition Rules
- Abstract methods can be defined only in abstract classes or interfaces
- Abstract methods cannot be declared **private** or **final** 
- Abstract methods must not provide a method body/implementation in the abstract class in wich they are declared.
- Implementing an abstract method in a subclass follows the same rules for overriding a method including covariant return types exception declarations etc


## implementing Interfaces
- any number of interfaces can be implemented
- interface is an abstract data type tyhat declares a list of abstract methods that any class implementing the interface must provide.
- interface can include constant variables.
- abstract methods and constant vars included with the interface are implicitly assumed to be public
- interface cannot be marked final

```
public/default abstract interface CanPurr{ 
    public abstract Float getSpeed(int start)
    public static final int MIN  = 2;
}
```
- **abstract** is implicit modifier. implicit modifier is a modifier that the compiler automatically adds to a class, interface, method or variable declaration.

## Implicit modifiers
- interfaces are assumed to be abstract
- interface variables are assumed to be public, static and final
- interface methods without a body are assumed to be abstract and public
- interface can implement another interface
- meerdere interfaces met dezelfde methods moeten compatible zijn
```
public interface Soar {
 int MAX_HEIGHT = 10;
 final static boolean UNDERWATER = true;
 void fly(int speed);
 abstract void takeoff();
 public abstract double dive();
}

public *abstract* interface Soar {
 *public static final* int MAX_HEIGHT = 10;
 *public* final static boolean UNDERWATER = true;
 *public abstract* void fly(int speed);
 *public* abstract void takeoff();
 public abstract double dive();
}

interface Dance {
 private int count = 4;// DNC
 protected void step(); //DNC
}
```

## Interfaces vs Abstract Classes
- interfaces make use of implicit modifiers

## Interface Definition Rules
- interfaces cannot be instantiated
- all top level types including interfaces, cannot be marked protected or private
- interfaces are assumed to be abstract and cannot be marked final
- interfaces may include zero or more abstract methods
- an interface can extend any number of interfaces
- an interface refenrece may be cast to any reference that inherits the interface although this may produce an exception at runtime if the classes arent related.
- the compiler will only report an unrelated type error for an instanceof operation with an interface on the right side if th ref on the left side is final classth at doesnot inherit the interface
- an interface method with a body must be marked default, private, static ot private static.

## abstract interface methods rules
- abstract methods can be defined only in abstract classes or interfaces
- abstract methods cannot be declared private or final
- abstract methods must not provide a method body/implementation in th eabstract class in which it is declared
- implementing an abstract method in  a subclass follows the same rules for overriding a method including covariant return types, exceptios,
- interface methods without a body are assumed to be abstract public

## Interface Variables Rules
- interface variables are assumed to be public, static and final
- because interface vars are marked final the must initialze with a value when they are declared.

# Inner Classes




```Java

```
[prev](http://hjh.devsnips.nl/ocp09)
[next](http://hjh.devsnips.nl/ocp10)