# OCP Chapter 03

_Status: Published_
_Created: 2024-07-29 10:48:32_

# Operators

- operator is a special symbol that can be applied to a set of variables or literals, referred as operants and returns a result  
- operand is operator applied to
- result value na uitvoering operation op operand.
- unary
- binary
- ternary




## Operator Precedence

Meneer Van Dale wacht Op Antwoord  

1. Post unary operators expression++
2. Pre unary operators --expressions
3. other unary operators - | ~ + (type)
4. Mult/div/modulus * / %
5. Shift << >> >>>
6. Relational logic operators < >  <= >= instanceof
7. (not) equal == !=
8. Logiacal & ^ |
9. short circuit logical && ||
10. ternary asda =123? a:b;
11. assign = += *= /= %= ^= |= <<= >>= >>>=
12. 

Fout:  

int p = !5; //DNC
boolean p =-true; //DNC
boolean p = !0; //DNC


## increment decrement operators ++ --

int p = 0  
sout(p);//0  
sout(++p);// 1  
sout(p);// 1  
sout(p--);// 1  
sout(p);// 0  




```Java
int lion = 3;
int tiger = ++lion * 5 / lion--;
System.out.println("lion: "+ lion);
System.out.println("tiger: "+ tiger);
```

    lion: 3
    tiger: 5


daarna van links naar rechts

## Numeric Promotion

1. if two value have different data types Java will auto promote one of the values to the larger valuetype
2. if one of the values is integral and the other is floating point java will auto promote the integral to floating
3. smaller data types byte short char are first promoted to int when used with binary aritmetic operator!
4. after all promotion th result will be of the promoted operands.

let op 3.  
short = 10;  
shot y= 3;
var z = x * y;  
Eerst naar int !!!!   
    

## Casting
lonf l = 10(long); //DNC !!!

## Overflow Underflow
wanneer de max wordt bereikt met int is de volgende stap de max_minum...



```Java
int i = Integer.MAX_VALUE+1;
System.out.println(i); // Wordt dus negatief
```

    -2147483648


## Comparing values
Equality  operators used:
- two numeric or char primitive types
- comparing two booleans
- comparing two objects, including null and String

Not compare two types!  
boolean b = true == 3; //DNC!!!  
boolean b = false != "grape"; //DNC!!!  
boolean b = 10.2 == "Koko"; //DNC!!!  

null == null; !!!! TRUEEE !!!

### Relational Operators < > >= <= a instanceof b

- comparing incompatible types  
public static void open(Number time) {  
  if(time instanceof String){} //DNC  
}


geldt alleen voor classes NIET voor INTERFACES......  


### null instanceof is altijd false

null instanceof null // DNC!!!








- AND & is only true when both are true
- inclusive OR |  is only false when both are false
- XOR ^ exclusif or is only true when both are different 

- && is only true when both are true
- ||  is only true when one is true


## NullPointerEXCEPTOIN
if(duck!=null && duck.getAge()<5) // Could throw NullPoijnterException


## Unperformed Side Effect

if (true || false ) // dankomt ie niet bij false gedeelte  




```Java
//boolean a = (boolean)true;
byte a = 5;
short b = 10;
short c = a + b;
```


    |   short c = a + b;

    incompatible types: possible lossy conversion from int to short

    
[ocp 02](http://hjh.devsnips.nl/ocp02)
[ocp 04](http://hjh.devsnips.nl/ocp04)