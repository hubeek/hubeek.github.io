# OCP Chapter 18

_Status: Published_
_Created: 2024-07-30 16:55:19_
_Tags: ocp_

# Concurrency

## Threads
- a Thread is the smallest unit of execution that can be scheduled by the operation system.
- a process is a group of associated threads that execute in th esame shared environment.
- single-threaded process have only one thread
- multithreaded process uses one or more threads
- shared environment share the same memory space and can directly communicate with one another.
-  a task is a single unit of work performed by a thread.
-  a task can be implemented as an lambda expression
-  a thread can complete multiple independent tasks but only task at a time.
-  for simplicity  we refer to threads that contain only a single user defined thread as a single-threaded application. Since we are uninterested in the system threads.
-  the property of executing multiple threads and processes at the same time is actually referred as concurrency.
- CPU uses thread scheduler to accomplish threads running
- a thread scheduler may employ a round-robin schedule
- when a thread alloted time is complete but the thread has not finished processing a context switch occurs. A context-switch is the process of storing a threads current state
- thread priority


### Thread Types
- system thread is created by the JVM and runs in the background of the application. fe garbage collection
- user-defined thread is one created by the applicationdeveloper to accopmplish a specific task.
- deamon thread is one that will not prevent the JVM from exiting when the program finishes. Both sysem an user defined threads can be marked as daemon threads

## Task with Runnable
```
@FunctionalInterface public interface Runnable {
   void run();
}
```


### Summary
This chapter introduced you to threads and showed you how to process tasks in parallel using the Concurrency API. The work that a thread performs can be expressed as lambda expressions or instances of Runnable or Callable.  

For the exam, you should know how to concurrently execute tasks using ExecutorService. You should also know which ExecutorService instances are available, including scheduled and pooled services.  

Thread‐safety is about protecting data from being corrupted by multiple threads modifying it at the same time. Java offers many tools to keep data safe including atomic classes, synchronized methods/blocks, the Lock framework, and CyclicBarrier. The Concurrency API also includes numerous collections classes that handle multithreaded access for you. For the exam, you should also be familiar with the concurrent collections including the CopyOnWriteArrayList class, which creates a new underlying structure anytime the list is modified.  

When processing tasks concurrently, a variety of potential threading issues can arise. Deadlock, starvation, and livelock can result in programs that appear stuck, while race conditions can result in unpredictable data. For the exam, you need to know only the basic theory behind these concepts. In professional software development, however, finding and resolving such problems is often quite challenging.


Finally, we discussed parallel streams and showed you how to use them to perform parallel decompositions and reductions. Parallel streams can greatly improve the performance of your application. They can also cause unexpected results since the results are no longer ordered. Remember to avoid stateful lambda expressions, especially when working with parallel streams.  





```
(new Thread(new PrintData())).start();

// Will compile but not start a new thread!!

(new PrintData()).run();
```

## Polling with Sleep
Polling is the process of intermittently checking data at some fixed interval.

```
public class CheckResults {
   private static int counter = 0;
   public static void main(String[] args) {
      new Thread(() -> {
         for(int i = 0; i < 500; i++) CheckResults.counter++;
}).start();
      while(CheckResults.counter < 100) {
System.out.println("Not reached yet");
      }
      System.out.println("Reached!");

```

## Concurrency API

- ExecutorService interface which creates and manage threads.

```
import java.util.concurrent.*;
public class ZooInfo {
   public static void main(String[] args) {
      ExecutorService service = null;
      Runnable task1 = () ->
         System.out.println("Printing zoo inventory");
      Runnable task2 = () -> {for(int i = 0; i < 3; i++)
            System.out.println("Printing record: "+i);};
try {
    service = Executors.newSingleThreadExecutor();
    System.out.println("begin");
    service.execute(task1);
    service.execute(task2);
    service.execute(task1);
    System.out.println("end");
} finally {
    if(service != null) service.shutdown();
} }
}
```
- SHUTDOWN NIET VERGETEN!!!
- shutdown stopt lopende threads niet, die lopen uit. dan gebruik shutdownNow()
- shutdownNow() returns a list<Runnable> with tasks that were submitted to the thread executor but that were never started.

## Submitting tasks
- fire-and-forget
- execute()
- submit() returns a Future, can check if task is completed.




|Method name |Description|
|-|-|
|void execute(Runnable command)|Executes a Runnable task at some point in the future|
|Future<?> submit(Runnable task)|Executes a Runnable task at some point in the future and returns a Future representing the task|
|<T> Future<T> submit(Callable<T> task) | Executes a Callable task at some point in the future and returns a Future representing the pending results of the task|
|<T> List<Future<T>> invokeAll(Collection<?extends Callable<T>>tasks) throwsInterruptedException|Executes the given tasks and waits for all tasks to complete. Returns a List of Future instances, in the same order they were in the original collection|
|<T> T invokeAny(Collection<? extends Callable<T>> tasks) throws InterruptedException,ExecutionException|Executes the given tasks and waits for at least one to complete. Returns a Future instance for a complete task and cancels any unfinished tasks|


## Waiting for Results
Future Methods
|Method name |Description|
|-|-|
|boolean isDone()|Returns true if the task was completed, threw an exception, or was cancelled|
|boolean isCancelled()|Returns true if the task was cancelled before it completed normally|
|boolean cancel(boolean mayInterruptIfRunning)|Attempts to cancel execution of the task and returns true if it was successfully cancelled or false if it could not be cancelled or is complete|
|V get()|Retrieves the result of a task, waiting endlessly if it is not yet available|
|V get(long timeout, TimeUnit unit)|Retrieves the result of a task, waiting the specified amount of time. If the result is not ready by the time the timeout is reached, a checked TimeoutException will be thrown.|

## Callable
- V call() throws Exception;
- Future<Integer> result = service.submit(()->1+2); result.get() //3

## Wait for finish
- do shutdown()
- awaitTermination()
- if awaitTermination is called before shutdown than full timeout value moet doorloopen worden

## submitting task collections
- List<Future> list = service.invokeAll(List.of(task,task,task));
- invokeAny() executes a collection of tasks and returns the result of one of the tasks that succesfully completes executions, canceling al unfinished tasks!
- invokeAll() will wait for all tasks to complete undefinitly untill all tasks are complete
- invokeAll() en involeAny() hebben ook overload met timeout.

## Scheduling tasks
- ScheduledExecutorService service = Executors.newSingleThreadScheduledExecutor(); + ScheduledFuture<?> r1 = service.schedule(task1, 2, TimeUnit.SECONDS);
- Executors.newSingleThreadScheduledExecutor loopt in de toekomst met delay

```
schedule(Callable<V> callable, long delay, TimeUnit unit) // after period
schedule(Runnable command, long delay, TimeUnit unit)
scheduleAtFixedRate(Runnable command, long initialDelay, long period, TimeUnit unit) // every period
scheduleWithFixedDelay(Runnable command, long initialDelay, long delay, TimeUnit unit)
```

### scheduleAtFixedRate
-service.scheduleAtFixedRate(command, 5, 1, TimeUnit.MINUTES);


## Concurrency with Pools

- ExecutorService newSingle ThreadExecutor()
- ScheduledExecutorService newSingleThreadScheduledExecutor()
- ExecutorService newCachedThreadPool()
- ExecutorService newFixedThreadPool(int)
- ScheduledExecutorService newScheduledThreadPool(int)

- single threaded executor will wait for a thread to become available
- a pooled-thread can execute the next task concurrently until the pool is filled then awaits etc

### Determine the thread pool size
- Runtime.getRuntime().availableProcessors()



## Writing Thread-Safe Code
- race-condition

## Protect Data with Atomic Classes
- atomic is the property of an operation to be carried out as a single unit of execution without any interference by another thread.


- AtomicBoolean
- AtomicInteger
- AtomicLong

## Improveing Acces with Synchronized Blocks
- Atomic alleen helpt nog niets in de volgordelijkheid daarom hulp van *monitor* that supports *mutual exclusion*

## Synchronizing Methods
ipv synchronize a var kan je ook de hele methode synchronizen



## Lock Framework
- ReentrantLock()

```
// Implementation #1 with a synchronized block
Object object = new Object();
synchronized(object) {
// Protected code
}

// Implementation #2 with a Lock
Lock lock = new ReentrantLock();
try {
   lock.lock();
// Protected code
} finally {
   lock.unlock();
}
```

- void lock()
- void unlock()
- boolean tryLock()
- booelean tryLock(long, TimeUnit)

### tryLock()
- used in try/finally block
```
Lock lock = new ReentrantLock();
new Thread(() -> printMessage(lock)).start(); if(lock.tryLock()) {
   try {
      System.out.println("Lock obtained, entering protected
code");
   } finally {
      lock.unlock();
}
} else {
   System.out.println("Unable to acquire lock, doing something
else");
}
```

### Duplicate Lock Requests
- critical to release all the locks!
- ReentrantReadWriteLock niet voor t examen maar wel handig!




## Orchestrating Tasks with a CyclicBarrier
- taken met CyclicBarrier kunnen gegroepeerd en op volgorde van groepen worden uitgevoerd.
- let op groote threadpool
- let op deadlock als je rules of poolgrootes regelt

```
import java.util.concurrent.*;

public class CyclicBarrierExample {
    public static final int NUMBER_OF_THREADS = 4;
    public static final int NUMBER_OF_STEPS = 3;

    public static void main(String[] args) {
        CyclicBarrier barrier = new CyclicBarrier(NUMBER_OF_THREADS, new Runnable() {
            @Override
            public void run() {
                System.out.println("All threads completed a step. Moving to the next step...\n");
            }
        });

        ExecutorService executorService = Executors.newFixedThreadPool(NUMBER_OF_THREADS);

        for (int i = 0; i < NUMBER_OF_THREADS; i++) {
            executorService.submit(new Worker(barrier));
        }

        executorService.shutdown();
    }
}

class Worker implements Runnable {
    private CyclicBarrier barrier;

    public Worker(CyclicBarrier barrier) {
        this.barrier = barrier;
    }

    @Override
    public void run() {
        try {
            for (int step = 1; step <= CyclicBarrierExample.NUMBER_OF_STEPS; step++) {
                performTask(step);
                System.out.println(Thread.currentThread().getName() + " completed step " + step);
                barrier.await(); // Wait for other threads
            }
        } catch (InterruptedException | BrokenBarrierException e) {
            e.printStackTrace();
        }
    }

    private void performTask(int step) {
        // Simulating task for each step
        System.out.println(Thread.currentThread().getName() + " is performing task for step " + step);
        try {
            Thread.sleep((long) (Math.random() * 1000)); // Simulate varying task durations
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
}
```

## Concurrent Collections
- om om memory consistency errors te vermijden. wanneer twee threads verschillende data krijgen die gelijk zou moeten zijn.
- concurrentModificationException at runtime

```
        var foodData = new HashMap<String, Integer>();
        foodData.put("penguin", 1);
        foodData.put("flamingo", 2);
        for (String key : foodData.keySet()) {
            foodData.remove(key); // Key klopt niet meer na key penguin removed
        }

// wel met:

        var foodData = new ConcurrentHashMap<String, Integer>();
        foodData.put("penguin", 1);
        foodData.put("flamingo", 2);
        for (String key : foodData.keySet()) {
            System.out.println("remove key " + key);
            foodData.remove(key);

        }
```
In principe hetzelfde als de niet concurrent collecties

|Class name |Java Collections Framework interfaces|Elements ordered? |Sort? |Blocking? |
|-|-|-|-|-|
|ConcurrentHashMap|ConcurrentMap|No|No|No|
|ConcurrentLinkedQueue|Queue|Yes|No|No|
|ConcurrentSkipListMap|ConcurrentMap SortedMap NavigableMap|Yes|Yes|No|
|ConcurrentSkipListSet|SortedSet NavigableSet|Yes|Yes|No|
|CopyOnWriteArrayList|List|Yes|No|No|
|CopyOnWriteArraySet|Set|No|No|No|
|LinkedBlockingQueue|BlockingQueue|Yes|No|Yes|


## Deleting when looping

```
List<String> birds = new CopyOnWriteArrayList<>();
birds.add("hawk");
birds.add("hawk");
birds.add("hawk");
for (String bird : birds) birds.remove(bird);
System.out.print(birds.size()); // 0

// kan dus ook met arraylist en iterator.

var iterator = birds.iterator();
while(iterator.hasNext()) {
   iterator.next();
   <b>iterator.remove()</b>;
}
System.out.print(birds.size());  // 0
```

## Blocking Queue waiting methods

|Method name| Description|
|-|-|
|offer(E e,long timeout,TimeUnit unit)|Adds an item to the queue, waiting the specified time and returning false if the time elapses before space is available|
|poll(long timeout,TimeUnit unit)| Retrieves and removes an item from the queue waiting the specified time and returning null if the time elapses before the item is available|

```
try {
var blockingQueue = new LinkedBlockingQueue<Integer>(); blockingQueue.offer(39);
blockingQueue.offer(3, 4, TimeUnit.SECONDS); System.out.println(blockingQueue.poll()); System.out.println(blockingQueue.poll(10,
TimeUnit.MILLISECONDS));
} catch (InterruptedException e) {
   // Handle interruption
}
```

## Obtaining Synchronized Collections
- synchronizedCollection(Collection<T> c)
- synchronizedList(List<T> list)
- synchronizedMap(Map<K,V> m)
- synchronizedNavigableMap(NavigableMap<K,V> m)
- synchronizedNavigableSet(NavigableSet<T> s)
- synchronizedSet(Set<T> s)
- synchronizedSortedMap(SortedMap<K,V> m)
- synchronizedSortedSet(SortedSet<T> s)

- If you know at the time of creation that your object requires synchronization, then you should use one of the concurrent collection classes listed in this table.



## Identifying Threading Problems

- liveness is ability of an application to be able to execute in a timely manner.
- kind of stuck state

- deadlock
- starvation
- livelock



### Deadlock
- Deadlock occurs when two or more threads are blocked forever, each waiting on the other.

### Starvation
- Starvation occurs when a single thread is perpetually denied access to a shared resource or lock.

### Livelock
- Livelock occurs when two or more threads are conceptually blocked forever, although they are each still active and trying to complete their task.
- gebeurt vaak als resultaat wanneer je een deadlock wilt voorkomen






## Race Conditions
- A race condition is an undesirable result that occurs when two tasks, which should be completed sequentially, are completed at the same time.
- For the exam, you should understand that race conditions lead to invalid data if they are not properly handled. Even the solution where both participants fail to proceed is preferable to one in which invalid data is permitted to enter the system.
- 

## Parallel Streams

- A parallel stream is a stream that is capable of processing results concurrently, using multiple threads.

### Calling parallel() on an existing Stream

```
Stream<Integer> s1 = List.of(1,2).stream();
Stream<Integer> s2 = s1.parallel();
```

### Calling parallelStream() on a Collection Object
```
Stream<Integer> s3 = List.of(1,2).parallelStream();
```

### PERFORMING A PARALLEL DECOMPOSITION

```

    public static void main(String[] args) {

        // feitelijk achter elkaar
//        long start = System.currentTimeMillis();
//        List.of(1,2,3,4,5)
//                .stream()
//                .map(w -> doWork(w))
//                .forEach(s -> System.out.print(s + " ")); // 12345

        // feitelijk naast elkaar
        long start = System.currentTimeMillis();
        List.of(1,2,3,4,5)
                .parallelStream()
                .map(w -> doWork(w))
                .forEach(s -> System.out.print(s + " ")); //3 4 5 2 1

        // naast elkaar maar in volgorde!
        List.of(5,2,1,4,3)
                .parallelStream()
                .map(w -> doWork(w))
                .forEachOrdered(s -> System.out.print(s + " ")); // 5 2 1 4 3 
    }

    private static int doWork(int input) {
        try {
            Thread.sleep(5000);
        } catch (InterruptedException e) {}
        return input;
    }


```


### PROCESSING PARALLEL REDUCTIONS

- Since order is not guaranteed with parallel streams, methods such as findAny() on parallel streams may result in unexpected behavior.
- Besides possibly improving performance and modifying the order of operations, using parallel streams can impact how you write your application. Reduction operations on parallel streams are referred to as parallel reductions. The results for parallel reductions can be different from what you expect when working with serial streams.

```
        System.out.println(List.of(1,2,3,4,5,6)
                .stream() .findAny().get());  // 1

        System.out.println(List.of(1,2,3,4,5,6)
                .parallelStream() .findAny().get()); // (vaak)4 (soms)1

        System.out.println(
                List.of(1,2,3,4,5,6).stream().unordered().findAny()); //Optional[1]
// unordedered can improve performance

```

### Combining Results with reduce()

```
System.out.println(List.of('w', 'o', 'l', 'f') .parallelStream()
.reduce("",
(s1,c) -> s1 + c,
(s2,s3) -> s2 + s3)); // wolf

```
`
- Intermediate result (s1 + c): o
- Intermediate result (s1 + c): f
- Intermediate result (s1 + c): w
- Intermediate result (s1 + c): l
- Combined result (s2 + s3): wo
- Combined result (s2 + s3): lf
- Combined result (s2 + s3): wolf
- Final result: wolf

`
## Order Order!
```
      System.out.println(List.of("w","o","l","f") .parallelStream()
                .reduce("X", String::concat)); // XwXoXlXf
        System.out.println(List.of("w","o","l","f") .stream()
                .reduce("X", String::concat)); // Xwolf
```


## Combining Results with collect()


```

<R> R collect(Supplier<R> supplier, BiConsumer<R, ? super T> accumulator, BiConsumer<R, R> combiner)


Stream<String> stream = Stream.of("w", "o", "l", "f").parallel();
SortedSet<String> set = stream.collect(ConcurrentSkipListSet::new,
Set::add,
Set::addAll);
System.out.println(set); // [f, l, o, w] natural soring dus alphabetish! 
```
## Requirements for Parallel Reduction with collect() 
- The stream is parallel.
- The parameter of the collect() operation has the Characteristics.CONCURRENT characteristic.
- Either the stream is unordered or the collector has the characteristic
Characteristics.UNORDERED.

`stream.collect(Collectors.toSet());  // Not a parallelreduction`

The Collectors class includes two sets of static methods for retrieving collectors, toConcurrentMap() and groupingByConcurrent(), that are both UNORDERED and CONCURRENT.


## Parallel reduction on a Collector
- Every Collector instance defines a characteristics() method that returns a set of Collector.Characteristics attributes. When using a Collector to perform a parallel reduction, a number of properties must hold true. Otherwise, the collect() operation will execute in a **single‐threaded** fashion.

### Requirements for Parallel Reduction with Collect()
- The stream is parallel.
- The parameter of the collect() operation has the Characteristics.CONCURRENT characteristic.
- Either the stream is unordered or the collector has the characteristic Characteristics.UNORDERED.

```
stream.collect(Collectors.toSet());  // Not a parallel reduction Set is unorded but is not concurrent characteristic
```
The Collectors class includes two sets of static methods for retrieving collectors, UNORDERED and CONCURRENT
- toConcurrentMap() 
- groupingByConcurrent()

```
Stream<String> ohMy =
Stream.of("lions","tigers","bears").parallel();
ConcurrentMap<Integer, String> map = ohMy
.collect(Collectors.toConcurrentMap(String::length, k -> k,
(s1, s2) -> s1 + "," + s2)); System.out.println(map); // {5=lions,bears, 6=tigers}
 System.out.println(map.getClass());
// java.util.concurrent.ConcurrentHashMap

// groupingby
var ohMy = Stream.of("lions","tigers","bears").parallel();
ConcurrentMap<Integer, List<String>> map = ohMy.collect(
Collectors.groupingByConcurrent(String::length));
System.out.println(map); // {5=[lions, bears], 6=[tigers]}
```


## Avoiding Stateful Operations
Side effects can appear in parallel streams if your lambda expressions are stateful. A *stateful lambda* expression is one whose result depends on any state that might change during the execution of a pipeline. On the other hand, a *stateless lambda* expression is one whose result does not depend on any state that might change during the execution of a pipeline.
```
public static List<Integer> addValues(IntStream source) {
   return source.filter(s -> s % 2 == 0)
                .boxed() .collect(Collectors.toList()); // zonder lambda
}
```
[prev](http://hjh.devsnips.nl/ocp17)
[next](http://hjh.devsnips.nl/ocp19)