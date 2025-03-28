# JUnit 5 CamelCase test func names.

_Status: Published_
_Created: 2023-03-28 14:41:52_

JUnit 5 CamelCase Replace with spaces for test methods.

```
@DisplayNameGeneration(ReplaceCamelCase.class)
class DemoUtilsTest {

    DemoUtils demoUtils;

    @BeforeAll
    static void setupBeforeAll() {
        System.out.println("before all");
    }

    @AfterAll
    static void tearDownAfterAll() {
        System.out.println("after all");
    }
    @BeforeEach
    void setUp() {
        System.out.println("setup each");
        demoUtils = new DemoUtils();
    }

    @AfterEach
    void tearDown() {
    }
}
```
## Replace Camel Case Class
```

import org.junit.jupiter.api.DisplayNameGenerator;

import java.lang.reflect.Method;

class ReplaceCamelCase extends DisplayNameGenerator.Standard {
    public ReplaceCamelCase() {
    }

    public String generateDisplayNameForClass(Class<?> testClass) {
        return this.replaceCapitals(super.generateDisplayNameForClass(testClass));
    }

    public String generateDisplayNameForNestedClass(Class<?> nestedClass) {
        return this.replaceCapitals(super.generateDisplayNameForNestedClass(nestedClass));
    }

    public String generateDisplayNameForMethod(Class<?> testClass, Method testMethod) {
        return this.replaceCapitals(testMethod.getName());
    }

    String replaceCapitals(String camelCase) {
        StringBuilder result = new StringBuilder();
        result.append(camelCase.charAt(0));
        for (int i=1; i<camelCase.length(); i++) {
            if (Character.isUpperCase(camelCase.charAt(i))) {
                result.append(' ');
                result.append(Character.toLowerCase(camelCase.charAt(i)));
            } else {
                result.append(camelCase.charAt(i));
            }
        }
        return result.toString();
    }
}
```
[Baeldung](https://www.baeldung.com/junit-custom-display-name-generator)