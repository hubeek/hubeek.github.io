# OCP Chapter 22

_Status: Published_
_Created: 2024-08-21 15:39:48_
_Tags: ocp, java_

# Security



## LIMITING ACCESSIBILITY

```
package animals.security;
public class ComboLocks {
   public Map<String, String> combos;
}
```
combos object has public access. This is also poor encapsulation. A key security principle is to limit access as much as possible. Think of it as “need to know” for objects. This is called the principle of least privilege.

better:
```
package animals.security;
public class ComboLocks {
private Map<String, String> combos;
   public boolean isComboValid(String animal, String combo) {
      var correctCombo = combos.get(animal);
      return combo.equals(correctCombo);
} }
```


## RESTRICTING EXTENSIBILITY

```
public class GrasshopperCage {
   public static void openLock(ComboLocks comboLocks, String
combo) {
      if (comboLocks.isComboValid("grasshopper", combo))
            System.out.println("Open!");
} }

// nu is mogelijk
public class EvilComboLocks extends ComboLocks {
   public boolean isComboValid(String animal, String combo) {
      var valid = super.isComboValid(animal, combo);
      if (valid) {
         // email the password to Hacker Harry
      }
      return valid;
   }
}

// nu is niet meer mogelijk

public **final** class ComboLocks { private Map<String, String> combos;
   // instantiate combos object
   public boolean isComboValid(String animal, String combo) {
      var correctCombo = combos.get(animal);
      return combo.equals(correctCombo);
} }

```

## CREATING IMMUTABLE OBJECTS

Although there are a variety of techniques for writing an immutable class, you should be familiar with a common strategy for making a class immutable.
1. Mark the class as final.
2. Mark all the instance variables private.
3. Don't define any setter methods and make fields final.
4. Don't allow referenced mutable objects to be modified.
5. Use a constructor to set all properties of theo bject,making a copy if needed.

```
  import java.util.*;

  public final class Animal {

        private final ArrayList<String> favoriteFoods;

        public Animal() {
           this.favoriteFoods = new ArrayList<String>();
           this.favoriteFoods.add("Apples");

     }

    public List<String> getFavoriteFoods() {
        return favoriteFoods;
    }
}
// kwetsbaar omdat favoriteFoods gewijzigd kan worden bv:  getFavoriteFoods().clear()

// dit zou al helpen ipv vorige getter
public int getFavoriteFoodsCount() {
    return favoriteFoods.size();
}
public String getFavoriteFoodsElement(int index) {
   return favoriteFoods.get(index);
}

// of
public ArrayList<String> getFavoriteFoods() {
   return new ArrayList<String>(this.favoriteFoods);
}

```



Let's say we want to allow the user to provide the favoriteFoods data, so we implement the following:
```

public Animal(ArrayList<String> favoriteFoods) {
   if(favoriteFoods == null)
      throw new RuntimeException("favoriteFoods is
   this.favoriteFoods = favoriteFoods;
}
public int getFavoriteFoodsCount() {
   return favoriteFoods.size();
}
public String getFavoriteFoodsElement(int index) {
   return favoriteFoods.get(index);
}

kan dan en dan is favfoods niet meer immutable:
void modifyNotSoImmutableObject() {
    var favorites = new ArrayList<String>();
    favorites.add("Apples");
    var animal = new Animal(favorites);
    System.out.print(animal.getFavoriteFoodsCount());
    favorites.clear();
    System.out.print(animal.getFavoriteFoodsCount());
}

// The solution is to use a copy constructor to make a copy of the list object containing the same elements.



public Animal(List<String> favoriteFoods) {
   if(favoriteFoods == null)
        throw new RuntimeException("favoriteFoods is required");
   this.favoriteFoods = new ArrayList<String> (favoriteFoods);
}
```

## CLONING OBJECTS
ava has a Cloneable interface that you can implement if you want classes to be able to call the clone() method on your object. This helps with making defensive copies.

`this.favoriteFoods = (ArrayList) favoriteFoods.clone();
`
```
// dan Clonable gebruyiken:
public final class Animal implements Cloneable {

//en
public static void main(String... args) throws Exception {
   ArrayList<String> food = new ArrayList<>();
   food.add("grass");
   Animal sheep = new Animal(food);
   Animal clone = (Animal) sheep.clone();
   System.out.println(sheep == clone);
   System.out.println(sheep.favoriteFoods == clone.favoriteFoods);
}

```
By default, the **clone() method makes a shallow copy** of the data, which means only the top‐level object references and primitives are copied. No new objects from within the cloned object are created.   


By contrast, you can write an implementation that does a deep copy and clones the objects inside. A deep copy does make a new ArrayList object. Changes to the cloned object do not affect the original.
```

public Animal clone() {
   ArrayList<String> listClone = (ArrayList)
    favoriteFoods.clone();
   return new Animal(listClone);
}


```

myObject.clone()
|
V
Implements Clonable? -> No -> Throws Exception
|
V
Overrides Clone() -> No -> Shallow copy
|
V
Implementation dependent  


In the last block, implementation‐dependent means you should probably check the Javadoc of the overridden clone() method before using it.




### Shallow Copy

A shallow copy of an object is a new instance of that object where the fields of the original object are copied as they are. However, if the object contains references to other objects (i.e., non-primitive fields), only the references are copied, not the actual objects they refer to. 

```
        Address address = new Address("New York");
        Person person1 = new Person("John", address);
        Person person2 = (Person) person1.clone();

        System.out.println(person1.address.city); // Outputs: New York
        System.out.println(person2.address.city); // Outputs: New York

        person2.address.city = "Los Angeles";

        System.out.println(person1.address.city); // Outputs: Los Angeles
        System.out.println(person2.address.city); // Outputs: Los Angeles
```
In this example, person1 and person2 are separate objects, but they share the same Address object. If you change the city in person2, it will also change in person1, demonstrating that only a shallow copy was made.

### Deep Copy
A deep copy of an object involves creating a new object and also recursively copying all objects referenced by the original object. This means that the copy and the original object do not share references to any mutable objects. Any changes made to the deep-copied object will not affect the original object.

```
// nu in person.class:
@Override
    protected Object clone() throws CloneNotSupportedException {
        Person clonedPerson = (Person) super.clone();
        clonedPerson.address = new Address(this.address); // Deep copy of Address
        return clonedPerson;
    }

// en dan
Address address = new Address("New York");
        Person person1 = new Person("John", address);
        Person person2 = (Person) person1.clone();

        System.out.println(person1.address.city); // Outputs: New York
        System.out.println(person2.address.city); // Outputs: New York

        person2.address.city = "Los Angeles";

        System.out.println(person1.address.city); // Outputs: New York
        System.out.println(person2.address.city); // Outputs: Los Angeles

```

Shallow copying is faster and uses less memory, but deep copying ensures that the two objects are entirely independent of each other.


## Introducing Injection and Input Validation

Injection is an attack where dangerous input runs in a program as part of a command. Kan bv met Statement met raw SQL.

`"monday' OR day IS NOT NULL OR day = 'sunday"`


An exploit is an attack that takes advantage of weak security. 

There are many sources of untrusted data. For the exam, you need to be aware of user input, reading from files, and retrieving data from a database. In the real world, any data that did not originate from your program should be considered suspect.

### Using PreparedStatement

If you remember only two things about SQL and security, remember to use a PreparedStatement and bind variables.

### INVALIDATING INVALID INPUT WITH VALIDATION


SQL injection isn't the only type of injection. Command injection is another type that uses operating system commands to do something unexpected.

```
Console console = System.console();
String dirName = console.readLine();
Path path = Paths.get("c:/data/diets/" + dirName);
try (Stream<Path> stream = Files.walk(path)) {
   stream.filter(p -> p.toString().endsWith(".txt"))
      .forEach(System.out::println);
}
// als je input .. is dan zie je de secrets dir... dus validate input

// bv whitelist
`if (dirName.equals("mammal") || dirName.equals("birds")) {
`


```

A blacklist is a list of things that aren't allowed. In the previous example, we could have put the dot ( .) character on a blacklist. The problem with a blacklist is that you have to be cleverer than the bad guys. There are a lot of ways to cause harm. For example, you can encode characters.

By contrast, the whitelist is specifying what is allowed. You can supply a list of valid characters. Whitelisting is preferable to blacklisting for security because a whitelist doesn't need to foresee every possible problem.

## Working with Confidential Information


### GUARDING SENSITIVE DATA FROM OUTPUT
The first step  is to avoid putting confidential information in a toString() method.
Dus oppassen bij
- Writing to a log file
- Printing an exception or stack trace
- System.out and System.err messages
- Writing to data files


### PROTECTING DATA IN MEMORY

if crashes:  

When calling the readPassword() on Console, it returns a char[] instead of a String. This is safer for two reasons.
- It is not stored as a String, so Java won't place it in the String pool, where it could exist in memory long after the code that used it is run.
- You can null out the value of the array element rather than waiting for the garbage collector to do it.

```
Console console = System.console();
char[] password = console.readPassword();
Arrays.fill(password, 'x');
```

When the sensitive data cannot be overwritten, it is good practice to set confidential data to null when you're done using it. If the data can be garbage collected, you don't have to worry about it being exposed later.
```
LocalDate dateOfBirth = getDateOfBirth();
// use date of birth
dateOfBirth = null;

```
The idea is to have confidential data in memory for as short a time as possible. 



## LIMITING FILE ACCESS

Another way is to use a security policy to control what the program can access.

It is good to apply multiple techniques to protect your application. This approach is called defense in depth.

```
// permissie read only
grant {
   permission java.io.FilePermission
    "C:\\water\\fish.txt",
    "read";
};

// permissie read write
grant {
   permission java.io.FilePermission
    "C:\\water\\fish.txt",
    "read, write";
};


```

When looking at a policy, pay attention to whether the policy grants access to more than is needed to run the program. If our application needs to read a file, it should only have read permissions. This is the principle of least privilege we showed you earlier.

## Serializing and Deserializing Objects

Imagine we are storing data in an Employee record. We want to write this data to a file and read this data back into memory, but we want to do so without writing any potentially sensitive data to disk. From Chapter 19, you should already know how to do this with serialization.


```
import java.io.*;
public class Employee implements Serializable {
   private String name;
   private int age;
   // Constructors/getters/setters
}

```


### SPECIFYING WHICH FIELDS TO SERIALIZE


marking a field as transient prevents it from being serialized.

```
private transient int age;

// Alternatively, you can specify fields to be serialized in an array.

private static final ObjectStreamField[]
serialPersistentFields =
   { new ObjectStreamField("name", String.class) };

```
You can think of serialPersistentFields as the opposite of transient. The former is a whitelist of fields that should be serialized, while the latter is a blacklist of fields that should not.

If you go with the array approach, make sure you remember to use the private, static, and final modifiers. Otherwise, the field will be ignored.



### CUSTOMIZING THE SERIALIZATION PROCESS

Security may demand custom serialization. 

Take a look at the following implementation that uses writeObject() and readObject() for serialization

```
import java.io.*;
public class Employee implements Serializable {
   private String name;
   private String ssn;
   private int age;

   // Constructors/getters/setters

   private static final ObjectStreamField[] serialPersistentFields =
            { new ObjectStreamField("name", String.class), new ObjectStreamField("ssn", String.class) };

    private static String encrypt(String input) {
      // Implementation omitted
    }
    private static String decrypt(String input) {
      // Implementation omitted
    }

    private void writeObject(ObjectOutputStream s) throws Exception {
          ObjectOutputStream.PutField fields = s.putFields();
          fields.put("name", name);
          fields.put("ssn", encrypt(ssn));
          s.writeFields();
    }
    
    private void readObject(ObjectInputStream s) throws Exception {
            ObjectInputStream.GetField fields = s.readFields();
    
            this.name = (String)fields.get("name", null);
            this.ssn = decrypt((String)fields.get("ssn", null));
    }

}
```
This version skips the age variable as before, although this time without using the transient modifier. It also uses custom read and write methods to securely encrypt/decrypt the Social Security number. Notice the PutField and GetField classes are used in order to write and read the fields easily.



## PRE/POST‐SERIALIZATION PROCESSING


```
import java.io.*;
import java.util.Map;
import java.util.concurrent.ConcurrentHashMap;
public class Employee implements Serializable {
   ...
   private Employee() {}
   private static Map<String,Employee> pool =
      new ConcurrentHashMap<>();
   public synchronized static Employee getEmployee(String
name) {
      if(pool.get(name)==null) {
         var e = new Employee();
         e.name = name;         pool.put(name, e);
}
      return pool.get(name);
   }
}

```
This method creates a new Employee if one does not exist. Otherwise, it returns the one stored in the memory pool.

### Applying readResolve()
Now we want to start reading/writing the employee data to disk, but we have a problem. When someone reads the data from the disk, it
deserializes it into a new object, not the one in memory pool. This could result in two users holding different versions of the Employee in memory!

Enter the readResolve() method. When this method is present, it is run after the readObject() method and is capable of replacing the reference of the object returned by deserialization.

```
import java.io.*;
import java.util.Map;
import java.util.concurrent.ConcurrentHashMap;
public class Employee implements Serializable {
   ...
    public synchronized Object readResolve() throws ObjectStreamException {
      var existingEmployee = pool.get(name);
      if(pool.get(name) == null) {
        // New employee not in memory
        pool.put(name, this);
        return this;
     } else {
        // Existing user already in memory
        existingEmployee.name = this.name;
        existingEmployee.ssn = this.ssn;
        return existingEmployee;
    }
 }
}

```
If the object is not in memory, it is added to the pool and returned. Otherwise, the version in memory is updated, and its reference is returned.
Notice that we added the synchronized modifier to this method. Java allows any method modifiers (except static) for the readResolve() method including any access modifier. This rule applies to writeReplace(), which is up next.



### Applying writeReplace()

Now, what if we want to write an Employee record to disk but we don't completely trust the instance we are holding? For example, we want to always write the version of the object in the pool rather than the this instance. By construction, there should be only one version of this object in memory, but for this example let's pretend we're not 100 percent confident of that.

The writeReplace() method is run before writeObject() and allows us to replace the object that gets serialized.

```
import java.io.*;
import java.util.Map;
import java.util.concurrent.ConcurrentHashMap;
public class Employee implements Serializable {
   ...
    public Object writeReplace() throws ObjectStreamException {
      var e = pool.get(name);
      return e != null ? e : this;
    }
}

```
This implementation checks whether the object is found in the pool. If it is found in the pool, that version is sent for serialization; otherwise, the current instance is used.



|Return type| Method |Parameters |Description|
|-|-|-|-|
|Object|writeReplace|None|Allows replacement of object before serialization|
|void|writeObject()|ObjectInputStream|Serializes optionally using PutField|
|void|readObject()| ObjectOutputStream|Deserializes optionally using GetField|
|Object|readResolve()|None|Allows replacement of object after deserialization|


### Making Methods final

### Making Classes final

### Making Constructor private

```
public class FoodOrder {
   private String item;
   private int count;

    private FoodOrder(String item, int count) { setItem(item);
        setCount(count);
    }
-> public FoodOrder getOrder(String item, int count) {
      return new FoodOrder(item, count);
   }
   public String getItem() { return item; }
   public void setItem(String item) { this.item = item; }
   public int getCount() { return count; }
   public void setCount(int count) { this.count = count; }
}
```

## HOW TO PROTECT THE SOURCE CODE

jars.....



### Preventing Denial of Service Attacks

A denial of service (DoS) attack is when a hacker makes one or more requests with the intent of disrupting legitimate requests. Most denial of service attacks require multiple requests to bring down their targets. Some attacks send a very large request that can even bring down the application in one shot.

By contrast, a distributed denial of service (DDoS) attack is a denial of service attack that comes from many sources at once. For example, many machines may attack the target. 

### LEAKING RESOURCES

### READING VERY LARGE RESOURCES


Another source of a denial of service attacks is very large resources.

```
public void transform(Path in, Path out) throws IOException  {
   var list = Files.readAllLines(in);
   list.removeIf(s -> s.trim().isBlank());
   Files.write(out, list);
}
```
gaat mis op grote files want je geheugen loopt vol...
To prevent this problem, you can check the size of the file before reading it.

### INCLUDING POTENTIALLY LARGE RESOURCES

An inclusion attack is when multiple files or components are embedded within a single file. Any file that you didn't create is suspect. Some types can appear smaller than they really are. For example, some types of images can have a “zip bomb” where the file is heavily compressed on disk. When you try to read it in, the file uses much more space than you thought.


Extensible Markup Language (XML) files can have the same problem. One attack is called the “billion laughs attack” where the file gets expanded exponentially.







### OVERFLOWING NUMBERS

When checking file size, be careful with an int type and loops. Since an int has a maximum size, exceeding that size results in integer overflow. Incrementing an int at the maximum value results in a negative number, so validation might not work as expected.

```
public static void main(String[] args) {
   System.out.println(enoughRoomToAddLine(100));
   System.out.println(enoughRoomToAddLine(2_000_000));
   System.out.println(enoughRoomToAddLine(Integer.MAX_VALUE));
}
public static boolean enoughRoomToAddLine(int requestedSize) {
   int maxLength = 1_000_000;
   String newLine = "END OF FILE";
   int newLineSize = newLine.length();
   return requestedSize + newLineSize < maxLength;
}

//true
//false
//true
```


### WASTING DATA STRUCTURES

One advantage of using a HashMap is that you can look up an element quickly by key. Even if the map is extremely large, a lookup is fast as long as there is a good distribution of hashed keys.



- Identify ways of preventing a denial of service attack. Using a try‐with‐ resources statement for all I/O and JDBC operations prevents resource leaks. Checking the file size when reading a file prevents it from using an unexpected amount of memory. Confirming large data structures are being used effectively can prevent a performance problem.
- Protect confidential information in memory. Picking a data structure that minimizes exposure is important. The most common one is using char[] for passwords. Additionally, allowing confidential information to be garbage collected as soon as possible reduces the window of exposure.
- Compare injection, inclusion, and input validation. SQL injection and command injection allow an attacker to run expected commands. Inclusion is when one file includes another. Input validation checks for valid or invalid characters from users.
- Design secure objects. Secure objects limit the accessibility of instance variables and methods. They are deliberate about when subclasses are allowed. Often secure objects are immutable and validate any input parameters.
- Write serialization and deserializaton code securely. The transient modifier signifies that an instance variable should not be serialized. Alternatively, serialPersistenceFields specifies what should be. The readObject(), writeObject(), readResolve(), and writeReplace() methods are optional methods that provide further control of the process.






[prev](http://hjh.devsnips.nl/ocp21)
[next](http://hjh.devsnips.nl/ocp01)