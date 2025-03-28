# OCP Chapter 04

_Status: Published_
_Created: 2024-07-29 10:49:40_
_Tags: ocp_

#  Chapter 04 Making Decisions

a Java *statement* is a complete unit of execution in Java terminated with a semicolon.  
*Control flow statement* break up th e flow execution by using decision making, looping branching aollowing breakup the flow to selectively exewcute segments of code.  


- statement => bla + ;
- control flow statement => single expression naar code block;

## Desicion Making Statements

```
if(a >1)  
b++;  


if(c>1) {  
  d++;    
}   
```






## if statement
```
if(booleaExpression) {

}
```
## else
```
if(booleaExpression) {

} else {

}
if(booleaExpression) {

} else if(booleaExpression2) {

}
```

## check of expression evaluetes in boolean

**0 en 1 zijn GEEN booleans...**
```
int a = 1;  
if(a) {} //DNC!!! moet boelean result zijn... 1 is geen boolean  

if(b=2){}//DNC ook geen boolean expression....
```

## Switch

- switch statement has a target variable that is not evaluated until runtime.
- NOT boolean long float double EXCLUDE from switch statments
- enums kunnen in switch
- int Integer
- short Short
- char Character
- String
- enum
- var


wordt pas tijdens runtime geevolueerd!  


```
switch (varToTest) {
  case constanExpression:
  // ...
    break;
    case constanExpression2:
  // ... // hier hoeft niet iets verplichts, mag leeg...
    break;
    default: // default is optionally!
    // ...
}
```


```Java
int a = 1;
switch(a){
        
} // GAAT GOED

switch(a) {
    case 1 | 2: 
}

```

```
int a = 5;
switch a {} // DNC BOOGJES om a!!!

switch (a)
    case 1: sout(); // DNC curly braces!!!

switch(a) {
    case 1: 2: sout(""); //DNC case voor 2:
}

switch(a) {
    case 1 || 2: sout(""); //DNC boolean expression mag niet
}


switch(a){
    case a == 1 ://zelfde als hierboven GEEN INT MAAR BOOLEAN
        break;
}

```

Switch werkt met:
- int Integer
- byte Byte
- short Short
- char Character
- String
- enum
- var met 1 van hierboven

!! Niet MET:
- boolean
- long
- float
- double






```Java
class A {int a = 1;}
A aa = new A();
switch (aa.a) {
    case 1:
        System.out.println("werkt");
}
```

    werkt


# alleen final var in case gedeelte DNC


# While
```
while (booleanExpression) {

}
```

# Do While

```
do {

} while (booleanExpression)
```


## For loops

### C style

for (init ; boolean; update) {}

- init value must be same type!

infinit loop  

for (;;) {}

multiple terms  

for (long x = 0, y =1, z = 2; x<4 && z <<6; x++,y++, z++) {}

Redecalring fails  
```
int x = 0;
for(int x = 4;x<5;x++){} //DNC
```


## For-each loops

for (datatype instance ; collection) {}  

- built in java araay
- an onject whose type implements java.lang.Iterable

```
String[] names = ...;
for (String name ; names) {}
```


```Java
// String[] names = new String[3];
// for(String name; names) { 
//     System.out.println(name);
// }
```


    |   for(String name; names) { 

    ';' expected

    


## Optional Labels

    ### break

    optionalLabel: while(boolExpr) {
      break optionalLabel;
    }

## Continue statement

[ocp 03](http://hjh.devsnips.nl/ocp03)
[ocp 05](http://hjh.devsnips.nl/ocp05)


