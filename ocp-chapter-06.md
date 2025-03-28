# OCP Chapter 06

_Status: Published_
_Created: 2024-07-30 11:53:57_
_Tags: ocp_

# Chapter 06 Lambdas
- Alles tussen curly braces...  
- work with interface with only one abstract method. (functional interface)
- SAM Single Abstract Method (SAM rule)

```
a -> a.canHop()
// zelfde als:
(Animal a) -> {return a.canHop();}
```


- single param
- arrow operator to seperate param and body
- one or more lines of code, incl semicolo and return statment.

Geen {} betekent dat ie returned. Gaat niet met 2 of meer return statements.  

wel valide....
```
s->{}
()-> true
a-> a.startsWith("test")
(a,b)-> a.startsWith("test")
(String a, String b) ->a.startsWith("test")
```
NIET valide
```
a,b -> a.startsWith("test") // missende boogjes
a -> {a.startsWith("test");} // missende return...
a -> {return a.startsWith("test")} // missende semicolon ;
```

## Functional Interfaces
- Predicate
- Consumer
- Supplier
- Comparator


## Predicate
```
public interface Predicate<T> {
    boolean test(T t);
}
```

## Consumer
```
void accept(T t)
```

## Supplier
```
T get()
//
Supplier<Integer> number = () -> 42;
Supplier<Integer> random = () -> newRandom().nextInt();
```

## Comparator

```
int compate(T o1, T o2)
// ascending sort
Comparator<Integer> ints = (i1,i2) -> i1 -i2;
// descending
Comparator<String> strings = (s1,s2) -> s2.compareTo(s1);
Comparator<String> moreStrings = (s1,s2) -> - s1.compareTo(s2);

```

| Func interface | params | return type |
| -------------- | ------ | ----------- |
| Comparator | Two | int |
| Consumer | One | void |
| Predicate | One | boolean |
| Supplier | None | One |





## Variables in Lambas

```
Predicate<String> p = x -> true;
Predicate<String> p = (var x) -> true;
Predicate<String> p = (Stringx) -> true;
```


## Local variable in Lambda body

 ```
(a,b) -> {init c = 0; return 5;}
(a,b) -> {init a = 0; return 5;} // DNC
 ```

## Variable referenced from the labmda body

- can access instance variable, method params, or local variables
- Method params and local variables are allowed if they are effectively final. (no change after set...)

|Variable type | Rule     |
|-------------- | ----------- |
| instance variable | allowed|
| static variable | allowed|
| local variable | allowed (if eff final) |
| method variable | allowed (if eff final) |
| lambda param | allowed|






## Calling APIs with Lambdas

## RemoveIf()
NOT on a Map! Map heeft keys and values...

## sort()
begint met twee vars en returns an int!!  

Not a sort on a Set of Map  

## forEach()
Kan wel op Set of Map, maar dan over de Keys of Values ;-)  


[ocp 05](http://hjh.devsnips.nl/ocp05)
[ocp 07](http://hjh.devsnips.nl/ocp07)