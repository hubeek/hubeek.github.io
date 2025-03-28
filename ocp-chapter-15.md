# OCP Chapter 15

_Status: Published_
_Created: 2024-07-30 16:49:58_
_Tags: ocp_

# Functional Programming

## Functional Interfaces


- Supplier
- Consumer, BiConsumer
- Predicate, BiPredicate
- Function apply(T), BiFunction aply(T,U), UnaryOperator apply(T), BinaryOperator apply(T,T)

en voor concurrency
- Callable
- Runnable

| Func Iinterface | method |
|-|-|
| Supplier| T get()|
| Consumer, BiConsumer | void accept()|
| Predicate, BiPredicate | Boolean test(T t)|
| Function apply(T), BiFunction aply(T,U), UnaryOperator apply(T), BinaryOperator apply(T,T)| apply()|





## Supplier

used when you want to generate or supply values whitout taking any input.  

```
T get();

Supplier<LocalDate> s1 = LocalDate::now;
Supplier<LocalDate> s2 = () -> LocalDate.now();

LocalDate d1 = s1.get();
LocalDate d2 = s2.get();
```





## Consumer & BiConsumer

used when you want to do something with a param but void return  

```
void accept(T t);

BiConsumer<String, Integer> printBiConsumer = (s, i) -> System.out.println(s + " " + i);

printBiConsumer.accept("Age:", 30);
printBiConsumer.accept("Score:", 100);
```

## Predicate & BiPredicate

used when filtering or matching.  

```
boolean test(T t);
boolean test(T t, U u);

        Predicate<String> p1 = String::isEmpty;
        System.out.println(p1.test(""));
        System.out.println(p1.test("asd"));

        BiPredicate<String, String> p2 = String::startsWith;
        System.out.println(p2.test("asd", "as"));
```


## Function UnaryOperator BinaryOperator
```
R apply(T t);
R apply(T t, U u);

Function<String, Integer> f1 = String::length;
System.out.println(f1.apply("hjh"));

BiFunction<String, String, String> f2 = String::concat;
System.out.println(f2.apply("hj","hubeek"));

UnaryOperator<String> u1 = String::toUpperCase;
System.out.println(u1.apply("hjh"));

BinaryOperator<String> b1 = String::concat;
System.out.println(b1.apply("hj","Hubeek"));

```

## Convinience methods
- Consumer, Function andThen()
- Function, compose()
- Predicate, and() negate() or()

```
Function<Integer, Integer> before = x -> x+1;
Function<Integer, Integer> after = x -> x+2;
Function<Integer, Integer> combined = after.compose(before); // gefore runs first...
System.out.println(combined.apply(3));


Predicate<String> egg = s -> s.contains("egg");
Predicate<String> brown = s -> s.contains("brown");
Predicate<String> brownEggs = egg.and(brown);
System.out.println(brownEggs.test("brownegg"));
```


# Optional
- When Optional is null it throws an NullPointerException...use if met .isPresent()
- Optional.empty()
- Optional.of(double)
- Optional.ofNullable(value)

```
Optional o = Optional.ofNullable(null);
System.out.println(o.isEmpty());

Optional o = null;
System.out.println(o.isEmpty()); // nullpointer exception

```

|Method|When Optional is empty|When Optional contains value|
|-|-|-|
|get()| throws Exception|returns value|
|ifPresent(Consumer c)| does nothing|calls consumer with value|
|ifPresent()| return false|returns true|
|orElse(T other)| return other param|returns value|
|orElseGet(Supplier s)| return result Supplier|returns value|
|orElseThrow()| Throws NoSuchElementException|returns value|
|orElseThrow(Supplier s)| Throws exception created by calling Supplier|returns value|
    

# Streams

- a sequence of data
- stream pipeline consists of operations that run on a stream to produce a result
- source -> operations -> terminal operation

## Finite Streams
```
Stream<String> empty = Stream.empty();
Stream<Integer> singleElem = Stream.of(4);
Stream<Integer> moreElem = Stream.of(4,54,78);

var list = List.of(234,354,564);
Stream<Integer> fromList = list.stream();
Stream<Integer> fromListParallel = list.parallelStream();
```

## Infinite Streams
```
// random numbers
Stream<Double> random = Stream.generate(Math::random);
Iterator<Integer> iterator = list.iterator();
random.forEach(System.out::println);

// odd numbers
Stream<Integer> oddNumbers = Stream.iterate(1, n -> n + 2);
Iterator<Integer> iterator = list.iterator();

oddNumbers.forEach(System.out::println);
```


## Stream Creation Methods
- finite streams Stream.empty(), Stream.of(), coll.stream()
- infinite streams Stream.generate(), Stream.iterate()



|Method|Finite or infinite|notes|
|-|-|-|
|Stream.empty() |Finite|Creates Stream with zero elements|
|Stream.of(varargs)|Finite|Creates Stream with elements listed|
|coll.stream()|Finite|Creates Stream from a Collection|
|coll.parallelStream()|Finite|Creates Stream from a Collection where the stream can run in parallel|
|Stream.generate(supplier)|Infinite|Creates Stream by calling the Supplier for each element upon request|
|Stream.iterate(seed, unaryOperator)|Infinite|Creates Stream by using the seed for the first element and then calling the UnaryOperator for each subsequent element upon request|
|Stream.iterate(seed, predicate,unaryOperator)|Finite or infinite|Creates Stream by using the seed for the first element and then calling the UnaryOperator for each subsequent element upon request. Stops if the Predicate returns false|

```
// Stream.iterate(seed, unaryOperator)
// Generate an infinite stream of even numbers starting from 0
Stream<Integer> evenNumbers = Stream.iterate(0, n -> n + 2);

// Limit the stream to the first 10 elements and print them
evenNumbers.limit(10).forEach(System.out::println);
```

## Intermediata Operations
- filter()
- distinct()
- limit() skip()
- map()
- flatMap()
- sorted()
- peek()

```
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
List<Integer> evenNumbers = numbers.stream()
                                   .filter(n -> n % 2 == 0)
                                   .collect(Collectors.toList());
// evenNumbers will be [2, 4, 6]

List<Integer> numbers = Arrays.asList(1, 2, 2, 3, 4, 4, 5);
List<Integer> distinctNumbers = numbers.stream()
                                       .distinct()
                                       .collect(Collectors.toList());
// distinctNumbers will be [1, 2, 3, 4, 5]


List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
List<Integer> firstThreeNumbers = numbers.stream()
                                         .limit(3)
                                         .collect(Collectors.toList());
// firstThreeNumbers will be [1, 2, 3]


List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
List<Integer> afterSkipTwo = numbers.stream()
                                    .skip(2)
                                    .collect(Collectors.toList());
// afterSkipTwo will be [3, 4, 5, 6]

List<String> words = Arrays.asList("hello", "world");
List<Integer> wordLengths = words.stream()
                                 .map(String::length)
                                 .collect(Collectors.toList());
// wordLengths will be [5, 5]


List<List<String>> nestedList = Arrays.asList(
    Arrays.asList("a", "b", "c"),
    Arrays.asList("d", "e", "f"));
List<String> flatList = nestedList.stream()
                                  .flatMap(List::stream)
                                  .collect(Collectors.toList());
// flatList will be ["a", "b", "c", "d", "e", "f"]


List<Integer> numbers = Arrays.asList(5, 3, 1, 4, 2);
List<Integer> sortedNumbers = numbers.stream()
                                     .sorted()
                                     .collect(Collectors.toList());
// sortedNumbers will be [1, 2, 3, 4, 5]

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
numbers.stream()
       .peek(System.out::println) // prints each element
       .map(n -> n * 2)
       .collect(Collectors.toList());
// Output will be each number printed to the console

```

```
// map element -> transformed element
List<Long> ids = people.stream()
                               .map(Person::getId)
                               .collect(Collectors.toList());

// flatMap -> multiple streams naar nieuwe stream
List<List<Integer>> listOfLists = Arrays.asList(
            Arrays.asList(1, 2, 3),
            Arrays.asList(4, 5),
            Arrays.asList(6, 7, 8, 9)
        );

        // Use flatMap to flatten the list of lists into a single list
        List<Integer> flattenedList = listOfLists.stream()
                                                 .flatMap(List::stream)
                                                 .collect(Collectors.toList());

```

## Common Terminal Operations
- count()
- min() max()
- findAny() findFirst()
- allMatch() anyMatch() noneMatch()
- forEach()
- reduce()
- collect()

```
Optional<Integer> maxNumber = numbers.stream().max(Integer::compareTo);
Optional<String> firstName = names.stream().findFirst();
boolean hasEvenNumber = numbers.stream().anyMatch(n -> n % 2 == 0);
```

|Method| what happens for infinite streams|return values|reduction|
|-|-|-|-|
|count()|Does not terminate|long|Yes|
|min() max()|Does not terminate|Optional<T >|Yes|
|findAny() findFirst()|Terminates|Optional<T >|No|
|allMatch() anyMatch() noneMatch()|Sometimes terminates|boolean|No|
|forEach()|Does not terminate|void|No|
|reduce()|Does not terminate|Varies|Yes|
|collect()|Does not terminate|Varies|Yes|

- count() in a finite stream number of elements. for infinite it never ends.
- min() max() : Optional return type.
- findAny() findFirst(): Optional
- allMatch(), anyMatch() noneMatch():

---

- foreach()
- reduce()

- filter()
- distinct() werkt met equals()
- limit()
- skip()
- map()
- flatMap()
- sorted()
- peek() voor debugging

## Primitive Streams

### creating
- IntStream
- LongStream
- DoubleStream

```
Stream<Integer> stream = Stream.of()1,2,3;
sout(stream.mapToInt(x->x).sum());

IntStream intStream = IntStream.of(1,2,3);
OptionalDouble avg = intStream.average();
```

- OptionalDouble average()
- Stream<T> boxed() naar Wrapper Class (!)
- OptionalInt OptionalDouble OptionalLong max() min()
- IntDoubleLongStream range(int a, int b)
- IntDoubleLong rangeClosed(a, b)
- int long double sum()
- IntSummaryStatistics summaryStatistics() -> numerous statistics

### Mapping

|Source streamclass| To create Stream| To create DoubleStream| To create IntStream| To create LongStream|    
|-|-|-|-|-|
|Stream<T>| map()| mapToDouble()| mapToInt()| mapToLong( )|
|DoubleStream|mapToObj()|map()|mapToInt()|mapToLong()|
|IntStream|mapToObj ()|mapToDouble()|map()|mapToLong()|
|LongStream|mapToObj ()|mapToDouble()|mapToInt()|map()|


```
Stream<String> objStream = Stream.of("penguin", "fish");
IntStream intStream = objStream.mapToInt(s -> s.length());
```


### Using Optional with Primitive Streams

- OptionalDouble voor double optionals
- Optional<Double> voor Double optionals ;-)

```
var stream = IntStream.rangeClosed(1,10);
OptionalDouble optional = stream.average();
```


## Functional Interface for Primitives

### Functional Interfaces for boolean
```
BooleanSupplier b1 = () -> true;
BooleanSupplier b2 = () -> Math.random()> .5;
System.out.println(b1.getAsBoolean()); // true
System.out.println(b2.getAsBoolean()); // false
```

    

# Working with advanced Stream Concepts

```
var cats = new ArrayList<String>();
 cats.add("Annie");
 cats.add("Ripley");
 var stream = cats.stream();
 cats.add("KC");
 System.out.println(stream.count()); // 3 van wege lazy evaluated
```

## Chaining Optionals
```
private static void threeDigit(Optional<Integer> optional) {
   optional.map(n -> "" + n)            // part 1
      .filter(s -> s.length() == 3)     // part 2
      .ifPresent(System.out::println);  // part 3
}
```
[prev](http://hjh.devsnips.nl/ocp14)
[next](http://hjh.devsnips.nl/ocp16)
