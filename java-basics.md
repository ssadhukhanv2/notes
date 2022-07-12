## Basic **Incomplete!!** [Please complete it](https://github.com/Java-Techie-jt/interview-qa)





* [**JVM Garbage Collection**](https://www.freecodecamp.org/news/garbage-collection-in-java-what-is-gc-and-how-it-works-in-the-jvm/)
  * **Serial GC** -> All garbage collection events are executed sequentially one by one. Used for small application
  * **Parallel GC** -> Multiple thread for young generation. Single Thread for old generation Useful for medium sized application. 
  * **Parallel Old GC** -> Multiple threads for both old and young generation.
  * **Concurrent Mark and Sweep(CMS)** -> Minor and Major garbage collection is multithreaded but reduces stop the world events.
  * **G1 (Garbage First) GC** -> Divides the head into small chunks and performs garbage collection on each chunk
  * **ZGC** -> Introduced in java 11.Useful for ultralow latency applications

* [New Features of Garbage Collection in Java 8](https://www.overops.com/blog/garbage-collectors-serial-vs-parallel-vs-cms-vs-the-g1-and-whats-new-in-java-8/)
   * **String Deduplication** In java 8, the G1 collector idetifies all strings with the same value and makes them point to the same char[] array, this avoides multiple copies of the same string from residing inefficiently in the heap
   * **PermGen modifed to Metaspace** Devs need not manage the PermGen, instead Metaspace is managed by the JVM

* [What is the **difference** between **String.valueOf()** -> returns "null" if object is null else calls Object.toString() & **Object.toString()** -> throws NullPointer Exception](https://stackoverflow.com/questions/27465731/string-valueof-vs-object-tostring)
* [What do you mean by **immutable class**(final class with all members as final & private, no setters, only getters, instantiation done via deep-copy in parameterized constructor) in java and **how will you create immutable class in java**](https://www.javatpoint.com/how-to-create-immutable-class)
* [How have you used the pillars of OOPS **Encapsulation, Inheritance, Polymorphism, Abstraction** in your project](https://youtu.be/fFnuer3AD8Q?t=160)
* [When have you used **Run time Polymorphism** in your project](https://youtu.be/fFnuer3AD8Q?t=445)
* Can you overriide static method
* [Explain **exception hierarchy**, While overriding methods that throws exception, is it mandatory for the child method to thow exception](https://youtu.be/fFnuer3AD8Q?t=603)
* [Explain overriding methods works](https://youtu.be/fFnuer3AD8Q?t=536)
* [Can you **override static & private methods**, why](https://youtu.be/fFnuer3AD8Q?t=741)
* [Explain about **Default & Static methods for interfaces** introduced in java 8](https://youtu.be/fFnuer3AD8Q?t=1151)
* [What is the use of **AutoCloseable** Interface](https://www.baeldung.com/java-try-with-resources)
* [What is the difference between **final**(keyword), **finally**(block) & **finalize**(method)](https://www.javatpoint.com/difference-between-final-finally-and-finalize)

## Exception Handling
* [Exception Hierarchy](https://rollbar.com/blog/java-exceptions-hierarchy-explained/#:~:text=The%20class%20at%20the%20top,direct%20subclasses%20%2D%20Exception%20and%20Error.&text=The%20Exception%20class%20is%20used,application%20may%20need%20to%20handle.)

  * **Throwable**
    * **Error** : States from which he **application cannot recover**. Not surrounded by try/catch
      * OutOfMemoryError
      * StackOverFlowError
    * **Exception**
      * **Checked Exception**: *Directly extends throwable or Exception but don't extend RunTime Exception.* **Needs to be explicitly handled program with try/catch or throws**. 
        * IOException
        * InterruptedException
      * **Unchecked Exception**: *Extends the RunTimeException*. **No need to surround with try catch**.
        * ArithmeticException
        * NullPointerException


## [Collections](https://youtu.be/GO67C7V-IbQ?t=2722)

* [How will you initialize an ArrayList in a single line](https://www.baeldung.com/java-init-list-one-line)
* [Difference between **List**(allows access by index, allows duplicates) and **Set**(unique objects)](https://www.geeksforgeeks.org/difference-between-list-and-set-in-java/) [java-techie](https://youtu.be/GO67C7V-IbQ?t=170)
* [Difference between **LinkedList** & **ArrayList**. ----- **ArrayList** -> uses **dynamic array to store data**, implements Queue & List, **slower manipulation since shifting is required**) **LinkedList**->uses **doubly linked list** to store data, implements List, faster manipulation as it's **node based so not much shifting is required**](https://www.javatpoint.com/difference-between-arraylist-and-linkedlist)
* [What is the use of **transient** keyword](https://www.geeksforgeeks.org/transient-keyword-java/)
* [**Can you add new objects to final List, yes** but you can't reassign new List to it](https://youtu.be/GO67C7V-IbQ?t=422)
* [How will you create your own **custom ArrayList with no duplicates**](https://youtu.be/GO67C7V-IbQ?t=588)
* [Why does **HashSet** **doesn't allow duplicate values**-> because the **objects in a HashSet is stored as Keys within a HashMap**, Since HashMap keys are unique, items in HashSet is also unique](https://youtu.be/GO67C7V-IbQ?t=845)
* [Suppose you find a **HashSet has duplicate objects**, **what is possible wrong**? Probably the **contract for .equals() & .hashCode() is not properly implemented**](https://youtu.be/GO67C7V-IbQ?t=877)
* [Explain the **difference between Comparable and Comparator**](https://www.javatpoint.com/difference-between-comparable-and-comparator)
* [Create a comparator that will **sort based on id then based on name**](https://youtu.be/GO67C7V-IbQ?t=1667)
* [Difference between **fail fast and fail safe iterator**](https://www.javatpoint.com/fail-fast-and-fail-safe-iterator-in-java#:~:text=Difference%20Between%20Fail%20Fast%20and,an%20exception%20in%20such%20scenarios.)[Java Techie](https://youtu.be/GO67C7V-IbQ?t=1877)
  * **Fail fast iterator** -> fails fast when we do any modification while iterating a collection. **ArrayList, HashMap, Vector** checkForModification() throws Concurrent modification exception based on value of modCount.
  * **Non Fail fast iterator** -> iterator which doesn't allow us to modify while iterating the collection. **CopyOnWriteArrayList, CopyOnWriteArraySet, ConcurrentHashMap**
* [Explain the difference between **```ConcurrentHashMap```**(**synchronized**, applies lock on specific segment **segment level locking or bucket level locking**, when there is an **need for Concurrent Modification of Data**, **doesn't allow null values**) over **```HashMap```**(**non-synchronized, locks the entire object, concurrent modification not allowed**, allows **null values**)](https://www.geeksforgeeks.org/difference-between-concurrenthashmap-hashtable-and-synchronized-map-in-java/)
* [What is the difference between **HashTable** and **HashMap**](https://www.geeksforgeeks.org/differences-between-hashmap-and-hashtable-in-java/)
  * **HashTable** -> Null Values not allowed, Synchronized, Balanced Tree Feature of java 8 not available
  * **HashMap** -> Allows null value for key and value, Synchronized, Balanced Tree feature is available


* [Since ConcurrentHashMap & HashTable are both synchronized, **why will you prefer to use ConcurrentHashMap instead of HashTable**->because HashTable places lock on entire object while ConcurrentHashMap places lock at segment or bucket level](https://youtu.be/-oafFAPgLao?t=1083)
* [How does **HashMap internally work**-> initially 16 bucket(expanded based on load factor, default is 75% of the capacity) of LinkedList nodes, in each put operation has is calculated and put in respective LinkedList Node, if there is a HashCollision and the object is not equal, object is place at the end of the of the corresponding LinkedList node](https://www.geeksforgeeks.org/internal-working-of-hashmap-java/)[java techie](https://youtu.be/GO67C7V-IbQ?t=2731)
* [Where is null value placed in a **HashMap**, in the 0 bucket](https://youtu.be/GO67C7V-IbQ?t=3078)
* [What is **Rehashing in HashMap** When the number of items in the Map crosses the threshold limit, the capacity of the Map is doubled. As discussed earlier, when capacity is increased, we need to equally distribute all the entries (including existing entries and new entries) across all buckets. Here, we need rehashing.That is, for each existing key-value pair, calculate the hash code again with increased capacity as a parameter.](https://www.baeldung.com/java-hashmap-load-factor#:~:text=Capacity%20is%20the%20number%20of%20buckets%20in%20the%20HashMap.&text=Finally%2C%20the%20default%20initial%20capacity,increases%2C%20the%20capacity%20is%20expanded.)
* [**Advancement of HasMap in Java 8**->at any given point of time if the number of items in a bucket is more than TREEIFY_THRESHOLD, HashMap starts using BalancedTree instead of LinkedList](https://javarevisited.blogspot.com/2016/01/how-does-java-hashmap-or-linkedhahsmap-handles.html#axzz7UR2Yz9T0)
* [How **TreeMap works internally** -> Sorts based on key](https://www.geeksforgeeks.org/internal-working-of-treemap-in-java/?ref=rp)[javatechie](https://youtu.be/GO67C7V-IbQ?t=3271)
* [Why do we need a **WeakHashmap** in java. If any of the objects which are keys within a WeakHashMap are set set to null, that object becomes eligible for garbage collection and once gc happens the size of weakhashmap is reduced](https://www.baeldung.com/java-weakhashmap)


* List:
  * ArrayList 
  * LinkedList 
  * CopyOnWriteArrayList **Non-fail fast iterator**
* Set
  * HashSet 
  * LinkedHashSet
  * TreeSet
  * CopyOnWriteArraySet **Non-fail fast iterator**
* [Map]
  * HashMap -> No Sorting Order
  * LinkedHashMap -> Maintain the Sorting order
  * TreeMap -> Maintains default sorting order
  * ConcurrentHashMap -> No sorting order. **Non-fail fast iterator**



## Java 8
* [What is the difference between Terminal & Non Terminal Stream Operations](https://blog.knoldus.com/operations-in-java-streams/)
* [Interview Questions!!!](https://youtu.be/k7fNLXoVCYg?t=49)
* [You have a map of String names and Integer salary, how will you **increment the salary by 2000** ``BiFunction`` ``Map.replaceAll``](https://youtu.be/GADhzhK6NU0?t=929)
* [Find **nth Highest/Lowest element in a Integer stream** ``.distinct() .skip() .findFirst()``](https://youtu.be/Hwg4-kNBBUU?t=20)
* [**Sort a Map of Employees and their rating** in Ascending & Descending order ***SortEmployeesBasedOnRating***]
* [**Sort Employees** based on **decreasing order of salary** ***SortEmployeesBasedOnSalaryAndName***](https://stackabuse.com/java-8-how-to-sort-list-with-stream-sorted/)
* [Find **Frequency of Occurrence of each character** in a given string ***streams examples FindFrequencyOfEachCharacterInAGivenStream*** using **```groupingBy()```**](https://youtu.be/k7fNLXoVCYg?t=3076)
* [Find **Highest Paid Employee in Each Department** ***streams examples FindHighestPaidEmployeeInEachDepartment*** using **```groupingBy()```**](https://youtu.be/k7fNLXoVCYg?t=3400)
* [Find **Number of Balls of each color** ***streams examples FindNumberOfBallsOfEachColor*** using **```groupingBy()```**]
* [How will you use **.filter(), .map() .reduce()** to calculate **max, min, average** for employees with attribute grade as A ***streams FindMinMaxSumAverageSalaryOfEmployees***](https://youtu.be/ePJrt5-G8eM?t=8667)
* [Find **Employee with Longest Name** with **.map() .reduce()** ***FindEmployeeWithLongestName***]
* [Find Phonenumbers of Employees that starts with 9 using .flatMap() ***FindAllPhoneNumbersOfEmployeesThatStartsWith9***]

* **DateTimeApi**
  * [What are some of the **disadvantage of using the older java Date API**, ambiguous package structure, not thread safe, formatting is a challege, limited support for different timezones](https://youtu.be/G4wYN58xW0I?t=32)
  * [How will you **add 5 days, 5 years, 5 months, 5 years** to the current day **``.plusDays()``**](https://beginnersbook.com/2017/11/java-8-adding-days-to-the-localdate/)
  * [How will you **parse/format LocalDate** using **DateTimeFormatter**](https://youtu.be/G4wYN58xW0I?t=498)
  * [What is **ZonedDateTime**](https://youtu.be/G4wYN58xW0I?t=692)



* [Streams](https://www.geeksforgeeks.org/stream-in-java/#:~:text=A%20stream%20is%20a%20sequence,Arrays%20or%20I%2FO%20channels.)
* [**Streams** advantages](https://youtu.be/ePJrt5-G8eM?t=3239) 
  * [When to use **.parallelStream() vs .stream()**](https://youtu.be/ePJrt5-G8eM?t=9850)
  * [How will you use with **Comparator**.compare(a,b) .comparing(Object:getAttribute) & **Comparable** .compareTo(o) to sort a **List and Stream**](https://youtu.be/ePJrt5-G8eM?t=4594)
  * [How will you **sort a primitive types in a Map** using **```Map.Entry.comparingByKey() Map.Entry.comparingByValue()```**](https://youtu.be/ePJrt5-G8eM?t=5612)
  * [How will you use **flatMap()** to deal with **Stream of Streams** instead of map()](https://youtu.be/ePJrt5-G8eM?t=6417) 
  * [What is he use of **Optional**, difference between **```Optional.of()```** & **```Optional.ofNullable()```**, .**```orElse() .orElseGet(), .orElseThrows()```**](https://youtu.be/ePJrt5-G8eM?t=7408)
* [Functional Interfaces](https://youtu.be/ePJrt5-G8eM?t=183)
  * [How will you use **Comparator** as **lamda function**](https://youtu.be/ePJrt5-G8eM?t=1208)
  * [**Consumer** void accept(T t)](https://youtu.be/ePJrt5-G8eM?t=1656) [**Predicate** boolean(T test)](https://youtu.be/ePJrt5-G8eM?t=1762) [**Supplier** T get()](https://youtu.be/ePJrt5-G8eM?t=1839) [**Function** R apply(T t)](https://www.geeksforgeeks.org/function-interface-in-java-with-examples/)
  * [**BiFunction**](https://youtu.be/GADhzhK6NU0?t=228) [**BiPredicate**](https://youtu.be/GADhzhK6NU0?t=1908) [**BiConsumer**](https://youtu.be/GADhzhK6NU0?t=1369)

## Tasks

* [How will you implement **Exception Handling with CompletableFuture** !!INCOMPLETE!!](https://www.callicoder.com/java-8-completablefuture-tutorial/)
* [How does **ForkJoin** in Java !!INCOMPLETE!!](https://www.baeldung.com/java-fork-join)
* [What is the ideal thread pool size for **CPU Intensive Task**(numberOfCores+1) **``Runtime.getRuntime().availableProcessors()``** & **IO Intensive Task**(Max Number can be more but depends)](https://youtu.be/k7fNLXoVCYg?t=4263)
* [What is the difference between **CachedThreadPool**(grows in size till Integer.MAX_VALUE, threads that have not been used for 60 secs are automatically removed) and **FixedThreadPool** in java](https://www.tutorialspoint.com/difference-between-fixed-thread-pool-and-cached-thread-pool)
* [How will you use **CompletableFuture** to implement a **book Ordering System** in Java](https://www.baeldung.com/java-completablefuture)
* [How will you execute a **schedule a Runnable Task** to run every 5 secs with **ScheduledExecutorService**](https://www.baeldung.com/java-executor-service-tutorial)
* [How will you **execute a List of Callable** with the **ExecutorService** by using **```executorService.invokeAll(callableList)```** method](https://www.baeldung.com/java-executor-service-tutorial)
* [How will you use **Callable** call() and **Future** to calculate factorial of 10 BigIntegers in a **FixedThreadPool** of 10 Threads and print them. How will you **ensure TimeOutException is thrown** if any of the computation takes more than 10 secs by using **``future.get(10000, TimeUnit.MILLISECONDS)``** ***callableFutureFactorial Calculator***](https://www.baeldung.com/java-future) 
* [How will you use **RecursiveTask** and **ForkJoinPool** to calculate Factorial Sum of a number](https://www.baeldung.com/java-future)
* [What is the differece between between **Callable(returns a value) & Runnable(doesn't return a value) Tasks** executed by the **ExecutorService**](https://stackoverflow.com/questions/141284/the-difference-between-the-runnable-and-callable-interfaces-in-java#:~:text=The%20Callable%20interface%20is%20similar,cannot%20throw%20a%20checked%20exception.)




## Thread
* [jvm parameters in java](https://www.baeldung.com/jvm-parameters)

* [Explain the **Thread Life Cycles** )](https://www.javatpoint.com/life-cycle-of-a-thread)

* **``NEW``**
* **``RUNNABLE``** -> after .start() method is called
* **``RUNNING``** -> when the thread is scheduled by the Thread Scheduler and run() is called
* **``BLOCKED``** -> waiting to acquire a lock
* **``WAITING``** -> when .wait() or .join() is called
)
* **``TIMED_WAITING``** .sleep(timeOut) .join(timeOut) .wait(timeOut)

* [.wait() .notify() and nofifyAll()](https://www.tutorialspoint.com/importance-of-wait-notify-and-notifyall-methods-in-java#:~:text=The%20wait()%20method%20causes,waiting%20on%20that%20object's%20monitor.)
* [Use of **.join()** allows one thread to wait until other thread has finished execution.](https://www.javatpoint.com/java-join-method)
* [Use of **Thread.yield() Thread.sleep() Thread.join()**  yield()halts the currently executing thread and **gives chance to other waiting thread of the same priority**. If there are not waiting threads with **same** priority, the same thread will continue to execute](https://www.geeksforgeeks.org/java-concurrency-yield-sleep-and-join-methods/)

* [Implement a Stack by using lock free datastructure like **AtomicReference** !!INCOMPLETE!!](https://tcsglobal.udemy.com/course/java-multithreading-concurrency-performance-optimization/learn/lecture/11200112#reviews)
* [**Difference** between **.wait()** -> lock is released and **.sleep()** -> lock is not released](https://www.geeksforgeeks.org/difference-between-wait-and-sleep-in-java/)

* [How will you use lockfree datastructure **AtomicInteger, AtomicBoolean, AtomicLong** for eliminating the usage of lock within existing code](https://tcsglobal.udemy.com/course/java-multithreading-concurrency-performance-optimization/learn/lecture/11200098#reviews)
* [How will you use **Condition Variable** for inter thread communication](https://www.linkedin.com/learning/parallel-and-concurrent-programming-with-java-2/condition-variable-java-demo?autoSkip=true&autoplay=true&resume=false&u=2154233)
* [**ReentrantLock**, .lockInterruptably(), .lock() .tryLock(), unlock(), how will you prevent concurrent access to a shared datastructure](https://tcsglobal.udemy.com/course/java-multithreading-concurrency-performance-optimization/learn/lecture/11200020#overviews)
* [How will you **implement producer consumer** with **Semaphore**? ***Producer Consumer With Semaphore Demo***](https://tcsglobal.udemy.com/course/java-multithreading-concurrency-performance-optimization/learn/lecture/11200058#reviews)
* [ How does **ReentrantReadWriteLock** offer performance benefit over **ReentrantLock**, how will you use it to **efficiently control read/write to a shared datastructure**, so that it allows concurrent reads but prevents **concurrent write & write** operations](https://tcsglobal.udemy.com/course/java-multithreading-concurrency-performance-optimization/learn/lecture/11200026#overview)
* [How will you use **Thread.setDaemon(true)** & **Thread.join()** to ensure thatyour main thread waits for 2 secs for each of the child thread before it's terminated. Hint: **Factorial Demo** ](https://tcsglobal.udemy.com/course/java-multithreading-concurrency-performance-optimization/learn/lecture/11198682#overview)
* [Override Runnable vs extend Thread](https://www.baeldung.com/java-runnable-vs-extending-thread)
* [How will you use objects with **Synchronized** keyword to control access to **Critical Section** of Code ***Inventory Counter Demo***](https://tcsglobal.udemy.com/course/java-multithreading-concurrency-performance-optimization/learn/lecture/11200008#overview)
* [Since **assignment of primitive data type long & double** are not **non-atomic operations**, how will you **make them atomic using the `volatile` keyword**, How will you **create a atomic method** by using **Synchronized**. ***Metric Printer Demo***](https://tcsglobal.udemy.com/course/java-multithreading-concurrency-performance-optimization/learn/lecture/11200012#overview) [Readmore on **Volatile**..](https://docs.oracle.com/javase/specs/jls/se7/html/jls-8.html#jls-8.3.1.4)
* [How to **prevent a Data Race for incrementing & decrementing integers** by using the **`volatile`** keyword ***handle dataraces demo***](https://tcsglobal.udemy.com/course/java-multithreading-concurrency-performance-optimization/learn/lecture/11200014#overview)
  * **Race Condition:** multiple thread access a shared resource, atleast one thread modifies the resource, timing/scheduling of threads may cause incorrect result. May be **prevented with ``synchronized``(all cases but takes performace hit) or ``volatile``(read/write from/to long and double)**
  * **Data Race:** compiler reorders the program instruction to efficiently execute the code, this may lead to incorrect results in read. **May be prevented with Synchronized(takes performance hit) or by declaraing the shared variables as ``volatile``**
* [How will you implement **Fine grained locking**(by using more than one lock object with synchronized) **within a class having multiple shared objects**, How to **deal with deadlocks** while using ***synchronized*** by avoiding circular waits and **enforcing an order in lock acquisition** ***Train Crossing Demo***](https://tcsglobal.udemy.com/course/java-multithreading-concurrency-performance-optimization/learn/lecture/11200018#overview)
* [How can prevent a Singleton class from getting cloned-
we need to implement/override the clone() method and throw an exception
 CloneNotSupportedException from the clone method](https://dzone.com/articles/prevent-breaking-a-singleton-class-pattern#:~:text=Deserialization,will%20break%20the%20Singleton%20pattern.)


[Interview Set 1](https://www.youtube.com/watch?v=7h3YVojqR3Q&t=505)


11)what is ConcurrentHashMap
12)ConcurrentHashMap vs HashTable

13)What is Garbage Collection
14)If I create a Object where it will be created
15)Different parts of the Heap Memory

16)Which JDK version you are using
17)Features of Java 8
18)What is default methods in Java 8


22)How can we break the singleton pattern
23)Serialization and Deserialization issues with Singleton
24)what design patterns you have worked on?
25)What is factory design pattern- Spring Bean Factory
is example of Factory Design Pattern

26)Default scope of Bean
27)Different types of Bean Scopes
28)What is Dependency Injection
29)Types of Depedency Injection- Constructor and Setter Injection

30)How polymorphism works in Spring- explain @Qualifier

31)Have you worked on Spring Security? How it works

32)Advantages of Microservice over Monolith
33)How do you scale the Application using Kubernetes
34)How will you run the Docker image and deploy..tell the commands
35)Can we achieve auto scaling using Docker or is there any limitation

36)Can you tell the services in your microservices application
and how do they interact with each other

37)What is Pub/Sub in Kafka
38)How many subscribers can subscribe to the Topic
37What is the role of Broker in Kafka
38)Diff between Power Mock and Mockito

39)Methods supported by Stream- filter(),map(),flatMap()
40)How can you find the second largest number in a list of integers
41)Avg salary of each department using stream
42)How can you convert the list into Map
43)Method references in Java 8
44)JPA specification executor- u can use criteria

45)What is executor in context of Threads
46)How can you remove the duplicate elements from the array without using
any built in classes or methods

47)How do you reverse a singly linked list
48)what is doubly linked list,circular linked list


50)git commands, rebase