# OCP Chapter 17

_Status: Published_
_Created: 2024-07-30 16:53:57_
_Tags: ocp_

# Modular Applications

|Derivative |Description|
|-|-|
|exports <package>|Allows all modules to access the package|
|exports <package> to <module>|Allows a specific module to access the package|
|requires <module>|Indicates module is dependent on another module|
|requires transitive <module> |Indicates the module and that all modules that use this module are dependent on another module
|uses <interface >|Indicates that a module uses a service |
|provides <interface> with <class> |Indicates that a module provides an implementation of a service|

## Comparing types of Modules
- named modules
- automatic modules
- unnamed modules

### Named Modules
- contains modul-info.java file
- is in the root of the jar
- default name is mudule when not named

### Automatic Modules
- no module-info.java file
- alleen de jar
- property call Automatic-Module-Name in the MANIFEST>MF
- based on the filename of the jar file
- converts - to . als de jar name omgezet wordt


### Unnamed Modules
- net zoals een automatic
- alleen op de classpath ipv module path
- treated as old code and second class citizen



|Property| Named| Automatic| Unnamed|
|-|-|-|-|
|A ______ module contains a module‐info file?|Yes|No|Ignored if present|
|A ______ module exports which packages to other modules?|Those in the module‐info file |All packages|No packages|
|A ______ module is readable by other modules on the module path?|Yes|Yes|No|
|A ______ module is readable by other JARs on the classpath?|Yes|Yes|Yes|


## JDK Dependencies

- java.base
- java.desktop
- java.loggin
- java.sql
- java.xml

beginnen allemaal met java.


### jdeps
- `jdeps -s bla.jar` is *summary* mode.  
- `jdeps --jdk-internals asd.jar` details about the unsupported APIs
- `-jdk-internals === --jdk-internals` provide details about unsupported APIs



## Migrating an Application
Strategies to connect to the world of modules.
- determing the order
- exploring bottom Up migration strategy
- Top down strategy
- split up and migration migration

## Determing the order
-need to know how the packages and libraries are structured
- not allowed cyclic dependencies

## Bottom UP Migration Strategy
1. Pick the lowest‐level project that has not yet been migrated.(Remember the way we ordered them by dependencies in the previous section?)
2. Add a module‐info.java file to that project. Be sure to add any exports to expose any package used by higher‐level JAR files. Also, add a requires directive for any modules it depends on.
3. Move this newly migrated named module from the class path to the module path.
4. Ensure any projects that have not yet been migrated stay as unnamed modules on the classpath.
5. Repeat with the next‐lowest‐level project until you are done.

advantages:
- more easy than other migrations
- it encourage care in what is exposed
- when having control of every jar in the project

## Top-down Migration Strategy
1. Place all projects on the module path.
2. Pick the highest‐level project that has not yet been migrated.
3. Add a module‐info file to that project to convert the automatic module into a named module. Again, remember to add any exports or requires directives. You can use the automatic module name of other modules when writing the requires directive since most of the projects on the module path do not have names yet.
4. Repeat with the next‐lowest‐level project until you are done.


|Category |Bottom‐Up |Top‐Down|
|-|-|-|
|A project that depends on all others|Unnamed module on the classpath|Named module on the module path|
|A project that has no dependencies|Named module on the module path|Automatic module on the module path|



## Creating a Service

## Service Locator
- uses load()

## Invoking a Cosumer

## Adding a Service provider

## Merging Service Locator and Consumer

## Reviewing Services

|Artifact |Part of the service|Directives required in module‐info.java|
|-|-|-|
|Service provider interface|Yes|exports|
|Service provider|No|requires provides|
|Service locator|Yes|exports requires uses|
|Consumer|No|requires|


[prev](http://hjh.devsnips.nl/ocp16)
[next](http://hjh.devsnips.nl/ocp18)