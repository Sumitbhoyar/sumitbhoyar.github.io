#Java Immutable Class
----------------------


**An immutable object is one whose state cannot and will not change after it’s initial creation.**

**Benefits:**

Immutable objects are great, mostly because they are Thread safe.
You can pass them around without fear they will be changed.
Almost all of the new features in Java 8 (Date and Time, Optionals and Streams) have been implemented in an immutable fashion. This allows much of the performance benefits that can come from things such as parallel Streams. Immutable Objects allow us to create side-effect free functions as seen in Functional Programming languages which are the basis for creating fast, lock free code.


**What are the advantages of immutability?**

- Immutable objects are automatically thread-safe, the overhead caused due to use of synchronization is avoided.
- Once created the state of the immutable object can not be changed so there is no possibility of them getting into an inconsistent state.
- The references to the immutable objects can be easily shared or cached without having to copy or clone them as there state can not be changed ever after construction.
- The best use of the immutable objects is as the keys of a map.


**How to create an immutable class?**

- Create a final class.
- Set the values of properties using constructor only.
- Make the properties of the class final and private
- Do not provide any setters for these properties.
- If the instance fields include references to mutable objects, don't allow those objects to be changed:
- Don't provide methods that modify the mutable objects.
- Don't share references to the mutable objects. Never store references to external, mutable objects passed to the constructor; if necessary, create copies, and store references to the copies. Similarly, create copies of your internal mutable objects when necessary to avoid returning the originals in your methods.


**List object are contain in immutable class so what changes we need to do?**

- We need to use deep cloning of that objects.



