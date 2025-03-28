# OCP Chapter 05

_Status: Published_
_Created: 2024-07-30 11:51:35_
_Tags: ocp_

# Core Java APIs

## Strings

### Concat with numbers
- if both numbers => addition
- if one is String => concat
- expressio is evaluated from left to right.

```
System.out.println("1+2");          // 3  
System.out.println("a" + "b");      // ab  
System.out.println("a" + "b" + 3);  // ab3  
System.out.println(1+2+"a");        // 3a 
System.out.println("a"+1+2);        // a12
```


```Java
System.out.println("a"+1+2+3);   
```

    a123


## Immutability

Once created it is not allowed to change.


```Java
String s1 = "1";
String s2 = s1.concat("2");
s2.concat("3");
System.out.println(s2);
```

    12


## String methods

### .length()
### .charAt() let op StringIndexOutOfBoundsException
### .indexOf() -1 when not found
### .substring() optional endIndex is er 1 voorbij end!!!


```Java
String s1 = "abcdef";
System.out.println(s1.length()); // 6
String s2 = s1.substring(2);
System.out.println(s2); // cdef

String s3 = s1.substring(2, 6); // 6 (is dus 1 er voorbij....)
System.out.println(s3); // cdef

String s4 = s1.substring(2, 3); 
System.out.println(s4); // c

String s5 = s1.substring(2, 2); 
System.out.println(s5); // EMPTY STRING


// s1.substring(2, 1); EXCEPTION 
// s1.substring(2, 7); EXCEPTION 
```

    6
    cdef
    cdef
    c
    


### .toLowerCase() .toUpperCase()
### .equals() .equalsIgnoreCase()
### .startsWIth() .endsWith() !! Case sensitive !!
### .replace()
### .contains()
"asd".contains('a') // Incompatible types
    


```Java
System.out.println("asd".contains("a"));
```

    true


### .trim()
### .strip() .stripLeading() .stripTrailing() Supports unicode!
### .intern()
    


```Java
System.out.println("asd".intern());
```

    asd


## StringBuilder
```
new StringBuilder;
new StringBuilder("saasdf");
new StringBuilder(12);
```

.charAt(), .indexOf(), .length(), .substring()  
.append()   
.insert()  

.delete()  
.deleteCharAt()  

String str = "asd";
str.deleteCharAt(5) // exception

StringBuilder sb = new StringBuilder("asd");
sb.delete(1,100);





```Java

StringBuilder sb = new StringBuilder("asd");
sb.delete(1,100);
```




    a



### .replace()
### .reverse()
### .toString()

## Equality

### equals() vs ==
- if class doesnt have equals method Java checks refences are equal when == is operator...
- == heeft zelfde type nodig
- == checking for reference equality

<,,,<


```Java
StringBuilder one = new StringBuilder();
StringBuilder two = new StringBuilder();
StringBuilder three = one.append("a"); // one and three are referencing to the same object! == works

System.out.println(one == two);//false
System.out.println(one == three);//true

String x = "hello";
String z = " hello";

System.out.println(x.equals(z.trim())); // true

// var a = x == one; // twee verschillende types... DNC
var b = x.equals(one) ? true : false; // false....twee verschillende types . doet t wel...
System.out.println(b); // 
```

    false
    true
    true
    false


## String Pool
Strings are immutable!!!!!

- contins literal values and constants
- "name" is literal
- myObject.toString() is a string but not a literal so it doesnt go to the stringpool
- Strings are reused

```
String x = "asd";
String y = "asd";
System.out.println(x == y); // true!!! 
```

```
String x = "asd";
String y = " asd".trim();
System.out.println(x == y); // false!!! computed at runtime...
```

```
String x = "Hello";
String y = new String("Hello");
System.out.println(x == y); // false!!! 
```
```
String x = "Hello";
String y = new String("Hello").intern();
System.out.println(x == y); // TRUE!!! 
```

.intern() en == is alleen voor examen. Gebruik nooit in je code.  



## Arrays

- char is primitive. char[] niet is een ref naar array van chars.
- array is ordered list
- array is van primitives of objects
- contents equality is with: Arrays.equals(array1, array2)

### Array of primitives
```
int[] nums = new int[3];

int nums2 = new int[] {1,2,3}; // inline

int[] nums;
int [] nums;
int []nums;
int nums[];
int nums [];
```





```Java
int[] nums = new int[3];

for(int i: nums) {
    System.out.println("asd");
} // array heeft dus 3 0-en!!

int ids[], types;

String[] strings = {"asdasd"};
Object[] objects = strings;
String[] againStrings = (String[]) objects;
// againStrings[0] = new StringBuilder(); // DNC String[] != StringBuiler class
// objects[0] = new StringBulder(); // Nu String[] in Object dus ook andere class
```

    asd
    asd
    asd


### Sorting
```
import java.util.*;
import java.util.Arrays;
```



```Java
import java.util.Arrays;
import java.util.Collections;

int [] nums = {5,3,1};
Arrays.sort(nums);
for(int num: nums) {
    System.out.println(num);
}
    System.out.println("---\n");
Integer[] numsObj = Arrays.stream(nums).boxed().toArray(Integer[]::new);
Arrays.sort(numsObj,  Collections.reverseOrder());
for(int num: numsObj) {
    System.out.println(num);
}
```

    1
    3
    5
    ---
    
    5
    3
    1


### Searching

## .binarySearch() 
- alleen als array is sorted()!!!!
- levert de index van gevonden elem of -1 op.



```
int [] numbers = {5,3,1};
Arrays.binarySearch(numbers, 1);// 2
```



### Comparing
- a negative number mean the first array is smaller than the second
- a zero means that they are equal
- positive means that the first array is larger than the second




```Java
// 1 - 1 => 0
System.out.println(Arrays.compare(new int[]{1}, new int[] {1})); // 0
// 1 - 2 => -1
System.out.println(Arrays.compare(new int[]{1}, new int[] {2})); // -1
// 2 - 1 => 1
System.out.println(Arrays.compare(new int[]{2}, new int[] {1})); // 1
// 1,1 - 1 => 1
System.out.println(Arrays.compare(new int[]{1,1}, new int[] {1})); // 1
// 1 - 1,1 => -1
System.out.println(Arrays.compare(new int[]{1}, new int[] {1,1})); // -1
// 3 - 1,1 => 1
System.out.println(Arrays.compare(new int[]{3}, new int[] {1,1})); // 1
System.out.println(Arrays.compare(new int[]{3}, new int[] {4,1})); // -1
System.out.println(Arrays.compare(new int[]{35,2}, new int[] {4,1})); // 1
System.out.println(Arrays.compare(new int[]{35,2}, new int[] {4,4})); // 1
//System.out.println(Arrays.compare(new int[]{1}, new char[] {'A'})); // DNC verschillende types
```

    0
    -1
    1
    1
    -1
    1
    -1
    1
    1


## .mismatch()
- if equal => -1
- anders index van de index waar ze het eerst ongelijk zijn!

# Varargs
bv String... args

## Multidimensional Arrays

```
int[][] vars; // 2d
int vars [][]; // 2d array
int[] vars[]; // 2d
int[] var1 [], var2 [][];// 2d en 3d array!!!

```

## ArrayList

```
ArrayList a = new ArrayList();
ArrayList b = new ArrayList(12);
ArrayList c = new ArrayList(a);

new ArraList<>(); // Is van type Object !!!
```
**You can store an ArrayList in a List maar niet ANDERSOM!**
```
List<String> list6 = new ArrayList<>();
ArrayList<String> list7 = new List<>(); // DNC
```

## ArrayList
### .add(E element)
.add(<op positie>, elem)  


### .remove(int index)
bij meerder dan eerst de eerste!

### .set(int index, E newElem)

### .isEmpty .size()

### .clear()

### .comtains() 
return Boolean

### .equals()
```
ArrayList one = new ArrayList<>();
ArrayList two = new ArrayList<>();
System.out.println(one.equals(two));// true
```
## Wrapper Classes
- int Integer etc
- wrapper classes are immutable
- has methods convert back to primitive

## "".parseInt()
- returns a primitive => int
## "".valueOf()
- returns wrapperClass => Integer
```
int primitive = Integer.parseInt("123");
Integer wrapper = Integer.valueOf("123");
```
if String is passed but not correct value => NumberFormatException!  




```Java
ArrayList list = new ArrayList<>();
list.add("asd");
list.add("qwe");
list.add("asd");
list.add(Boolean.TRUE);
System.out.println(list);

ArrayList numlist = new ArrayList<>();
numlist.add(1);
numlist.add(2.0f);
numlist.add(2.001);
System.out.println(numlist);

list.remove("asd");
System.out.println(list);
```

    [asd, qwe, asd, true]
    [1, 2.0, 2.001]
    [qwe, asd, true]


## Autoboxing and Unboxing

unbox an null en je krijgt de NULLPOIINTEREXCEPTION  

```
List<Integer> list = new ArrayList<>();
list.add(null);
int h = list.get(0); // NULL POINTER EXCEPTION
```



```Java
List<Integer> list = new ArrayList<>();
list.add(null);
//int h = list.get(0); // NULLPOINTER EXCEPTION!!!
```




    true



## Converting tussen array en list

- list.toArray();
- Arrays.asList(array);

```
List<String> l1 = Arrays.asList("234","wer");
List<String> l1 = List.of("234","wer");
```
Je hebt nu wel fixed length!  

```
List<String> fixed = Arrays.asList("a","b","c");
List<String> expandable = new ArrayList<>(fixed);


```

Sorting Collections.sort(numbers)


## Sets

- Set<Integer> set = new HashSet<>();

## Maps
```
Map<String, String> map = new HashMap<>();
map.put("asd","zxc");
```


## MAth APIs
```
Math.min(1,2);
Math.max(1,2);
Math.round(1.232);
Math.pow(5,2);
Math.random(1,2);
```
[ocp 04](http://hjh.devsnips.nl/ocp04)
[ocp 06](http://hjh.devsnips.nl/ocp06)