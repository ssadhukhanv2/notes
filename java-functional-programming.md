* [Functional & Reactive programming in Java : Modern Style - Basics Strong](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977295#overview)
* [Functional Programming with Java Streams](https://tcsglobal.udemy.com/course/functional-programming-with-java/)

# **Functional Programming**


## **Functional Interface || Lambda || Imperative vs Declarative vs Functional Programming**

* [What is Lambda](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977241#announcements) 
  * Lambda is the building block for functional programming. It's a function without a name and is also known as anonymous function. 
  * Allows passing behaviours.
  * Lambdas are smart anonymous functions, they use type inference and dynamic type languge like features using already existing **InvokeDynamic** functionality.
  * Apart from reducing the lines of code, it **reduces the memory footprint** as compared to using anonymous inner classes.

        ()->System.out.println("Hello World");

* [What is a Functional Interface](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977243#announcements) Functional Interface has a single abstract method, they are used to create lambdas. The main reason of having a single abstract method within a functional interface is elminate any abmiguity regarding the method that will be invoked incase a lambda is fired.
  * Lambda's are backed by functional interfaces so if we need to write lambda we need functional interfaces.
  * With Lambda we can change behavior on the fly.


        @FunctionalInterface
        public interface MyFunctionalInterface {
            public void myAbstractMethod();
        }
        public class MyFunctionalInvoker {
            public void invokeMyFunctionalInterface(MyFunctionalInterface myFunctionalInterface){
                myFunctionalInterface.myAbstractMethod();
            }
        }
        MyFunctionalInvoker myFunctionalInvoker = new MyFunctionalInvoker();
        myFunctionalInvoker
                .invokeMyFunctionalInterface(() -> System.out.println("Hello World")));


* [Generic Functional Interface](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977161#announcements)

        @FunctionalInterface
        public interface MyGenericFunctionalInterface<R, T> {
            public T execute(R r);
        }

        MyGenericFunctionalInterface<String, String> stringLambda = s -> s.substring(2);
        String resultStr = stringLambda.execute("HelloWorld");
        MyGenericFunctionalInterface<String, Integer> intLambda = s -> s.length();
        int resultInt = intLambda.execute("HelloWorld");

* [What is the advantage of using Lambda as compared to using anonymous inner classes](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977245#announcements)
  * **Using Lambda is much lightweight as Compared to Anonymous Inner Classes:** Each implementation of a Functional Interface using Anonymous Inner is compiled as a separate class. These additional classes makes .jar more bulky. Lambda's takes advantage of InvokeDynamic feature so we can have any many implementation of lamda without creating separate classes.
  **``InvokeDynamic``** is a jvm feature that came with java 1.7. It is a byte code instruction that facilitates implementation of dynamic languages through dynamic method invocaton. Scala and other language is already taking advantage of this. Invoke dynamic is a benefit for statically type programming languge like java which allows us to provide method implementation at runtime using lambda.


* [Explain the differences between Imperative vs Declarative/Functional way of writing code and the advantages](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977247#announcements)

    * **Imperative Programming:** Here programmer  says how to do it.<br/>
        * Code has much more variable mutations.
        * We are doing explicit mutation of the variable sumOfEvens
                
                public void testSumImperative() {
                    //Imperative
                    int sumOfEvens = 0;
                    for (int i = 0; i <= 100; i++) {
                        if (i % 2 == 0)
                            sumOfEvens += i;
                    }
                    Assertions.assertEquals(2550, sumOfEvens);
                }
    * **Delarative Programming:** Here programmer says what to do instead of how to do it. It's much more consise.
        * **Functional Programmming** This is a subset of declarative programming.
            * Code looks Much more readable and consise.
            * Variable Mutations are taking place under the hood and is taken care by the jvm. The final sum is then assigned to sumOfEvens.
            * The code is thread safe and performs much better in multithreaded environments.

                    public void testSumDeclarative() {
                        //Declarative (Functional)
                        int sumOfEvens = IntStream.rangeClosed(0, 100)
                                .filter(i -> i % 2 == 0)
                                .reduce(0, (a, b) -> a + b);
                        Assertions.assertEquals(2550, sumOfEvens);
                    }



## **``Predefined Functional Interfaces`` || Predicate || Consumer || Function || Supplier || UnaryOperator || BiFunction ||BinaryOperator || BiPredicate || BiFunction**

* [Explain the predefined functional interfaces and their specialized classes](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977157#announcements)

* **Predicate\<T>** ||  T->boolean || take type T and returns boolean || **``boolean(T test)``**
  * ``IntPredicate, LongPredicate, DoublePredicate``
* **Consumer\<T>**  ||  T->void  || takes type T but doesn't return any thing ||  **``void accept(T t)``**
  * ``IntConsumer, LongConsumer, DoubleConsumer``
* **Function\<T,R>** || T->R || Takes type T and returns R || **``R apply(T t)``**
  * ``IntToDoubleFunction, IntToLongFunction, LongToDoubleFunction, LongToIntFunction``
  * ``IntFunction<R>, LongFunction<R>, DoubleFunction<R>, ToIntFunction<T>, ToDoubleFunction<T>, ToLongFunction<T>``
* **Supplier\<T>**  || ()->T || takes nothing but returns an elemnt of Type T || **``T get()``**
  * ``BooleanSupplier, IntSupplier, LongSupplier, DoubleSupplier``
* **UnaryOperator\<T>** || T->T || Similar to Function, however it take argumument of type T and returns object of the same type.
  * ``IntUnaryOperator, LongUnaryOperator, DoubleUnaryOperator``
* **BiFunction\<T,U,R>** || T,U,R->R || Similar to Function, this has 3 generic types. So it takes 2 arguments of type T & U and returns eleement of type R.
  * ``ToIntBiFunction<T,U>, ToLongBiFunction<T,U>, ToDoubleBiFunction<T,U>``
* **BinaryOperator\<T>** || T,T->T || Similar to Function, however it takes two arguments of type T and returns an object of the same type
  * ``IntBinaryOperator, LongBinaryOperator, DoubleBinaryOperator``
* **BiPredicate\<L,T>** || L,R->boolean || Similar to Predicate, takes two argument of type L & T and returns a boolean
* **BiConsumer\<U,T>** || T,U-> void || Similar to Consumer,, however this takes two argument of type U & T but doesn't return anything.
  * ``ObjIntConsumer<T>, ObjLongConsumer<T>, ObjDoubleConsumer<T>``


* [Explain how Predicate works](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977165#announcements) Predicate is a functional interface with method **``boolean(T test)``**. So it take an argument of type T and return a boolean based on our implementaion.
    
      public <T> List<T> filterList(List<T> list, Predicate<T> predicate) {
        List<T> resultList = new ArrayList<>();
        for (T t : list) {
            if (predicate.test(t))
                resultList.add(t);
        }
        return resultList;
      }
      
      List<String> stringList = Arrays.asList("hello", "", "world", "");
      Predicate<String> stringPredicate = (s) -> !s.isEmpty();
      Assertions.assertThat(filterList(stringList, stringPredicate))
                .contains("hello", "world");


* [Explain how Consumer works](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977167#overview) Consumer is a functional interface with method **``void accept(T t)``**. So it takes an argument of type T and performs some operation on the argument based on our implementaion. It doesn't return anything.

        public <T> void printElementsFromList(List<T> list, Consumer<T> consumer) {
            for (T t : list) {
                consumer.accept(t);
            }
        }
        
        List<Integer> integerList = List.of(34, 68, 8, 23, 67, 89, 90);
        Assertions.assertDoesNotThrow(() -> printElementsFromList(integerList, System.out::println));
      

* [Explain how Supplier works](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977169#overview) Supplier is a functional interface with method **``T get()``**. It's used to produce results without taking any inputs.

        Supplier<Double> randomSupplier = () -> Math.random();
        Assertions.assertInstanceOf(Double.class, randomSupplier.get());


* [Explain how Function work](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977171#overview) Function is a functional interface with methods **``R apply(T t)``**. It's generally used for transformation purposes.

        private static <T, R> List<R> applyFunctionOnList(List<T> list, Function<T, R> function) {
            List<R> sizeList = new ArrayList<R>();
            for (T element : list) {
                sizeList.add(function.apply(element));
            }
            return sizeList;
        }

        List<String> stringList = Arrays.asList("Tick", "Tack", "Toe");
        List<Integer> sizeList = applyFunctionOnList(stringList, (str) -> str.length());
        Assertions.assertThat(sizeList).containsExactly(4, 4, 3);


* [Explain how UnaryOperator works](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977175#overview) Unary operator extends from Function, but it accepts a single argument and returns an object of the same type. Unary operator itself doesn't contain any abstract method but since it extends the Function interface, it inherits the ``R apply(T t)`` method, but since it has a single generic type the method functions behaves like ``T apply(T t)``.<br/>
We typically use unary operator in scenarios where we need to return a function with same type parameter.

        public <T> List<T> transformList(List<T> list, UnaryOperator<T> unaryOperator) {
            List<T> transformedList = new ArrayList<T>();
            for (T t : list) {
                transformedList.add(unaryOperator.apply(t));
            }
            return transformedList;
        }
        List<Integer> integerList = Arrays.asList(1, 2, 3, 4, 5);
        UnaryOperator<Integer> unaryOperatorMultiplyBy100 = (a) -> a * 100;
        List<Integer> resultList = transformList(integerList, unaryOperatorMultiplyBy100);
        Assertions.assertThat(resultList).containsExactly(100, 200, 300, 400, 500);


* [Explain how BiFunction works](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977177#overview) BiFunction has abstract function ``R apply(T t, U u)`` accepts two arguments which may be of different types and may return a transformed object of third type.

        BiFunction<String, String, Integer> biFunction = (a, b) -> (a + b).length();
        int result = biFunction.apply("hello", "world");
        Assertions.assertEquals(10, result);


* [Explain how BinaryOperator works](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977181#overview) BinaryOperator takes two arguments of the same type and returns a transformed object of the same type. Binary operator itself doesn't have any abstract methods but since it extends from BiFunction it inherits the abstract function ``R apply(T t, U u)``, but since it has a single generic type, the function behaves like ``T apply(T t1, T t2)``

        BinaryOperator<String> binaryOperator = (a, b) -> a + "." + b;
        String result = binaryOperator.apply("subhrajit", "sadhukhan");
        Assertions.assertEquals("subhrajit.sadhukhan", result);



## **Method Reference || Constructor Reference**

* [Why do we need Method Reference](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977123#questions/11094811) With Functional Interface  we can pass behaviour on the fly by writing Lambdas, but there may be situations where we may need to executed preexisting class methods as Lambdas. This can be achieved using Method Reference.
    * Method reference makes the code even more consise and readable.
    * Within Method reference we can avoid writing the same implementation over and over again in lamdas.
* [What is a Method Reference](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977133#questions/11094811) Method reference is a way of executing pre-existing methods of classes as Lambda functions.

        <T> void printElements(List<T> list, Consumer<T> consumer) {
                for (T t : list) {
                    consumer.accept(t);
                }
            }
        List<Integer> integerList = List.of(89, 78, 34, 645, 12, 67, 88);
        //Consumer
        Consumer<Integer> consumer = System.out::println;
        printElements(integerList, consumer);
        //Supplier
        Supplier<Double> supplier = Math::random;
        Assertions.assertDoesNotThrow(() -> System.out.println(supplier.get()));
    

    * [Method Reference Types:](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977133#questions)
      * **object::instanceMethod**: Method reference to an instance of an existing object.
              
              Consumer<Integer> consumer = System.out::println;
      * **Class::staticMethod**: Method reference to a static method of a class.
              
              Supplier<Double> supplier = Math::random;
      * **Class::instanceMethod**: Method reference to an instance of a class.

              Function<String> function=String::length;
      * **Class::new** Method Reference to a constructor of a class. [Read more..](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17977135#questions)

            Function<Runnable, Thread> threadGenerator = Thread::new;
            Runnable r1 = () -> System.out.println("First Thread");
            Runnable r2 = () -> System.out.println("Second Thread");
            Runnable r3 = () -> System.out.println("Third Thread");
            threadGenerator.apply(r1).start();
            threadGenerator.apply(r2).start();
            threadGenerator.apply(r3).start();


## **Functional Programming**

* [Explain what is Functional Programming and how is it different from Imperative Programming](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17976333#questions/11094811)  Functional programming is a declarative programming paradigm where we write everything in **``pure mathemetical functions``**. 
    * **Pure Mathemetical Functions**: The job of a pure mathemetical function is to perform calculation on the basis of provided algorithm and data. It should not have any effect on the outer environment, i.e **``it does not change object state``** It just uses the provided data to perform calculation.
    * **Focuses on what to solve rather than how to solve it** Instead of writing statements one after the other Functional programming makes use of expressions.
    * **Based on Lambda calculus** Lamda calculus forms the basis of all functional programming language. Lambda expressions were introduced in java 1.8
    * **Difference with Imperative Programming** Functional programming coexists with imperative programming but there are some differences and not one is better than the other.
        * **Object State Modification** In imperative programming we typically modify the object state within a function and return the the modified state of the object from the method. So with OOPs we typically modify the outer environment as it changes object states. But with functional programming the object state remains unchanged.
        * **Method Arguments** 
        In OOP or the imperative type we pass objects to method arguments and return objects<br/> 

                Object method(Object obj);
        
          With Functional Programming we can pass a Function to a method argument and return a function.
                
                Supplier method(Function fun);



## **``Functional Programming Concepts``** || **Functions As First Class Citizens || Pure Functions - No side effects || Higher Order Function || Referential Transperency**

* [Functional Programming Concepts](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17976337#questions/11094811)
  * Functions as First Class Citizens/Higher Order Function
  * Pure Functions
  * Referencial Transperency

* [Explain what you mean by Functions as First Class Citizens](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17976341#questions/11094811) Programming languge that supports Function as **first class citizens** should be able to: 
    * Pass functions as method arguments
    * Return functions as return type of methods
    * Store function in data structures.
        
            public Function method(Function function) {
            return function;
            }
            Function function = method((a) -> a.toString());

* [What are Higher Order Functions](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17976355#questions/11094811) Higher order functions are functions that do any of the following:
    * Accept argument as function/lambda
    * Return function/lambda.
    * Both accept and return function/lambda as lambda argument or return type.

* [Explain the characteristics of Pure Functions](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17976347#questions/11094811) A pure function has the following characteristics.
    * The output of a pure function depends only on:
        * it's input parameters.
        * it's internal algorithm.<br/>
    This means if we call a pure function with the same set of parameters we will get the same result.
    * It does not modify the parameters passed to them.
    * A pure function doesn't have any side effects. Side effect means anything that a method does apart from computing or return a value. So a pure function will not read or write from the outside world, it will not change the instance fields in the class, it doesn't perform a webservice call, it doesn't read/write data from database, it should not write to console, file, network connection etc. Basically it has no affect or relevance on the changes in the outside world, apart from the parameters passed to it and the algorithm it implements.
    * Pure function calls can be substituted with their return values without any changes in behavior.


            String.upperCase();
            String.lowerCase();
            Math.min();
            Math.max();
        
      Note that **Consumer is not a pure function** as it's expected to have side effects.

    * Advantages:
      * Provides clarity of though & is easy to reason about, as Pure Functions are like black box and once they implemented their complexities can be put aside and you then you then can use them as building blocks for computing operations of ascending complexity.
      * Since they do not alter shared state or variables pure functions can be used in multithreaded programs without additional complexity.

* [Explain what is Referential Transparency](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17976361#questions/11094811) Referential Transparency is a property of a function, variable or expression where by the function/expression can be replaced by it's evaluated value.
Pure functions are typically Referentially Transparent.<br/>
    * Functional programming avoids functions which are not referentially transparent.
    * Referential transparency makes reasoning about programs much easy which makes them much more readable.
    * It makes subprograms independent which makes them easy for unit testing and refactoring.

            
            public class PureFunction {
                public int pureFunctionSum(int a, int b) {
                    return a + b;
                }
            }
            PureFunction pureFunction = new PureFunction();
            int result1 = pureFunction.pureFunctionSum(
                    pureFunction.pureFunctionSum(50, 50),
                    pureFunction.pureFunctionSum(150, 50)
            );
            int result2 = pureFunction.pureFunctionSum(100, 200);
            Assertions.assertEquals(result1, result2);


## **``Functional Programming Techniques``** || **Chaining || Composition || Closures || Currying || Lazy Evaluation || Tail Call Optimization**


* [What is method chaining](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17976603#questions/11094811) Function chaining is a technique where we can chain functions one after the other in a in a single statement without needing additional parameters to store intermediate results. 
  * It is used to simplify code where multiple functions are called in sequence one after the other.

        
        @FunctionalInterface
        public interface MyConsumer<T> {
            void accept(T t);
            default MyConsumer<T> thenAccept(MyConsumer<T> myConsumerNext) {
                Objects.requireNonNull(myConsumerNext);
                return (T t) -> {
                    this.accept(t);
                    myConsumerNext.accept(t);
                };
            }
        }        
        MyConsumer<String> myConsumer1 = s -> System.out.println(s);
        MyConsumer<String> myConsumer2 = s -> System.out.println(s);
        MyConsumer<String> myConsumer3 = s -> System.out.println(s);
        MyConsumer<String> myChainedConsumer = myConsumer1.thenAccept(myConsumer2).thenAccept(myConsumer3);
        Assertions.assertDoesNotThrow(() -> myChainedConsumer.accept("Hello"));

  * When we chain Function, the first function is executed first, then the next function is executed on the result returned by the first function.

        Function<Integer, Integer> function1 = f -> f * 10;
        Function<Integer, Integer> function2 = f -> f + 10;
        Function<Integer, Integer> function3 = f -> f - 5;
        Function<Integer, Integer> chained = function1.andThen(function2).andThen(function3);
        Integer result = chained.apply(9);
        Assertions.assertEquals(9 * 10 + 10 - 5, result);


* [What is Function Composition](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17976607#questions/11094811) Function Composition takes a reverse approach to chaining, this means that if two functions a & b are composed in order ``a.compose(b)``. b is first executed and a is executed on the result of b.

        @FunctionalInterface
        public interface MyFunction<T, R> {
            R apply(T t);
            default <V> MyFunction<V, R> compose(MyFunction<V, T> before) {
                Objects.requireNonNull(before);
                return (V v) -> this.apply(before.apply(v));
            }
        }
        MyFunction<Square, Integer> getAreaFromSquare = square -> square.getArea();
        MyFunction<Integer, Double> getSideFromArea = area -> Math.sqrt(area);
        MyFunction<Square, Double> getSideFromSquare =
                getSideFromArea.compose(getAreaFromSquare);
        Square square = new Square(100);
        Double result = getSideFromSquare.apply(square);
        Assertions.assertEquals(10, result);



* [What is closure in context of functional programming](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17976613#questions/11094811)  A closure is a ``function``(or ``method``) that refers to ``free variables`` in their lexical ``context.`` 
  * **``function``** is a block of code, it may produce a result
  * **``free variable``** is an identifier used but not defined by the closure.
  * **``lexical context``** or lexical scope is a convention that sets the scope of variable so that it may only be called from within the block of code in which it's defined.
  
        @FunctionalInterface
        public interface Task {
            void doTask();
        }
        class ClosureTest {
            @Test
            void testClosure() {
                int val = 8080;
                Task task = () -> {
                    System.out.println("Hello World " + val);
                };
                executeTask(task);
            }
            public void executeTask(Task task) {
                task.doTask();
            }


        }
    
    * The beauty here is that variable ``val`` which is a local variable in function ``testClosure()`` is getting accessed from within ``executeTask()``
    * Where ever a lambda uses a free variable within the same scope, the value of that variable is saved by the jvm and whenever the lambda is called it's passed along with that. So here this closure is using free variable present in it's lexical scope. 
    * Closures are important as they control what is or isn't in the scope of a function.


    But the catch is the variable should be effectively final.


*  [What is currying](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17976619#questions/11094811) Currying break up a single function that takes multiple parameters which take single argument each.

        //Fluent
        Function<Integer, Function<Integer, Function<Integer, Integer>>> function = u -> v -> w -> u + v + w;
        Integer result = function.apply(2).apply(4).apply(9);
        Assertions.assertEquals(15, result);

        //Non Fluent
        Function<Integer, Function<Integer, Function<Integer, Integer>>> function1 = u -> v -> w -> u + v + w;
        Function<Integer, Function<Integer, Integer>> function2 = function1.apply(2);
        Function<Integer, Integer> function3 = function2.apply(4);
        Integer result = function3.apply(9);
        Assertions.assertEquals(15, result);



*  [What is Lazy evaluation](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17976621#questions/11094811) Lambda's are not evaluted where they are declared but they are only evaluated when they are actually invoked. This means that they are lazily evaluated.
    * Lazy evaluation is an evaluation strategy which delays the evaluation of an expression until the value is actually needed.
    * We can take advantage of this behavior to delay or avoid method evaluation or invocation of an expression because some values/expression may never be needed depending on certain conditions.
    For example:

            Supplier<Employee> supplier=()->new Employee(1,"Sam",60000);
            if(condition){
                supplier.get();
            }

      ``supplier.get()`` will never be invoked if value of ``condition`` is ``false``. This mean in such scenario the employee object will also not be created. This way unnecessary object creation may be be avoided.
    * So lazy evaluation of lambda saves computing resources by avoiding unnecessary computations.


* [What is Tail Call Optimization](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17976625#questions/11094811) 
    * **Non Tailed Recursion:** A function is called non tailed recursive function if the last thing excuted by the function has something other than than calling a recursive function. With tailed recursion more stack frames created, so it uses more memory to execute.
        
            public long factorialNonTailed(int n) {
                if (n <= 1) return 1;
                return n * factorialNonTailed(n - 1);
            }

    * **Tailed Recursion:** A recursive function is tail recursive when a recursive call is the last thing executed by the function. Since recursive call is the last call here there is nothing left to do in the current function, so saving functions stack frame is not required. This saves memory.

            public long factorialtailed(int n, int a) {
                if (n <= 1) return a;
                return factorialtailed(n - 1, n * a);
            }

        * In functional programming we may use a lot of recursion, so it's important we use tailed recursion as much as we can so that the compiler can perform tail call optimization.



# **Streams**

* [What are Streams](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975881#questions) A stream is a sequence of elements from a datasource that supports data processing operations.
We get the data from the data source, apply processing operations and then we collect the data to a destination container or it simply consume the stream.

        String genre = "fiction";
        int rating = 4;
        List<Book> filteredList = database.stream()
                    .filter(book -> book.getGenre().equalsIgnoreCase(genre))
                    .filter(book -> book.getRating() >= rating).collect(Collectors.toList());
            Assertions.assertThat(filteredList).hasSize(1);
   
* Streams are: 
    * **Flexible:** Stream are flexible to take data from any datasource, like list, file,  & output resources and perform operations on them and return the data into the containtainer the user wants or just consume the data.

    * **Declarative**: Java 8 stream api allows us to write declarative code, which is much more consise and readable.

    * **Parallelizable**: With larger collections we may want to processes a stream in parallel. Writing parallel code is complicated but with streams we can easily use the ``database.stream().parallel()`` or  ``.parallelStream()`` methods.

* [Intermediate Stages of a Stream](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975885#questions)

* [What is a stream pipeline](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975887#questions) A stream pipeline consists of a source, zeo or more intermediate operations and a terminal operation.
    * **Source**: Source is from where we generate the stream such as collection, array, file, system input/output resources, a generator function.
    * **Intermediate Operation**: These intermediate operations are operation that are applied on a stream and they return another stream.
    * **Terminal Operation**: Terminal operation produce the result or side effect(example: print statements) from a stream. Terminal operation produces non stream results, for example a Collection or no value at all. This is why terminal opertion cannot be further changed.

            
            String genre = "fiction";
            int rating = 4;

            //1 Source
            Stream<Book> bookStream = database.stream();
            //2 Filter Operation 1
            Stream<Book> bookStreamFilteredByGenre = bookStream.filter(book -> book.getGenre().equalsIgnoreCase(genre));
            //3 Filter Operation 2
            Stream<Book> bookStreamFilteredByGenreRating = bookStreamFilteredByGenre.filter(book -> book.getRating() >= rating);
            //4 Collection Operation
            List<Book> filteredList = bookStreamFilteredByGenreRating.collect(Collectors.toList());

            Assertions.assertThat(filteredList).hasSize(1);



* [How are streams different from collection](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975893#questions) 

    * Streams are not data containers, they are like fancy iterators. 
    * We can iterate over a Stream using the .stream() function, this abstracts away iterator related code. Collections are traversed using explicit iterators. 
    * Streams can be operated upon only once but with Collection we can operate as many times as we want. 
    * Once you operate on a stream it becomes empty. So if we try to traverse the same stream more than once we get IllegalStateException.
            
            String genreFiction = "fiction";
            String genreComputerScience = "computer-science";
            int rating = 4;

            Stream<Book> bookStream = database.stream();

            List<Book> fictionBookList = bookStream
                    .filter(book -> book.getGenre().equalsIgnoreCase(genreFiction))
                    .filter(book -> book.getRating() > rating)
                    .collect(Collectors.toList());

            org.junit.jupiter.api.Assertions.assertThrows(IllegalStateException.class, () -> {
                List<Book> computerScienceBookList = bookStream
                        .filter(book -> book.getGenre().equalsIgnoreCase(genreComputerScience))
                        .filter(book -> book.getRating() > rating)
                        .collect(Collectors.toList());
            });



## **Stream Operations || ``Higher Order Functions`` in Streams || ``.filter() || .map() || .reduce()``**
* [What are the different higher order functions in Streams/ Stream Operations](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975897#questions)
    * .filter()
    * .map()
    * .reduce()

    We should not modify data within a stream as it may lead to ConcurrentModificationException at Runtime. Also functional programming dictates that we should not change state of an object in functional programming.


* [Explain the .filter() method in java streams](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975897#questions) ``.filter()`` takes a Predicate and ``Predicate`` has a ``test()`` function which we pass using lambda.
  * The filter method returns a new stream of object for which the Predicate expression evaluates to true.
  * Syntax: ``Stream<T> filter(Predicate<? super T> predicate);``


        Stream<Integer> integerStream = Stream.of(34, 678, 89, 4, 52, 31, 325, 6);
        List<Integer> evenList = integerStream.filter(e -> e % 2 == 0).collect(Collectors.toList());
        Assertions.assertThat(evenList).containsExactly(34, 678, 4, 52, 6);

* [Explain how the .map() method work in java streams](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975899#questions) ``.map()`` operation takes a mapper function which is actually a ``Function`` and has a method ``apply()``
  * The .stream() method takes a stream element and maps it to a different vallue.
  * Syntax: ``<R> Stream<R> map(Function<? super T, ? extends R> mapper);``

        Stream<Integer> integerStream = Stream.of(34, 678, 89, 4, 52, 31, 325, 6);
        List<Integer> multiplicationTableOf25 = integerStream.map(i -> i * 25).collect(Collectors.toList());
        Assertions.assertThat(multiplicationTableOf25).containsExactly(850, 16950, 2225, 100, 1300, 775, 8125, 150);


        List<String> bookNameList = database.stream().map(Book::getName).collect(Collectors.toList());
        Assertions.assertThat(bookNameList)
                .containsExactly("monolith to microservice",
                        "a tale of null",
                        "containerization the effective way",
                        "clean code", "java primer",
                        "faithful lies", "evening in la",
                        "hitch hicker guide to the galaxy");


* [What is the use of .reduce() operation](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975903#questions) ``.reduce()`` method is used when we need to reduce the stream to a single value. For example to find the sum, product, min, max  etc. .reduce() operation is used to combine all stream elements.
    * Syntax: ``T reduce(T identity, BinaryOperator<T> accumulator);``
      * **``identity``**: this is a value that has no effect when used in an operation. for example for sum identity would be 0, for product it would be 1.
      * **``accumulator``**: accumulator is a ``BinaryOperator``.


            List<Integer> integerList = Arrays.asList(1, 12, 23, 34, 45, 56, 67, 78, 89, 90);
            Integer sum = integerList.stream().reduce(0, (a, b) -> a + b);
            Assertions.assertEquals(495, sum);



* [What do you mean by Lazy Evaluation in Stream](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975905#questions) The intermediate operations of streams are lazily evaluated and the terminal operations in streams are eagarly evaluated. This means that the intermediate operations will not be invoked until the terminal operation in invoked. Once the terminal operation is invoked the whole stream pipeline is executed.


        public void testFilter_LazyEvaluation() {
            String genre = "fiction";
            int rating = 4;
            Stream<Book> bookStream = database.stream()
                    .filter(book -> book.getGenre().equalsIgnoreCase(genre))
                    .peek(book -> System.out.println("From .peek() " + book))
                    .filter(book -> book.getRating() > rating);
            List<Book> filteredBookList = collectBook(bookStream);
            Assertions.assertThat(filteredBookList).hasSize(1);
        }

        private List<Book> collectBook(Stream<Book> bookStream) {
            System.out.println("Collecting Books");
            return bookStream.collect(Collectors.toList());
        }

   Output: 

        Collecting Books
        From .peek() Book(name=faithful lies, author=autumn winbird, genre=fiction, rating=3.1)
        From .peek() Book(name=evening in la, author=la sophie, genre=fiction, rating=3.5)
        From .peek() Book(name=hitch hicker guide to the galaxy, author=barry cooper, genre=fiction, rating=4.9)

    ``peek()`` method takes a Consumer and it's generally used to peek into the stream.
    Syntax: ``Stream<T> peek(Consumer<? super T> action);``



## **Primitive Streams || ``IntStream`` || ``DoubleStream`` || ``LongStream``**


* [Why are Primitive Streams in java and why do need them](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975911#questions) 
  * Primitive Streams like ``IntStream``, ``DoubleStream`` and ``LongStream`` provides ready made mathemetical functionality like average, sums etc for Streams using methods like ``.average(), .sum(), .count() etc``. 
  * Since they are streams of primitive types so it **avoids the cost of boxing and unboxing**. 
  * **Creating Primitive Streams**: We can use the **``.of(....)``** method to create a Primitive Stream.
        
        DoubleStream doubleStream = DoubleStream.of(4.6, 4.3, 4.8, 3.9, 4.3, 3.1, 3.5, 4.9);
        IntStream intStream = IntStream.of(4, 4, 4, 3, 3, 1, 5, 9);
        LongStream longStream = LongStream.of(4L, 3L, 3L, 1L, 5L, 9L);

  * **Converting Object Stream to ``Primitive Streams``**: Currently there are 3 primitive types in Java:
    * **IntStream** : We get the IntStream from a Stream using the ``.mapToInt()`` method.
    * **DoubleStream**: We get the DoubleStream from a Stream using the ``.mapToDouble()`` method.
    * **LongStream**:  We get the LongStream from a Stream using the ``.mapToLong()`` method.

            DoubleStream doubleStream = listOfBooks.stream().mapToDouble(Book::getRating);
            OptionalDouble optionalResult = doubleStream.average();
            double average = optionalResult.getAsDouble();
            long count = doubleStream.count();
            Double sum = doubleStream.sum();
  
  * **Converting Primitive Streams to ``Object stream``**: To convert Primitive Stream to Object Stream we may use the ``.boxed()`` or ``.mapToObject()`` present in the Primitive stream classes.

        DoubleStream doubleStream = listOfBooks.stream().mapToDouble(Book::getRating);
        List<Double> resultListUsingBoxed = doubleStream.boxed().toList();
        List<Double> resultListUsingMapToObject = doubleStream.mapToObj(i -> i).toList();


* [Explain some of the popular methods present in the Primitive Streams in java](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975931#questions) Some of the popular Primitive Stream methods are:

    * **.sum()** : Sums the element in the Primitive Stream.
      * For IntStream & and LongStream it returns Long
      * For DoubleStream it returns Double.
    * **.min()**: Finds the minimum element in the Primitive Stream.
    * **.max()**: Finds the maxium element in the Primitive Stream.
    * **.average()**: Finds the average element in the Primitive Stream.
      * For IntStream  ``.min() .max() & .average()`` returns OptionalInt
      * For DoubleStream  ``.min() .max() & .average()`` returns OptionalDouble
      * For LongStream  ``.min() .max() & .average()`` returns OptionaLong
    * **.summaryStatistics()**: This is used to find statistics about the Primitive Stream like sum, average, count etc in a single object.
      * Returns a ``IntSummaryStatistics``, ``DoubleSummaryStatistics`` or ``LongSummaryStatistics`` depending on the type of the Primitive Stream. 

    
            IntSummaryStatistics summaryStatistics = intStream.summaryStatistics();
            Assertions.assertEquals(50, summaryStatistics.getSum());
            Assertions.assertEquals(5.555555555555555, summaryStatistics.getAverage());
            Assertions.assertEquals(1, summaryStatistics.getMin());
            Assertions.assertEquals(10, summaryStatistics.getMax());
            Assertions.assertEquals(9, summaryStatistics.getCount());

## **Bounded vs Infinite Streams || Processing Stream of Streams using .``flatMap()``**

* [How can we create Bounded Streams in Java](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975915#overview) We can create a Stream with a specific number of elements, these streams are known as Bounded Streams. 

    Bounded streams may be created from:
    1. **``Collections``**
    2. **``Maps``**
    3. **``Arrays``**
    4. **``Stream.Builder``**
  * **From Collections**: We can use the ``.stream()`` method to obtain a stream from collection.

        List<Integer> integerList = List.of(1, 4, 7, 9, 4);
        Stream<Integer> integerStream = integerList.stream();
  * **From Map**: Maps are key value pairs so they can't be directly streamed. But we can ``.stream()`` the entrySet or keySet or the list of values from a map.
    * **``map.entrySet()``**: We can get the Entries in a map as a collection using ``map.entrySet()``  method.
    * **``map.keySet()``**: We can obtain the set of keys using ``map.keySet()`` 
    * **``map.values()``** We can obtain a collection of values present in the map using ``map.values()``<br/>
    
    Then we may use the ``.stream()`` method on these collections to stream them.

        Map<Integer, String> map = Map.of(1, "one", 2, "two", 3, "three", 4, "four");
        Stream<Map.Entry<Integer, String>> entryStream = map.entrySet().stream();
        Stream<Integer> keyStream = map.keySet().stream();
        Stream<String> valueStream = map.values().stream();
  * **From Arrays**: We can create streams from primitive or object arrays. 
    * **Primitive Arrays:** We can use ``Arrays.stream()`` method to obtain the stream but it returns ``Primitive Stream``.
            
    * **Object Arrays:** We can use ``Arrays.stream()`` method to obtain the stream but this returns an Object Stream.
            
            int[] intArr = {3, 5, 7, 89, 9};
            IntStream intStream = Arrays.stream(intArr); //Primitive
            Integer[] integerArr = {3, 5, 7, 89, 9};
            Stream<Integer> integerStream = Arrays.stream(integerArr); //Object
  * **Stream.Builder**: ``Stream.build()`` returns a ``Stream.Builder`` object, where we can add elements using ``add()`` or ``accept()`` methods, then we can use the **``build()``** method on the builder object to build stream. This method is particularly useful if we need to insert multiple elements into the stream based on condition.
    
        Stream.Builder<Integer> streamBuilder = Stream.builder();
        streamBuilder.add(3).add(5);
        streamBuilder.accept(7);
        if(condition){
            streamBuilder.add(89);
            streamBuilder.add(9);
        }
        Stream<Integer> integerStream = streamBuilder.build();


* [What are Infinite Streams in java and how do you create them](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975919#overview) Infinite Stream in java does not have a limit on the number of elements in a stream, an infinite set of elements will be streamed. 

    Infinite Stream in java may be created using the following Stream or Primitive Stream methods.
    * **Stream.iterate():** Stream.iterate() takes in a seed and an unary operator. At each step the unaryOperator is evaluated and a new element is generated based on the seed.
    ``Stream.iterate(T seed, UnaryOperator u)``
    
            Stream<Integer> infiniteObjectStream = Stream.iterate(0, i -> i + 5);
      This will generate a stream 0, 5, 10, 15, 20, 25, 30, 35, 40, 45........

    * **Stream.generate():** Strean.generate() takes in a supplier and returns an infinite stream. Each element in the stream pipeline is generated using the Supplier.get() method. ``Stream.generate(Supplier supplier)``
        
            Stream<String> infiniteStreamString = Stream.generate(() -> "Hello");
            Assertions.assertThat(firstTenObjectOfInfiniteStreamString)
                .hasSize(10)
                .containsExactly("Hello", "Hello", "Hello", "Hello", "Hello", "Hello", "Hello", "Hello", "Hello", "Hello");

            Stream<Integer> infiniteStreamInt = Stream.generate(new Random()::nextInt);
            Assertions.assertThat(firstTenObjectOfInfiniteStreamInteger)
                .hasSize(10);
      This will generate a stream of infinite Random Integers.



* [What is the use of .flatMap() operation](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975923#overview) .flatMap() operation is useful when we have an element within the stream that returns another stream and we want to combine those streams. For example

    * We can combine 3 streams to output a single stream

            Stream<String> appetizers = Stream.of("Tomato Soup");
            Stream<String> mainCourse = Stream.of("Rice", "Chicken Curry", "Daal Makhni");
            Stream<String> desert = Stream.of("Rasgulla", "Gulab Jamun");

            Stream<Stream<String>> streamOfStreamMealItemList = Stream.of(appetizers, mainCourse, desert);

            List<String> mealItems = streamOfStreamMealItemList.flatMap(i -> i).collect(Collectors.toList());

            Assertions.assertEquals(6, mealItems.size());


    * We can read String lines from a file, then split the lines by " " and get the words present in the file.

            Path path = Paths.get("C:\\Users\\subhr\\mission-interview\\java\\functional-programming\\src\\main\\resources\\LOA.txt");
            try (Stream<String> streamOfLines = Files.lines(path)) {
                List<String> words = streamOfLines
                        .flatMap(line -> Arrays.stream(line
                                .split(" "))).collect(Collectors.toList())
            } catch (IOException e) {
                e.printStackTrace();
            }



## **Parallel Streams || Stateful vs Stateless Operations in Streams || Manage Concurrency using Fork Join Pool** 


* [Why do we need Parallel Stream](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975929#overview) Now-a-days most computers come with multicore processors, so we can design our programs in a way that can take advantage of Multicore Processing. This means more resources work simultaneously to get the job done faster. Java Streams has APIs that supports parallel processing. This may be achieved in 2 ways:
  * **stream().parallel()**: By default streams are sequential, we can make it parallel by invoking the ``.parallel()`` on the ``.stream()`` method.
  
        Stream<Employee> parallelEmployeeStream=employeeList.stream().parallel();
  * **Collection.parallelStream()**: While creating streams from collections, we can use the .parallelStream() to create the parallel stream directly.
        
        Stream<Employee> parallelEmployeeStream=employeeList.parallelStream();

  * **``Parallel processing``** though powerful has it's own implication. While applying parallel processing on streams, stream should be:
    * **``Stateless``** We should only be using parallel streams with stateless intermediate operations
    * **``Non-interfering``**: The stream should be non-interfering, this means that the datasource should not be affected during the operation.
    * **``Associative``**: The stream should be associative, this means, one operation should not get affected by the order of data under processing.

  * Parallel Streams are build on top of fork-join framework which is build on top of Multithreading framework so there should not be any synchronization or visibility issues, but we need to ensure that ``we are not changing the state of the object throughout the pipeline``.



* [What are stateful and stateless operations in Streams](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975933#overview)

    **Stateless operations:**
    * Stateless operations are performed one by one on the element and it doesn't need any outside information for the Stream to be processed. 
    * Ordering of elements doesn't matter.
    * Stateless operations can be run in parallel.
    * ``.filter() .map() .reduce()`` etc are Stateless operations.
            
            long numbersAbove5 = intList.stream().parallel().filter(i -> i > 5).count();

    **Stateful Operations:**
    * Stateful operation are the ones that uses outside information.
    * Ordering of elements matters.
    * Stateful operations are not suitable for parallel execution.
    * ``.skip() .limit()`` etc are some of the Stateful operations.
            
            List<Integer> topThreeElementsNotContainingMax = intList.stream()
                    .sorted(Comparator.reverseOrder())
                    .skip(1).limit(3).collect(Collectors.toList());

    * The above code is stateful as we are trying to fetch top 3 highest values in the list. 
* [How will you manage the concurrency level for your Streams that's using the fork-join pool](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975935#overview) The .parallelStream() by default makes use of fork join pool. 

    * By default the parallelism 1 less than the available number of cores. We can set the parallelism level of fork-join pool using the following:
            
            System.setProperty("java.util.concurrent.ForkJoinPool.common.parallelism", "100");

    * Code:
            
            ForkJoinPool forkJoinPool = new ForkJoinPool(100);
            int povertyThreshold = 700000;
            Future<Long> countFuture = forkJoinPool.submit(() -> employeeList.stream()
                    .filter(employee -> employee.getSalary() > povertyThreshold).count());

    * For **Computation Intensive task** set the number of threads/parallelism to ``less than`` number of CPU Cores.
    * For **IO Intensive task** we can set the number of threads/parallelism to ``greater than`` number of CPU Cores, because most of the time the threads will be waiting on IO input and thus we can leverage the idle cpu cycles.


## **Spliterator** || **``Methods & Characteristics``** || **Creating Custom Spliterator**


* [What is the use of Spliterator](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975757#questions) Spliterator is an interface which we may use to create a stream from a custom source like file. 
    * It is an object to access the data which the stream can use.
    * The Collection classes by default has their own implementation of the Spliterator interface, which are used to create streams from them.
    * The Spliterator interface has 4 abstract methods which we may be implemented to create a stream from a custom source. The abstract methods are:
        * **tryAdvance():** This takes a consumer, so if a remaining element exists it performs certain action on it and returns boolean. **``boolean tryAdvance(Consumer<? super T> action);``**
        * **trySplit():** It splits the elements, some of the implemetation available for this method is BalancedTree. **``Spliterator<T> trySplit();``**
        * **estimateSize():** This returns the number of elements that would be encountered by a for each traversal. **``long estimateSize();``**
        * **characteristics():** Returns a set of characteristics of the Spliterator **``int characteristics();``**


* [What do you mean by the Characteristics or State of Stream and how does it help optimize functional code](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975759#overview) 

    * **Spliterator:** The ``Spliterator`` interface has 8 primitive integer constants which are called the spliterator characteristics. These constants are used to define/represent the stream's State.
    * **Spliterator Characteristics** The .characteristics() method helps us set the characteristics of a stream which helps in performance optimization. Typically the .characteristics() should return a primitive integer which is "|" of all the Characteristics that are set for a particular Stream. For example for the List class the method looks like the following:
 
            public int characteristics() {
                return Spliterator.ORDERED | Spliterator.SIZED | Spliterator.SUBSIZED;
            }
        *  The following constants in the Spliterator interface may be included in the characteristics() method while defining a stream:
            * **Spliterator.ORDERED** : Denotes the order of elements are preserved in a stream, for example the stream generated from ``ArrayList``.
            * **Spliterator.DISTINCT**: Denotes that there is no duplication, for example the stream generated from a ``HashSet``.
            * **Spliterator.SORTED**:  Denotes that the stream is sorted, for example the stream generated from a ``SortedSet``, ``TreeSet`` etc.
            * **Spliterator.SIZED**: Denotes that the size of the Spliliterator is known.
            * **Spliterator.NONNULL**: Denotes that there are no null values in the stream.
            * **Spliterator.IMMUTABLE**: Denotes that the stream is immutable.
            * **Spliterator.CONCURRENT**: Denotes that the stream is built on a concurrent structure, for example stream generated from ``ConcurrentHashMap``
            * **Spliterator.SUBSIZED**: Denotes that the size is know and additionally, the Spliterator generated from the trySplit() method will also be sized, when we go parallel.

        * To determine if a Spliterator has a particular state we check in two ways: 
            * Perform AND "&" of the value returned by the Spliterator and the state itself.
            * Use the spliterator.hasCharacteristics() method.


                    int spliteratorCharacteristics = list.stream().spliterator().characteristics();
                    int result = spliteratorCharacteristics & Spliterator.ORDERED;
                    Assertions.assertEquals(result, Spliterator.ORDERED);
                    Assertions.assertTrue(spliterator.hasCharacteristics(Spliterator.ORDERED));
    * **Performance Optimization with Spliterator Characteristics**: Suppose we invoke a .sorted() method on a stream pipeline build around TreeSet. Since TreeSet is a sorted collection, the corresponding spliterator will have Spliterator.SORTED set in it's characteristics() method. So while executing the stream pipeline, the .sorted() method will be skipped. So with the characteristics while execution of the stream pipeline the jvm may skip one or more operations in order to optimize the stream execution.
    However if .sorted() method is called on a stream from ArrayList, the Spliterator.SORTED will be set in the corresponding spliterator of the stream.
    So the operations may set, preserve or clear a characteristic which decides how the pipeline will be executed. 


* [How will you create a Custom Spliterator](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975761#overview) **``Check BookListReaderTest.java``**




## **Collectors**

* [What is the use of Collectors](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975693#overview) The terminal operation in a stream pipeline may be doing any one of the following:
    * Consuming the data using a Consumer. Example : ``.forEach(System.out::println)``
    * Accumulating the data using BinaryOperator and/or identity. Example: ``.reduce(i,(a,b)->a+b)``
    * Collecting the data to a Data Container like Collection. Example: ``.collect(Collectors.toUnmodifiableList())``<br/>

  **Collectors is an utility class that provide ready made reduction algorithms that can **``accumulate, aggregate & summarise``** elements into Collections.**
  * The Collectors class  has different static methods that allow us to collect the data into various structures or containers. 
  * The Collectors class is defined as final  and all static methods of the Collectors Class return an instance of Collector interface.

        Stream<Integer> streamEven=integerList.filter(n->n%2);
        Collector collector=Collectors.toList();
        List<Integer> integerList=streamEven.collect(collector);

  *The only way to ``collect data without using Collectors`` is to **``use the .reduce() operation``** where we need to implement our own algorithm to collect the data into our desired structure*

* [How will you collect a Stream to List and Set](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975695#overview) A stream may be collected to a list or set using the below methods.
    * Collecting to a List
        * Collectors.toList();
        * Collectors.toUnmodifiableList();
    * Collecting to a Set
        * Collectors.toSet();
        * Collectors.toUnmodifiableSet();
    * Collecting to any Collection
        * Collectors.toCollection(collectionSupplier)
    * Sample Code for collecting to List & Set:

            List<String> employeeNames = employeeList.stream().map(employee -> employee.getName()).collect(Collectors.toList());
            Set<String> employeeNames = employeeList.stream().map(employee -> employee.getDesignation()).collect(Collectors.toUnmodifiableSet());

    * Sample Code for collecting to any Collection:

            //Employee implements Comparable
            TreeSet<Employee> employeeListSortedById = employeeList
                .stream().collect(Collectors.toCollection(TreeSet::new));



* [How will you collect data to a Map](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975697#overview) We can collect stream to a Map using the below collectors

    * **Collectors.toMap()**: Returns a Map of the stream using the keyMapperFunction &  valueMapperFunction **``Collectors.toMap(keyMapperFunction,valueMapperFunction)``**

            Map<Integer, String> employeeNameIdMap = employeeList.stream().collect(
                    Collectors.toMap(
                            employee -> employee.getId(),
                            employee -> employee.getName()
                    )
                );
    * **Collectors.toUnmodifiableMap()**: Returns an unmodifiable Map of from the stream using the keyMapperFunction &  valueMapperFunction. **``Collectors.toUnmodifiableMap(keyMapperFunction,valueMapperFunction)``**
    * **Collectors.partitioningBy()** Partitions the data into two groups. Returns a Map having two elements, one element has data for the predicate evaluated to true and the other element has data for the predicate evaluated as false. Key is boolean and Value is List. **``Collectors.partitioningBy(predicate)``**

            Map<Boolean, List<Employee>> employeeMapPartitionedByGender = employeeList.stream().collect(
                    Collectors.partitioningBy(
                        employee -> employee.getGender() == 'M'
                    )
                );
    * **Collectors.groupingBy()** Groups the data based on a given classifier function. Returns a Map that has elements equal to the number of distinct values for the classifier. **``Collectors.groupingBy(classifier)``**

            Map<String, List<Employee>> employeesPerDept = employeeList.stream()
                .collect(
                    Collectors.groupingBy(
                        employee -> employee.getDesignation()
                    )
                );



* [How will you collect data to a String](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975699#overview) We can use the **``Collection.joining(delimiterString)``** to get a string consisting of elements joined by joined by the delimeter.
    
        String empNames = employeeList.stream()
                .map(employee -> employee.getName())
                .collect(Collectors.joining(","));



* [What do you mean by Collector Cascading or Collector nesting ](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975709#overview) Using java we can nest the Collectors furthers to do further post processing. There are collector methods which themselves can take Collectors as argument. When we use a Collector inside a Collector we call the inside Collector a downStream Collector. For example we have **``Collectors.groupingBy(classifier, downStream)``** [Examples](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975709#overview)

    * **Count of employees per designation** using **``Collectors.counting()``**

            Map<String, Long> employeesPerDesignation = employeeList.stream().collect(
                    Collectors.groupingBy(employee -> employee.getDesignation(),
                    Collectors.counting()
                    )
            );

    * **Sum & Average salaries of Employees in each designation** using **``Collectors.summingDouble()``** & **``Collectors.averagingDouble()``**

            Map<String, Double> sumOfEmployeeSalariesPerDept = employeeList.stream().collect(
                Collectors.groupingBy(Employee::getDesignation, 
                    Collectors.summingDouble(Employee::getSalary))
            );
            Map<String, Double> averageOfEmployeeSalariesPerDept = employeeList.stream().collect(
                Collectors.groupingBy(Employee::getDesignation, 
                    Collectors.averagingDouble(Employee::getSalary))
            );

    * **Highest Paid OptionalEmployee in Each Designation** using **``Collectors.maxBy(comparator)``**
    
            Map<String, Optional<Employee>> maxSalaryPerDesignation = employeeList.stream().collect(
                Collectors.groupingBy(Employee::getDesignation,
                    Collectors.maxBy(Comparator.comparing(Employee::getSalary)))
            );

    * **Highest Paid Employee in Each Designation** using **``Collectors.collectingAndThen()``**

            Map<String, Employee> maxSalaryPerDesignation = employeeList.stream().collect(
                        Collectors.groupingBy(Employee::getDesignation,
                                Collectors.collectingAndThen(
                                        Collectors.maxBy(Comparator.comparing(Employee::getSalary)), Optional::get)
                        )
                );

    * **Max Optional Salary per Designation** using **``Collectors.mapping()``**  **``Collectors.maxBy(Comparator.comparing(Function.identity())``** 
        * Collectors.mapping() is like the .map() function but used inside a Collector
        * Function.identity() is same as writing i->i
        
                Map<String, Optional<Double>> maxSalaryPerDesignation = employeeList.stream().collect(
                        Collectors.groupingBy(Employee::getDesignation,
                            Collectors.mapping(Employee::getSalary,
                                Collectors.maxBy(Comparator.comparing(Function.identity()))
                            )
                        )
                    );


    * **Max Salary per Designation** using **``collectingAndThen()``**

            Map<String, Double> maxSalaryPerDesignation = employeeList.stream().collect(
                            Collectors.groupingBy(Employee::getDesignation,
                                    Collectors.mapping(Employee::getSalary,
                                            Collectors.collectingAndThen(Collectors.maxBy(Comparator.comparing(i -> i)),Optional::get)
                                    )
                            )
                    );




* [How does Collectors internally work](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975657#overview) ``Stream.collect(collector)`` method takes Collector as an argument. Collector is an interface with 5 abstract methods. Out of these 5 methods, apart from characteristics are higher order functions. 

    * The methods are:
        * supplier() This returns a Supplier. For example for Collectors.toList() this function returns an empty ArrayList.
        * accumulator() This returns a BiConsumer. The BiConsumer adds elements to the container when the accept method is called on the BiConsumer. For example-The stream elements are added one by one to the ArrayList using the BiConsumer.
        * combiner() This returns a BinaryOperator. This step is used to merge the partial results from differnt threads into a final result, incase we want parallel processing.
        * finisher() This returns a Function. We pass container object to the apply() method to get the final object. Performs final transformation on the intermediate accumulation type to the Final Result Type.
        * characteristics() This returns a Set of Characteristics of the Collector. The collector characteristics help determine whether some or all of the above function would be executed.

    * We can use the existing implementation of Collector class already defined in the ``Collectors`` as a nested ``static class CollectorImpl``. The constructor of CollectorImpl take in the higher order functions as arguments and it's responsible for calling the relevant methods(functions) in order to get the final object.


    When we call stream().collect(collector) the following steps are executed in order. 

        container=collector.supplier().get();
        BiConsumer accumulator=collector.accumulator();
        forEach(u->accumulator.accept(container,u));
        //Combiner Steps
        return collector.finisher().apply(container);

    These steps are defined in the class **``java.util.stream.ReferencePipeline``**


* [How can you create a custom Collector to collect a stream to an ArrayList](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975661#overview)

        //This collector doesn't include a finisher
        Collector<Integer, ArrayList<Integer>, ArrayList<Integer>> arrayListCollector = 
        Collector.of(
                ArrayList::new,//Supplier
                (list, e) -> list.add(e),//BiConsumer
                (list1, list2) -> {//BiFunction
                    list1.addAll(list2);
                    return list1;
                },
                // IDENTITY_FINISH mean return type of accumulator and
                // finisher would be same, hence the finisher is missing
                Collector.Characteristics.IDENTITY_FINISH);


* [How will you write a custom collector that collects a stream to an ArrayList which is ordered](https://tcsglobal.udemy.com/course/functional-programming-and-reactive-programming-in-java/learn/lecture/17975663#overview)

        Collector<Integer, ArrayList<Integer>, ArrayList<Integer>> sortedArrayListCollector =
                Collector.of(
                        ArrayList::new,
                        (list, e) -> list.add(e),
                        (list1, list2) -> {
                            list1.addAll(list2);
                            return list1;
                        },
                        (list) -> {
                            Collections.sort(list);
                            return list;
                        },
                        Collector.Characteristics.UNORDERED
                );