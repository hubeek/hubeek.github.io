# OCP Chapter 13

_Status: Published_
_Created: 2024-07-30 16:48:10_
_Tags: ocp_

# Annotations
- assign metadata tp classes methods variables and other Java types
- an annotation ascribes custom information on the declaration where it is defined
- annotations zal compileren niet in de weg zitten
- case sensitive!
- zijn impliciet abstract =. dus geen protected, private en final
- required element, optional element, constant element
- all requiremed elements must be provided
- marker annotation has no elements
```
// creeerr Annotatie
public @interface Exercise {}

// gebruik m
@Exercise public class Blah{}
```

## annotation element
- zonder value => dan dus REQUIRED
```
public @interface Exercise {
 int hoursPerDay();
}

// =>

@Exercise(hoursPerDay=34)public class Blah {}
```
### providing an optional element with default
- NOT NULL
- type mag primitive, Class, enum, another annotation or an array of these types
- leeg mag wel => "" als empty String
```
public @interface Exercise {
 int hoursPerDay();
 int startHour() default 6; // optional element
}
```
### Adding a constant var
```
public @interface Exercise {
 int MINVALUE = 21;
}
```



## Applying Annotations



[prev](http://hjh.devsnips.nl/ocp12)
[next](http://hjh.devsnips.nl/ocp14)
