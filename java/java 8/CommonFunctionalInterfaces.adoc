
# Commonly used functional interfaces

4 fundamental and most commonly used functional interfaces.

- Consumer<T>: Represents an operation that accepts a single input argument and returns no result.
- Function <T, R>: Represents a function that accepts one argument and produces a result.
- Predicate<T>: Represents a predicate (boolean-valued function) of one argument.
- Supplier<T>: Represents a supplier of results.

## java.util.function.Predicate

**Abstract Method:**

    boolean test(T t):

T is the type of input to the predicate
boolean test(T t) returns true if the input argument matches the predicate(the test condition), otherwise returns false
Example:

    Predicate<Integer> positive = i -> i > 0;
    predicate.test(5)

**Default methods**

**and()**: It does logical AND of the predicate on which it is called with another predicate. 
Example: 

    predicate1.and(predicate2)
    (i->i>0).and(i->i>10)	

**or()**: It does logical OR of the predicate on which it is called with another predicate. 
Example: 

    predicate1.or(predicate2)
    (i->i>0).or(i->i>10)

**negate()**: It does boolean negation of the predicate on which it is invoked. 
Example: 

    predicate1.negate()
    (i->i>0).negate()	

	

**Static method**

**isEqual()**:
Its defined as – static <T> Predicate<T> isEqual(Object targetRef) 
It returns a predicate that tests if two arguments are equal according to Objects.equals(Object, Object).

## java.util.function.Consumer

**Abstract Method:**

void **accept**(T t):
accept() method takes as input the type T and returns no value.
Example:

    Consumer<Integer> consumer= i-> System.out.print(" "+i);
    consumer.accept(13);

**Default methods**

Consumer<T> **andThen**(Consumer<? super T> after):
Takes as input another instance of Consumer interface and returns as a result a new consumer interface which represents aggregation of both of the operations defined in the two Consumer interfaces.
Example:

    Consumer<Integer> consumer= i-> System.out.print(" "+i);
    Consumer<Integer> consumerWithAndThen = consumer.andThen( i-> System.out.print("(printed "+i+")"));


## java.util.function.Function

**Abstract Method:**

R **apply**(T t)
T is the type of the input and R is the output type.
Method takes as input a parameter t of type T and gives an output object of type R.
Example:

    Function<Employee, String> funcEmpToString= (Employee e)-> {return e.getName();};
    funcEmpToString.apply(emp)

**Default methods**

<V> Function<V, R> **compose**(Function<? super V, ? extends T> before)
Example: 

    <V> Function<T, V> **andThen**(Function<? super R, ? extends V> after)	

**Static method**

<T> Function<T, T> identity()

## java.util.function.Supplier

**Abstract Method**

**T get();**
Supplier has been defined with the generic type T which is the same type which its get() methods return as output.

Example:

    Supplier<String> helloStrSupplier = () -> new String("Hello");
    String helloStr = helloStrSupplier.get();
