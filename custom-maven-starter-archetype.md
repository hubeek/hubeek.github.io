# Custom Maven Starter Archetype

_Status: Published_
_Created: 2024-04-26 04:44:06_
_Tags: java, maven, mvn, bash_

## Create Maven Archetype
- create an empty Maven project
```
mvn archetype:generate \
    -DgroupId=nl.appall.java \
    -DartifactId=java \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false

```
- modify the pom file with for example to add Junit5 and Java 11.
```
<properties>
    <maven.compiler.source>11</maven.compiler.source>
    <maven.compiler.target>11</maven.compiler.target>
</properties>

<dependencies>
    <!-- JUnit Jupiter API for writing tests -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.7.0</version>
        <scope>test</scope>
    </dependency>

    <!-- JUnit Jupiter Engine for running tests -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-engine</artifactId>
        <version>5.7.0</version>
        <scope>test</scope>
    </dependency>
</dependencies>

```
- Use the maven-archetype-plugin to create an archetype from your project:
```
mvn archetype:create-from-project
```
- Deploy the generated archetype to a repository (local or remote) so it can be reused:
```
mvn install
```
- create a Maven Settings file
```
mkdir -p ~/.m2
echo '<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
  <localRepository/>
  <interactiveMode/>
  <usePluginRegistry/>
  <offline/>
  <pluginGroups/>
  <servers/>
  <mirrors/>
  <proxies/>
  <profiles/>
  <activeProfiles/>
</settings>' > ~/.m2/settings.xml

```
use your archetype to generate a new project like:
```
mvn archetype:create-from-project
``` 
## In bashrc
To automate the creation of a new blank project with your custom archetype you can update your bashrc like ~/.zshrc
```
march() {
         if [ -z "$1" ]; then
             echo "Error: No project name provided."
             echo "Usage: march <projectname>"
            return 1
        fi
   
        mvn archetype:generate \
            -DarchetypeGroupId=nl.appall.java \
            -DarchetypeArtifactId=java-archetype \
            -DarchetypeVersion=1.0-SNAPSHOT \
            -DgroupId=nl.appall.newproject \
            -DartifactId=$1 \
            -Dversion=1.0-SNAPSHOT \
            -DinteractiveMode=false
   
        cd $1
        idea .
   }
```
now `march yourProject` creates the project , gets in the folder and starts intellij.