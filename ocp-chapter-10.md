# OCP Chapter 10

_Status: Published_
_Created: 2024-07-30 16:42:10_
_Tags: ocp_

# Exceptions

- Throwable superclass
- Throwable is parent van Exception en Error
- Exception is parent van RuntimeException

- RuntimeException kan altijd gegooid worden. De andere Exceptions moeten worden gechecked
- Exception hoeft niet bad te zijn
- checked exception => CHECKED by the compiler
- unchecked exception => NOTCHECKED by the compiler

- Bij overriding methods only same or less exceptions NOT more exceptions

Throwable     
&nbsp;&nbsp;Exception    
&nbsp;&nbsp;&nbsp;&nbsp;RuntimeException  

&nbsp;&nbsp;Error   
&nbsp;&nbsp;&nbsp;&nbsp;OutOfMemoryError    
&nbsp;&nbsp;&nbsp;&nbsp;StackOverflowError  



## exceptions
![exceptions.png](OCP Chapter 10_files/c8216fb0-f902-4794-92cd-7ac0b87ee4dc.png)
    




## Exception Types
- Throwable
- Exception
- Error



## Checked Exceptions
- must be declared or handled by the application where it is thrown
- checked exception inherit Exception but not RuntimeException
- try catch blocks
- handle or declare rule


## Unchecked Exceptions
- checked exceptions
- unchecked exceptions (Runtime exceptions)
- unchecked do not need to be declared or handled where it is thrown. RuntimeExceptions or Error
- unexpected but not fatal.


## throws and throw

## Recognizing Exception Classes
- RuntimeException 
- checked Exception (oplossen!)
- Error


|type|how to recognize|okay for program to catch|Is program required to handle or declare|
|----|----------------|-------------------------|----------------------------------------|
|Runtime Exception|Subclass of RuntimeException| YES|No|
|Checked Exception|Subclass of Exception but not RuntimeException| YES|YES|
|Runtime Exception|Subclass of Error| No|No|


```
RuntimeException e  = new RuntimeException();
throw e;
Exception e  = new Exception(); 
throw e; // DNC

public class MyRuntimeException extends RuntimeException {

    public MyRuntimeException() {
        super("My runtime exception");
    }
}

public static void main(String[] args) {
        MyCheckedException e = new MyCheckedException(); // DNC
        throw e; //DNC
    }
```

Checked exception
- program continues na catch

RuntimeException
- continues in try catch
- stops als niet in try catch

Error stopt altijd


## Recognizing Exception CLasses

- ArithmeticException - Thrown when code attempts to divide by zero  
- ArrayOutOfBoundsException - array en illegal index
- ClassCastException - illegal cast to another class
- NullPointerException - when there is a null reference when object is required..
- IllegalArgumentException - method input illegal (handig als guard met specifieke error)
- NumberFormatException - "123abc" is een string die niet naar nummer kan SUBCLASS van IllegalArgumentException

## ClassCastException
let op:
```
String s = "sdf";
        Object o = s;
        Integer i = (Integer) o;
// bouwt wel maar runtime error

String s = "sdf";
Integer i = (Integer) s; // bouwt niet.
```


## Checked Exceptions Classes

- IOException while reading/writing file 
- FileNotFoundException subclass of IOException

## Error Classes

- ExceptionInInitializerError static init throws
- StackOverflowError endless loop in memry
- NoClassDeffoundError 



## Handling Exceptions

- eerst subclass dan parent anders unreachable code => DNC
- multicatch met | => catch( exception1 | exception2 error) {}
- multicatch met 1x error variable!
- multicatch niet met sub and parent classes DNC
- exception kan maar in 1 catch voorkomen
- catch niet verplicht kan maar moet niet
- 
## Finally
- als geen catch dan finally
- finally will always run!
- finally kan zonder catch
- allen System.exit(0); kan finally doen ontlopen
- finally is handig om resources af te knopen

## Closing resources

- *try-with-resources* statement or automatically cloase all resources openend in a try clause.  
- mag catch en finnally overslaan
- implicit finally runs FIRST
- 1x finally is max
- declaring multiple resources gescheiden door ;

## Scope of try-with-resources
- Scope is alleen in de try. Niet catch en finally....
- resources are closed after try en before catch&finally
- resource closed in reveoerse order of creation

## Declaring and Overriding Methods with exceptions
- minder CHECKED exceptions mag in child NIET in parent
- child mag ook child van exception
- unchecked exception mag minder of meer in childs en parents

## printing exceptions
- sout(e)
- sout(e.message())
- e.printStackTrace()

[prev](http://hjh.devsnips.nl/ocp09b)
[next](http://hjh.devsnips.nl/ocp11)