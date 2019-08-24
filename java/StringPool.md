# String Pool

String Pool in java is a pool of Strings stored in Java Heap Memory. We know that String is special class in java and we can create String object using new operator as well as providing values in double quotes.
String Pool is possible only because String is immutable in Java and it’s implementation of String interning concept. String pool is also example of Flyweight design pattern.

String pool helps in saving a lot of space for Java Runtime although it takes more time to create the String.

When we use double quotes to create a String, it first looks for String with same value in the String pool, if found it just returns the reference else it creates a new String in the pool and then returns the reference.

When we create a String via the new operator, the Java compiler will create a new object and store it in the heap space reserved for the JVM.
Every String created like this will point to a different memory region with its own address.

Manually interning the String will store its reference in the pool, and the JVM will return this reference when needed.

Before Java 7, the JVM placed the Java String Pool in the PermGen space, which has a fixed size — it can’t be expanded at runtime and is not eligible for garbage collection.

The risk of interning Strings in the PermGen (instead of the Heap) is that we can get an OutOfMemory error from the JVM if we intern too many Strings.

From Java 7 onwards, the Java String Pool is stored in the Heap space, which is garbage collected by the JVM. The advantage of this approach is the reduced risk of OutOfMemory error because unreferenced Strings will be removed from the pool, thereby releasing memory.

```
String first = "Sumit";
String second = "Sumit";
System.out.println(first == second); // True

String third = new String("Sumit");
String fourth = new String("Sumit");
System.out.println(third == fourth); // False

String fifth = "Sumit";
String sixth = new String("Sumit");
System.out.println(fifth == sixth); // False

String newString = new String("interned Sumit");
String internedString = newString.intern();
System.out.println(newString == internedString); // False

String newStringLiteral = "interned Sumit";
System.out.println(newStringLiteral == internedString); // True
```
