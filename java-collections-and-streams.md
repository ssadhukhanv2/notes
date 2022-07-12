* [Java Collections from basics to Advanced - Basics Strong
](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/)



# **Collections**

* [Difference between Arrays & Collection](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270290#overview)

    * Arrays are of fixed size, while Collections are growable in nature
    * Arrays can hold only homogeneous datatype, while Collections can hold homogeneous and heterogeneous data types
    * Arrays should be used in situation where the size of the elements are known in advance, while Collections can be used in scenarios where the exact size is unknown.
    * Arrays can hold only hold primitive datatypes while Collections can hold both Primitive & Object types.
    * With arrays there are no additional underlying datastructure, while each Collection has inbuild datastructure and algorithm.

* [Collections Framework](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270298#overview)

  * ``Collection``
    * ``List`` : Allows duplicates & preserves insertion order [Read More](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270332#reviews)
      * ArrayList
      * LinkedList (Also implements Dequeue)
      * Vector
        * Stack

    * ``Set`` : Does not allow duplicates [Read More](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270420#overview)
      * HashSet: Does not allow duplicate & does not preserve insertion order
        * LinkedHashSet: Does not allow duplicate but preserves insertion order
      * ``SortedSet``
        * ``NavigableSet``
          * TreeSet
    * ``Queue`` : FIFO
      * Dequeue
        * LinkedList (Also implements List)
      * PriorityQueue
      * BlockingQueue
        * PriorityBlockingQueue
        * LinkedBlockingQueue
  * ``Map``
    * HashMap
      * LinkedHashMap
    * WeakHashMap
    * IdentityHashMap
    * HashTable (this also implements ``Dictionary``)
      * Properties
    * ``SortedMap``
      * ``NavigableMap``
        * TreeMap


* [**Collection**](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270312#reviews) This is an interface. Set, List, Queue implements this interface. Collections has the following methods.
    * **add():** adds object to the collection. Returns True is the object is successfully added. Returns False if the object is can't be added. ``boolean add(Object o);`` 
    * **addAll()** adds a collection to the collection. ``boolean addAll(Collection c);``
    * **remove()** removes an element from the collection. ``boolean remove(Object o);``
    * **removeAll()** removes the elements in a given collections which is passed as parameter from a collection. ``boolean removeAll(Collection c);``
    * **retainAll()** Removes all elements from the collection apart from the ones in the collection passed in the argument ``boolean retainAll(Collection c);``
    * **clear()** Removes all elements from the collection. ``void clear()``
    * **contains()** Returns true if object is present. Returns false if object is not found. ``boolean contains(Object obj)``
    * **containsAll()** Returns true if all elements in Collection c are present in the invoking collection. ``boolean containsAll(Object obj)``
    * **isEmpty()** Returns true if collection is empty. ``boolean isEmpty()``
    * **size()** Returns the size of the collection. ``int size()``
    * **iterator()** Provides cursor to get objects of a collection one by one. ``Iterator iterator()``
    * **toArray()** Converts invoking collection to an array ``Object[] toArray()``

* [What is the difference between **Collection** and **Collections**](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270316#reviews)
 Collection is the base interface for the Collection framework.
 Collections is an utity class which defines methods such as sort(), reverse(), shuffle(), binarySearch(), disjoint() etc.


## **``List``** || **ArrayList** || **LinkedList** || **Vector** || **Stack**

* [Explain the properties of ArrayList](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270334#reviews)
  * Allows duplicate elements
  * Preserves Insertion order
  * Accepts heteregeneous elements(i.e if we don't specify a generic type, we can insert object of any type)
  * Accepts null values.
* [How does ArrayList internally work](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270334#reviews) If we don't specify a size ArrayList initially starts of with size of 10. Every time the ArrayList is fully filled up and a new item needs to be added a new array is allocated of size 10*3/2+1=16 & all the elements are copied to this new array along with the new element. The old array is garbage collected.  
* [What are some of the use cases for ArrayList](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270366#reviews) ArrayList implements Serializable & Cloneable making it good candidate for using it while trasferng data over network. It implements the RandomAccess marker interface. ArrayList supports random access by index in constant time, but since it internally uses resizable arrays, performace takes a hit if we need to delete/insert in the middle of the arraylist.

* [Explain the properties of LinkedList](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270336#reviews)
  * Allows duplicate elements
  * Preserves Insertion Order
  * Accepts heteregeneous elements(i.e if we don't specify a generic type, we can insert object of any type)
  * Accepts null values.
  * LinkedList also implements the DeQueue interface so it **``can be used as a queue``** using methods like **poll(), remove(), element(), peek()**

* [What is the difference between ArrayList & LinkedList](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270384#reviews)
  * **Internal Data Structure** ArrayList uses dynamic array to store elements while LinkedList uses doubly linked list to store the elements
  * **Data Insertion/Deletion** Insertion of data in the middle of the ArrayList is slow because internally it uses a dynamic array. And if any element is added/removed from the array, all the bits needs to be shifted in the memory. Manipulation with LinkedList is faster than ArrayList as it interally uses a doubly LinkedList so no shifting is required.
  * **Data Access:** Accessing data is faster in ArrayList as compared to LinkedList as within the ArrayList the array can be accessed via index. LinkedList is better suited for manipulating data quickly rather than accessing data requires traversal of nodes.

* [Explain the properties of Vector](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270336#reviews)
  * Legacy class.
  * Allows duplicate elements
  * Preserves Insertion Order
  * Accepts heteregeneous elements(i.e if we don't specify a generic type, we can insert object of any type)
  * Accepts null values.
  * Vectors are Thread safe.
  * Implements serializable, cloneable and Random Access Interface.

* [What is the difference between ArrayList and Vector](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270340#overview)
  * **Thread Safety** Methods in ArrayList are not Synchronized so they are not Thread safe. Methods in Vector are synchronized.
  * **Performance** Since ArrayList is not synchronized, performance of ArrayList is better as compared to Vector.
  * **Legacy** ArrayList is a non legacy class while Vector is a legacy class.
  * **Internal Size** If the ArrayList of capacity n is filled up of the dynamic array resized to ``n*3/2+1`` (i.e for 10 it would increase to ``10*3/2+1=15+1=16``), while incase of vector the capacity would be increased to ``n*2`` (i.e. for 10 it would be increased to ``10*2=20``)

* [Explain the properties of Stack](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270344#overview)
  * Allows duplicate elements
  * Preserves the insertion order
  * Accepts heterogeneous objects
  * Based on LIFO so ``push(), pop(), peek(), search()`` methods available

## **``Cursors``** || **Enumeration** || **Iterator** || **ListIterator** || **SplitIterator**
* [What are Cursors and what is the difference between Enumeration, Iterator, ListIterator](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270350#overview) Cursors allows us to traverse over elements of a collection object. 
  * **Enumeration**: 
    * Used with Legacy classes like Vector, Stack etc.
    * Only allows forward traversal. Allows reads.<br/>
  
  Code Snippet:

        
        Enumeration enumeration = vector.elements();
        while (enumeration.hasMoreElements()){
            System.out.println(enumeration.nextElement());
        }
  * **Iterator**: 
    * Can be used with any collection object. 
    * Only allows forward traversal. Allows read & remove access.<br/>
  
  Code Snippet:

        Iterator<Integer> iterator = arrayList.iterator();
        while (iterator.hasNext()) {
            Integer element = iterator.next();
            if(element==2){
                iterator.remove();
            }
        }

  * **ListIterator**: 
    * Can be only used with any List collection object. 
    * Allows  forward & backward traversal. 
    * Allows read, replace, add. <br/>
  
  Code Snippet:
        
        ListIterator<Integer> listIterator = arrayList.listIterator();
        while (listIterator.hasNext()) listIterator.next();
        while (listIterator.hasPrevious()) {
            Integer element = listIterator.previous();
            if (element == 1) {
                listIterator.add(9);//adds element after the current element
            }
            if (element == 2) {
                listIterator.set(5);
            }
            if (element == 3) {
                listIterator.remove();
            }
        }


  * **SplitIterator**


## **``Set``** || **HashSet** || **LinkedHashSet** || **``SortedSet``** || **``NavigableSet``** || **TreeSet**

* [Explain the properties of HashSet](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270426#overview)
    * Underlying Datastructure of HashSet is HashTable.
    * Doesn't allow duplicates.
    * Insertion order is not preserved.
    * Allows heterogeneous objects.
    * We can add null values.
    * Implements the Serializable and Cloneable interafaces


* [How does HashSet internally work and in what scenarios should you use HashSet](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270426#overview) When we perform add(obj) operation on a HashSet, the hashCode is calculated for the passed obj. If the ``capacity of the HashSet`` is ``"n"``, `hashcode of the object` is ``"h"``, then the object is placed at ``h%n`` position. ``LoadFactor`` represents at what level the hashSet capaciity is changed. **Default capacity of HashSet is 16 & default loadfactor is 0.75**. This means if we have a HashSet of capacity 16, it can atmost have ``16*75/100=12``  elements, after which a new hashtable is allocated with ``double`` capacity  where all elements are copied, and the old hastable is garabage collected. HashSet are good for quick data access, so if searching is a frequent operation we should go for HashSet.

        hashSet=new HashSet(100);// We can specify initial capacity in constructor
        hashSet=new HashSet(100, 0.95f);//Initial Capacity 100, Load Factor 0.95
        hashSet = new HashSet(Arrays.asList(1, 2, 3, 4, 3));// Hashset can also be initialized from list

* [Explain the properties of LinkedHashSet and how does it internally work](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270428#overview)

    * Underlying Datastructure of HashSet is a combination of LinkedList &  HashTable.
    * Preserves the insertion order.
    * Doesn't allow duplicates.
    * Allows heterogeneous objects.
    * We can add null values.
    * Implements the Serializable and Cloneable interafaces

* LinkedList Constructors:

        linkedHashSet = new LinkedHashSet(); //Default Initial Capacity 16, Load Factor 0.75
        linkedHashSet=new LinkedHashSet(100);// We can specify initial capacity in constructor
        linkedHashSet=new LinkedHashSet(100, 0.95f);//Initial Capacity 100, Load Factor 0.75
        linkedHashSet = new LinkedHashSet(Arrays.asList(1, 2, 3, 4, 3));// Hashset can also be initialized from list


* [Explain the properties of SortedSet](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270430#overview)
    * Insertion order is not preserved
    * Elements in the sorted set are ordered asper the natural sort order or by the Comparator passed in the constructor.
    * Allows only homogeneous elements because with hetergenous element we can't perform comparison
    * Provides methods like ``first(), last(), tailSet(), headSet(), comparator()``
* Common methods
    
        SortedSet<Integer> sortedSet= new TreeSet<Integer>(10,30,50,70,90,20,40,60,80);
        Integer result = sortedSet.first(); //10
        Integer result = sortedSet.last(); //90
        SortedSet<Integer> resultSet = sortedSet.headSet(50); // 10,20,30,40
        SortedSet<Integer> resultSet = sortedSet.tailSet(50); // 50,60,70,80,90
        SortedSet<Integer> resultSet = sortedSet.subSet(20, 80); //20,30,40,50,60,70
        Comparator comparator = sortedSet.comparator(); //return null incase of natural sort order


* [Explain the properties of NavigableSet](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14288684#reviews)
    * Insertion order is not preserved
    * Allows only homogeneous elements because with hetergenous element we can't perform comparison
    * Extends from SortedSet so all functionality of SortedSet like ``first(), last(), tailSet(), headSet(), comparator()`` are present
    * Along with that methods related to navigation is present like ``floor(), ceil(), higher(), lower(), pollFirst(), pollLast(), descendingSet()``

* Common Methods:

        NavigableSet<Integer> navigableSet=new TreeSet<Integer>(Arrays.asList(1000, 3000, 13000, 40000, 54000));
        
        Integer result = navigableSet.floor(13500); //13000 //returns greatest element which is less than or equal to argument

        Integer result = navigableSet.lower(14000); //13000//returns greatest element which is less than argument

        Integer result = navigableSet.ceiling(2500); //3000 //returns greatest element which is greater than or equal to argument

        Integer result = navigableSet.higher(4000); //13000 //returns greatest element which is greater than argument

        Integer result = navigableSet.pollFirst(); //3000, 13000, 40000, 54000 //returns and removes the first element
        
        Integer result = navigableSet.pollLast(); //1000, 3000, 13000, 40000 //returns and removes the last element
        
        SortedSet<Integer> resultSet = navigableSet.descendingSet();//54000, 40000, 13000, 3000, 1000 //returns the elements of the sorted set in a descending order


* [Explain the properties of TreeSet and how does it internally work](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270446#reviews)
    * TreeSet is the implementation class for NavigableSet & SortedSet. So it has all functionalities of NavigableSet and SortedSet.
    * Internally it uses a **BalancedTree**. So any new element which is added to TreeSet is checked against the root/current node, if it's greater than it's placed on the right, if it's smaller it's placed on the left. If the right or left of the root/current node is not leaf node, then recursive checking happens and the element is placed accordingly.
    * **Elements in TreeSet must implement the Comparable Interface** because the elements needs to be sorted in Natural Order if no Comparator is provided in the constructor.
    * **Add null to TreeSet results in NullPointerException.** TreeSet adds elements to it according to their natural order. This internally compares the elements with each other using the compareTo (or compare) method. If you try to compare any object with a null value using one of these methods, a NullPointerException will be thrown
    * Insertion order is not preserved
    * Allows only homogeneous elements because with hetergenous element we can't perform comparison
    * Extends from SortedSet so all functionality of SortedSet like ``first(), last(), tailSet(), headSet(), comparator()`` are present
    * Along with that methods related to navigation is present like ``floor(), ceil(), higher(), lower(), pollFirst(), pollLast()``

## **Comparable || Comparator**

[Comparable Vs Comparator](
https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270456#reviews)

* **Natural vs Custom Sorting order**: Comparable interface is used to sort the objects with natural ordering. Comparator is used to sort objects on an attributes which may not be same as the natural sorting order.
* **Comparable** compares the current object to the object specified in argument.<br/> With **Comparator** there are two objects specified in the method argument which is compared against each other.
* **Comparable** is present in ``java.lang.*`` package.<br/>
**Comparator** is present in  ``java.util.*`` package.
* To implement **Comparable** the original class needs to be modified.<br/> **Comparator** can be easily passed in stream operation or collection method arguments to define a custom sort order. The original class need not be modified.
* **Comparable** has the  ``public int compareTo(T o);`` to compare object to the current object. <br/>**Comparator** has ``int compare(T o1, T o2)`` & ``boolean equals(Object obj);``.

* **Why do we not need to provide implementation of equals() while working with Comparator?**
The parent of all class in java is the Object class which by default provides an implementation of the equals, this is why we don't need to provide implementation of the equals method while working with Comparator.


## **``Queue``** || **PriorityQueue**

* [Explain the methods in a queue](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14288674#reviews)
  * **``boolean add(T t)``** : adds element to the tail of the queue(or according to priority incase of priority queue)
  * **``boolean offer(T t)``** : adds element to the tail of the queue(or according to priority incase of priority queue)
  * **``E poll()``** : Retrieves and removes the head of this queue
  * **``E remove()``** : Retrieves and removes the head of this queue, but throws NoSuchElementException if queue is empty.
  * **``E element()``** : Retrieves the head of the queue without removing it.
  * **``E peek()``** : Retrieves the head of the queue & removes it. Throws NoSuchElementException if queue is empty
* [Explain the properties of PriorityQueue](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14288678#reviews)
  * Insertion order is not preserved but based on priority.
  * Duplicates & null values are not allowed.
  * Heteregeneous Objects are not allowed.

        priorityQueue = new PriorityQueue<Integer>(); //Default capacity is 11
        priorityQueue = new PriorityQueue<Integer>(100);
        priorityQueue = new PriorityQueue<Integer>(10, (a, b) -> b - a);

## **``Map``** || **HashMap** || **HashTable** || **LinkedHashMap** || **WeakHashMap** || **IdentityHashMap** || **SortedMap** || **NavigableMap** || **TreeMap**
* [Explain the properties of Map](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270508#reviews) 
  * Map is an interface present in the java.util.* package that represents a key and a value.
  *  Not extended from Collection class but is a part of the Collection framework.
  * Keys and Values are object references and can be of any type.
  * Duplicate Keys are not allowed.
  * There may be duplicate values present against different keys.
  * Each mapping is called Entry. So a map is a collection of Map.Entry objects. ;) 


* [Explain the functionality of different methods available as part of the Map Interface](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270508#reviews)
  * **size()** Returns the number of key value mappings in the map. **``int size()``**
  * **isEmpty()** Returns true if the map doesn't contain if there are no key value mapping **``boolean isEmpty()``**
  *  **containsKey()** Returns true if the map contains a mapping for the specified key. **``boolean containsKey(Object key)``**
  * **containsValue()** Returns true if the map contains a mapping for the specified value. **``boolean containsValue(Object value)``**
  * **get()** Returns value for the specified mapped key, if the mapping is not available returns null. **``V get(Object key)``**
  * **put()** The key value mapping is updated/inserted in the map. **``V put(K key, V value)``**
  * **remove()** Removes the mapping for a key from this map. If the no mapping is found returns null, else the previous value is returned. 
    * **``V remove(Object key)``** 
    * **``default boolean remove(Object key,
                       Object value)``**
  * **replace()** Replaces the entry for the specified key
    * **``default boolean replace(K key, V oldValue, V newValue)``**
    * **``default V replace(K key, V value)``**
  * **putAll()** Copies all mapping from the specified map in argument to the current map. **``void putAll(Map<? extends K,? extends V> m)``**
  * **clear()** Empties the map. **``void clear()``**
  * **keySet()** Returns a Set of Keys in the map **``Set<K> keySet()``**
  * **values()** Returns a collection view of the values withina map **``Collection<V> values()``**
  * **entrySet()** Returns a set of Map.Entry having the mappings within the map. **``Set<Map.Entry<K,V>> entrySet()``**
  * Other Methods: ``getOrDefault(), merge(), replaceAll(), putIfAbsent(), computeIfAbsent(), computeIfPresent(), compute()``

* [How does Hashing & HashTable work and what is the significance of equals() & hashCode() methods](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270524#reviews)
  * **hashCode() & equals()**:  hashCode() method returns a numeric value of an object in java. Object class by default provides implementation for both methods. We may provide custom implementation for hashCode() method but we need to remember that while overriding the hashCode() method we also need to override the equals() method, both should have the same contract.
  * **HashTable**: For adding new object to the HashTable the hash is calculated for the object. Say the hashCode is ``"h1"`` and the size of the HashTable is ``"size"``, then the object will be placed at ``"h1 % size"``. 
  * **Handling Hash Collisions**: HashTable may be implemented as a collection of LinkedLists, so that incase of Hash Collisions, where two objects are having the same hashCode, they are placed in the LinkedList at the corresponding index.
  Say we have elements A & B having the same hashCode 29 & the HashTable has size of ``25``. Then both the elements will be inserted into the LinkedList present at at index ``29 % 25 = 4``. 

* [Explain the properties of HashMap](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270526#reviews)
  * Insertion Order is not preserved.
  * Duplicate Keys are not allowed, duplicate values are allowed.
  * Allows a single null key.
  * Allows multiple null values.
  * Heterogeneous elements are allowed as both keys and values.
  * Implements Serializeable and Cloneable marker interfaces.
  * Extends AbstractMap class.
  * Best choice for search operations.
  * It uses hashing to store the data, the Hashing is applied on the key.
  * HashMap is a collection of nodes. 
  * Nodes in a HashMap has the following:
    * Hash
    * Key
    * Value
    * Next
  * [How does HashMap internally work](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270534#overview) Each time a new mapping needs to be inserted in a HashMap, the hashCode for the key is computed. It's modulo by the capacity of the HashMap and placed in the appropriate node index. Incase there is a Hash collision, a new node is added at the specified index.
  * Initial Capacity of HashMap is 16 & loadFactor is 0.75

* [Difference between HashMap & HashTable](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14270546#questions/17116044)
  * **Synchronization and Data Consistency:** 
    * HashMap is non synchronized so it's not thread safe which mean if more than one thread is using the same HashMap there may be data inconsistency. To get a synchronized version of the Map we may use the ``Collections.synchronizedMap(marksHashMap);`` method.<br/>
    * HashTable is synchronized so it's thread safe. More than one thread using the same HashTable doesn't lead to data inconsistency issues.
  * **Null Values**
    * HashMap allows a single null key and multiple null values.
    * HashTable does not allow null keys or values.
  * **Legacy vs NonLegacy**
    * HashMap is a NonLegacy class introduced in version 1.2 and it extends the AbstractMap class.
    * HashTable is a Legacy class and it extends the Dictionary class.
  * **Speed**
    * Since HashMap is not synchronized it's are much faster as compared to  HashTable which is synchronized and is thus slower.

* [Explain the properties of LinkedHashMap and how it's different from HashMap](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14288452#questions/17116044)
  * Same as HashMap with the below differences
  * LinkedHashMap uses LinkedList and HashTable as internal Datastructure while HashMap uses only HashTable as it's internal DataStructure
  * LinkedHashMap preserves the insertion order but with HashMap insertion order is not preserved.
  * LinkedHashMap and HashMap are both used to develop cache based applications.


* [Explain the properties of IdentityHashMap and how it's different from HashMap](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14288460#questions/17116044)
  * During put() operation when after the hashCode() is calculated on the key HashMap uses equals() to compare if the key already exists, but IdentityHashMap uses == operator to compare the keys.
  * This means that if there two different object references as keys, the map will have  two different mappings.<br/>
  **Code:** Even though subject1 & subject2 has the same string but the object references are different, so 2 entries are created as subject1==subject2 is evaluated to false.

        IdentityHashMap<String, Integer> identityHashMap = new IdentityHashMap<String, Integer>();
        String subject1 = new String("physics");
        String subject2 = new String("physics");
        identityHashMap.put(subject1, 90);
        identityHashMap.put(subject2, 80);
        Assertions.assertThat(identityHashMap)
        .hasSize(2).contains(Assertions.entry(subject1, 90),
                Assertions.entry(subject2, 80));


* [Explain the properties of WeakHashMap and how is it different from HashMap](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14288696#questions/17116044)
  * **WeakHashMap uses Weak References while HashMap uses Strong References**
    * WeakHashMap uses weak references as Keys. This means incase of WeakHashMap if an object which is a key in the weakhashMap is set to null, it's garbage collected  and the size of the weakHashMap is reduced.
    * HashMap uses strong references as Keys. HashMap key references are not garbage collected if they are set to null.
  * Serializable & Cloneable Interfaces are not implemented by WeakHashMap but HashMap implements them.

        public class TempElement {
            public String toString() {
                return "Temp Element";
            }
            protected void finalize() {
                System.out.println("Temp Element is Garbage Collected");
            }
        }
        WeakHashMap weakHashMap = new WeakHashMap();
        TempElement tempElement = new TempElement();
        weakHashMap.put(tempElement, 9);
        Assertions.assertThat(weakHashMap).hasSize(1);
        tempElement = null; //tempElement set to null, so it becomes eligible for garbage collection
        System.gc();
        Thread.sleep(3000);
        Assertions.assertThat(weakHashMap).hasSize(0);// System.gc() has been called so the size of the weakHashMap is reduced


* [Explain the characteristics of SortedMap](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14288466#questions/17116044) 
  * In SortedMap the Entries are sorted in Natural Ascending order of Keys or by the specified Comparator.
  * Null keys and values are not allowed.
  * Methods include ``subMap(), headMap(), tailMap(), firstKey(), lastKey()``

* [Explain the properties of NavigableMap](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14288468#questions/17116044)
  * Sorted by Natural order of Keys or based on custom Comparator.
  * Null keys and values are not allowed.
  * Sub interface of SortedMap so it has all the functionalities of SortedMap. ``subMap(), headMap(), tailMap(), firstKey(), lastKey()``
  * Contains methods related to navigation. ``ceilingEntry(), floorKey(), higherKey(), lowerKey(), ceilingKey(), descendingKeySet(), descendingMap(), headMap(), higherEntry(), navigableKeySet()``

* [Explain the properties of TreeMap](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14288472#questions/17116044)
  * InsertionOrder is not preserved.
  * TreeMap uses a red-black self balancing binary tree.
  * TreeMap is the implementation class of SortedMap & NavigableMap
  * Sub interface of SortedMap so it has all the functionalities of SortedMap. ``subMap(), headMap(), tailMap(), firstKey(), lastKey()``
  * Sub Interface of Navigable Map so has methods ``ceilingEntry(), floorKey(), higherKey(), lowerKey(), ceilingKey(), descendingKeySet(), descendingMap(), headMap(), higherEntry(), navigableKeySet()``
  * Duplicate keys are not allowed. 
  * For TreeMap that's created with without custom comparator as contstructor argument, the Keys of the TreeMap should be homogeneous and implement comparable else there are chances of ClassCastException.
  * Incase Comparator is passed as Contructor argument, keys may be heterogeneous.
  * Null keys are not allowed.
  * May contain null values.


## **Concurrent Collections** || **ConcurrentHashMap** || **CopyOnWriteArrayList** || **CopyOnWriteArraySet**

* [Why do we need Concurrent Collection](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14269570#questions/17116044) Since the regular collections are not synchronized using them in multithreaded environment may lead into **data inconsistency**. We may used the following methods to get synchronized version for List, Set, Map:
    * Collections.synchronizedList(list);
    * Collections.synchronizedMap(map);
    * Collections.synchronizedSet(set);<br/>

  Or we may choose to use the below legacy classes which are synchronized:
    * Vector
    * Stack
    * HashTable<br/>
  
  However the issue with these collections is that synchronization is achieved by **putting lock on the entire object** which makes them less efficient.
  
  <br/> Concurrent Collections like ``ConcurrentHashMap, CopyOnWriteArrayList, CopyOnWriteArraySet`` solved these problems by introducing locking at a segment level instead of locking the full datastructure. So they were introduced to overcome the challenges with the earlier datastructures.


* [Explain about ConcurrentModificationException](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14269580#questions/17116044)
 While iterating a collection using fail fast iterators, if the underlying collection is modified,  ConconcurrentModificationException may be thrown.

        List<String> list = new ArrayList<String>();
        list.add("bob");
        list.add("sally");
        list.add("charlie");
        Iterator<String> iterator = list.iterator();
        while (iterator.hasNext()) {
            if (iterator.next().equals("sally")) {
                list.add("john");//ConcurrentModificationException
            }
        }

 * **Fail fast iterators**: Some iterators that throw ConcurrentModificationException if the underlying collection is modified while iterating over them, these iterators are know as FailFastIterator. Example iterators of ArrayList, HashMap, Vector etc.
  * **Non Fail fast iterator**: Iterators of CopyOnWriteArrayList, CopyOnWriteArraySet, ConcurrentHashMap doesn't allow modification of the collection while iterating over them so these are the non fail fast iterators.

  * Concurrent Collection Hierarchy
    * Collection
        * ``Map``
            * ``ConcurrentMap``
                * ConcurrentHashMap 
        * ``List``
            * CopyOnWriteArrayList
        * ``Set``
            * CopyOnWriteArraySet



  * [Explain the properties and inner working of ConcurrentHashMap](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14269632#questions/17116044)
    * Inner Working:
        * The buckets of ConcurrentHashMap are grouped into regions. The total number of regions is called the Concurrency Level. While reading data there is no locks but while writing data locks are placed on the region that is being written to. 
        * By default the capacity is 16, which means there are 16 buckets.
        * The concurrentLevel is set to 16 so there would be 16 regions. Lock may be placed on any of these regions if threads are writing to them. 
        * The loadfactor is set to 0.75, so the capacity would be doubled if 75% of the ConcurrentHashMap is filled up. 
    * ConcurrentHashMap only locks a portion of the collection on update.
    * ConcurrentHashMap is much better than HashMap & HashTable 
      * HashMap is not thread safe, so in a multithreading environment this may lead to data inconsistency issues.
      * HashTable is thread safe but the full object is locked during read or write, this leads to poor performance.
      * With ConcurrentHashMap there is no lock during read, lock is placed  on a specific segment during write. This leads to better performance. So it's thread safe and at the same time handles concurrency much better.
    * Null Keys are not allowed.
    * Level of Concurrency may be choosen by the programmer, the default is 16.
    * Iterator of CurrentHashMap is fail safe.
    
            ConcurrentHashMap<Integer, String> stringConcurrentHashMap = new ConcurrentHashMap<Integer, String>(16,0.75f,16);

    
* [How does CopyOnWriteArrayList internally work](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14269652#questions/17116044) 
  * CopyOnWriteArrayList is a thread safe version of ArrayList. If multiple threads are operating on a CopyOnWriteArrayList for read operation there is no locks but incase of a write operation a the internal datastructure is cloned and the write is performed on the cloned object rather than the actual object. Later these two objects are synced internally be the JVM. This is how CopyOnWriteArrayList achieve thread safety.
  * Iterator of CopyOnWriteArrayList is fail safe but does not support .remove() method as it may cause inconsistency during sync. UnSupportedOperationException is thrown.
  * Please note there is a performance overhead in cloning so we should be use this collection carefully.


 * [How does CopyOnWriteArraySet internally work](https://tcsglobal.udemy.com/course/collections-and-concurrent-collection-video-lectures-and-tutorials/learn/lecture/14269670#questions/17116044)
    * Same as CopyOnWriteArrayList
    * Read operation happens on the actual internal datastructure while incase of write operation the datastructure is cloned and write is performed o this cloned object. The clone and the original object is later synced internallyby the JVM.
    * Iterator is failsafe.
    * Performance overhead is present.



