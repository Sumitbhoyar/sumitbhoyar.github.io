
# Thread contention 

A Java thread dump is a snapshot what every thread in the JVM is doing at a particular point in time. Each thread in the JVM is listed with it's name and id, it's current state and the Java call stack showing what monitor it has locked or is waiting on. This is especially useful if your Java application sometimes seems to hang when running under load, as an analysis of the dump will show where the threads are stuck, either by deadlock or other thread contention.


## Thread Status
In order to analyze a thread dump, you need to know the status of threads. The statuses of threads are stated on java.lang.Thread.State.

- NEW: The thread is created but has not been processed yet.
- RUNNABLE: The thread is occupying the CPU and processing a task. (It may be in WAITING status due to the OS's resource distribution.)
- BLOCKED: The thread is waiting for a different thread to release its lock in order to get the monitor lock.
- WAITING: The thread is waiting by using a wait, join or park method.
- TIMED_WAITING: The thread is waiting by using a sleep, wait, join or park method. (The difference from WAITING is that the maximum waiting time is specified by the method parameter, and WAITING can be relieved by time as well as external changes.) 


## Terminologies
- **Thread contention** is a status in which one thread is waiting for a lock, held by another thread, to be lifted. Different threads frequently access shared resources on a web application. For example, to record a log, the thread trying to record the log must obtain a lock and access the shared resources.

- **Deadlock** is a special type of thread contention, in which two or more threads are waiting for the other threads to complete their tasks in order to complete their own tasks.

- Thread synchronization on Java can be done using **monitor**. Every Java object has a single monitor. The monitor can be owned by only one thread. For a thread to own a monitor that is owned by a different thread, it needs to wait in the wait queue until the other thread releases its monitor.


## Getting Thread Dump

- jstack -l 22004 > e:/thread.txt
- jVisualVM
- JConsole

Thread Information from the Thread Dump File

- Thread name: When using Java.lang.Thread class to generate a thread, the thread will be named Thread-(Number), whereas when using java.util.concurrent.ThreadFactory class, it will be named pool-(number)-thread-(number).
- Priority: Represents the priority of the threads.
- Thread ID: Represents the unique ID for the threads. (Some useful information, including the CPU usage or memory usage of the thread, can be obtained by using thread ID.)
- Thread status: Represents the status of the threads.
- Thread callstack: Represents the call stack information of the threads. 

## Thread Dump Patterns to look for
#### When Unable to Obtain a Lock (BLOCKED)
This is when the overall performance of the application slows down because a thread is occupying the lock and prevents other threads from obtaining it.


    "Thread-0" #11 prio=5 os_prio=0 tid=0x0000000018f1c000 nid=0x14b5c waiting for monitor entry [0x000000001991e000]
       java.lang.Thread.State: BLOCKED (on object monitor)
    	at DeadlockProgram$DeadlockRunnable.run(DeadlockProgram.java:25)
    	- waiting to lock <0x00000000d5d43110> (a java.lang.Object)
    	- locked <0x00000000d5d43100> (a java.lang.Object)
    	at java.lang.Thread.run(Thread.java:748)
	
#### When in Deadlock Status
This is when thread A needs to obtain thread B's lock to continue its task, while thread B needs to obtain thread A's lock to continue its task. 	

        Found one Java-level deadlock:
        "Thread-1":
          waiting to lock monitor 0x0000000002c5dd58 (object 0x00000000d5d43100, a java.lang.Object),
          which is held by "Thread-0"
        "Thread-0":
          waiting to lock monitor 0x0000000002c5b2b8 (object 0x00000000d5d43110, a java.lang.Object),
          which is held by "Thread-1"
    
    Java stack information for the threads listed above:
    "Thread-1":
    	at DeadlockProgram$DeadlockRunnable.run(DeadlockProgram.java:25)
    	- waiting to lock <0x00000000d5d43100> (a java.lang.Object)
    	- locked <0x00000000d5d43110> (a java.lang.Object)
    	at java.lang.Thread.run(Thread.java:748)
    "Thread-0":
    	at DeadlockProgram$DeadlockRunnable.run(DeadlockProgram.java:25)
    	- waiting to lock <0x00000000d5d43110> (a java.lang.Object)
     	- locked <0x00000000d5d43100> (a java.lang.Object)
        	at java.lang.Thread.run(Thread.java:748)
    Found 1 deadlock.

#### When Waiting

The thread is maintaining WAIT status. In the thread dump, IoWaitThread thread keeps waiting to receive a message from LinkedBlockingQueue. If there continues to be no message for LinkedBlockingQueue, then the thread status will not change.


    "IoWaitThread" prio=6 tid=0x0000000007334800 nid=0x2b3c waiting on condition [0x000000000893f000]
       java.lang.Thread.State: WAITING (parking)
                    at sun.misc.Unsafe.park(Native Method)
                    - parking to wait for  <0x00000007d5c45850> (a java.util.concurrent.locks.AbstractQueuedSynchronizer$ConditionObject)
                    at java.util.concurrent.locks.LockSupport.park(LockSupport.java:156)
				
## How to Solve common Problems by Using Thread Dump
#### Example 1: When the CPU Usage is Abnormally High
Extract the thread that has the highest CPU usage.

    [user@linux ~]$ ps -mo pid.lwp.stime.time.cpu -C java
         PID         LWP          STIME                  TIME        %CPU
    10029               -         Dec07          00:02:02           99.5
             -       10040        Dec07          00:00:00              0.1
             -       10039        Dec07          00:00:00           95.5
		 
From the application, find out which thread is using the CPU the most.

Acquire the Light Weight Process (LWP) that uses the CPU the most and convert its unique number (10039) into a hexadecimal number (0x2737).

After acquiring the thread dump, check the thread's action.

Extract the thread dump of an application with a PID of 10029, then find the thread with an nid of 0x2737.


#### Example 2: When the Processing Performance is Abnormally Slow

After acquiring thread dumps several times, find the list of threads with BLOCKED status.

    " DB-Processor-13" daemon prio=5 tid=0x003edf98 nid=0xca waiting for monitor entry [0x000000000825f000]
    java.lang.Thread.State: BLOCKED (on object monitor)
                    at beans.ConnectionPool.getConnection(ConnectionPool.java:102)
				
Acquire the list of threads with BLOCKED status after getting the thread dumps several times.

If the threads are BLOCKED, extract the threads related to the lock that the threads are trying to obtain.


