# OCP Chapter 07

_Status: Published_
_Created: 2024-07-30 16:34:56_
_Tags: ocp_

# Methods and Encapsulation


| acces modifier | optional specifier | return type | method name | ( params) | exception (optional) |
|----------------|--------------------|-------------|-------------|-----------|----------------------|
| public | final | void | nap | ( int minutes ) | throws Exception |


```
public final void nap(int minutes) throws Exception {
    // do a nap
}
```

- method declaration
- method signature (name and param list)

| Element | value in nap() | Required |
|---------|----------------|----------|
| Acces modifier| public | NO |
| optional specifier| final | NO |
| RETURN TYPE| void | YES |
| METHOD NAME | nap | YES |
| Param list| (int minutes) | YES () can be empty |
| Optional Exception List| public | NO |
| METHOD BODY | public | YES {} can be empty |


## Access Modifiers
- private , only from the same class
- default (Package Private) Acces, from same package (no keyword!)
- protected , same package or subclasses , bij extends Clazz
- public, can be called from any class

```
public void walk() {}
default void walk() {} // DNC
void public walk() {} // DNC
void walk() {}
```

## Optional Specifiers
- may be multiple!
- static,
- abstract, when a method body is not provided.
- final not allowed to be overriden by subclass
- synchronized, multithreaded code
- native , when interacting with code from another language
- strictfp , floating point calc portable

```
public void walk() {}
public final void walk() {}
public static final void walk() {}
public final static void walk() {}
public modifier void walk() {} //DNC
public void final walk() {} //DNC
final public void walk() {}
```

## Return Type

- must have, moet er zijn mag er niet uit, gebruik void


```
public void walk() {}
public void walk() {return;}
public String walk() {return "":}
public String walk() {} //DNC
public walk() {} // DNC
public String int walk() {} //DNC
String walk(int a) {if (a==4) return "";} //DNC
```

## Method Name
- alleen letter, nummers $ of _ maar eerst character is niet nummer, en geen reserved words
- _ alleen mag ook niet
- begint met kleine letter

```
public void walk() {}
public void 2walk() {} //DNC
public walk3 void() {} //DNC
public void Walk_$() {}
public _() {} //DNC
public void () {} //DNC
```

## Parameter list
- not required 0 of meer
- separeer met komma

```
public void walk() {}
public void walk {} //DNC
public void walk(int a) {}
public void walk(int a; int b) {} //DNC
public void walk(int a, int b) {}
```

## Optional Exception List
- 0 of meer exceptions, komma gescheiden

## Method Body
- moet er zijn, mag leeg

## Varargs
- moet laatste element vd param list zijn
- mag dus maar 1 zijn
- als laatste
- met varargs kanje ook komma gescheiden aanleveren
```
public void walk(int... nums){}
public void walk(int start, int... nums){}
public void walk(int... nums, int start){} // DNC
public void walk(int... nums, int...start){} // DNC

public static void walk(int start, int... nums) {
    System.out.println(nums.length);
}
public static void main(String[] args){

walk(1); // 0
walk(1,2); //1
walk(1,2,3);//2
walk(1, new int[]{4,5});//2


}
```










## Let op!

```
package pond.shore;
public class Bird {
    protected String text = "floating";
    protected void floatInWater() {
        System.out.println(text);
    }
}

package pond.swan;
import pond.Bird;
public class Swan extends Bird {
    public void smwin() {
        floatInWater();            //sublcass access to super class
        System.out.println(text);  //sublcass access to super class
    }


    public void helpOtherSwanSwim() {
        Swan other = new Swan();
        other.floatInWater();            //sublcass access to super class
        System.out.println(other.text);  //sublcass access to super class
    }

    public void helpOtherBirdSwim() {
        Bird other = new Bird();         // <-- !!! Bird ref en Bird is in ander package.
        other.floatInWater();            //DNC
        System.out.println(other.text);  //DNC
    }
    
}
```

| method in  __ can access a __ meber | private | default | protected | public |
|-------------------------------------|---------|---------|-----------|--------|
| same class | YES | YES | YES| YES|
| same package | NO | YES | YES| YES |
| subclass in diff package | NO | NO | YES| YES |
| unrelated + diff package | NO | NO | NO| YES |



```Java
public class ASD {

    public static void main(String[] args) {
        long a = test();
        System.out.println("longe int");
    }
    
    static long test() {
        System.out.println("int past wel in long");
        return 12;
    }
}
ASD a = new ASD();
a.test();

```

    int past wel in long





    12



## Static keywordp

- dont require an instance of a class
- shared, independed lifecycle
- for utility or helper methods like uppcase()
- for state that is shared like a counter
- from static cannot to non static.


### Static vs Instance
- only one static method. no copys. 
### Static variables
- static **final** is a constant

### Static Initialization
- static block runs first when class is first used..

### Static imports
- for **members** of classes
```
import static java.util.Arrays.asList;
import static statics.A.TYPE;
import static statics.B.TYPE; // DNC mag niet dezelfde naam hebben
```

### Passing Data 
#### Pass By Value
- Java is pass by value language
- assigning a new primitive or reference to a parameter doesnt change the caller
- Calling methods on a reference to an Object DO AFFECT the caller!


```
public static void main(String[] args) {
    int ori1 = 1;
    int ori2 = 2;
    String letters = "asd";
    swap(ori1,ori2);
    voegToe(letters);
    System.out.println(ori1); // GEBEURT NIX!!! GEEN SWAP
    System.out.println(ori2);
    System.out.println(letter);
}

public static void swap(int a, int b) {
    int temp = a;
    a = b;
    b = temp;

}
public static void voegToe(String letters) {
    letters += "d";
    

}
```
TODO


```Java
public static void main(String[] args) {
    int ori1 = 1;
    int ori2 = 2;
    String letters = "asd";
    swap(ori1,ori2);
    voegToe(letters);
    System.out.println(ori1); // GEBEURT NIX!!! GEEN SWAP
    System.out.println(ori2);
    System.out.println("na voegtoe "+letters);
    letters = voegToe2(letters);
    System.out.println("na voegtoe2 "+letters);
    ori1 = voegToe1(ori1);
    System.out.println(ori1);
}

public static void swap(int a, int b) {
    int temp = a;
    a = b;
    b = temp;

}
public static void voegToe(String letters) {
    letters += "d";
}

public static int voegToe(int a) {
    a += 8;
    return a;
}

public static String voegToe2(String letters) {
    letters += "d";
    return letters;
}
main(new String[]{}); // ZIJN DUS NIET GESWAPPED!!!!

```

    1
    2
    na voegtoe asd
    na voegtoe2 asdd
    9



```Java
public class Koala {
    public static int count = 0;
    public static void main(String[] args) {
       System.out.println("init "+count); 
    }
}

Koala k = new Koala();
System.out.println("first "+k.count); 
k = null;
System.out.println("second "+k.count); 
Koala.count = 4;
Koala k1 = new Koala();
Koala k2 = new Koala();
Koala.count = 6;
Koala.count = 5;
System.out.println("last "+k.count); 
```

    first 5
    second 5
    last 5


## Overloading Methods
- same name in  the same class
- same name different signature (method input params)
- diff acces modifiers
- specifiers
- return types (return type is niet onderdeel vd signature, als param list niet gelijk is)
- exceptions

- Werkt niet met niet-static en static

### Varargs
let op! array en varargs zijn hetzelfde nl array...

```
public void fly(int[] lengths){}
public void fly(int... lengths){} // DNC want is hetzelfde al hierboven...
```

### Autoboxing
- Java will match the correct version if there is an option

```
public void fly(int length) {
    System.out.println("int "); 
}

public void fly(Integer length) {
    System.out.println("Integer "); 
}
// Autoboxing....
fly(new Integer(12));
fly(12);
//Integer
//in
```
### Reference types
-  Java try to find a direct match

### Primitives
- Java tries to find the most matching overload.

### Generics
```
public static void walk(int[] a){}
public static void walk(Integer[] a){}

// Type Erasue 
public void walk(List<String> str) {}
public void walk(List<Integer> int) {} //DNC

// want na compile ziet t t er zo uit
public void walk(List str) {}
public void walk(List str) {}
// En zijn dan de dezelfde paramlists....
```


### Only 1 conversion...
```
public class TooManyConversions{
    public static void play(Long l){}
    public static void play(Long... l){}
    public static void main(String[] args) {
        play(4);// DNC want int -> long -> Long !!!!
    }
}
```

### Encapsulating Data
- access control mbv private fields
- getters setters
- setter == mutator




```Java
public static void walk(int[] a){}
public static void walk(Integer[] a){}
class Move {
public void walk(List<String> str) {}

//public void walk(List<Integer> int) {} //DNC
}
Move a = new Move();
```


```Java
public void fly(int length) {
    System.out.println("int "); 
}

public void fly(Integer length) {
    System.out.println("Integer "); 
}
// Autoboxing....
fly(new Integer(12));
fly(12);
```

    Integer 
    int 



```Java

```
[ocp 06](http://hjh.devsnips.nl/ocp06)
[ocp 08](http://hjh.devsnips.nl/ocp08)