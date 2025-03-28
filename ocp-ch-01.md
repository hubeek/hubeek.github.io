# OCP - CH 01

_Status: Unpublished_
_Created: 2023-03-12 08:17:24_
_Tags: ocp, java_

# Chapter 01 


javac compiles .java to .class files. java is the launcher program.  
javac generates bytecode.   
java -jar runs the jar files.  
java starts JVM. JVM runs bytecode.  
javadoc for generating documentation.  

java no jre anymore.  
jre subset to run only.  
jlink can generate a runnable programm for devs.  

java:  
- object oriented
- encapsulation
- platform independent
- robust
- simple
- secure
- multithreaded
- backward compatible

## classes 

object is an runtime object instance of a class in memory  
reference is a variable that points to the object  

methods  
fields  

methods + parameter = method signature

1 file 1 public class met de filename als className

write *.java file, compile javac *.java en run with: java ClassName
write Zoo.java , compile javac Zoo.java , run java Zoo
java -cp target/DirExplorer-1.0-SNAPSHOT.jar nl.appall.explorer.AppD
java -cp target/JAR_NAME.jar package_name.AppWithMain

standaard einde code 0

zonder static error: =>main is not static  
zonder public main: =>method not found  
zonder args: main method not found  
String[] args  
String options []  
String … options  
String… options  

bij ref naar args[1] en die is er niet => arrayIndexOutOfBoundsException  

java one liner hoeft geen javac : single-file-source-code  
alleen 1 file  
met alleen imports from jdk  






