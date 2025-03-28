# Java collections

_Status: Published_
_Created: 2021-01-03 04:47:37_
_Tags: java, collections_

```
list.forEach(System.out::print);
```

## Array
```
int[] a = new int[5];
 
a[0] = 1;
a[1] = 2;
a[2] = 4;
a[3] = 8;
a[4] = 16;
```
String => array with  .split() & .join()

## ArrayList
ordered, index based, dyn sizing, non sync, duplicates allowed
```
//Non-generic arraylist - NOT RECOMMENDED !!
ArrayList list = new ArrayList();
 
//Generic Arraylist with default capacity(=16)
List<Integer> numbers = new ArrayList<>(); 
 
//Generic Arraylist with the given capacity
List<Integer> numbers = new ArrayList<>(6); 
 
//Generic Arraylist initialized with another collection
List<Integer> numbers = new ArrayList<>( Arrays.asList(1,2,3,4,5) ); 
```
```
List<Integer> numbers = new ArrayList<>(6); 
numbers.add(1);

ArrayList<String> charList = new ArrayList<>(Arrays.asList(("A", "B", "C"));
String aChar = alphabetsList.get(0);

ArrayList<Integer> digits = new ArrayList<>(Arrays.asList(1,2,3,4,5,6));
 
Iterator<Integer> iterator = digits.iterator();
 
while(iterator.hasNext()) 
{
    System.out.println(iterator.next());
}
for(int i = 0; i < digits.size(); i++) 
{
    System.out.print(digits.get(i));
}
for(Integer d : digits) 
{
    System.out.print(d);
}
```
sorting
```
public class AgeSorter implements Comparator<Employee> 
{
    @Override
    public int compare(Employee e1, Employee e2) {
        //comparison logic
    }
}
```


link: https://howtodoinjava.com/java-collections/