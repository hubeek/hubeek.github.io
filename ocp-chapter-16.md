# OCP Chapter 16

_Status: Published_
_Created: 2024-07-30 16:51:32_
_Tags: ocp_

# Reviewing Exceptions

## Handling Exceptions

```
        try {
            // protected code
        } catch (IOException e) {
            // handler
        } catch (ArithmeticException | IllegalArgumentException e) {
            // multi catch
        } finally {
            // allways run this
        }
```

### throw throws

```
public String getDataFromDatabase() throws SQLException {
    throw new UnsupportedOperationException();
}
```

## Exception category
- all exception inherit from Throwable
- handling exceptions from Exception
- checked exception MUST be handled or declared
- unchecked exceptions does not need to be handled or declared

### Unchecked Exceptions inherit RUntomeException
- ArithmeticException
- ArrayIndexOutOfBoundsException
- ArrayStoreException
- ClassCastException
- IllegalArgumentException
- IllegalStateException
- MissingResourceException
- NullPointerException
- NumberFormatException
- UnsupportedOperationException

* ! NumberFormatException inherits from IllegalArgumentException

### Checked Exception
- FileNotFoundException
- IOException
- NotSerializableException
- ParseException
- SQLException

* ! FileNotFoundException and NotSerializableException inherits from IOException

- broad to specific exception=> DNC
```
try {
   throw new IOException();
} catch (IOException | FileNotFoundException e) {} // DOES NOT COMPILE (parent + child...)

try {
   throw new IOException();
} catch (IOException e) {
} catch (FileNotFoundException e) {} // DOES NOT COMPILE (Order...)
```


## Creating Custom Exceptions

When creating your own exception, you need to decide whether it should be a checked or unchecked exception. While you can extend any exception class, it is most common to extend Exception (for checked) or RuntimeException (for unchecked).  

```
class CannotSwimException extends Exception {}

  class DangerInTheWater extends RuntimeException {}

  class SharkInTheWaterException extends DangerInTheWater {}

  class Dolphin {
   public void swim() throws CannotSwimException {

   }
}


// constructors

    public class CannotSwimException extends Exception {

    public CannotSwimException() {
      super();  // Optional, compiler will insert automatically
    }

    public CannotSwimException(Exception e) {
      super(e);
    }

    public CannotSwimException(String message) {
          super(message);
    }
}
```

## Printing Stack Traces
- e.printStackTrace();



## Automating resource managment
- constructing with try-with-resources statements
- AutoClosable interface
- OMGEKEERDE volgorde van opruimen...
- try scope blijft in try scope!!
```
public class MyFileReader implements AutoCloseable { private String tag;
    public MyFileReader(String tag) { this.tag = tag;}
    @Override public void close() {
      System.out.println("Closed: "+tag);
    }
}

try (var bookReader = new MyFileReader("monkey")) {
    System.out.println("Try Block");
} finally {
   System.out.println("Finally Block");
}

//Try Block
//Closed: monkey
//Finally Block

// scoping

try (Scanner s = new Scanner(System.in)) {
 s.nextLine();
 } catch(Exception e) {
 s.nextInt(); // DOES NOT COMPILE
 } finally {
 s.nextInt(); // DOES NOT COMPILE
}
```

## effectively Final Feature
it is possible to use resources declared prior to the try‐with‐resources statement, provided they are marked final or effectively final. 
```
public void relax() {

final var bookReader = new MyFileReader("4");
MyFileReader movieReader = new MyFileReader("5");

try (bookReader;
     var tvReader = new MyFileReader("6");
movieReader) {
    System.out.println("Try Block");
} finally {
   System.out.println("Finally Block");
}
```

## Suppressed Exceptions
- de eerste wordt als main exception gezien
- die daarna erbij komen als suppressed
- 
```
public class TurkeyCage implements AutoCloseable { public void close() {
      System.out.println("Close gate");
   }
public static void main(String[] args) {
    try (var t = new TurkeyCage()) {
         System.out.println("Put turkeys in");
    }
} }
```

# Assertions
- assert test_value;
- assert test_value : message;
- assert => false => AssertionError
- AssertionError is fatal and ends the program
- JVM heeft moet -enableassertions of -ea flag hebben
- -ea zonder iets dan geldt t voor alles in de running package
- -ea:com.demos... voor alles in demos en eronder
- -ea:comdemos.TestColors my.program.Main voor specifiek die Class

- -disableassertions of -da om uit te zetten

```
// correct!
assert 1 == age;
assert(2 == height);
assert 100.0 == length : "Problem with length";
assert ("Cecelia".equals(name)): "Failed to verify user data";


// DNC
assert(1);
assert x -> true;
assert 1==2 ? "Accept" : "Error";
assert.test(5> age);
```

```
public class Party {

    public static void main(String[] args) {
       int numGuests = -5;
       assert numGuests> 0;
       System.out.println(numGuests);


    }
 }
```

**Assertions should never alter outcomes.**

```
int x = 10;
assert ++x> 10;
```



# Dates and Times
**Dates beginnen met een 1 NIET een 0...** gebruik daarom Month.October


|Class |Description |Example|
|-|-|-|
|java.time.LocalDate|Date with day, month, year|Birth date|
|java.time.LocalTime|Time of day|Midnight|
|java.time.LocalDateTime|Day and time with no time zone|10 a.m. next Monday|
|java.time.ZonedDateTime|Date and time with a specific time zone|9 a.m. EST on 2/20/2021|

## .now()
```
// hebben allemaal .now()
System.out.println(LocalDate.now());     // 2020-10-14
System.out.println(LocalTime.now());     // 12:45:20.854
System.out.println(LocalDateTime.now()); // 2020-10-14T12:45:20.854
System.out.println(ZonedDateTime.now()); // 2020-10-14T12:45:20.854-04:00[America/New_York]
```

## .of()
```
LocalDate date1 = LocalDate.of(2020, Month.OCTOBER, 20);
LocalDate date2 = LocalDate.of(2020, 10, 20);
```
## formatting
- format()
- getDayOfWeek()
- getMonth()
- getYear()
- getDayOfYear()

**DateTimeFormatter**
```
LocalDate date = LocalDate.of(2020, Month.OCTOBER, 20);
System.out.println(date.format(DateTimeFormatter.ISO_LOCAL_DAT E));

// or custom
var f = DateTimeFormatter.ofPattern("MMMM dd, yyyy 'at' hh:mm");
System.out.println(dt.format(f)); // October 20, 2020 at 11:12

// of de oude classes
DateFormat s = new SimpleDateFormat("MMMM dd, yyyy'at' hh:mm");
System.out.println(s.format(new Date()));  // October 20, 2020 at 06:15
```

- y Year 20, 2020
- M Month 1, 01, Jan, January
- d Day 5, 05
- h Hour 9, 09
- m Minute 45
- s Second 52
- a a.m./p.m. AM, PM
- z Time Zone Name Eastern Standard Time,EST
- Z Time Zone Offset ‐0400

**M Month m minute**  


Supported data/time symbols
|Symbol|LocalDate|LocalTime|LocalDateTime|ZonedDateTime|
|-|-|-|-|-|
|y|√| |√|√|
|M|√| |√|√|
|d|√| |√|√|
|h| |√|√|√|
|m| |√|√|√|
|s| |√|√|√|
|a| |√|√|√|
|z| | | |√|
|Z| | | |√|

- LocalDate : YMd
- LocalTime : hsma
- LocaldateTime : YMdhmsa
- ZonedDateTime : alles

## Custom Text values
- concat
- use '' 'var f = DateTimeFormatter.ofPattern("MMMM dd, yyyy 'at' hh:mm");'
- escape ' met  ' 'var g1 = DateTimeFormatter.ofPattern("MMMM dd', Party''s at' hh:mm");'


# Internationalization i18n
**Locale**

```
Locale locale = Locale.getDefault();
System.out.println(locale);
```
- first lowercase language
- language is allways required
- then _ with UPPERcase country
- Locale.GERMAN => de
- Locale.GERMANY => de_DE

met builder()
```
Locale l1 = new Locale.Builder()
                .setLanguage("en")
                .setRegion("US")
                .build();
```

### specific for your program
in scope van program, niet machine
```
System.out.println(Locale.getDefault()); // en_US
Locale locale = new Locale("fr");
Locale.setDefault(locale); // change the default
System.out.println(Locale.getDefault()); // fr
```




## Localing Dates
- DateTimeFormatter.ofLocalizedDate(dateStyle)
- DateTimeFormatter.ofLocalizedTime(timeStyle)
- DateTimeFormatter.ofLocalizedDateTime(dateStyle, timeStyle)

- .SHORT .MEDIUM .FULL



# Localizing Numbers

- java.text
- eerst formatten dan pas number va maken

Factory methods to get a NumberFormat
|Description| Using default Locale and a specified Locale|
|-|-|
|A general‐purpose formatter|NumberFormat.getInstance()|
| | NumberFormat.getInstance(locale)|
|Same as getInstance|NumberFormat.getNumberInstance()|
| |NumberFormat.getNumberInstance(locale)|
|For formatting monetary amounts|NumberFormat.getCurrencyInstance()|
| |NumberFormat.getCurrencyInstance(locale)|
|For formatting percentages|NumberFormat.getPercentInstance()|
| |NumberFormat.getPercentInstance(locale)|
|Rounds decimal values before displaying|NumberFormat.getIntegerInstance()|
| |NumberFormat.getIntegerInstance(locale)|
Once you have the NumberFormat instance, you can call format() to turn a number into a String, or you can use parse() to turn a String into a number.



```
double price = 48;
var myLocale = NumberFormat.getCurrencyInstance();
System.out.println(myLocale.format(price));

String s = "23.45";
var en = NumberFormat.getInstance(Locale.US);
System.out.println(en.parse(s)); // 23.45

// LET OP!!

String s = "23.45";
var en = NumberFormat.getInstance(Locale.FRANCE);
System.out.println(en.parse(s)); //  !! 23 vanwege de .

// currency

String s = "$23.45"; // "23.45" DNC !!!
var en = NumberFormat.getCurrencyInstance(Locale.US);
System.out.println(en.parse(s));


```

## Custom Number Formatter

- \#  , Omit the position if no digit exists for it. , $2.2

- 0 - Put a 0 in the position if no digit exists for it - $002.20

```
 double d = 1234567.467;
 NumberFormat f1 = new DecimalFormat("###,###,###.0");
 System.out.println(f1.format(d)); // 1,234,567.5

 NumberFormat f2 = new DecimalFormat("000,000,000.00000");
 System.out.println(f2.format(d)); // 001,234,567.46700

 NumberFormat f3 = new DecimalFormat("$#,###,###.##");
 System.out.println(f3.format(d)); // $1,234,567.47
```


## Locale Category
- DISPLAY
- FORMAT
- Locale.setDefault() doet DISPLAY en FORMAT

```
    public static void printCurrency(Locale locale, double money) {
        System.out.println(
                NumberFormat.getCurrencyInstance().format(money) + ", " + locale.getDisplayLanguage());
    }

    public static void main(String[] args) throws ParseException {
        var spain = new Locale("es", "ES");
        var money = 1.23;

        // Print with default locale
        Locale.setDefault(new Locale("en", "US"));
        printCurrency(spain, money); // $1.23, Spanish

        // Print with default locale and selected locale display
        Locale.setDefault(Locale.Category.DISPLAY, spain);
        printCurrency(spain, money); // $1.23, espaÑol  ! let op NUMBERFORMAT is changed...

        // Print with default locale and selected locale format
        Locale.setDefault(Locale.Category.FORMAT, spain);
        printCurrency(spain, money); // 1,23 €, espaÑol
    }
```
    

## Resource Bundle
- op goede locatie...

```
ResourceBundle.getBundle("name");          // default locale
ResourceBundle.getBundle("name", locale);
```

1. Lookfortheresourcebundlefortherequestedlocale,followedbytheone for the default locale.
2. Foreachlocale,checklanguage/country,followedbyjustthelanguage.
3. Usethedefaultresourcebundleifnomatchinglocalecanbefound.

having:
- Zoo_en.properties
- Zoo_hi.properties
- Zoo.properties
```
Locale.setDefault(new Locale("hi"));
ResourceBundle rb = ResourceBundle.getBundle("Zoo", new Locale("en"));
```
Worden ALLE drie geladen!


## Formatting Messages
- {0} {1} als markers

## Properties Class
- HashMap<String, String>


```
System.out.println(props.getProperty("camel")); // null
System.out.println(props.getProperty("camel", "Bob")); // Bob is default waarde omdat camel er niet is
```

[prev](http://hjh.devsnips.nl/ocp15)
[next](http://hjh.devsnips.nl/ocp17)