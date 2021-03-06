# Java Memory model

### The Stack: 
Stack memory is responsible for holding references to heap objects and for storing value types (also known in Java as primitive types), which hold the value itself rather than a reference to an object from the heap.
The stack memory in Java is allocated per Thread. Therefore, each time a Thread is created and started, it has its own stack memory — and cannot access another thread’s stack memory.

### The Heap: 
This part of memory stores the actual object in memory. Those are referenced by the variables from the stack.
There exists only one heap memory for each running JVM process. Therefore, this is a shared part of memory regardless of how many threads are running.
The heap itself is divided into a few parts, which facilitates the process of garbage collection.
We can use -Xms and -Xmx JVM option to define the startup size and maximum size of heap memory. We can use -Xss to define the stack memory size.
When stack memory is full, Java runtime throws java.lang.StackOverFlowError whereas if heap memory is full, it throws java.lang.OutOfMemoryError: Java Heap Space error.

**Heap Memory**

- Eden space

- Old gen

- Survivor space

**Non Heap Memory**

- Code Cache

- Permanent Generation

### Reference Types
**Strong Reference:** These are the most popular reference types that we all are used to. The object on the heap it is not garbage collected while there is a strong reference pointing to it, or if it is strongly reachable through a chain of strong references.

**Weak Reference:** In simple terms, a weak reference to an object from the heap is most likely to not survive after the next garbage collection process. A weak reference is created as follows:
```
WeakReference<StringBuilder> reference = new WeakReference<>(new StringBuilder());
```
A nice use case for weak references are caching scenarios. Imagine that you retrieve some data, and you want it to be stored in memory as well — the same data could be requested again. On the other hand, you are not sure when, or if, this data will be requested again. So you can keep a weak reference to it, and in case the garbage collector runs, it could be that it destroys your object on the heap. Therefore, after a while, if you want to retrieve the object you refer to, you might suddenly get back a null value. A nice implementation for caching scenarios is the collection WeakHashMap<K,V>. 

**Soft Reference:** These types of references are used for more memory-sensitive scenarios, since those are going to be garbage collected only when your application is running low on memory. Therefore, as long as there is no critical need to free up some space, the garbage collector will not touch softly reachable objects. Java guarantees that all soft referenced objects are cleaned up before it throws an OutOfMemoryError.
```
SoftReference<StringBuilder> reference = new SoftReference<>(new StringBuilder());
```

**Phantom Reference**
Used to schedule post-mortem cleanup actions, since we know for sure that objects are no longer alive. Used only with a reference queue, since the .get() method of such references will always return null. These types of references are considered preferable to finalizers.

### Garbage collection steps:
**Marking:** This is the first step where garbage collector identifies which objects are in use and which ones are not in use
**Normal Deletion:** Garbage collector removes the unused objects and reclaims the free space to be allocated to other objects
**Deletion with compacting:** For better performance, after deleting unused objects, all the survived objects can be moved to be together. This will increase the performance of allocation of memory to newer objects

### Regions in JVM Memory
**[Young Generation/Nursery] Eden Space**
All new objects are first created in the Eden Space. As soon as it reaches an arbitrary threshold decided by the JVM, a minor garbage collection (Minor GC) kicks in. It first removes all the non-referenced objects and moves referenced objects from the ‘eden’ and ‘from’ into the ‘to’ survivor space. Once the GC is over, the ‘from’ and ‘to’ roles (names) are swapped.

**[Young Generation/Nursery] Survivor 1 (From)**
This is a part of the survivor space (You may think of this a role in the survivor space). This was the ‘to’ role during the previous garbage collection (GC).

**[Young Generation/Nursery] Suvrivor 2 (To)**
This is also a part of the survivor space (You may think of this also a role in the survivor space). It is here, where during the GC, all the referenced objects
are moved to, from ‘from’ and ‘eden’ .

**[Old Generation] Tenured**
Depending on the threshold limits, which can be checked by using -XX:+PrintTenuringDistribution, which shows the objects (space in bytes) by age – Objects are moved from the ‘to’ Survivor space to the Tenured space. ‘Age’ is the number of times that it has moved within the survivor space. There are other important flags like, -XX:InitialTenuringThreshold, -XX:MaxTenuringThreshold and -XX:TargetSurvivorRatio which lead to an optimum utilization of the tenured as well as the survivor spaces. By setting -XX:InitialTenuringThreshold and -XX:MaxTenuringThreshold we allow an initial value and an maximum value for ‘Age’ while maintaining the percentage utilization in the ‘Survivor (To)’ as specified by the -XX:+NeverTenure and -XX:+AlwaysTenure, as they suggest are used to either never tenure an object (risky to use) and the opposite usage is to always tenure, which is to always use the ‘old generation’. The garbage collection that happens here is the major garbage collection (Major GC). This is usually triggered when the heap is full or the old generation is full. This is usually a ‘Stop-the-World‘ event or thread that takes over to perform the garbage collection. There is another type of GC named as the full garbage collection (Full GC) which involves other memory areas such as the permgen space.

**[Permanent Generation] Permgen space**
The ‘Permgen’ is used to store the following information: Constant Pool (Memory Pool), Field & Method Data and Code. Each of them related to the same specifics as their name suggests.

### Types of GC
**Minor GC:** It’s also called as Scavenge GC. This is the GC which collects garbage from the Young Generation.
**Major GC:** This GC collects garbage from the Old Generation
**Full GC:** This GC collects garbage from all regions i.e. Young, Old, Perm, Metaspace.
When Major or Full GC run all application threads are paused. It’s called a stop-the-world event. In Minor GCs, stop-the-world events occurs, but only momentarily.

### Types of GC Algorithms
**Serial GC (-XX:+UseSerialGC):** Serial GC uses the simple mark-sweep-compact approach for young and old generations garbage collection that is, Minor and Major GC

**Parallel GC (-XX:+UseParallelGC):** Parallel GC is same as Serial GC except that, it spawns N threads for young generation garbage collection where N is the number of CPU cores in the system. We can control the number of threads using –XX:ParallelGCThreads=n JVM option

**Parallel Old GC (-XX:+UseParallelOldGC):** This is same as Parallel GC except that it uses multiple threads for both young generation and old generation garbage collection

**Concurrent Mark Sweep (CMS) Collector (-XX:+UseConcMarkSweepGC):** CMS is also referred as concurrent low pause collector. It does the garbage collection for old generation. CMS collector tries to minimize the pauses due to garbage collection by doing most of the garbage collection work concurrently within the application threads. CMS collector on young generation uses the same algorithm as that of the parallel collector. This garbage collector is suitable for responsive applications where we can’t afford longer pause times. We can limit the number of threads in CMS collector using –XX:ParallelCMSThreads=n JVM option

**G1 Garbage Collector (-XX:+UseG1GC):** The garbage first or G1 Garbage Collector is available from Java 7 and its long term goal is to replace the CMS collector. The G1 collector is a parallel, concurrent and incrementally compact low-pause garbage collector. Garbage first collector doesn’t work like other collectors and there is no concept of young and old generation space. It divides the heap space into multiple equal-sized heap regions. When a garbage collector is invoked, it first collects the region with lesser live data, hence “Garbage First”

### Important change in Memory Management in Java 8
Oracle has completely gotten rid of ‘PermGen’ and replaced it with Metaspace.
With Java 8, there is NO PermGen. So no more OutOfMemory Errors due to PermGen.
The key difference between PermGen and Metaspace is this: PermGen is not part of the HEAP and is not controlled by Garbage collection. Rather Metaspace is part of Native Memory (process memory) which is only limited by the Host Operating System.

While you will NOT run out of PermGen space anymore (since there is NO PermGen), you may consume excessive Native memory making the total process size large. The issue is, if your application loads lots of classes (and/or interned strings), you may actually bring down the Entire Server (not just your application). Why ? Because the native memory is only limited by the Operating System. This means you can literally take up all the memory on the Server. 
It is critical that you add the new option -XX:MaxMetaspaceSize  which sets the Maximum Metaspace size for your application.

### GC Monitoring:
- Utilization of the different memory pools (Eden, Survivor and old generation). Memory shortage is the number-one reason for increased GC activity
- If overall memory utilization is increasing continuously despite garbage collection, there is a memory leak, which will inevitably lead to an out-of-memory. In this case, a memory heap analysis is necessary
- The number of young generation collections provides information on the churn rate (the rate of object allocations). The higher the number, the more objects are allocated. A high number of young collections can be the cause of a response-time problem and of a growing old generation (because the young generation cannot cope with the quantity of objects anymore)
- If the utilization of old generation fluctuates greatly without rising after GC, then objects are being copied unnecessarily from the young generation to the old generation. There are three possible reasons for this: the young generation is too small, there is high churn rate or there is too much transactional memory usage
- High GC activity generally has a negative effect on CPU usage. However, only suspensions (stop-the-world-events) have a direct impact on response time. Contrary to the popular opinion, suspensions are not limited to Major GCs. It is therefore important to monitor suspensions in correlation to application response time


