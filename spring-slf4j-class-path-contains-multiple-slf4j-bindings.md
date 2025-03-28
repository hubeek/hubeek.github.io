# Spring SLF4J: Class path contains multiple SLF4J bindings.

_Status: Published_
_Created: 2021-01-14 16:20:22_

adding SLF4J
and get rid of the error

```
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-log4j2</artifactId>
</dependency>
```

results in error after building

```
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/Users/hjhubeek/.m2/repository/ch/qos/logback/logback-classic/1.2.3/logback-classic-1.2.3.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/Users/hjhubeek/.m2/repository/org/apache/logging/log4j/log4j-slf4j-impl/2.13.3/log4j-slf4j-impl-2.13.3.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [ch.qos.logback.classic.util.ContextSelectorStaticBinder]
```
something doubled up according to: Class path contains multiple SLF4J bindings.

mvn dependency:tree

or

the IntelliJ maven tab

will show

```
[INFO] +- org.springframework.boot:spring-boot-starter-log4j2:jar:2.4.1:compile
[INFO] |  +- org.apache.logging.log4j:log4j-slf4j-impl:jar:2.13.3:compile
[INFO] |  |  +- org.slf4j:slf4j-api:jar:1.7.30:compile
[INFO] |  |  \- org.apache.logging.log4j:log4j-api:jar:2.13.3:compile
[INFO] |  +- org.apache.logging.log4j:log4j-core:jar:2.13.3:compile
[INFO] |  +- org.apache.logging.log4j:log4j-jul:jar:2.13.3:compile
[INFO] |  \- org.slf4j:jul-to-slf4j:jar:1.7.30:compile
```

in the error message you find the hint for the solution.

SLF4J: Found binding in [jar:file:/Users/hjhubeek/.m2/repository/org/apache/logging/log4j/log4j-slf4j-impl/2.13.3/log4j-slf4j-impl-2.13.3.jar!/org/slf4j/impl/StaticLoggerBinder.class]

the groupId will be in there /org/apache/logging/log4j -> org.apache.logging.log4j

and artefact log4j-slf4j-impl -> log4j-slf4j-impl

will be solved:
```
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-log4j2</artifactId>
    <exclusions>
      <exclusion>
        <groupId>org.apache.logging.log4j</groupId>
          <artifactId>log4j-slf4j-impl</artifactId>
      </exclusion>
    </exclusions>
 </dependency>
```