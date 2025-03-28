# OCP Chapter 20

_Status: Published_
_Created: 2024-07-30 16:57:21_
_Tags: ocp_

# NIO

NIO.2 is an acronym that stands for the second version of the Non‐blocking Input/Output API, and it is sometimes referred to as the “New I/O.”. At its core, NIO.2 is a replacement for the legacy java.io.File class you learned about in Chapter 19. The goal of the API is to provide a more intuitive, more feature‐rich API for working with files and directories.

The cornerstone of NIO.2 is the java.nio.file.Path interface. A Path instance represents a hierarchical path on the storage system to a file or directory. You can think of a Path as the NIO.2 replacement for the java.io.File class, although how you use it is a bit different. Both java.io.File and Path objects may refer to an absolute path or relative path within the file system. In addition, both may refer to a file or a directory.

Unlike the java.io.File class, the Path interface contains support for **symbolic links**. A symbolic link is a special file within a file system that serves as a reference or pointer to another file or directory. In general, symbolic links are transparent to the user, as the operating system takes care of resolving the reference to the actual file. NIO.2 includes full support for creating, detecting, and navigating symbolic links within the file system.

## CREATING PATHS

Since Path is an interface, we can't create an instance directly. After all, interfaces don't have constructors! Java provides a number of classes and methods that you can use to obtain Path objects.

why is Path an interface? When a Path is created, the JVM returns a file system–specific implementation, such as a Windows or Unix Path class. In the vast majority of circumstances, we want to perform the same operations on the Path, regardless of the file system. By providing Path as an interface using the factory pattern, we avoid having to write complex or custom code for each type of file system.

`
// Path factory method
public static Path of(String first, String... more)

// impl
Path path1 = Path.of("pandas/cuddly.png");
Path path2 = Path.of("c:\\zooinfo\\November\\employees.txt");
Path path3 = Path.of("/home/zoodirectory");
`
The first example creates a reference to a relative path in the current working directory. The second example creates a reference to an absolute file path in a Windows‐based system. The third example creates a reference to an absolute directory path in a Linux or Mac‐based system.

### ABSOLUTE VS. RELATIVE PATHS

- If a path starts with a forward slash ( /), it is absolute, with / as the root directory. Examples: /bird/parrot.png and /bird/../data/./info
- If a path starts with a drive letter ( c:), it is absolute, with the drive letter as the root directory. Examples: c:/bird/parrot.png and d:/bird/../data/./info
- Otherwise, it is a relative path. Examples: bird/parrot.png and bird/../data/./info

The Path.of() method also includes a varargs to pass additional path elements. The values will be combined and automatically separated by the operating system–dependent file separator.

```
Path path1 = Path.of("pandas", "cuddly.png");
Path path2 = Path.of("c:", "zooinfo", "November", "employees.txt");
Path path3 = Path.of("/", "home", "zoodirectory");
```

## Obtaining a Path with the Paths Class (met zonder S)

The Path.of() method is actually new to Java 11. Another way to obtain a Path instance is from the java.nio.file.Paths factory class. Note the s at the end of the Paths class to distinguish it from the Path interface.
```
Path path1 = Paths.get("pandas/cuddly.png");
Path path2 = Paths.get("c:\\zooinfo\\November\\employees.txt");
Path path3 = Paths.get("/", "home", "zoodirectory");
```

## Obtaining a Path with a URI Class

Another way to construct a Path using the Paths class is with a URI value. A uniform resource identifier (URI) is a string of characters that identify a resource. It begins with a schema that indicates the resource type, followed by a path value. Examples of schema values include file:// for local file systems, and http://, https://, and ftp:// for remote file systems.
The java.net .URI class is used to create URI values.

// URI Constructor
```
public URI(String str) throws URISyntaxException
```
// URI to Path, using Path factory method
```
public static Path of(URI uri)
```
// URI to Path, using Paths factory method
```
public static Path get(URI uri)
```
// Path to URI, using Path instance method
```
public URI toURI()
```
The following examples all reference the same file:

```
URI a = new URI("file://icecream.txt");
Path b = Path.of(a);
Path c = Paths.get(a);
URI d = b.toUri();
```

Some of these examples may actually throw an IllegalArgumentException at runtime, as some systems require URIs to be absolute. The URI class does have an isAbsolute() method, although this refers to whether the URI has a schema, not the file location.

A URI can be used for a web page or FTP connection.

```
Path path5 = Paths.get(new URI("http://www.wiley.com"));
Path path6 = Paths.get(new URI("ftp://username:secret@ftp.example.com"));
```

## Obtaining a Path from the FileSystem Class

NIO.2 makes extensive use of creating objects with factory classes. As you saw already, the Paths class creates instances of the Path interface. Likewise, the FileSystems class creates instances of the abstract FileSystem class.

```
Path path1 = FileSystems.getDefault().getPath("pandas/cuddly.png");
Path path2 = FileSystems.getDefault().getPath("c:\\zooinfo\\November\\employees.txt");
Path path3 = FileSystems.getDefault().getPath("/home/zoodirectory");
```

### CONNECTING TO REMOTE FILE SYSTEMS

While most of the time we want access to a Path object that is within the local file system, the FileSystems class does give us the freedom to connect to a remote file system, as follows:

```
// FileSystems factory method
public static FileSystem getFileSystem(URI uri)
```

The following shows how such a method can be used:

```
FileSystem fileSystem = FileSystems.getFileSystem( new URI("http://www.selikoff.net"));
Path path = fileSystem.getPath("duck.txt");
```

This code is useful when we need to construct Path objects frequently for a remote file system. NIO.2 gives us the power to connect to both local and remote file systems, which is a major improvement over the legacy java.io.File class.

## Obtaining a Path from the java.io.File Class

Last but not least, we can obtain Path instances using the legacy java.io.File class. In fact, we can also obtain a java.io.File object from a Path instance.

```
// Path to File, using Path instance method
public default File toFile()
// File to Path, using java.io.File instance method
public Path toPath()

File file = new File("husky.png");
Path path = file.toPath();
File backToFile = path.toFile();
```

## Reviewing NIO.2 Relationships

By now, you should realize that NIO.2 makes extensive use of the factory pattern. You should become comfortable with this paradigm. Many of your interactions with NIO.2 will require two types: an abstract class or interface and a factory or helper class. The diagram shows the relationships among NIO.2 classes, as well as select java.io and java.net classes.
diagram:

```
              Creates

┌─────────────┐    ┌─────────────┐                       ┌─────────────┐
│ FileSystems │────▶ FileSystems │◀──────────┐         ▲ │java.io.File │
└─────────────┘    └─────────────┘           │         │ └─────────────┘
                                             ├─────────┘
                                             │
                                             ▼
                                      ┌─────────────┐
                             Creates  │             │Converts
                                  ┌──▶│    Path     │◀─┐
                                  │   │             │  │
                 ┌─────────────┐  │   └─────────────┘  │  ┌─────────────┐
                 │    Paths    │──┘          ▲         └─▶│java.net.URI │
                 └─────────────┘             │            └─────────────┘
                                        Uses │
                                      ┌─────────────┐
                                      │    Files    │
                                      └─────────────┘

```

When working with NIO.2, keep an eye on whether the class name is singular or plural. The classes with plural names include methods to create or operate on class/interface instances with singular names. Remember, a Path can also be created from the Path interface, using the static factory of() method.

Included in the diagram is the class java.nio.file.Files. For now, you just need to know that it is a helper or utility class that operates primarily on Path instances to read or modify actual files and directories.

## UNDERSTANDING COMMON NIO.2 FEATURES

### Applying Path Symbols

Absolute and relative paths can contain path symbols. A path symbol is a reserved series of characters that have special meaning within some file systems.

| Symbol | Description                                        |
| ------ | -------------------------------------------------- |
| .      | A reference to the current directory               |
| ..     | A reference to the parent of the current directory |

### Providing Optional Arguments

Many of the methods in this chapter include a varargs that takes an optional list of values.

Common NIO.2 method arguments
|Enum type|Interface inherited|Enum value|Details|
|-|-|-|-|
|LinkOption|Copy Option Open Option|NOFOLLOW_LINKS|Do not follow symbolic links.|
|Standard CopyOption|Copy Option|ATOMIC_MOVE|Move file as atomic file system operation.|
|Standard CopyOption|Copy Option|COPY_ATTRIBUTES|Copy existing attributes to new file.|
|Standard CopyOption|Copy Option|REPLACE_EXISTING|Overwrite file if it already exists.|
|Standard OpenOption|Open Option|APPEND|If file is already open for write, then append to the end.|
|Standard OpenOption|Open Option|CREATE|Create a new file if it does not exist.|
|Standard OpenOption|Open Option|CREATE_NEW|Create a new file only if it does not exist, fail otherwise.|
|Standard OpenOption|Open Option|READ|Open for read access.|
|Standard OpenOption|Open Option|TRUNCATE_EXISTING|If file is already open for write, then erase file and append to beginning.|
|Standard OpenOption|Open Option|WRITE|Open for write access.|
|FileVisitOption|N/A|FOLLOW_LINK|Follow symbolic links.|

```
Path path = Paths.get("schedule.xml");
boolean exists = Files.exists(path, LinkOption.NOFOLLOW_LINKS);
```

The Files.exists() simply checks whether a file exists. If the parameter is a symbolic link, though, then the method checks whether the target of the symbolic link exists instead. Providing LinkOption.NOFOLLOW_LINKS means the default behavior will be overridden, and the method will check whether the symbolic link itself exists.

some methods accept a variety of enums types. For example, the Files.move() method takes a CopyOption vararg so it can take enums of different types.

```
void copy(Path source, Path target) throws IOException {
   Files.move(source, target,
    LinkOption.NOFOLLOW_LINKS,
    StandardCopyOption.ATOMIC_MOVE);
}
```

Many of the NIO.2 methods use a varargs for passing options, even when there is only one enum value available. The advantage of this approach, as opposed to say just passing a boolean argument, is future‐proofing. These method signatures are insulated from changes in the Java language down the road when future options are available.

### Handling Methods That Declare IOException

- Loss of communication to underlying file system.
- File or directory exists but cannot be accessed or modified.
- File exists but cannot be overwritten.
- File or directory is required but does not exist.

In general, methods that operate on abstract Path values, such as those in the Path interface or Paths class, often do not throw any checked exceptions. On the other hand, methods that operate or change files and directories, such as those in the Files class, often declare IOException.
There are exceptions to this rule, as we will see. For example, the method Files.exists() does not declare IOException. If it did throw an exception when the file did not exist, then it would never be able to return false!

## Interacting with Paths

Just like String values, Path instances are immutable. In the following example, the Path operation on the second line is lost since p is immutable:

```
Path p = Path.of("whale");
p.resolve("krill");
System.out.println(p);  // whale (!)

// chaining
Path.of("/zoo/../home").getParent().normalize().toAbsolutePath();
```

## VIEWING THE PATH WITH TOSTRING(), GETNAMECOUNT(), AND GETNAME()

```
public String toString()
public int getNameCount()
public Path getName(int index)
```

The first method, toString(), returns a String representation of the entire path. In fact, it is the only method in the Path interface to return a String. Many of the other methods in the Path interface return Path instances.

The getNameCount() and getName() methods are often used in conjunction to retrieve the number of elements in the path and a reference to each element, respectively. These two methods do not include the root directory as part of the path.

```
Path path = Paths.get("/land/hippo/harry.happy");
System.out.println("The Path Name is: " + path);
for(int i=0; i<path.getNameCount(); i++) {
    System.out.println(" Element " + i + " is: " + path.getName(i));
}

The Path Name is: /land/hippo/harry.happy
   Element 0 is: land
   Element 1 is: hippo
   Element 2 is: harry.happy
```

Even though this is an absolute path, the root element is not included in the list of names. As we said, these methods do not consider the root as part of the path.

```
var p = Path.of("/");
System.out.print(p.getNameCount()); // 0
System.out.print(p.getName(0)); // IllegalArgumentException
```

### CREATING A NRE PATH WITH SUBPATH()

The references are inclusive of the beginIndex, and exclusive of the endIndex. The subpath() method is similar to the previous getName() method, except that subpath() may return multiple path components, whereas getName() returns only one. Both return Path instances, though.

```
public Path subpath(int beginIndex, int endIndex)


var p = Paths.get("/mammal/omnivore/raccoon.image");
System.out.println("Path is: " + p);
for (int i = 0; i < p.getNameCount(); i++) {
    System.out.println(" Element " + i + " is: " + p.getName(i));
}
System.out.println();
System.out.println("subpath(0,3): " + p.subpath(0, 3));
System.out.println("subpath(1,2): " + p.subpath(1, 2));
System.out.println("subpath(1,3): " + p.subpath(1, 3));

Path is: /mammal/omnivore/raccoon.image
   Element 0 is: mammal
   Element 1 is: omnivore
   Element 2 is: raccoon.image
subpath(0,3): mammal/omnivore/raccoon.image
subpath(1,2): omnivore
subpath(1,3): omnivore/raccoon.image
```

Like getNameCount() and getName(), subpath() is 0‐indexed and does not include the root. Also like getName(), subpath() throws an exception if invalid indices are provided.

```
var q = p.subpath(0, 4); // IllegalArgumentException
var x = p.subpath(1, 1); // IllegalArgumentException
```

The first example throws an exception at runtime, since the maximum index value allowed is 3. The second example throws an exception since the start and end indexes are the same, leading to an empty path value.

## ACCESSING PATH ELEMENTS WITH GETFILENAME(), GETPARENT(), AND GETROOT()

The getFileName() returns the Path element of the current file or directory, while getParent() returns the full path of the containing directory. The getParent() returns null if operated on the root path or at the top of a relative path. The getRoot() method returns the root element of the file within the file system, or null if the path is a relative path.

```
public void printPathInformation(Path path) {
    System.out.println("Filename is: " + path.getFileName());
    System.out.println(" Root is: " + path.getRoot());
    Path currentParent = path;
    while((currentParent = currentParent.getParent()) != null)
    {
      System.out.println("   Current parent is: " + currentParent);
    }
}

printPathInformation(Path.of("zoo"));
printPathInformation(Path.of("/zoo/armadillo/shells.txt"));
printPathInformation(Path.of("./armadillo/../shells.txt"));


Filename is: zoo
   Root is: null
Filename is: shells.txt
   Root is: /
   Current parent is: /zoo/armadillo
   Current parent is: /zoo
   Current parent is: /
Filename is: shells.txt
   Root is: null
   Current parent is: ./armadillo/..
   Current parent is: ./armadillo
   Current parent is: .
```

The while loop in the printPathInformation() method continues until getParent() returns null.

## CHECKING PATH TYPE WITH ISABSOLUTE() AND TOABSOLUTEPATH()

The first method, isAbsolute(), returns true if the path the object references is absolute and false if the path the object references is relative. As discussed earlier in this chapter, whether a path is absolute or relative is often file system–dependent, although we, like the exam writers, adopt common conventions for simplicity throughout the book.
The second method, toAbsolutePath(), converts a relative Path object to an absolute Path object by joining it to the current working directory. If the Path object is already absolute, then the method just returns the Path object.

```
var path1 = Paths.get("C:\\birds\\egret.txt");
System.out.println("Path1 is Absolute? " + path1.isAbsolute());
System.out.println("Absolute Path1: " + path1.toAbsolutePath());
var path2 = Paths.get("birds/condor.txt");
System.out.println("Path2 is Absolute? " + path2.isAbsolute());
System.out.println("Absolute Path2 " + path2.toAbsolutePath());

Path1 is Absolute? true
Absolute Path1: C:\birds\egret.txt
Path2 is Absolute? false
Absolute Path2 /home/work/birds/condor.txt

```

## JOINING PATHS WITH RESOLVE()

```
public Path resolve(Path other)
public Path resolve(String other)

Path path1 = Path.of("/cats/../panther");
Path path2 = Path.of("food");
System.out.println(path1.resolve(path2));
/cats/../panther/food

Path path3 = Path.of("/turkey/food");
System.out.println(path3.resolve("/tiger/cage"));
// Since the input parameter path3 is an absolute path, the output would be the following:
/tiget/cage
```

If an absolute path is provided as input to the method, then that is the value that is returned. Simply put, you cannot combine two absolute paths using resolve(). when you see Files.resolve(), think concatenation.

## DERIVING A PATH WITH RELATIVIZE()

The Path interface includes a method for constructing the relative path from one Path to another, often using path symbols.

```
var path1 = Path.of("fish.txt");
var path2 = Path.of("friendly/birds.txt");
System.out.println(path1.relativize(path2));
System.out.println(path2.relativize(path1));

../friendly/birds.txt
../../fish.txt

```

The idea is this: if you are pointed at a path in the file system, what steps would you need to take to reach the other path? For example, to get to fish.txt **from** friendly/birds.txt, you need to go up two levels (the file itself counts as one level) and then select fish.txt.

If both path values are relative, then the relativize() method computes the paths as if they are in the same current working directory.

Remember, most methods defined in the Path interface do not require the path to exist.

The relativize() method requires that both paths are absolute or both relative and throws an exception if the types are mixed.

```
Path path1 = Paths.get("/primate/chimpanzee");
Path path2 = Paths.get("bananas.txt");
path1.relativize(path2); // IllegalArgumentException
```

## CLEANING UP A PATH WITH NORMALIZE()

So far, we've presented a number of examples that included path symbols that were unnecessary. Luckily, Java provides a method to eliminate unnecessary redundancies in a path

```
var p1 = Path.of("./armadillo/../shells.txt"); System.out.println(p1.normalize()); // shells.txt
var p2 = Path.of("/cats/../panther/food"); System.out.println(p2.normalize()); // /panther/food
var p3 = Path.of("../../fish.txt"); System.out.println(p3.normalize()); // ../../fish.txt


var p1 = Paths.get("/pony/../weather.txt");
var p2 = Paths.get("/weather.txt");
System.out.println(p1.equals(p2)); // false
System.out.println(p1.normalize().equals(p2.normalize())); // true
```

he equals() method returns true if two paths represent the same value. In the first comparison, the path values are different. In the second comparison, the path values have both been reduced to the same normalized value, /weather.txt. This is the primary function of the normalize() method, to allow us to better compare different paths.

## RETRIEVING THE FILE SYSTEM PATH WITH TOREALPATH()

This method is similar to normalize(), in that it eliminates any redundant path symbols. It is also similar to toAbsolutePath(), in that it will join the path with the current working directory if the path is relative.

Unlike those two methods, though, toRealPath() will throw an exception if the path does not exist. In addition, it will follow symbolic links, with an optional varargs parameter to ignore them.

```
System.out.println(Paths.get("/zebra/food.txt").toRealPath());
System.out.println(Paths.get(".././food.txt").toRealPath());

/horse/food.txt

```

## REVIEWING PATH METHODS

| Path methods               | Path methods                   |
| -------------------------- | ------------------------------ |
| Path of(String, String...) | Path getParent()               |
| URI toURI()                | Path getRoot()                 |
| File toFile()              | boolean isAbsolute()           |
| String toString()          | Path toAbsolutePath()          |
| int getNameCount()         | Path relativize()              |
| Path getName(int)          | Path resolve(Path)             |
| Path subpath(int, int)     | Path normalize()               |
| Path getFileName()         | Path toRealPath(LinkOption...) |

## Operating on Files and Directories

Most of the methods we covered in the Path interface operate on theoretical paths, which are not required to exist within the file system. What if you want to rename a directory, copy a file, or read the contents of a file?
Enter the NIO.2 Files class. The Files helper class is capable of interacting with real files and directories within the system. Because of this, most of the methods in this part of the chapter take optional parameters and throw an IOException if the path does not exist. The Files class also replicates numerous methods found in the java.io.File, albeit often with a different name or list of parameters.

### CHECKING FOR EXISTENCE WITH EXISTS()

The first Files method we present is the simplest. It just checks whether the file exists.
This method does not throw an exception if the file does not exist, as doing so would prevent this method from ever returning false at runtime.

```
public static boolean exists(Path path, LinkOption... options)

var b1 = Files.exists(Paths.get("/ostrich/feathers.png"));
System.out.println("Path " + (b1 ? "Exists" : "Missing"));

var b2 = Files.exists(Paths.get("/ostrich"));
System.out.println("Path " + (b2 ? "Exists" : "Missing"));
```

### TESTING UNIQUENESS WITH ISSAMEFILE()

Since a path may include path symbols and symbolic links within a file system, it can be difficult to know if two Path instances refer to the same file.

The method takes two Path objects as input, resolves all path symbols, and follows symbolic links. Despite the name, the method can also be used to determine whether two Path objects refer to the same directory.
While most usages of isSameFile() will trigger an exception if the paths do not exist, there is a special case in which it does not. If the two path objects are equal, in terms of equals(), then the method will just return true without checking whether the file exists.

```
public static boolean isSameFile(Path path, Path path2) throws IOException


```

This isSameFile() method does not compare the contents of the files. Two files may have identical names, content, and attributes, but if they are in different locations, then this method will return false.

### MAKING DIRECTORIES WITH CREATEDIRECTORY() AND CREATEDIRECTORIES()

The createDirectory() will create a directory and throw an exception if it already exists or the paths leading up to the directory do not exist.
The createDirectories() works just like the java.io.File method mkdirs(), in that it creates the target directory along with any nonexistent parent directories leading up to the path. 
If all of the directories already exist, createDirectories() will simply complete without doing anything. This is useful in situations where you want to ensure a directory exists and create it if it does not.

Both of these methods also accept an optional list of `FileAttribute<?>` values to apply to the newly created directory or directories. We will discuss file attributes more later in the chapter.

```
Files.createDirectory(Path.of("/bison/field"));
Files.createDirectories(Path.of("/bison/field/pasture/green"));
```

The first example creates a new directory, field, in the directory /bison, assuming /bison exists; or else an exception is thrown. Contrast this with the second example, which creates the directory green along with any of the following parent directories if they do not already exist, including bison, field, and pasture.

## COPYING FILES WITH COPY()

The method copies a file or directory from one location to another using Path objects. The following shows an example of copying a file and a directory:

```
Files.copy(Paths.get("/panda/bamboo.txt"), Paths.get("/panda-save/bamboo.txt"));
Files.copy(Paths.get("/turtle"), Paths.get("/turtleCopy"));
```

When directories are copied, the copy is **shallow**. A **shallow copy** means that the files and subdirectories within the directory are not copied. A **deep copy** means that the entire tree is copied, including all of its content and subdirectories.

### Copying and Replacing Files

By default, if the target already exists, the copy() method will **throw an exception**. You can change this behavior by providing the StandardCopyOption enum value REPLACE_EXISTING to the method. The following method call will overwrite the movie.txt file if it already exists:

```
Files.copy(Paths.get("book.txt"), Paths.get("movie.txt"), StandardCopyOption.REPLACE_EXISTING);
```

### Copying Files with I/O Streams

The first method reads the contents of a stream and writes the output to a file. The second method reads the contents of a file and writes the output to a stream. They are quite convenient if you need to quickly read/write data from/to disk.

```
public static long copy(InputStream in, Path target, CopyOption... options) throws IOException
public static long copy(Path source, OutputStream out) throws IOException

try (var is = new FileInputStream("source-data.txt")) { // Write stream data to a file
    Files.copy(is, Paths.get("/mammals/wolf.txt"));
}
Files.copy(Paths.get("/fish/clown.xsl"), System.out);
```

While we used FileInputStream in the first example, the streams could have been any valid I/O stream including website connections, in‐memory stream resources, and so forth. The second example prints the contents of a file directly to the System.out stream.

### Copying Files into a Directory

For the exam, it is important that you understand how the copy() method operates on both files and directories. For example, let's say we have a file, food.txt, and a directory, /enclosure. Both the file and directory exist.

```
var file = Paths.get("food.txt");
var directory = Paths.get("/enclosure");
Files.copy(file, directory);
```

If you said it would create a new file at /enclosure/food.txt, then you're way off!!! It actually throws an exception. The command tries to create a new file, named /enclosure. Since the path /enclosure already exists, an exception is thrown at runtime.

On the other hand, if the directory did not exist, then it would create a new file with the contents of food.txt, but it would be called
/enclosure. Remember, we said files may not need to have extensions, and in this example, it matters.

This behavior applies to both the copy() and the move() methods, the latter of which we will be covering next.

correct:

```
var file = Paths.get("food.txt");
var directory = Paths.get("/enclosure/food.txt");
Files.copy(file, directory);

// or
var directory = Paths.get("/enclosure").resolve(file.getFileName());
```

## MOVING OR RENAMING PATHS WITH MOVE()

```
Files.move(Path.of("c:\\zoo"), Path.of("c:\\zoo-new"));
Files.move(Path.of("c:\\user\\addresses.txt"), Path.of("c:\\zoo-new\\addresses2.txt"));
```

The first example renames the zoo directory to a zoo‐new directory, keeping all of the original contents from the source directory. The second example moves the addresses.txt file from the directory user to the directory zoo‐new, and it renames it to addresses2.txt.

### Similarities between move() and copy()

Like copy(), move() requires REPLACE_EXISTING to overwrite the target if it exists, else it will throw an exception. Also like copy(), move() will not put a file in a directory if the source is a file and the target is a directory. Instead, it will create a new file with the name of the directory.

### Performing an Atomic Move

Another enum value that you need to know for the exam when working with the move() method is the StandardCopyOption value ATOMIC_MOVE.

```
Files.move(Path.of("mouse.txt"), Path.of("gerbil.txt"), StandardCopyOption.ATOMIC_MOVE);
```

You may remember the atomic property from Chapter 18, “Concurrency,” and the principle of an atomic move is similar. An atomic move is one in which a file is moved within the file system as a single indivisible operation. Put another way, any process monitoring the file system never sees an incomplete or partially written file. If the file system does not support this feature, an AtomicMoveNotSupportedException will be thrown.

Note that while ATOMIC_MOVE is available as a member of the StandardCopyOption type, it will likely throw an exception if passed to a copy() method.

## DELETING A FILE WITH DELETE() AND DELETEIFEXISTS()

The Files class includes two methods that delete a file or empty directory within the file system.

To delete a directory, it must be **empty**. Both of these methods throw an exception if operated on a nonempty directory. In addition, **if the path is a symbolic link, then the symbolic link will be deleted**, not the path that the symbolic link points to.

The methods differ on how they handle a path that does not exist. The delete() method throws an exception if the path does not exist, while the deleteIfExists() method returns true if the delete was successful, and false otherwise. Similar to createDirectories(), deleteIfExists() is useful in situations where you want to ensure a path does not exist, and delete it if it does.

## READING AND WRITING DATA WITH NEWBUFFEREDREADER() AND NEWBUFFEREDWRITER()

NIO.2 includes two convenient methods for working with I/O streams.

```
public static BufferedReader newBufferedReader(Path path) throws IOException
public static BufferedWriter newBufferedWriter(Path path, OpenOption... options) throws IOException
```

There are overloaded versions of these methods that take a Charset.
You can wrap I/O stream constructors to produce the same effect, although it's a lot easier to use the factory method.

```
var path = Path.of("/animals/gopher.txt");
try (var reader = Files.newBufferedReader(path)) {
   String currentLine = null;
   while((currentLine = reader.readLine()) != null)
    System.out.println(currentLine);
}

```

This example reads the lines of the files using a BufferedReader and outputs the contents to the screen.

```
var list = new ArrayList<String>();
list.add("Smokey");
list.add("Yogi");
var path = Path.of("/animals/bear.txt");
try (var writer = Files.newBufferedWriter(path)) {
   for(var line : list) {
      writer.write(line);
      writer.newLine();
   }
}
```

This code snippet creates a new file with two lines of text in it. Did you notice that both of these methods use buffered streams rather than low‐ level file streams?

## READING A FILE WITH READALLLINES()

The Files class includes a convenient method for turning the lines of a
file into a List.
The following sample code reads the lines of the file and outputs them to the user:

```
var path = Path.of("/animals/gopher.txt");
final List<String> lines = Files.readAllLines(path);
lines.forEach(System.out::println);

```

Be aware that the entire file is read when readAllLines() is called, with the resulting List<String> storing all of the contents of the file in memory at once. If the file is significantly large, then you may trigger an OutOfMemoryError trying to load all of it into memory.

| Files Methods                                     | Files Methods                                          |
| ------------------------------------------------- | ------------------------------------------------------ |
| boolean exists(Path, LinkOption...)               | Path move(Path, Path, CopyOption...)                   |
| boolean isSameFile(Path,Path)                     | void delete(Path)                                      |
| Path createDirectory(Path, FileAttribute<?>...)   | boolean deleteIfExists(Path)                           |
| Path createDirectories(Path, FileAttribute<?>...) | BufferedReader newBufferedReader(Path)                 |
| Path copy(Path, Path, CopyOption...)              | BufferedWriter newBufferedWriter( Path, OpenOption...) |
| long copy(InputStream,Path, CopyOption...)        | List<String>readAllLines(Path)                         |
| long copy(Path,OutputStream)                      |                                                        |

## Managing File Attributes

The Files class also provides numerous methods for accessing file and directory metadata, referred to as file attributes. A file attribute is data about a file within the system, such as its size and visibility, that is not part of the file contents.

## Reading Common Attributes with isDirectory(), isSymbolicLink(), and isRegularFile()

The Files class includes three methods for determining type of a Path.

```
public static boolean isDirectory(Path path, LinkOption... options)
public static boolean isSymbolicLink(Path path)
public static boolean isRegularFile(Path path, LinkOption... options)
```

The isDirectory() and isSymbolicLink() methods should be self‐ explanatory, although isRegularFile() warrants some discussion. Java defines a regular file as one that can contain content, as opposed to a symbolic link, directory, resource, or other nonregular file that may be present in some operating systems. If the symbolic link points to an actual file, Java will perform the check on the target of the symbolic
link. In other words, it is possible for isRegularFile() to return true for a symbolic link, as long as the link resolves to a regular file.

```
System.out.print(Files.isDirectory(Paths.get("/canine/fur.jpg" )));
System.out.print(Files.isSymbolicLink(Paths.get("/canine/coyote")));
System.out.print(Files.isRegularFile(Paths.get("/canine/types.txt")));
```

The first example prints true if fur.jpg is a directory or a symbolic link to a directory and false otherwise. The second example prints true if /canine/coyote is a symbolic link, regardless of whether the file or directory it points to exists. The third example prints true if types.txt points to a regular file or alternatively a symbolic link that points to a regular file.

While most methods in the Files class declare IOException, these three methods do not. They return false if the path does not exist.

## Checking File Accessibility with isHidden(), isReadable(), isWritable(), and isExecutable()

In many file systems, it is possible to set a boolean attribute to a file that marks it hidden, readable, or executable. The Files class includes methods that expose this information.

```
public static boolean isHidden(Path path) throws IOException public static boolean isReadable(Path path)
public static boolean isWritable(Path path)
public static boolean isExecutable(Path path)
```

A hidden file can't normally be viewed when listing the contents of a directory. The readable, writable, and executable flags are important in file systems where the filename can be viewed, but the user may not have permission to open the file's contents, modify the file, or run the file as a program, respectively.

```
System.out.print(Files.isHidden(Paths.get("/walrus.txt")));
System.out.print(Files.isReadable(Paths.get("/seal/baby.png")) );
System.out.print(Files.isWritable(Paths.get("dolphin.txt")));
System.out.print(Files.isExecutable(Paths.get("whale.png")));
```

If the walrus.txt exists and is hidden within the file system, then the first example prints true. The second example prints true if the baby.png file exists and its contents are readable. The third example prints true if the dolphin.txt file is able to be modified. Finally, the last example prints true if the file is able to be executed within the operating system. Note that the file extension does not necessarily determine whether a file is executable. For example, an image file that ends in .png could be marked executable in some file systems.
With the exception of isHidden(), these methods do not declare any checked exceptions and return false if the file does not exist.

## Reading File Size with size()

The Files class includes a method to determine the size of the file in
bytes.

```
public static long size(Path path) throws IOException
```

The size returned by this method represents the conceptual size of the data, and this may differ from the actual size on the persistent storage device.

The Files.size() method is defined only on files. Calling Files.size() on a directory is undefined, and the result depends on the file system. If you need to determine the size of a directory and its contents, you'll need to walk the directory tree.

## Checking for File Changes with getLastModifiedTime()

Most operating systems support tracking a last‐modified date/time value with each file. Some applications use this to determine when the file's contents should be read again. In the majority of circumstances, it is a lot faster to check a single file metadata attribute than to reload the entire contents of the file.
The Files class provides the following method to retrieve the last time a file was modified:

```
public static FileTime getLastModifiedTime(Path path, LinkOption... options) throws IOException
```

The method returns a FileTime object, which represents a timestamp. For convenience, it has a toMillis() method that returns the epoch time, which is the number of milliseconds since 12 a.m. UTC on January 1, 1970.
The following shows how to print the last modified value for a file as an epoch value:

```
final Path path = Paths.get("/rabbit/food.jpg");
System.out.println(Files.getLastModifiedTime(path).toMillis());
```

## IMPROVING ATTRIBUTE ACCESS

Up until now, we have been accessing individual file attributes with multiple method calls. While this is functionally correct, there is often a cost each time one of these methods is called. Put simply, it is far more efficient to ask the file system for all of the attributes at once rather than performing multiple round‐trips to the file system. Furthermore, some attributes are file system–specific and cannot be easily generalized for all file systems.

NIO.2 addresses both of these concerns by allowing you to construct views for various file systems with a single method call. A view is a group of related attributes for a particular file system type. That's not to say that the earlier attribute methods that we just finished discussing do not have their uses. If you need to read only one attribute of a file or directory, then requesting a view is unnecessary.

## Understanding Attribute and View Types

NIO.2 includes two methods for working with attributes in a single method call: a read‐only attributes method and an updatable view method. For each method, you need to provide a file system type object, which tells the NIO.2 method which type of view you are requesting. By updatable view, we mean that we can both read and write attributes with the same object.

## Retrieving Attributes with readAttributes()

The Files class includes the following method to read attributes of a class in a read‐only capacity:

```
public static <A extends BasicFileAttributes> A readAttributes(Path path,Class<A> type,LinkOption... options) throws IOException
```

Applying it requires specifying the Path and BasicFileAttributes.class parameters.

```
var path = Paths.get("/turtles/sea.txt");
BasicFileAttributes data = Files.readAttributes(path,BasicFileAttributes.class);


System.out.println("Is a directory? " + data.isDirectory());
System.out.println("Is a regular file? " +
data.isRegularFile());
System.out.println("Is a symbolic link? " +
data.isSymbolicLink());
System.out.println("Size (in bytes): " + data.size());
System.out.println("Last modified: " +
data.lastModifiedTime());
```

The BasicFileAttributes class includes many values with the same name as the attribute methods in the Files class. The advantage of using this method, though, is that all of the attributes are retrieved at once.

## Modifying Attributes with getFileAttributeView()

The following Files method returns an updatable view:

```
public static <V extends FileAttributeView> V
getFileAttributeView(
   Path path,
Class<V> type, LinkOption... options)
```

We can use the updatable view to increment a file's last modified date/time value by 10,000 milliseconds, or 10 seconds.

```
// Read file attributes
var path = Paths.get("/turtles/sea.txt"); BasicFileAttributeView view = Files.getFileAttributeView(path,
   BasicFileAttributeView.class);
BasicFileAttributes attributes = view.readAttributes();
// Modify file last modified time
FileTime lastModifiedTime = FileTime.fromMillis(
attributes.lastModifiedTime().toMillis() + 10_000); view.setTimes(lastModifiedTime, null, null);
```

After the updatable view is retrieved, we need to call readAttributes() on the view to obtain the file metadata. From there, we create a new FileTime value and set it using the setTimes() method.

```
// BasicFileAttributeView instance method public void setTimes(FileTime lastModifiedTime,
   FileTime lastAccessTime, FileTime createTime)

```

This method allows us to pass null for any date/time value that we do not want to modify. In our sample code, only the last modified date/time is changed.

Not all file attributes can be modified with a view. For example, you cannot set a property that changes a file into a directory. Likewise, you cannot change the size of the object without modifying its contents.

# Applying Functional Programming

## LISTING DIRECTORY CONTENTS

Let's start with a simple Stream API method. The following Files method lists the contents of a directory:

```
public static Stream<Path> list(Path dir) throws IOException
```

The Files.list() is similar to the java.io.File method listFiles(), except that it returns a Stream<Path> rather than a File[]. Since streams use lazy evaluation, this means the method will load each path element as needed, rather than the entire directory at once.

Printing the contents of a directory is easy.

```
try (Stream<Path> s = Files.list(Path.of("/home"))) { s.forEach(System.out::println);}
```

Let's do something more interesting, though. Earlier, we presented the Files.copy() method and showed that it only performed a shallow copy of a directory. We can use the Files.list() to perform a deep copy.

```
public void copyPath(Path source, Path target) {
   try {
      Files.copy(source, target);
      if(Files.isDirectory(source))
try (Stream<Path> s = Files.list(source)) { s.forEach(p -> copyPath(p,
               target.resolve(p.getFileName())));
         }
   } catch(IOException e) {
      // Handle exception
   }
}
```

The method first copies the path, whether it be a file or a directory. If it is a directory, then only a shallow copy is performed. Next, it checks whether the path is a directory and, if it is, performs a recursive copy of each of its elements. What if the method comes across a symbolic link? Don't worry, we'll address that topic in the next section. For now, you just need to know the JVM will not follow symbolic links when using this stream method.

### CLOSING THE STREAM

Did you notice that in the last two code samples, we put our Stream objects inside a try‐with‐resources method? The NIO.2 stream‐based methods open a connection to the file system that must be properly closed, else a resource leak could ensue. A resource leak within the file system means the path may be locked from modification long after the process that used it completed.
If you assumed a stream's terminal operation would automatically close the underlying file resources, you'd be wrong. There was a lot of debate about this behavior when it was first presented, but in short, requiring developers to close the stream won out.
On the plus side, not all streams need to be closed, only those that open resources, like the ones found in NIO.2. For instance, you didn't need to close any of the streams you worked with in Chapter 15.
Finally, the exam doesn't always properly close NIO.2 resources. To match the exam, we will sometimes skip closing NIO.2 resources in review and practice questions. Please, in your own code, always use try‐with‐resources statements with these NIO.2 methods.

## TRAVERSING A DIRECTORY TREE

Traversing a directory, also referred to as walking a directory tree, is the process by which you start with a parent directory and iterate over all of its descendants until some condition is met or there are no more elements over which to iterate.

### DON'T USE DIRECTORYSTREAM AND FILEVISITOR

While browsing the NIO.2 Javadocs, you may come across methods that use the DirectoryStream and FileVisitor classes to traverse a directory. These methods predate the existence of the Streams API and were even required knowledge for older Java certification exams. Even worse, despite its name, DirectoryStream is not a Stream API class.
The best advice we can give you is to not use them. The newer Stream API–based methods are superior and accomplish the same thing often with much less code.

## Selecting a Search Strategy

There are two common strategies associated with walking a directory tree: a depth‐first search and a breadth‐first search. A depth‐first search traverses the structure from the root to an arbitrary leaf and then navigates back up toward the root, traversing fully down any paths it skipped along the way. The search depth is the distance from the root to current node. To prevent endless searching, Java includes a search depth that is used to limit how many levels (or hops) from the root the search is allowed to go.
Alternatively, a breadth‐first search starts at the root and processes all elements of each particular depth, before proceeding to the next depth level. The results are ordered by depth, with all nodes at depth 1 read before all nodes at depth 2, and so on. While a breadth‐first tends to be balanced and predictable, it also requires more memory since a list of visited nodes must be maintained.

you just need to be aware that the NIO.2 Streams API methods use depth‐first searching with a depth limit, which can be optionally changed.

## Walking a Directory with walk()

That's enough background information; let's get to more Steam API methods. The Files class includes two methods for walking the directory tree using a depth‐first search.

```
public static Stream<Path> walk(Path start, FileVisitOption... options) throws IOException
public static Stream<Path> walk(Path start, int maxDepth, FileVisitOption... options) throws IOException
```

Like our other stream methods, walk() uses lazy evaluation and evaluates a Path only as it gets to it. This means that even if the directory tree includes hundreds or thousands of files, the memory required to process a directory tree is low. The first walk() method relies on a default maximum depth of Integer.MAX_VALUE, while the overloaded version allows the user to set a maximum depth. This is useful in cases where the file system might be large and we know the information we are looking for is near the root.

Java uses an int for its maximum depth rather than a long because most file systems do not support path values deeper than what can be stored in an int. In other words, using Integer.MAX_VALUE is effectively like using an infinite value, since you would be hard‐ pressed to find a stable file system where this limit is exceeded.

Rather than just printing the contents of a directory tree, we can again do something more interesting. The following getPathSize() method walks a directory tree and returns the total size of all the files in the directory:

```
private long getSize(Path p) {
   try {
     return  Files.size(p);
   } catch (IOException e) {
      // Handle exception
   }
    return 0L;
}
public long getPathSize(Path source) throws IOException {
    try (var s = Files.walk(source)) {
      return s.parallel()
            .filter(p -> !Files.isDirectory(p))
            .mapToLong(this::getSize)
            .sum();
    }
}

var size = getPathSize(Path.of("/fox/data")); System.out.format("Total Size: %.2f megabytes", (size/1000000.0));
Total Directory Tree Size: 15.30 megabytes
```

The getSize() helper method is needed because Files.size() declares IOException, and we'd rather not put a try/ catch block inside a lambda expression.

## Applying a Depth Limit

Let's say our directory tree was quite deep, so we apply a depth limit by changing one line of code in our getPathSize() method.

```
try (var s = Files.walk(source, 5)) {
```

This new version checks for files only within 5 steps of the starting node. A depth value of 0 indicates the current path itself. Since the method calculates values only on files, you'd have to set a depth limit of at least 1 to get a nonzero result when this method is applied to a directory tree.

## Avoiding Circular Paths

Many of our earlier NIO.2 methods traverse symbolic links by default, with a NOFOLLOW_LINKS used to disable this behavior. The walk() method is different in that it does not follow symbolic links by default and requires the FOLLOW_LINKS option to be enabled. We can alter our getPathSize() method to enable following symbolic links by adding the FileVisitOption:

```
try (var s = Files.walk(source, FileVisitOption.FOLLOW_LINKS)) {
```

When traversing a directory tree, your program needs to be careful of symbolic links if enabled. For example, if our process comes across a symbolic link that points to the root directory of the file system, then every file in the system would be searched!

Worse yet, a symbolic link could lead to a cycle, in which a path is visited repeatedly. A cycle is an infinite circular dependency in which an entry in a directory tree points to one of its ancestor directories.

Be aware that when the FOLLOW_LINKS option is used, the walk() method will track all of the paths it has visited, throwing a FileSystemLoopException if a path is visited twice.

## SEARCHING A DIRECTORY WITH FIND()

In the previous example, we applied a filter to the Stream<Path> object to
filter the results, although NIO.2 provides a more convenient method.

```
public static Stream<Path> find(Path start,int maxDepth, BiPredicate<Path,BasicFileAttributes> matcher, FileVisitOption... options) throws IOException
```

The find() method behaves in a similar manner as the walk() method, except that it takes a BiPredicate to filter the data. It also requires a depth limit be set. Like walk(), find() also supports the FOLLOW_LINK option.

## READING A FILE WITH LINES()

Earlier in the chapter, we presented Files.readAllLines() and commented that using it to read a very large file could result in an OutOfMemoryError problem. Luckily, NIO.2 solves this problem with a Stream API method.

```
public static Stream<String> lines(Path path) throws IOException
```

The contents of the file are read and processed lazily, which means that only a small portion of the file is stored in memory at any given time.

```
Path path = Paths.get("/fish/sharks.log"); try (var s = Files.lines(path)) {
   s.forEach(System.out::println);
}
```

Taking things one step further, we can leverage other stream methods for a more powerful example.

```
Path path = Paths.get("/fish/sharks.log"); try (var s = Files.lines(path)) {
   s.filter(f -> f.startsWith("WARN:"))
      .map(f -> f.substring(5))
      .forEach(System.out::println);
}
This sample code searches a log for lines that start with WARN:, outputting the text that follows. Assuming that the input file sharks.log is as follows:

INFO:Server starting
DEBUG:Processes available = 10
WARN:No database could be detected
DEBUG:Processes available reset to 0
WARN:Performing manual recovery
INFO:Server successfully started

=>
No database could be detected
Performing manual recovery
```

## FILES.READALLLINES() VS. FILES.LINES()

For the exam, you need to know the difference between readAllLines() and lines(). Both of these examples compile and run:

```
Files.readAllLines(Paths.get("birds.txt")).forEach(System .out::println);
Files.lines(Paths.get("birds.txt")).forEach(System.out::p rintln);
```

The first line reads the entire file into memory and performs a print operation on the result, while the second line lazily processes each line and prints it as it is read. The advantage of the second code snippet is that it does not require the entire file to be stored in memory at any time.

You should also be aware of when they are mixing incompatible types on the exam. Do you see why the following does not compile?

```
Files.readAllLines(Paths.get("birds.txt"))
   .filter(s -> s.length()> 2)
   .forEach(System.out::println);
```

The readAllLines() method returns a List, not a Stream, so the filter() method is not available.

| Legacy I/O File method   | NIO.2 method                    |
| ------------------------ | ------------------------------- |
| file.delete()            | Files.delete(path)              |
| file.exists()            | Files.exists(path)              |
| file.getAbsolutePath()   | path.toAbsolutePath()           |
| file.getName()           | path.getFileName()              |
| file.getParent()         | path.getParent()                |
| file.isDirectory()       | Files.isDirectory(path)         |
| file.isFile()            | Files.isRegularFile(path)       |
| file.lastModified()      | Files.getLastModifiedTime(path) |
| file.length()            | Files.size(path)                |
| file.listFiles()         | Files.list(path)                |
| file.mkdir()             | Files.createDirectory(path)     |
| file.mkdirs()            | Files.createDirectories(path)   |
| file.renameTo(otherFile) | Files.move(path,otherPath)      |



[prev](http://hjh.devsnips.nl/ocp19)
[next](http://hjh.devsnips.nl/ocp20)