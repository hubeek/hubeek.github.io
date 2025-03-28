# OCP Chapter 14

_Status: Published_
_Created: 2024-07-30 16:49:13_
_Tags: ocp_

# Generics and Collections

## Functional Interfaces
|Functional interface| return type| method name| params|
|-|-|-|-|
|Supplier<T>|T|get()|0|
|Consumer<T>|void|accept()|1(T)|
|BiConsumer<T, U>|void|accept(T,U)|2(T,U)|
|Predicate<T>|boolean|test(T)|1(T)|
|BiPredicate<T, U>|boolean|test(T, U)|2(T, U)|
|Functio<T, R>|R|apply(T)|1(T)|
|BiFunctio<T, U, R>|R|apply(T, U)|2(T, U)|
|Unary<T>|T|apply(T)|1(T)|

    

## Method references
- static methods
- instance methods on a particular instance
- instance methods on a parameter to be determined at runtime
- constructors

### Static Methods
.sort() is static method on Collections. Eerst vb : // Java magie om die ene param om te zetten naar input param en method overloading keuze. bij compiler twijfel  -> Error
```
Consumer <List<Integer>> methodRef = Collections::sort 
Consumer<List<Integer>> lambda = Collections.sort(x);
```

### instance method
```
var str = "asd";
Predicate<String> methodRef = str::startsWith;
Predicate<String> lambda = str.startsWith(s);
```

### instance method on a parameter
```
Predicate<String> methodRef = str::isEmpty;
Predicate<String> lambda = str.isEmpty();
```
### Calling constructor
```
Supplier<List<String>> methodRef = ArrayList::new;
Supplier<List<String>> lmbda = () -> new ArrayList();

Function<Integer,List<String>> methodRef = ArrayList::new;
Function<Integer, List<String>> lmbda = () -> new ArrayList();
```


## Using wrapper class
voor primitives .valueOf()

## Diamond operator
- ONLY right side

```
var list = new ArrayList<>(); // Worden List<Object> als niet gespecificieerd
var list = new ArrayList<Integer>(); // Worden List<Integer>
List<> list2 = new ArrayList<Integer>(); // DNC!!
```


## List Maps Sets and Queues

4 interfacces:

- list: ordered collections with int index  
- set: collection without dupes UNordered 
- queue: coolection that orders elements for operation in typical order  
- map: collection maps keys + values. no dupe key allowed.

Collection is parent of all except map!  


### Common collections methods
- add()
- remove() (let op bij enhanced for loop for(var a: coll) {} )
- isEmpty, size()
- clear()
- contains()
- removeIf(<Predicate>)
- forEach(<Supplier>)
```
list.forEach(System.out::println);
list.forEach(element -> System.out.println(element));

```


## List interface
No adding or deleting:
- Arrays.asList(varargs) , fixed size, replace yes
- List.of(varargs) , immutable list
- List.copyOf(varargs), imuutable with copies of ori values

### List methods
- boolean add(E element), adds at the end
- void add(int index, E elem) adds at index moves rest to end
- E get(in t index)
- E remove(int index) removes at index and moves to front
- void replaceAll(UnaryOperator<E> op) replaces
- set(int index, E e) replaces and returns original(!)

```
for (String string: list) {
System.oiut.println(string);
}
```
```
Iterator<String> iter = list.iterator();
while (iter.hasNext()) {
    String string = iter.next();
System.out.println(string);
}
```


## Queue Interface
- ordered

### Queue methods
- boolean add(E e)        -> (can throw Exc)
- E element()             ->(can throw Exc)
- boolean offer(E e)
- E remove()              -> (can throw Exc)
- E poll()
- E peek()

## Map
unordered  
Hashmap  
TreeMap


### Map methods
- void clear()
- boolean containsKey
- boolean conatinsVlaue
- Set<Map.entry<K,V>> entrySet()
- void forEach(BiConsumer(K,V))
- V get(Object key)
- V getOrDefault(Object key, V defaultValue)
- boolean isEmpty
- Set<K> keySet()
- V merge(K key, V value, Function(<V,V,V> func))
- put(K,V)
- V putIfAbsent(K,V)
- V remove(Object k)
- V replace(K,V)
- void replaceAll(BiFunction<K,V,V> func)
- int size()
- Collection<V> values()

```
map.forEach((k,v) -> System.out.println(v));
map.values().forEach(System.out::println);
map.entrySet().forEach(e->System.out.println(e.getKey() +e.getValue()))
```

## Comparing CollectionTypes

|Type|Dupes|Ordered|KV|Add/Remove in specifi order|
|-|-|-|-|-|
|List|Yes|Yes(by index)|No|No|
|Set|No|No|No|No|
|Queue|Yes|Yes(retrieved in defined order)|No|Yes|
|Map|Yes|No|Yes|No|

### Which data structures allow null
- die gesorteerd kunnen worden mogen geen null hebben...
- 

### Oude collections
- Vector -> List
- Hashtable -> HashMap
- Stack -> Queue

## Sorting
- Collections.sort() returns void because sorts method param.
- Numbers > letters
- Uppercase > lowercase
- Pas op Comparable <-> Comparator interface


```
var list = new ArrayList<String>();
        list.add("asda");
        list.add("123asda");
        list.add("ASD");
        list.sort(null);
        System.out.println(list); //[123asda, ASD, asda]
```



## Comparable class
- id - a.id ASC
- a.id - id DESC

## Comparator class
- uit java.util
- specifiek gemaakte vergelijking

```
        Comparator byWeight = new Comparator<Duck>() {
            @Override
            public int compare(Duck o1, Duck o2) {
                return o1.getWeight() - o2.getWeight();
            }
        };
        Comparator<Duck> byWeight = (d1, d2) -> d1.getWeight() - d2.getWeight();
        Comparator<Duck> byWeight = Comparator.comparing(Duck::getWeight);
        Collections.sort(ducks, byWeight);
```
**Belangrijk**
|Difference|Comparable|Comparator|
|-|-|-|
|package name| java.lang|java.util|
|interface must be implemented by class comparing|Yes|No|
|method name|compareTo()|compare()|
|Number of params|1|2|
|Common to declare using a lambda|No|Yes|



## Multiple fields

```
public class Squirrel {
    private int weight;
    private String species;
// all the getters setter constructorsetc
}

public class MultiFieldComparator implements Comparator<Squirrel> {
    public int compare(Squirrel s1, Squirreel s2) {
        int result = s1.getSpecies().compareTo(s2.s2.getSpecies());
        if(result != 0) {return result;}
        return s1.getWeight()-s2.getWeight();
    }
}

// OF

Comparator<Squirrel> c = Comparator.comapre(Squirrel::getSpecies).thenComparingIn(Squirrel::getWeight);

// kan ook met .reversed()
```
## Methods
- ---- helper static methods ----
- comparing(function)
- comparingDouble(func)
- comparingInt(func)
- comparingLong(func)
- naturalOrder()
- reversedOrder()
- ---- helper default methods ----
- reversed()
- thenComparing(func)
- thenComparingDouble/Int/Long(func)

- Collections.binarySearch() !!!
- binarySearch requires a sorted List.

## TreeSet needs sorted collection
init
```
Set<Rabbit> rabbits = new TreeSet<> ((r1,r2) -> r1.id =r2.id);
rabbits.add(new Rabbit()); //Werkt nu wel
```



# Generics
- E element
- K map Key
- V map Value
- N number
- T generic data type
- S,U,V for multiple generic types

## type erasure
Alles onderwater na compilen Object geworden. en dan verdwijnt dus eigenlijk t class-type

## Generic Interfaces
interface can declare formal type param.
```
public interface Abc<T> {
    void doSomething(T t);
}

```

### No nos with Generic Types
- calling constructor T() als constructor is not allwed
- creating an array of that generic type
- calling instanceOf (want alles is onderwater natuurlijk een Object...)
- using the primitive type as a generic type param... moet dan dus met de wrapper class...
- static variable T no no

## Generic methods
<T> staat voor return type: `public <T> int calc(){return -1;}`
```
public class Handler {
    public static <T> void prepare(T t) {
    
    sout("T: "+ t);
    }
}
```
## confusing T tricky
class T is not same as method T!!!
```
public class Crate<T> { //

    public <T> T tricky(T t) {
        return t;
    }
}
```

## Bounding Generic Types <?>
- generics are treated as Object...
- ? wildcard
- *bounded param type*
- *wildcard generic type*
- List<?> en ArrayList<>

### Types of generic wildcard bounds
- unbounded wildcard, ? , any type is OK
- upper bound, ? extends type ? 
- lower bound, ? super type 

```
// unbounded
List<?> l = new ArrayList<String>();

// upper bounded
List<? extends Exception> l = new ArrayList<RuntimeException>();

// lower bounded
List<? super Exception> l = new ArrayList<Object>();
```

#### unbounded
not the same!
```
List<?> q = new ArrayList<>();
var q2 = new ArrayList<>();
```

#### upper bounded
- list becomes immutable...


```
    public static long total(List<? extends Number> nums) {
        long result = 0;
        for (Number num: nums) {
            result += num.longValue();
        }
        return result;
    }

// of voor beter resultaat met floats erin

    public static double total(List<? extends Number> nums) {
        BigDecimal result = BigDecimal.ZERO;
        for (Number num: nums) {
            result = result.add(new BigDecimal(num.toString()));
        }
        return result.setScale(1, BigDecimal.ROUND_HALF_UP).doubleValue();
    }
```

#### lower bound
- zelfde class of subclasses...
- let op met exceptions

## collections in de rebound

### List
- arrayList
- LinkedList

## Set
- HashSet, unorded elements
- TreeSet, sorted, null NOT allowed

## Queue
- LinkedList

## Map
- HashMap
- TreeMap, sorted, null NOT allowed


[prev](http://hjh.devsnips.nl/ocp13)
[next](http://hjh.devsnips.nl/ocp15)