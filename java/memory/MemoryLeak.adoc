
# Java Memory Leak:

A memory leak is when memory is marked "in use" even though it's no longer needed, and it will never be freed by the process that created it.

The **OutOfMemoryError** is a common indication of a memory leak. Essentially, the error is thrown when there’s insufficient space to allocate a new object. Try as it might, the garbage collector can’t find the necessary space, and the heap can’t be expanded any further. Thus, an error emerges, along with a stack trace.
 
 
## Tools to get Heap Dump
- JVisualVM
- JConsole

## VM argument to get heap dump automatically on out of memory error.
- -XX:+HeapDumpOnOutOfMemoryError  -XX:HeapDumpPath=E:\

## VM Argument to identify GC activity and how much memory getting free after GC
- -verbosegc

## Tool: Eclipse Memory Analyzer Tool

It visualizes the references to objects based on Java heap dumps and provides tools to identify potential memory leaks.
Steps:
- Download MAT as standalone or add in eclipse as plug-in.
- Get the Heap Dump of the application.
- Open it in MAT.

#### Things to look for in MAT report
- Objects getting accumulated
- Class whose objects are getting accumulated.
- Accumulated object tree
