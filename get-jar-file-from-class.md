# Get Jar/File from class

_Status: Published_
_Created: 2023-05-14 04:15:09_

The Java reflection API provides information about the structure of classes, methods, fields, etc., but it does not provide direct access to the underlying JAR file or file name. 

However, you can still get the class file path or JAR file path from the class's ProtectionDomain and CodeSource using reflection. Here's an example: 

```java

import java.lang.reflect.CodeSource;
import java.lang.reflect.Method;
import java.security.ProtectionDomain;

public class ClassName {
    public static void main(String[] args) {
        Class<?> clazz = ClassName.class;
        
        ProtectionDomain protectionDomain = clazz.getProtectionDomain();
        CodeSource codeSource = protectionDomain.getCodeSource();
        
        if (codeSource != null) {
            String location = codeSource.getLocation().getPath();
            
            if (location.endsWith(".jar")) {
                String jarName = location.substring(location.lastIndexOf("/") + 1);
                System.out.println("JAR file name: " + jarName);
            } else {
                String className = clazz.getName().replace('.', '/') + ".class";
                String fileName = location.substring(0, location.length() - className.length());
                System.out.println("File name: " + fileName);
            }
        } else {
            System.out.println("Unable to determine file or JAR name.");
        }
    }
}
```