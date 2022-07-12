## [Creational](https://www.baeldung.com/creational-design-patterns)

### **Singleton Pattern** -> ensures that atmost only one object exist throughout the application

* [How do you create a **Singleton Class** in Java (private constructor, static field containing only the instance, getInstance() method)](https://www.baeldung.com/java-singleton)
* [In which scenarios will you use **Singleton Class**](https://www.baeldung.com/creational-design-patterns)
    * Creation of expensive object(example- database connections)
    * Loggers, Configuration Settings, Resources that are accessed in shared mode
* [How to **avoid serialization issues with Singleton**, implement the readResolveMethod()](https://www.geeksforgeeks.org/prevent-singleton-pattern-reflection-serialization-cloning/#:~:text=Overcome%20Cloning%20issue%3A%2D%20To,hence%20our%20class%20remains%20singleton.)


### **Factory Pattern** -> defines an interface for creating the objects and lets subclass decide which class to instatiate
* [How will you implement **Factory Pattern** in java (create an interface, have multiple class implemeent the interface, create a class that will have the factory method and returns subclasses of the interface based on input from the user ``polygon``)](https://www.baeldung.com/creational-design-patterns)
* [In what scenarios will you use the **Factory Method**](https://www.baeldung.com/creational-design-patterns)
  * create families of related dependent objects
  * when implementation of the interface gets frequently changed
  * when current implementation can't easily accomodate a new change


### **Abstract Factory Pattern** -> provides an interface to create a family of related or dependant objects without specifying their concrete classes
* [How will you **implement Abstract Factory Pattern** in Java refer: ``AnimalFactory`` and ``BirdFactory``](https://www.baeldung.com/java-abstract-factory-pattern)
* [In what sceanrios will you use the AbstractFactoryPattern](https://www.baeldung.com/java-abstract-factory-pattern)
    * Client is independent of how we create and compose objects in the system
    * System is composed of multiple objects and they are designed to work together

### **Builder Pattern** -> simplfies the creation of complex objects by isolating the instantion process into a builder class that will have fluent api to create objects.
* [How will you **implement the Builder Pattern**, refer ``BankAccount``](https://www.baeldung.com/creational-design-patterns)
* In what scenarios will you use the Builder Pattern?
    * When the object creation process is complex with lot of mandatory and optional parameters.
    * Number of Constructor parameter is high.

### **Prototype Pattern** -> when we already have instance of the class(prototype) and we like to create new objects just by copying the prototype
* [How will you **implement the Prototype Pattern** in  java](https://www.baeldung.com/java-pattern-prototype)
* [What type of copy will you consider for implementing the Prototype Pattern ``deep copy vs shallow copy`` ]



## [Structural](https://refactoring.guru/design-patterns/structural-patterns)


### **Adaptor Pattern** -> allows incompatible object types to collaborate
* [How will you implement **Adaptor Pattern** ``convert Tesla car speed given in MPH to be adapted into KMPH``](https://www.baeldung.com/java-adapter-pattern)
* What are the usecase for the Adaptor Pattern
    * When an outside component provides a functionality that we wanna reuse but  it's incompatible with our current application.
    * When we want to use reuse legacy application code in our application