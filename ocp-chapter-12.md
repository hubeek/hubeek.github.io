# OCP Chapter 12

_Status: Published_
_Created: 2024-07-30 16:46:51_
_Tags: ocp_

# applying final modifier

- not needed to assign a value when final variable is declared.
- abstract <=> final. of t 1 of t ander. `public abstract final bla();` DNC
- final kan niet meer veranderen, one time assignement, not more
- variables + static variables
- final methods cannot be overriden by subclass
- na final class geen extends meer...
- `final interface` DNC...

## Enums
- an enum is a type of class that mainly contains static members
- values gescheiden door komma ,
- it contains helper func .values(), .ordinal(), .toString(), .compareTo(s), .equals(s)
- can create (abstract) methods
- enum value can be composed! END with semicolon ;!
- wanneer enum value composed dan  constructors for fields and methods

## Nested Classes
- inner class
- static nested class
- local class
- anonymous class

can acces members of outer class  

kan ook zo geinstantieerd worden...
```
Outer outer = Outer();
Inner inner = outer.new Inner();
```
### scoping vars inner class
De private vars blijven bereikbaar vanuit nested en parent.
```

public class Outer {

    private int x = 10;

    Outer() {
        Inner inner = new Inner();
        Inner.InnerDeeper inDeep = inner.new InnerDeeper();// niet Inner.new InnerDeeper()..
    }

    class Inner {

        private int x  = 20;

        Inner() {
            System.out.println("constructor inner");
            System.out.println("this private x");
            System.out.println(x);
            System.out.println(this.x);
        }

        public void doSomething() {
            System.out.println("inner does something");
            InnerDeeper innerDeeper = new InnerDeeper();

        }

        class InnerDeeper {
            private int x = 30;

            InnerDeeper() {
                System.out.println("In innerdeeper");
                System.out.println(x);
                System.out.println(this.x);
                System.out.println(Inner.this.x);
                System.out.println(Outer.this.x);
            }
        }
    }

    public void callInner() {
        Inner i = new Inner();
        i.doSomething();
    }
}

```


```
public class A {

    private int x = 10;

    class B {

        private int x = 20;

        class C {

            private int x = 30;

            public void allTheX(){
                System.out.println(x);//30
                System.out.println(this.x);//30
                System.out.println(B.this.x);//20
                System.out.println(A.this.x);//10
            }

        }
    }
}
```

    

## Static nested class
- can be instantiated without instance enclosing class
- cant access instance variables or methods in outer class directly. explicit reference to outer class is needed.
- enclosing class wordt als namespace gezien bij imports


  

## Local Class
- gewoon als local variable
- GEEN acces modifier
- toegang tot alle vars (als final, effectifly final) en methods in enclosing class
- Als local Class in Method dan vars in de method moeten effectively final zijn!!!


## Anonymous Class
- vergeet de ; niet!!


modifiers in nested classes
|permitted Modifiers|Inner Class| static nested class|Local class|Anonymous class|
|-------------------|-----------|--------------------|-----------|---------------|
|acces modifiers    | All       | All                | None      | None          |
|abstract           | Yes       | Yes                | Yes       | No          |
|final              | Yes       | Yes                | Yes       | No          |

members in nested classes
|permitted Members|Inner Class| static nested class|Local class|Anonymous class|
|-------------------|-----------|--------------------|-----------|---------------|
|Instance Methods    | Yes       | Yes                | Yes       | YES          |
|Instance Variables  | Yes       | Yes                | Yes       | YES          |
|static Methods    | No       | Yes           | No       | NO          |
|static Variables    | Yes (if final) | Yes           | Yes (if final)        | Yes (if final)           |

nested class acces rules
| |Inner class|static nested class| Local class|Anonymous class|
|-|-|-|-|-|
|can extend any class or implement any number of interfaces|Yes|Yes|Yes|No - exact 1 superclass or interface|
|can acces instance memebrs of enclosing class without reference|Yes|No|Yes(if declared in instance method)|Yes(if declared in instance method)|
|can access local var of enclosing method|N/A|N/A|Yes(if final)|No - exact 1 superclass or interface|




## Default Interface Method Definition Rules
1. default method may be declared only within an interface
2. default method must be marked with default keyword and include a body
3. default method is assumed to be public
4. default cannot be marked abstract, final or static
5. default may be overriden by a class that implements the interface
6. if a class inherits two or more default methods with the same method signature the the class must override the method

- default method is a method defined in an interface with default keyword and includes a method body

- default method alleen in interfaces!

## Inheriting duplicate default methods
- geen duplicate default methods wanneer er meerdere worden implemented
- wel duplicate als de dubbele word overriden




## static Interface methods
1. static method must be marked with static keyword and include method BODY
2. static method without acces modifier is public
3. static method kan niet abstract of final zijn
4. static method is not inherited and cannot be accessed in a class implementing the interface without a reference to the interface name...


## private interface methods
- tegen code duplication en als helper

1. private interface method must be marked with private modifier and include BODY
2. private interface method may be called by default and private (non-static) methods

## private static interface methods
1. must be marked private static + BODY
2. can be used by the other methods in the interface.


# Functional Programming

- annotations are optional
- Functional Interface is an interface that contains a single abstract method
- SAM regel Single Abstract Method
- any functional interface can be implemented as lambda expression


(in interface als method geen body heeft is ie impliciet abstract...)  

## Object parent heeft methods
- toString()
- equals(Object)
- hashCode()
- DEZE TELLEN NIET MEE in SAM regel




[prev](http://hjh.devsnips.nl/ocp11)
[next](http://hjh.devsnips.nl/ocp13)