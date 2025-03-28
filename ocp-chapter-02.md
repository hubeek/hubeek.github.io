# OCP Chapter 02

_Status: Published_
_Created: 2024-07-29 10:47:12_
_Tags: ocp_

# Java Building blocks
p. 38

- Primitive Data Types

## Creating Objects
instanciate a class:    
```Park p = new Park();```
p stores the refe to object  
constructor:    
- the name of the constructor matches the name of the class.
- NO return type.
purpose of a constructor is to initialize fields.  

initialize on line  
or  
initialize in constructor  

```
public classs Chick {
    public Chick(){
        // do something..
    }
}
```
```
public classs Chick {
    public void Chick(){} // NOT A CONSTRUCTOR (return type...)
}
```



# Volgorde init telt

- Order of appearance!
- constructor runs after all fields and instance init blocks have run!

## Werkt niet
```
public class ObjectsInits {
    public static void main(String[] args) {
        Name n = new Name();
        System.out.println(n.full);
    }
}

class Name {
    String full = first + " " + last; // first en last zijn er nog niet... Illegal forward reference
    String first = "hj";
    String last = "hubeek";
    
}
```

## Werkt wel
```
class Name {
    String first = "hj";
    String last = "hubeek";
    String full = first + " " + last; // nu wel ...
}
```


```Java
class Name {
    
    String first = "hj";
    String last = "hubeek";
    String full = first + " " + last; // speel met hier of hierboven plaatsen... spoiler hierboven gaat t mis ivm illegal forward referrence
}
Name n = new Name();
System.out.println(n.full);
```

    hj hubeek


## blocks in classes

gaan op volgorde van de code  
dan constructor!!!  

Niet correcte open en closing braces => wont compile  
*balanced parentheses problem*  

count blocks => tel de {}  
count instance initializers NIET IN METHOD!!!



```Java
class BlockesInMyClass{
    String name;
    {System.out.println("vanuit block boven constructor...");}
    BlockesInMyClass() {
        System.out.println("vanuit constructor...");
        this.name = "hjh";
    }
    {System.out.println("vanuit block onder constructor...");}
    public void func(){
        // do something...
        {System.out.println("block in func...");}
        
    }
}

BlockesInMyClass b = new BlockesInMyClass();
System.out.println(b.name);
b.func();

```

    vanuit block boven constructor...
    vanuit block onder constructor...
    vanuit constructor...
    hjh
    block in func...


# 2 Types: Primitive & Reference Types

**8 primitive types**  
a primitive is just a single value in memory  
String is NOT a primitive  maar object    

| Type    | Bits   | Standard Default | Minimum Value                | Maximum Value                |
|---------|--------|------------------|------------------------------|------------------------------|
| boolean | varies | false            | N/A                          | N/A                          |
| byte    | 8-bit  | 0                | -128                         | 127                          |
| short   | 16-bit | 0                | -32768                       | 32767                        |
| char    | 16-bit | '\u0000'         | 0 ('\u0000')                 | 65535 ('\uffff')             |
| int     | 32-bit | 0                | -2147483648                  | 2147483647                   |
| float   | 32-bit | 0.0f             | -3.4e+38                     | 3.4e+38                      |
| double  | 64-bit | 0.0d             | -1.79e+308                   | 1.79e+308                    |
| long    | 64-bit | 0L               | -9223372036854775808         | 9223372036854775807          |


.MAX_VALUE
float en double hebben ook .POSITIVE_INFINITY and NaN


alle numeric types zijn SIGNED dus 1 bit voor negative value  

range kennen van byte -128 tot 127  

char is UNSIGNED  

char dus geen negative waarden  

char kan dus (2x) grotere waarden bevatten dan short  
  


```Java
short d = 'd';
char mammal = (short) 83;
int i = 0b10;

System.out.println(d);
System.out.println(mammal);
System.out.println(i);
```

    100
    S
    2


## literals
when a numbers is represented in code dan heet t n literal.  

long max = 3123123123123; does not compile want is int(!)  

long max = 3123123123123L; nu wel want is long  

long max = 3123123123123l; nu wel (Met kleine letter l!!!!!)NIET DOEN!!! LEEST ALS een 1 ws... GRGRG!   


### Octal
zet er een 0 voor
017

### Hex
0x of 0X ervoor
0xde

### Binairy
0b od 0B ervoor
0b10

## underscore

**Niet als eerste of laatste character**  

**Niet voor of na de komma in t numme**  


double notAtStart = _1000.00;      // DOES NOT COMPILE  

double notAtEnd = 1000.00_;        // DOES NOT COMPILE  

double notByDecimal = 1000_.00;    // DOES NOT COMPILE 

double notByDecimal = 1000._00;    // DOES NOT COMPILE 


double magWel = 10_0_0.0_0;    // WERKT WEL MAAR LELIJK  

double magWel2 = 1________2;    // WERKT WEL MAAR LELIJK  



# Reference Types

reference types refers to an object.  

a ref points to an object by storing its memory address. pointer.  

a value is assigned :  
- to another obj of the same or compatible type  
- to a new object using the new keyword.

Reference type can be null; NULL  
Primitive Types NEVER can be NULL!!!!  


int v = null; //DOES NOT COMPILE  

String s = null;// wel!  

Types beginnen standaard met null;  

Will je null of een helper method voor bool, byte, short, int, char,double, float, long use wrapper classes:
Boolean, Byte, Short, Integer, Character, Double, Float, Long  




```Java
long l = null;

```


    |   long l = null;

    incompatible types: <nulltype> cannot be converted to long

    


# Declaring vars

initializing a var

## Identifiers
naming  

snake_case  
cameCase  


---

variablelen beginnen met:  

letter  
$    Dollar sign   
_     Underscore



geen number als start    
_ alleen als naam mag niet meer....   
geen reserved keyword...    

---



MAG NIET:   
int 3DjqkoewarClass; NIET MET NUMBER STARTEN   
byte holly@vine; GEEN @   
String *$coffee; GEEN *   
boudle public; RESERVED keyword   
shirt _; geen underscore..... is geen swift   


## Declaring multiple vars

int i1, i2, i3 =0; 3 declared 1 initialized.

int num, String value; DOES NOT COMPILE DIFFERENT TYPE in same statement...

double d1, double d2; MAG OOK NIET

## Local vars

public int notValid() {
 int y= 10;
 int x;
 int reply = x+ y; // DOES NOT COMPILE
 return reply;
}

public int isValid() {
 int y= 10;
 int x;
 x = 3
 int reply = x+ y; // DOES COMPILE
 return reply;
}

## Passing Constructor and Method Params
moeten declared and init zijn

## Var keyword
voor leesbaarheid...

assign en define on same line!!!

var is reserved TYPEname not a reserved word!!!! Dus kan als class, interface of enum...niet doen dus...

public class VarKeyWord{
    var tricky = "this is a string";// DOEs NOT COMPILE
}

public void twoTypes() {
int a, var b = 3; /// DNC
var n = null; ///DNC
}

var o = (String)null;//Doet t wel...

---

Can be used:
Local variable declaration inside methods or initializers.
Local variables in for-loops.

Cannot be used:
Class or instance variable declaration.
Method parameters.
Method return types.
Constructor parameters.
Multiple var declaration

---


## Var scope

scope binnen   
constructor  
method  
initializer block   



public void eat(int pieces){
    int bites = 1;
} // heeft dus 2 vars


public void eatIfHungry(boolean hungry){  
    if(hungry) {  
        int cheese = 1;  
    }  
    System.out.println(cheese); // DNC !!!  
}  

public int bla(var a, var b) {} // DNC!!! alleen BINNEN constructor Method init blockkk!!!!!    

public classs Var {    
  public void var() {  
    var var = "var";  
  }  
  public void Var() {  
    Var var = new Var();  
  }

}  
COMILES!!!!! Var is niet een system keyword....  

public class var { public var(){} } ?? DNC !!!!!!!!    


DUS var NIET VOOR CLASS INTERFACE EN ENUM!!!!!!


## Garbage Collection

System.gc();

not garanteed to do anything.

- the object no longer has any ref to it.
- all refs to obj are out of scope.

finalize() is deprecated in java 9. can run zero or 1 times. never twice.



# var Rules
1. var is used as a local variable in a constructor, method or initializer block
2. var cannot be used in params of constructor, method, instance vars, class variables...
3. var is always initialized on the same line where it is declared. declared + initiialized.
4. value var can change, type NEVER
5. var cannot be init with null
6. var niet in multiple-variable declaration
7. var is reserved type name not reserved word. can be used as an identifier for class, interface or enum name...


[ocp 01](http://hjh.devsnips.nl/ocp01)
[ocp 03](http://hjh.devsnips.nl/ocp03)