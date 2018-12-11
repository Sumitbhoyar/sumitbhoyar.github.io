# Functional Interface

- Any Interface with exactly one abstract method is functional interface.
- No restriction on number of default or static methods.
- @FunctionalInterface annotation can be used on interface to declare it as Functional.
- @FunctionalInterface is an informative annotation, i.e. it is not mandatory to use this annotation for classifying the given interface as a valid functional interface.
- It is mandatory to have exactly one abstract method for a interface with @FunctionalInterface, otherwise it will not compile.

Example: java.lang.Runnable, java.lang.Callable, java.util.function.Predicate