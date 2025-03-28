# OCP Chapter 01

_Status: Published_
_Created: 2024-07-29 10:35:57_
_Tags: ocp_

- Java Development Kit with compiler javac. 
- javac converts .java to .class files. 
- Also archiver for .jar files and javadoc

## Javac
```bash
javac HelloWorld.java

```

## Jar
```
jar cvf HelloWorld.jar HelloWorld.class
```
- c: Creates a new archive file.
- v: Generates verbose output to standard output.
- f: Specifies the archive file name.

## Javadoc
```
javadoc -d doc HelloWorld.java
```
-d: Specifies the destination directory for the generated documentation.

## Jdeps
 is a command-line tool provided by the Java Development Kit (JDK) to analyze Java class files. 
 ```
jdeps myapp.jar // basic analysis
jdeps --verbose myapp.jar // verbose output
jdeps --summary myapp.jar // summary
jdeps --jdk-internals myapp.jar // detecting internal usage
jdeps --generate-module-info . myapp.jar // general module info
```

- Code Quality: Helps improve code quality by identifying unnecessary dependencies and dependencies on unstable internal APIs.
- Migration to Modules: Facilitates the migration of legacy codebases to the Java module system.
- Maintenance: Assists in maintaining and refactoring large codebases by providing clear insights into dependencies.

## JVM
Java Virtual Machine

## JRE
Java Runtime Enviroment is not anymore in there
jlink

## Java
Assuming you have compiled a Java program named HelloWorld that is in a file named HelloWorld.class, you can run this program using the java command as follows:
```
java HelloWorld
```
Assuming your class file is in ./com/example/HelloWorld.class, you would run:
```
java com.example.HelloWorld
```
If you're using a JAR file, you can run your application with the -jar option, like so:
```
java -jar YourApplication.jar
```

### Common Options
- -cp or -classpath: Specifies a list of directories, JAR archives, and ZIP archives to search for class files.
- -Xmx: Specifies the maximum size of the memory allocation pool (for example, -Xmx512m for 512 megabytes).
- -Xms: Specifies the initial size of the memory allocation pool.
- -version: Displays version information and exits.
- -verbose: Enables verbose output.

## Benefits of Java

- Object Oriented
- Encapsulation
- Platform Independent
- Robust
- Simple
- Secure
- Multithreaded
- Backwards Compatibility

  **OEPRSSMB**
  
  **SPERMBOS**  


## Class

- Java Class with which you create an Object.  
- An Object is a runtime instance in memory.  
  
- reference is a variable that points to an object.  

Class members:
-  fields and methods
   - method is an operation that can be called.
   - method signature = methodName + params
   - method declaration has return type
   - return type

```
public class Demo {
}
```
word with special meaing is a **keyword**
public + class is keyword

A java file can have more classes! But max one needs to be public + same as the file name!



```
public class Demo {

    String name;

    public getName() {
        return name;
    }

    publi void setName(String newName) {
        name = newName;
    }
}
```

### Comments
```
// until end of line

/*
 * Multi line comment
*/

/**
 * javadoc
 */
```

## Main()
public static void main(String[] args)

is startup of a java process managed by the JVM.
JVM allocate memory CPU access file and so on.

toegestane declaratie vd de argumenten:
String[] args  
String args []  
String... args  


## Java Version

```
javac -version
java -version
```



## Run a Java program


```Java
public class Zoo {

    public static void main(String[] args) {
        
    }
}
```

compile and run
```
javac Zoo.java
java Zoo
```

vanaf 11 kan ook meteen in 1 file runnen : 
```java Zoo.java```
maar dan alleen JDK imports


to compile a .java file is needed
name of the file must be the same as the containing class
results in bytecode in the .class file

public is access modifier
static results in Zoo.main()

voor java applicatie static main func is obligotory

String[] args  

String args[]  

String... args  


Als argumenten niet kloppen met run command dan ArrayIndexOutOfBoundException






```Java
Random r = new Random();
System.out.println(r.nextInt(12));
```

    4


## Imports

Er zijn Java built-in classes

andere classes zijn te vinden in packages die je kan importeren

### Conflicts
double same named Class will not compile

### Static imports

### Redundant imports

### Same Name 
dan bv 1 importeren en de andere helemaal uitschrijven.

```
import java.util.Data;

public class Conflicts {
    Date date;
    java.sql.Date sqlDate;

  // .... etc ...
}

```




## Alternate dir for compiling code

javac -d classes packagea/ClassA.java packageb/ClassB.java

zowel bij java als bij javac werken alle drie:
- java -cp classes packageb.ClassB
- java -classpath classes packageb.ClassB
- java --class-path classes packageb.ClassB
- -d <dir>

## Order packages imports
    
Package needs to be the first element  
    
Imports after package   


    



JDK Java Development Kit  
java  
javac  
jar  
javadoc  
Java Virtual Machine JVM  
JRE Java Runtime Enviroment  
jlink
jdeps (!)
API APplication Programming Interfaces  
  
Class  
Object  
reference  
members  
fields  
methods  
comments  
type  
returntype  
void  

[next ocp 02](http://hjh.devsnips.nl/ocp02)