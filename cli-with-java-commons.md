# Cli with java commons

_Status: Published_
_Created: 2021-09-02 15:17:12_
_Tags: java, cli_

## pom.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>testffCli</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
    </properties>
    <dependencies>
        <dependency>
            <groupId>commons-cli</groupId>
            <artifactId>commons-cli</artifactId>
            <version>1.4</version>
        </dependency>
    </dependencies>
    <build>
        <finalName>Cli</finalName>
    </build>
</project>
```

## Cli.java  
```
import org.apache.commons.cli.*;
import java.io.PrintWriter;

public class Cli {
    private static final Option ARG_ADD = new Option("a", "addition", false, "Add numbers together.");
    private static final Option ARG_SUBTRACT = new Option("s", "subtract", false, "Subtracts numbers together.");
    private static final Option ARG_MULTIPLY = new Option("m", "multiply", false, "Multiply numbers together.");
    private static final Option ARG_DIVIDE = new Option("d", "divide", false, "Divide numbers together.");

    public static void printHelp(Options options) {
        HelpFormatter hf = new HelpFormatter();
        PrintWriter pw = new PrintWriter(System.out);
        pw.println("Math App " + Cli.class.getPackage().getImplementationVersion());
        pw.println();
        hf.printUsage(pw, 100, "java -jar Cli.jar [OPTIONS] Number Number");
        hf.printOptions(pw, 100, options, 2, 5);
        pw.close();
    }

    public static void main(String[] args) {

        CommandLineParser clp = new DefaultParser();
        Options options = new Options();
        options.addOption(ARG_ADD);
        options.addOption(ARG_SUBTRACT);
        options.addOption(ARG_MULTIPLY);
        options.addOption(ARG_DIVIDE);

        try {
            CommandLine cl = clp.parse(options, args);

            if (cl.getArgList().size() < 2) {
                printHelp(options);
                System.exit(-1);
            }

            var a = Integer.parseInt(cl.getArgList().get(0));
            var b = Integer.parseInt(cl.getArgList().get(1));

            if (cl.hasOption(ARG_ADD.getLongOpt())) {
                System.out.println(String.format("%1$d + %2$d = %3$d", a, b, (a + b)));
            } else if (cl.hasOption(ARG_SUBTRACT.getLongOpt())) {
                System.out.println(String.format("%1$d - %2$d = %3$d", a, b, (a - b)));
            } else if (cl.hasOption(ARG_MULTIPLY.getLongOpt())) {
                System.out.println(String.format("%1$d * %2$d = %3$d", a, b, (a * b)));
            } else if (cl.hasOption(ARG_DIVIDE.getLongOpt())) {
                System.out.println(String.format("%1$d / %2$d = %3$d", a, b, (a / b)));
            } else {
                printHelp(options);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }

    }
}
```