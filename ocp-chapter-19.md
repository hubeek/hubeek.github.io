# OCP Chapter 19

_Status: Published_
_Created: 2024-07-30 16:56:20_
_Tags: ocp_

# OCP Chapter 19 I/O

- read write data console + file using I/O streams
- use IO stream to read write files
- read write object by using serialization

using `java.io` API to interact with files and streams  

I/O streams zijn niet gelijk of hebben niets te maken met streams voor collections....  






## Files  Directories
- *root*
- *path*
- *path seperator* character / or \
- data is stored in *bytes*

### File Class
The File class is used to read information about existing files AND directories, list the contents of a directory, and create/delete files and directories. An instance of a File class represents the path to a particular file or directory on the file system. The File class can NOT read or write data within a file, although it can be passed as a reference to many stream classes to read or write data.    

#### Creating a File Object
A File object often is initialized with a String containing either an absolute or relative path to the file or directory within the file system. The absolute path of a file or directory is the full path from the root directory to the file or directory, including all subdirectories that contain the file or directory. Alternatively, the relative path of a file or directory is the path from the current working directory to the file or directory.

absolute path:  
/home/tiger/data/stripes.txt   

relative path from /home/tiger  
data/stripes.txt  


```
var zooFile1 = new File("/home/tiger/data/stripes.txt");
System.out.println(zooFile1.exists()); // true if the file exists
```
## Constructors
```
public File(String pathname)
public File(File parent, String child)
public File(String parent, String child)
```

```
File zooFile3 = new File("stripes.txt");
System.out.println(zooFile3.exists()); // File object is niet de file zelf
//                                       ...alleen t path naar de file.....

// dan is zooFile3.createNewFile() nodig
        File zooFile3 = new File("stripes.txt");
        try {
            if (zooFile3.createNewFile()) {
                System.out.println("File created: " + zooFile3.getName());
            } else {
                System.out.println("File already exists.");
            }
        } catch (IOException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
        }
        System.out.println("File exists: " + zooFile3.exists());
```




## Commonly used java.io.File methods
- boolean delete() Deletes the file or directory and returns true only if successful. If this instance denotes a directory, then the directory must be empty in order to be deleted.
- boolean exists() Checks if a file exists
- String getAbsolutePath() Retrieves the absolute name of the file or directory within the file system
- String getName() Retrieves the name of the file or directory.
- String getParent() Retrieves the parent directory that the path is contained in or null if there is none
- boolean isDirectory() Checks if a File reference is a directory within the file system
- boolean isFile() Checks if a File reference is a file within the file system
- long lastModified() Returns the number of milliseconds since the epoch (number of milliseconds since 12 a.m. UTC on January 1, 1970) when the file was last modified
- long length() Retrieves the number of bytes in the file
- File[] listFiles() Retrieves a list of files within a directory
- boolean mkdir() Creates the directory named by this path
- boolean mkdirs() Creates the directory named by this path including any nonexistent parent directories
- boolean renameTo(File dest) Renames the file or directory denoted by this path to dest and returns true only if successful


Let op!!! Kan file maar ook **Directory** zijn!!!
```
/data/zoo.txt
```



```Java
// Print current working directory
System.out.println("Current working directory: " + System.getProperty("user.dir"));

// Ensure the directory exists
java.io.File dir = new java.io.File("hjh");
if (!dir.exists()) {
    boolean created = dir.mkdirs();
    System.out.println("Directory created: " + created);
} else {
    System.out.println("Directory already exists.");
}

// Ensure the file exists
java.io.File file = new java.io.File("hjh/test.txt");
try {
    if (file.createNewFile()) {
        System.out.println("File created: " + file.getName());
    } else {
        System.out.println("File already exists.");
    }
} catch (java.io.IOException e) {
    System.err.println("An error occurred while creating the file.");
    e.printStackTrace();
}

// Verify the directory
if (dir.exists() && dir.isDirectory()) {
    System.out.println("Directory contents:");
    for (String f : dir.list()) {
        System.out.println(f);
    }
} else {
    System.out.println("Directory 'hjh' does not exist.");
}

// Verify the specific file
System.out.println("File exists: " + file.exists());

```

    Current working directory: /Users/hjhubeek/Development/jupyter/IJava
    Directory already exists.
    File already exists.
    Directory contents:
    stripes.txt
    test.txt
    File exists: true



```Java

File parent = new File("hjh");
// Ensure the parent directory exists
if (!parent.exists()) {
    boolean dirCreated = parent.mkdirs();
    if (dirCreated) {
        System.out.println("Directory 'hjh' created.");
    } else {
        System.out.println("Failed to create directory 'hjh'.");
    }
} else {
    System.out.println("Directory 'hjh' already exists.");
}
File zooFile3 = new File(parent,"stripes.txt");
try {
    if (zooFile3.createNewFile()) {
        System.out.println("File created: " + zooFile3.getName());
    } else {
        System.out.println("File already exists.");
    }
} catch (IOException e) {
    System.out.println("An error occurred.");
    e.printStackTrace();
}
System.out.println("abs path: " + zooFile3.getAbsolutePath());
System.out.println("File exists: " + zooFile3.exists());

```

    Directory 'hjh' already exists.
    File already exists.
    abs path: /Users/hjhubeek/Development/jupyter/IJava/hjh/stripes.txt
    File exists: true


## Byte Stream vs Character Streams

- Byte streams read/write binary data ( 0s and 1s) and have class names that end in InputStream or OutputStream.
- Character streams read/write text data and have class names that end in Reader or Writer.

The API frequently includes similar classes for both byte and character streams, such as FileInputStream and FileReader.

**character encoding** determines how characters are encoded and stored in bytes in a stream and later read back or decoded as characters.

The character encoding can be specified using the Charset class by passing a name value to the static Charset.forName()
```
Charset usAsciiCharset = Charset.forName("US-ASCII");
Charset utf8Charset = Charset.forName("UTF-8");
Charset utf16Charset = Charset.forName("UTF-16");
```
For character encoding, just remember that using a character stream is better for working with text data than a byte stream. The character stream classes were created for convenience, and you should certainly take advantage of them when possible.



## Input vs. Output Streams

Most Reader classes have a corresponding Writer class. For example, the FileWriter class writes data that can be read by a FileReader.

There are exceptions to this rule. For the exam, you should know that PrintWriter has no accompanying PrintReader class. Likewise, the PrintStream is an OutputStream that has no corresponding InputStream class. It also does not have Output in its name.




## Low‐Level vs. High‐Level Streams

A **low‐level** stream connects directly with the source of the data, such as a file, an array, or a String. Low‐level streams process the raw data or resource and are accessed in a direct and unfiltered manner. For example, a FileInputStream is a class that reads file data one byte at a time.

Alternatively, a **high‐level** stream is built on top of another stream using wrapping. Wrapping is the process by which an instance is passed to the constructor of another class, and operations on the resulting instance are filtered and applied to the original instance.

```
try (var br = new BufferedReader(new FileReader("zoo- data.txt"))) {
   System.out.println(br.readLine());
}
```
Fileread is the low-level stream readeer and BufferedReader is the high-level stream that takes the FileReader as input.

High‐level streams can take other high‐level streams as input. For example, although the following code might seem a little odd at first, the style of wrapping a stream is quite common in practice:
```
try (var ois = new ObjectInputStream( new BufferedInputStream(
new FileInputStream("zoo-data.txt")))) { System.out.print(ois.readObject());
}
```


## Stream Base Classes

The java.io library defines four abstract classes that are the parents of all stream classes defined within the API: 
- InputStream
- OutputStream
- Reader
- Writer

```
new BufferedInputStream(new FileReader("z.txt"));  // DOES NOT COMPILE
new BufferedWriter(new FileOutputStream("z.txt")); // DOES NOT COMPILE
new ObjectInputStream(   new FileOutputStream("z.txt")); // DOES NOT COMPILE
new BufferedInputStream(new InputStream()); // DOES NOT COMPILE
```
The first two examples do not compile because they mix Reader/ Writer classes with InputStream/ OutputStream classes, respectively. The third example does not compile because we are mixing an OutputStream with an InputStream. Although it is possible to read data from an InputStream and write it to an OutputStream, wrapping the stream is not the way to do so. As you will see later in this chapter, the data must be copied over, often iteratively. Finally, the last example does not compile because InputStream is an abstract class, and therefore you cannot create an instance of it.




## Decoding I/O Class Names

Pay close attention to the name of the I/O class on the exam, as decoding it often gives you context clues as to what the class does. 

### Review of java.io Class Name Properties

- A class with the word InputStream or OutputStream in its name is used for reading or writing binary or byte data, respectively.
- A class with the word Reader or Writer in its name is used for reading or writing character or string data, respectively.
- Most, but not all, input classes have a corresponding output class.
- A low‐level stream connects directly with the source of the data.
- A high‐level stream is built on top of another stream using wrapping.
- A class with Buffered in its name reads or writes data in groups of bytes or characters and often improves performance in sequential file systems.
- With a few exceptions, you only wrap a stream with another stream if they share the same abstract parent.

|Class Name| Description|
|-|-|
|InputStream|Abstract class for all input byte streams|
|OutputStream|Abstract class for all output byte streams|
|Reader|Abstract class for all input character streams|
|Writer|Abstract class for all output character streams|


|Class Name|Low/High Level|Description|
|-|-|-|
|FileInputStream|Low|Reads file data as bytes|
|FileOutputStream|Low|Writes file data as bytes|
|FileReader|Low|Reads file data as characters|
|FileWriter|Low|Writes file data as characters|
|Buffered InputStream|High|Reads byte data from an existing InputStream in a buffered manner, which improves efficiency and performance|
|Buffered OutputStream|High|Writes byte data to an existing OutputStream in a buffered manner, which improves efficiency and performance|
|Buffered Reader|High|Reads character data from an existing Reader in a buffered manner, which improves efficiency and performance|
|Buffered Writer|High|Writes character data to an existing Writer in a buffered manner, which improves efficiency and performance|
|ObjectInputStream|High|Deserializes primitive Java data types and graphs of Java objects from an existing InputStream|
|ObjectOutputStream|High|Serializes primitive Java data types and graphs of Java objects to an existing OutputStream|
|PrintStream|High|Writes formatted representations of Java objects to a binary stream|
|PrintWriter|High|Writes formatted representations of Java objects to a character stream|




## Common I/O Stream Operations

### Reading and Writing Data
I/O streams are all about reading/writing data, so it shouldn't be a surprise that the most important methods are read() and write(). 

```
// InputStream and Reader
public int read() throws IOException

// OutputStream and Writer
public void write(int b) throws IOException
```
Why do the methods use int instead of byte? Remember, the byte data type has a range of 256 characters. They needed an extra value to indicate the end of a stream. The authors of Java decided to use a larger data type, int, so that special values like ‐1 would indicate the end of a stream. The output stream classes use int as well, to be consistent with the input stream classes. 

### Closing the Stream

```
// All I/O stream classes
public void close() throws IOException
```

In many file systems, failing to close a file properly could leave it locked by the operating system such that no other processes could read/write to it until the program is terminated. Throughout this chapter, we will close stream resources using the try‐with‐resources syntax since this is the preferred way of closing resources in Java.

What about if you need to pass a stream to a method? That's fine, but **the stream should be closed in the method that created it**.

The following example is valid and will result in three separate close() method calls but is unnecessary:
```
try (var fis = new FileOutputStream("zoo-
banner.txt"); // Unnecessary
         var bis = new BufferedOutputStream(fis);
         var ois = new ObjectOutputStream(bis)) {
       ois.writeObject("Hello");
}
```
Instead, we can rely on the ObjectOutputStream to close the BufferedOutputStream and FileOutputStream. The following will call only one close() method instead of three:
```
try (var ois = new ObjectOutputStream(
      new BufferedOutputStream(
         new FileOutputStream("zoo-banner.txt")))) {
   ois.writeObject("Hello");
}
```

### MANIPULATING INPUT STREAMS
All input stream classes include the following methods to manipulate the order in which data is read from a stream:

```
// InputStream and Reader
public boolean <b>markSupported()</b>
public void void mark(int readLimit)
public void reset() throws IOException
public long skip(long n) throws IOException
```

#### mark() and reset()

The mark() and reset() methods return a stream to an earlier position. Before calling either of these methods, you should call the **markSupported() method**, which returns true only if mark() is supported. The skip() method is pretty simple; it basically reads data from the stream and discards the contents.

```
public void readData(InputStream is) throws IOException {
System.out.print((char) is.read()); // L
    if (is.markSupported()) {
       is.mark(100); // Marks up to 100 bytes
       System.out.print((char) is.read()); // I
       System.out.print((char) is.read()); // O
       is.reset(); // Resets stream to position before I
    }
}
System.out.print((char) is.read()); // I 
System.out.print((char) is.read()); // O 
System.out.print((char) is.read()); // N

```

#### skip()

```
System.out.print ((char)is.read()); // T
is.skip(2); // Skips I and G
is.read(); // Reads E but doesn't output it
System.out.print((char)is.read()); // R
System.out.print((char)is.read()); // S
```
This code prints TRS at runtime. We skipped two characters, I and G. We also read E but didn't store it anywhere, so it behaved like calling skip(1).

The return parameter of skip() tells us how many values were actually skipped. For example, if we are near the end of the stream and call skip(1000), the return value might be 20, indicating the end of the stream was reached after 20 values were skipped.



## FLUSHING OUTPUT STREAMS

When data is written to an output stream, the underlying operating system does not guarantee that the data will make it to the file system immediately. In many operating systems, the data may be cached in memory, with a write occurring only after a temporary cache is filled or after some amount of time has passed.
If the data is cached in memory and the application terminates unexpectedly, the data would be lost, because it was never written to the file system. To address this, all output stream classes provide a flush() method, which requests that all accumulated data be written immediately to disk.

```
// OutputStream and Writer
public void flush() throws IOException
```

The flush() method helps reduce the amount of data lost if the application terminates unexpectedly. It is not without cost, though. Each time it is used, it may cause a noticeable delay in the application, especially for large files. Unless the data that you are writing is extremely critical, the flush() method should be used only intermittently. For example, it should not necessarily be called after every write.


## Common I/O Stream Methods

|Stream Class| Method Name| Description|
|-|-|-|
|All streams|void close()|Closes stream and releases resources|
|All input streams|int read()|Reads a single byte or returns ‐1 if no bytes were available|
|InputStreamReader |int read(byte[] b) int read(char[] c)|Reads values into a buffer. Returns number of bytes read|
|InputStream|int read(byte[]b, int offset,int length)|Reads up to length values into a buffer starting from position offset. Returns number of bytes read|
|Reader|int read(char[]c, int offset,int length)| |
|All OutputStreams|void write(int)|Writes a single byte|
|OutputStream Writer|void write(byte[] b) void write(char[] c)|Writes an array of values into the stream|
| OutputStream|void write(byte[] b, int offset, int length)|Writes length values from an array into the stream, starting with an offset index|
|Writer|void write(char[] c, int offset, int length)| All input streams|
|All input streams| boolean markSupported()|Returns true if the stream class supports mark()|
|All input streams| mark(int readLimit)|Marks the current position in the stream|
|All input streams| void reset()|Attempts to reset the stream to the mark() position|
|All input streams| long skip(long n)|Reads and discards a specified number of characters|
|All output streams|void flush()|Flushes buffered data through the stream|

Remember that input and output streams can refer to both byte and character streams throughout this chapter.


## Working with I/O Stream Classes

### READING AND WRITING BINARY DATA

the most basic file stream classes, FileInputStream and FileOutputStream

They are used to read bytes from a file or write bytes to a file, respectively.

```
public FileInputStream(File file) throws FileNotFoundException
public FileInputStream(String name) throws FileNotFoundException
public FileOutputStream(File file) throws FileNotFoundException
public FileOutputStream(String name) throws FileNotFoundException
```
If you need to append to an existing file, there's a constructor for that. The FileOutputStream class includes overloaded constructors that take a boolean append flag. When set to true, the output stream will append to the end of a file if it already exists. This is useful for writing to the end of log files, for example.

```
void copyFile(File src, File dest) throws IOException { try (var in = new FileInputStream(src);
var out = new FileOutputStream(dest)) { int b;
while ((b = in.read()) != -1) { out.write(b);
} }
}
```
If the source file does not exist, a FileNotFoundException, which inherits IOException, will be thrown. If the destination file already exists, this
implementation will overwrite it, since the append flag was not sent. The copy() method copies one byte at a time until it reads a value of ‐1.



### BUFFERING BINARY DATA
While our copyFile() method is valid, it tends to perform poorly on large files.

```
public BufferedInputStream(InputStream in)
public BufferedOutputStream(OutputStream out)
```

```
void copyFileWithBuffer(File src, File dest) throws IOException {
    try (var in = new BufferedInputStream(new FileInputStream(src));
            var out = new BufferedOutputStream(new FileOutputStream(dest))) {
        var buffer = new byte[1024];
        int lengthRead;
        while ((lengthRead = in.read(buffer))> 0) {
            out.write(buffer, 0, lengthRead);
            out.flush();
        }
    }
}
```
Instead of reading the data one byte at a time, we read and write up to 1024 bytes at a time. The return value lengthRead is critical for determining whether we are at the end of the stream and knowing how many bytes we should write into our output stream. We also added a flush() command at the end of the loop to ensure data is written to disk between each iteration.


### READING AND WRITING CHARACTER DATA

The FileReader and FileWriter classes, along with their associated buffer classes, are among the most convenient I/O classes because of their built‐in support for text data. They include constructors that take the same input as the binary file classes.
The following is an example of using these classes to copy a text file:
```
public FileReader(File file) throws FileNotFoundException
public FileReader(String name) throws FileNotFoundException
public FileWriter(File file) throws FileNotFoundException
public FileWriter(String name) throws FileNotFoundException
```

```
void copyTextFile(File src, File dest) throws IOException {
 try (var reader = new FileReader(src);
      var writer = new FileWriter(dest)) {
    int b;
    while ((b = reader.read()) != -1) { writer.write(b);
    }
 }
}
```
Wait a second, this looks identical to our copyFile() method with byte stream! Since we're copying one character at a time, rather than one byte, it is.

The FileReader class doesn't contain any new methods you haven't seen before. The FileWriter inherits a method from the Writer class that allows it to write String values.

```// Writer
public void write(String str) throws IOException
```

For example, the following is supported in FileWriter but not FileOutputStream:
```writer.write("Hello World");```




### BUFFERING CHARACTER DATA

Java includes high‐level buffered character streams that improve performance. The constructors take existing Reader and Writer instances as input.

```
public BufferedReader(Reader in)
public BufferedWriter(Writer out)
```
They add two new methods, readLine() and newLine(), that are particularly useful when working with String values.

```
void copyTextFileWithBuffer(File src, File dest) throws IOException {
    try (var reader = new BufferedReader(new FileReader(src)); var writer = new BufferedWriter(new FileWriter(dest)))
    {
        String s;
        while ((s = reader.readLine()) != null) {
         writer.write(s);
         writer.newLine();
        }
    }
}
```
In this example, each loop iteration corresponds to reading and writing a line of a file. Assuming the length of the lines in the file are reasonably sized, this implementation will perform well.

There are some important distinctions between this method and our earlier copyFileWithBuffer() method that worked with byte streams. First, instead of a buffer array, we are using a String to store the data read during each loop iteration. By storing the data temporarily as a String, we can manipulate it as we would any String value. For example, we can call replaceAll() or toUpperCase() to create new values.

Next, we are checking for the end of the stream with a null value instead of ‐1. Finally, we are inserting a newLine() on every iteration of the loop. This is because readLine() strips out the line break character. Without the call to newLine(), the copied file would have all of its line breaks removed.



## SERIALIZING DATA

**Serialization** is the process of converting an in‐ memory object to a byte stream. Likewise, deserialization is the process of converting from a byte stream into an object. Serialization often involves writing an object to a stored or transmittable format, while deserialization is the reciprocal process.

To serialize an object using the I/O API, the object must implement the java.io.Serializable interface. The Serializable interface is a marker interface, similar to the marker annotations you learned about in Chapter 13, “Annotations.” By marker interface, it means the interface does not have any methods. Any class can implement the Serializable interface since there are no required methods to implement.

The purpose of using the Serializable interface is to inform any process attempting to serialize the object that you have taken the proper steps to make the object serializable. All Java primitives and many of the built‐in Java classes that you have worked with throughout this book are Serializable.

```
import java.io.Serializable;

public class Gorilla implements Serializable {
   private static final long serialVersionUID = 1L;
   private String name;
   private int age;
   private Boolean friendly;

   private transient String favoriteFood;
   // Constructors/Getters/Setters/toString() omitted
}
```
The Gorilla class contains three instance members ( name, age, friendly) that will be saved to a stream if the class is serialized. 

Any field that is marked transient will not be saved to a stream when the class is serialized.

### Marking Data transient

Oftentimes, the transient modifier is used for sensitive data of the class, like a password.

There are other objects it does not make sense to serialize, like the state of an in‐memory Thread. If the object is part of a serializable object, we just mark it transient to ignore these select instance members.

### Ensuring a Class Is Serializable

Any process attempting to serialize an object will throw a NotSerializableException if the class does not implement the Serializable interface properly.

- The class must be marked Serializable.
- Every instance member of the class is serializable, marked transient, or has a null value at the time of serialization.

```
public class Cat implements Serializable {
   private Tail tail = new Tail();
}
public class Tail implements Serializable {
   private Fur fur = new Fur();
}
public class Fur {}
```
Cat contains an instance of Tail, and both of those classes are marked Serializable, so no problems there. Unfortunately, Tail contains an instance of Fur that is not marked Serializable.
Either of the following changes fixes the problem and allows Cat to be serialized:

```
public class Tail implements Serializable {
    private transient Fur fur = new Fur();
}
public class Fur implements Serializable {}
```
We could also make our tail or fur instance members null, although this would make Cat serializable only for particular instances, rather than all instances.

### Storing Data with ObjectOutputStream and ObjectInputStream
The ObjectInputStream class is used to deserialize an object from a stream, while the ObjectOutputStream is used to serialize an object to a stream. They are high‐level streams that operate on existing streams.

```
public ObjectInputStream(InputStream in) throws IOException
public ObjectOutputStream(OutputStream out) throws IOException
```
While both of these classes contain a number of methods for built‐in data types like primitives, the two methods you need to know for the exam are the ones related to working with objects.

```
// ObjectInputStream
public Object readObject() throws IOException, ClassNotFoundException
// ObjectOutputStream
public void writeObject(Object obj) throws IOException
```

```
void saveToFile(List<Gorilla> gorillas, File dataFile)
      throws IOException {
    try (var out = new ObjectOutputStream( new BufferedOutputStream(
              new FileOutputStream(dataFile)))) {
      for (Gorilla gorilla : gorillas)
            out.writeObject(gorilla);
    }
}
```

Once the data is stored in a file, we can deserialize it using the following method:
```
List<Gorilla> readFromFile(File dataFile) throws IOException, ClassNotFoundException {
    var gorillas = new ArrayList<Gorilla>();
    try (var in = new ObjectInputStream(
           new BufferedInputStream(
              new FileInputStream(dataFile)))) {
        while (true) {
            var object = in.readObject();
            if (object instanceof Gorilla)
                gorillas.add((Gorilla) object);
            }
    } catch (EOFException e) {
      // File end reached
    }
    return gorillas;
}
```
Since the return type of readObject() is Object, we need an explicit cast to obtain access to our Gorilla properties. Notice that readObject() declares a checked ClassNotFoundException since the class might not be available on deserialization.

```
var gorillas = new ArrayList<Gorilla>();
gorillas.add(new Gorilla("Grodd", 5, false));
gorillas.add(new Gorilla("Ishmael", 8, true));
File dataFile = new File("gorilla.data");
saveToFile(gorillas, dataFile);
var gorillasFromDisk = readFromFile(dataFile); System.out.print(gorillasFromDisk);
```


## Understanding the Deserialization Creation Process

When you deserialize an object, the constructor of the serialized class, along with any instance initializers, is not called when the object is created. Java will call the no‐arg constructor of the first nonserializable parent class it can find in the class hierarchy.

As we stated earlier, any static or transient fields are ignored. Values that are not provided will be given their default Java value, such as null for String, or 0 for int values.

make sure you understand that the constructor and any instance initializations defined in the serialized class are ignored during the deserialization process. Java only calls the constructor of the first non‐ serializable parent class in the class hierarchy.




## PRINTING DATA

PrintStream and PrintWriter are high‐level output print streams classes that are useful for writing text data to a stream. We cover these classes together, because they include many of the same methods. Just remember that one operates on an OutputStream and the other a Writer.

The print stream classes have the distinction of being the only I/O stream classes we cover that do not have corresponding input stream classes. And unlike other OutputStream classes, PrintStream does not have Output in its name.

```
public PrintStream(OutputStream out)
public PrintWriter(Writer out)
```
For convenience, these classes also include constructors that automatically wrap the print stream around a low‐level file stream class, such as FileOutputStream and FileWriter.

```
public PrintStream(File file) throws FileNotFoundException
public PrintStream(String fileName) throws FileNotFoundException

public PrintWriter(File file) throws FileNotFoundException
public PrintWriter(String fileName) throws FileNotFoundException
```

Furthermore, the PrintWriter class even has a constructor that takes an OutputStream as input. This is one of the few exceptions in which we can mix a byte and character stream.
```
public PrintWriter(OutputStream out)
```
Besides the inherited write() methods, the print stream classes include numerous methods for writing data including print(), println(), and format(). Unlike the majority of the other streams we've covered, the methods in the print stream classes do not throw any checked exceptions. If they did, you would have been required to catch a checked exception anytime you called System.out.print()! The stream classes do provide a method, checkError(), that can be used to check for an error after a write.

When working with String data, you should use a Writer, so our examples in this part of the chapter use PrintWriter. Just be aware that many of these examples can be easily rewritten to use a PrintStream.

### print()

The most basic of the print‐based methods is print(). The print stream classes include numerous overloaded versions of print(), which take everything from primitives and String values, to objects. Under the covers, these methods often just perform String.valueOf() on the argument and call the underlying stream's write() method to add it to the stream.

### println()

The next methods available in the PrintStream and PrintWriter classes are the println() methods, which are virtually identical to the print() methods, except that they also print a line break after the String value is written. These print stream classes also include a no‐argument version of println(), which just prints a single line break.

```
System.getProperty("line.separator");
System.lineSeparator();
```

### format()

Each print stream class includes a format() method, which includes an overloaded version that takes a Locale.

```
// PrintStream
public PrintStream format(String format, Object args...)
public PrintStream format(Locale loc, String format, Object args...)

// PrintWriter
public PrintWriter format(String format, Object args...)
public PrintWriter format(Locale loc, String format, Object args...)
```

The method parameters are used to construct a formatted String in a single method call, rather than via a lot of format and concatenation operations. They return a reference to the instance they are called on so that operations can be chained together.
As an example, the following two format() calls print the same text:

```
String name = "Lindsey";
int orderId = 5;
// Both print: Hello Lindsey, order 5 is ready

System.out.format("Hello "+name+", order "+orderId+" is ready");

System.out.format("Hello %s, order %d is ready", name, orderId);
```

|Symbol |Description|
|-|-|
|%s|Applies to any type, commonly String values|
|%d|Applies to integer values like int and long|
|%f|Applies to floating‐point values like float and double|
|%n|Inserts a line break using the system‐dependent line separator|

Mixing data types may cause exceptions at runtime. For example, the following throws an exception because a floating‐point number is used when an integer value is expected:

```
System.out.format("Food: %d tons", 2.0); // IllegalFormatConversionException
```

### USING FORMAT() WITH FLAGS
Besides supporting symbols, Java also supports optional flags between the % and the symbol character. In the previous example, the floating‐point number was printed as 90.250000. By default, %f displays exactly six digits past the decimal. If you want to display only one digit after the decimal, you could use %.1f instead of %f. The format() method relies on rounding, rather than truncating when shortening numbers. For example, 90.250000 will be displayed as 90.3 (not 90.2) when passed to format() with %.1f.

The format() method also supports two additional features. You can specify the total length of output by using a number before the decimal symbol. By default, the method will fill the empty space with blank spaces. You can also fill the empty space with zeros, by placing a single zero before the decimal symbol. The following examples use brackets, [], to show the start/end of the formatted value:


```
var pi = 3.14159265359;
System.out.format("[%f]",pi);      // [3.141593]
System.out.format("[%12.8f]",pi);  // [  3.14159265]
System.out.format("[%012f]",pi);   // [00003.141593]
System.out.format("[%12.2f]",pi);  // [        3.14]
System.out.format("[%.3f]",pi);    // [3.142]
```
The format() method supports a lot of other symbols and flags. You don't need to know any of them for the exam beyond what we've discussed already.




### INPUTSTREAMREADER AND OUTPUTSTREAMWRITER

Most of the time, you can't wrap byte and character streams with each other, although as we mentioned, there are exceptions. The InputStreamReader class wraps an InputStream with a Reader, while the OutputStreamWriter class wraps an OutputStream with a Writer.

```
try (Reader r = new InputStreamReader(System.in); Writer w = new OutputStreamWriter(System.out)) { }
```

These classes are incredibly convenient and are also unique in that they are the only I/O stream classes to have both InputStream/ OutputStream and Reader/ Writer in their name.

# Interacting with Users

## PRINTING DATA TO THE USER

Java includes two PrintStream instances for providing information to the user: System.out and System.err. While System.out should be old hat to you, System.err might be new to you. The syntax for calling and using System.err is the same as System.out but is used to report errors to the user in a separate stream from the regular output information.

```
try (var in = new FileInputStream("zoo.txt")) {
   System.out.println("Found file!");
} catch (FileNotFoundException e) {
   System.err.println("File not found!");
}
```

How do they differ in practice? In part, that depends on what is executing the program. For example, if you are running from a command prompt, they will likely print text in the same format. On the other hand, if you are working in an integrated development environment (IDE), they might print the System.err text in a different color. Finally, if the code is being run on a server, the System.err stream might write to a different log file.

### USING LOGGING APIS
While there are many logging APIs available, they tend to share a number of similar attributes. First, you create a static logging object in each class. Then, you log a message with an appropriate logging level: debug(), info(), warn(), or error(). The debug() and info() methods are useful as they allow developers to log things that aren't errors but may be useful.

The log levels can be enabled as needed at runtime. For example, a server might only output warn() and error() to keep the logs clean and easy to read. If an administrator notices a lot of errors, then they might enable debug() or info() logging to help isolate the problem.
Finally, loggers can be enabled for specific classes or packages. While you may be interested in a debug() message for a class you write, you are probably not interested in seeing debug() messages for every third‐party library you are using.

## READING INPUT AS A STREAM

```
var reader = new BufferedReader(new InputStreamReader(System.in));
String userInput = reader.readLine();
System.out.println("You entered: " + userInput);
```

## CLOSING SYSTEM STREAMS

You might have noticed that we never created or closed System.out, System.err, and System.in when we used them. In fact, these are the only I/O streams in the entire chapter that we did not use a try‐with‐ resources block on!
Because these are static objects, the System streams are shared by the entire application. The JVM creates and opens them for us. They can be used in a try‐with‐resources statement or by calling close(), although closing them is not recommended. Closing the System streams makes them permanently unavailable for all threads in the remainder of the program.

```
try (var out = System.out) {}
System.out.println("Hello");
```
Nothing. It prints nothing. Remember, the methods of PrintStream do not throw any checked exceptions and rely on the checkError() to report errors, so they fail silently.

```
try (var err = System.err) {}
System.err.println("Hello");
```
This one also prints nothing. Like System.out, System.err is a PrintStream. Even if it did throw an exception, though, we'd have a hard time seeing it since our stream for reporting errors is closed! Closing System.err is a particularly bad idea, since the stack traces from all exceptions will be hidden.

```
var reader = new BufferedReader(new InputStreamReader(System.in));
try (reader) {}
String data = reader.readLine(); // IOException
```
It prints an exception at runtime. Unlike the PrintStream class, most InputStream implementations will throw an exception if you try to operate on a closed stream.

## ACQUIRING INPUT WITH CONSOLE
The java.io.Console class is specifically designed to handle user interactions. After all, System.in and System.out are just raw streams, whereas Console is a class with numerous methods centered around user input.
The Console class is a singleton because it is accessible only from a factory method and only one instance of it is created by the JVM.

For example, if you come across code on the exam such as the following, it does not compile, since the constructors are all private:
```Console c = new Console();  // DOES NOT COMPILE```

The following snippet shows how to obtain a Console and use it to retrieve user input:
```
Console console = System.console();
if (console != null) {
    String userInput = console.readLine();
    console.writer().println("You entered: " + userInput);
} else {
   System.err.println("Console not available");
}
```
The Console object may not be available, depending on where the code is being called. If it is not available, then System.console() returns null. It is imperative that you check for a null value before attempting to use a Console object!

### reader() and writer()
The Console class includes access to two streams for reading and writing
data.
```
public Reader reader()
public PrintWriter writer()
```
Accessing these classes is analogous to calling System.in and System.out directly, although they use character streams rather than byte streams. In this manner, they are more appropriate for handling text data.

### format()
For printing data with a Console, you can skip calling the writer().format() and output the data directly to the stream in a single call.

```
Console console = System.console();
if (console == null) {
   throw new RuntimeException("Console not available");
} else {
   console.writer().println("Welcome to Our Zoo!");
   console.format("It has %d animals and employs %d people", 391, 25);
   console.writer().println();
   console.printf("The zoo spans %5.1f acres", 128.91);
}
//Welcome to Our Zoo!
//It has 391 animals and employs 25 people
//The zoo spans 128.9 acres.
```

#### USING CONSOLE WITH A LOCALE
Unlike the print stream classes, Console does not include an overloaded format() method that takes a Locale instance. Instead, Console relies on the system locale. Of course, you could always use a specific Locale by retrieving the Writer object and passing your own Locale instance, such as in the following example:
```
Console console = System.console();
console.writer().format(new Locale("fr", "CA"), "Hello World");

```

### readLine() and readPassword()

The Console class includes four methods for retrieving regular text data
from the user.

```
public String readLine()
public String readLine(String fmt, Object... args)

public char[] readPassword()
public char[] readPassword(String fmt, Object... args)
```

Like using System.in with a BufferedReader,the Console readLine() method reads input until the user presses the Enter key. The overloaded version of readLine() displays a formatted message prompt prior to requesting input.
The readPassword() methods are similar to the readLine() method with two important differences.
- The text the user types is not echoed back and displayed on the screen as they are typing.
- The data is returned as a char[] instead of a String.

The first feature improves security by not showing the password on the screen if someone happens to be sitting next to you. 

The second feature involves preventing passwords from entering the String pool.

### Reviewing Console Methods


```
Console console = System.console();
if (console == null) {
   throw new RuntimeException("Console not available");
} else {
   String name = console.readLine("Please enter your name: ");
   console.writer().format("Hi %s", name);
   console.writer().println();
   console.format("What is your address? ");
   String address = console.readLine();
   char[] password = console.readPassword("Enter a password " + "between %d and %d characters: ", 5, 10);
   char[] verify = console.readPassword("Enter the password again: ");
   console.printf("Passwords " + (Arrays.equals(password, verify) ? "match" : "do notmatch"));
}
Please enter your name: Max
Hi Max
What is your address? Spoonerville
Enter a password between 5 and 10 digits:
Enter the password again:
Passwords match
```


### 


[prev](http://hjh.devsnips.nl/ocp18)
[next](http://hjh.devsnips.nl/ocp20)