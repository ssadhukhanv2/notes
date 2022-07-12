## Spring Boot


* [How do you load custom properties file in Spring Boot](https://stackoverflow.com/questions/61683020/load-custom-properties-file-in-spring-boot-mvc-main)

      @Configuration
      @PropertySource("classpath:A.properties")
      public class AConfiguration {

      }

* [Advantages of using SpringBoot]()

* [What are the different Bean Scopes in Spring](https://www.baeldung.com/spring-bean-scopes)
  * **Singleton**  ``@Scope("singleton")``
  * **Prototype** ``@Scope("prototype")``
  * Webaware scopes
    * **RequestScope** ``@RequestScope``
    * **SessionScope** ``@SessionScope``
    * **ApplicationScope** ``@ApplicationScope`` Similar to Singleton but if the same instance of the bean is being shared with multiple servlet application using the same servlet context, then with Application Scope the bean will be shared, with Singleton each application will have own bean.
     * **WebSocketScope** ``@Scope(scopeName = "websocket", proxyMode = ScopedProxyMode.TARGET_CLASS)``


  


* [Difference between **POST**(create), **PATCH**(only update) vs **PUT**(create if not exists, else update)](https://stackoverflow.com/questions/31089221/what-is-the-difference-between-put-post-and-patch#:~:text=POST%20is%20always%20for%20creating,always%20for%20updating%20a%20resource)
* [Request Param vs Path Param](https://www.baeldung.com/spring-requestparam-vs-pathvariable)
* [**Difference** between **@Service**(Used to annotate classes where business logic is implemented) and **@Repository**(classes with logic to access the database are annotated with this. catches  all persistence related exception and throws them as SpringDataAccessException, uses PersistenceExceptionTranslationPostProcessor)](https://www.baeldung.com/spring-component-repository-service)
* [What is the **difference between @RestController and @Controller**](https://www.geeksforgeeks.org/difference-between-controller-and-restcontroller-annotation-in-spring/#:~:text=%40RestController-,%40Controller%20is%20used%20to%20mark%20classes%20as%20Spring%20MVC%20Controller,specialized%20version%20of%20%40Component%20annotation.)
* [How will you **configure Profile Specific Properties file** -> Spring Boot load application.properties & if a spring.profiles.active=dev is set, then it addtionally tries to load application-dev.properties and loads it ](https://www.baeldung.com/spring-profiles)
* [How do you handle properties in Spring Boot @ConfigurationProperties(prefix="com.prefix") or @Value("${kjkj}")](https://www.baeldung.com/configuration-properties-in-spring-boot)
* [How does **Spring Boot Internally work**](https://dzone.com/articles/how-springboot-autoconfiguration-magic-works)[java-techie](https://youtu.be/qlygg_H1M20?t=127)
  * **``spring-boot-starter``** dependencies pull multiple jars into the class path
  * **``spring-boot-autoconfigure/META-INF/spring.factories``** has the relavant classes defined the classpath(Example: JpaRepositoriesAutoConfiguration.class) which are loaded based on the annotations **@Configuration @ConditionalOnClass @ConditionalOnMissingBean, @ConditionalOnProperty** and other default Conditions. 
* [What is the use of **``@SpringBootApplication``**](https://youtu.be/qlygg_H1M20?t=408)
  * Internally uses **``@SpringBootConfiguration``**(which is an alias for configuration) **``@EnableAutoConfiguration``**(enables the autoconfiguration of beans) **``@ComponentScan``**(Scans the basepackage and loads beans marked with annotations)
* [Why do we need main method in Spring Boot Application (not required for war deployment, used when internal tomcat is being used)](https://youtu.be/qlygg_H1M20?t=622)
* [What is the use of **``SpringApplication.run(Main.class,args)``** -> kicks of and creates the application context, initializes the declared beans annotated with **@Configuration**, after creating the beans it automatically configures the dispatcher servlet & registers the handler mappings](https://youtu.be/qlygg_H1M20?t=751)
  * Creates the application context
  * Checks the ApplicationType
  * Registers the annotated class in the context
  * Creates an instance of TomcatEmbeddedServletContainer and adds to the context
* [How Dispatcher Servlet works with Spring](https://www.baeldung.com/spring-boot-dispatcherservlet-web-xml#:~:text=The%20DispatcherServlet%20is%20the%20front,xml%20file.)
* What is the difference between Spring and Spring Boot
* How will you perform global exception handling with Spring
* **Spring Exception Handling**
  * [How will you perform Exception Handling in Spring **``exception-handling``**](https://www.baeldung.com/exception-handling-for-rest-with-spring)
    * **Controller Level ``@ExceptionHandler``** -> No provision to pass ResponseStatus codes
    * **Create Component extending ``AbstractHandlerExceptionResolver``**
    and **``@Override``** the **``doResolveException()``** method -> we return a **ModelAndView** — this is the body of the response,
    * **Global @ControllerAdvice extending ``ResponseEntityExceptionHandler``**
    and defining appropriate handler methods with ``@ExceptionHandler`` annotation -> best way to do it






## Spring Security
* [JWT](https://youtu.be/soGRyl9ztjI?list=PLqq-6Pq4lTTYTEooakHchTGglSvkZAjnE&t=54)
* [Why do you **need Spring Security** -> to secure the application](https://youtu.be/rb3wUXZD2EQ?t=58)
* [How does spring security secure your application at a high level -> **provides authentication & authorization**](https://youtu.be/rb3wUXZD2EQ?t=118)
* [Core **Concepts of Spring Security**](https://youtu.be/rb3wUXZD2EQ?t=629)
  * **Authentication** -> process of identifying the user 
  * **Authorization** -> checking if the user is allowed to perform a certain operation
  * **Principal** -> authenticated user
  * **Granted Authority** -> bunch of permission allowed for an user
  * **Roles** -> group of authorities assigned together
* How does JWT work in Spring Security
* [Different Types of Autowiring]




## Spring Batch
* [What is Spring Batch](https://youtu.be/hr2XTbKSdAQ?t=35)
* Spring Batch is a **robust batch processing system** offered by Spring the spring framework, which may be used to create batch processing applications.
* Batch processing is a technique which processes data in large groups instead of single elements. With Batch processing you can process high volume of data with minimal user interaction.
* [What scenarios will you use Spring Batch](https://youtu.be/hr2XTbKSdAQ?t=61)
  * Billing Analysis System (Load .csv files to database)
  * Report Generation System (Create .csv file from database)
* [Spring Batch architecture](https://youtu.be/hr2XTbKSdAQ?t=156)
  * **Job Launcher** -> Interface which is used to launch a Spring Batch Job. Interface to initiate a job. It has a method called run, that triggers the Job Component
  * **Job** -> Work to be executed by the Spring Batch. May be simple or complex.
  * **Job Repository** -> Helps to mantain the state of the job. May use a database for storing state.
  * **Step** -> A job may have one or more steps. Each step may have ItemReaders, ItemProcessors and/or ItemWriter




## Spring Data JPA


* [How will you implement Optimistic Locking with Hibernate Entity Manager](https://www.baeldung.com/jpa-optimistic-locking)
* [How will you implement Optimistic Locking with Spring Data Repository](https://www.baeldung.com/java-jpa-transaction-locks)
* [Hibernate **Criteria Queries**](https://www.baeldung.com/hibernate-criteria-queries)
* [How will you implement  **Criteria Queries** using JPA](https://www.baeldung.com/spring-data-criteria-queries)
* [How will you implement **Query By Example** using Spring Data JPA](https://www.baeldung.com/spring-data-query-by-example)
* [How will you perform **joins in JPQL**](https://tcsglobal.udemy.com/course/hibernate-jpa-tutorial-for-beginners-in-100-steps/learn/lecture/7907598#overview)
* [When will you prefer **Optimistic Locking**(versioning can be enabled using @Version which will allow managing locks at a Database level which request is coming from multiple application nodes to the same database) over **Pessimistic Locking**(manages transaction locking at the application level, so it can't handle request coming from multiple servers)](https://vladmihalcea.com/optimistic-vs-pessimistic-locking/)
* [How will you implement **Optimistic Locking** for your application](https://www.baeldung.com/jpa-optimistic-locking)
  * Different lock modes
    * OPTIMISTIC
    * OPTIMISTIC_FORCE_INCREMENT
    * READ
    * WRITE
  * OptimisticLockException
  *  @Version
* [How will you **implement locks with Spring Data JPA**](https://www.baeldung.com/java-jpa-transaction-locks)
* [How will you implement **Pessimistic Locking** for your application](https://www.baeldung.com/jpa-pessimistic-locking)
* [What are the **ACID properties of Transactions** and what does **Atomicity Consistency Isolation and Durability**](https://tcsglobal.udemy.com/course/hibernate-jpa-tutorial-for-beginners-in-100-steps/learn/lecture/7907612#overview)
* [How will you control **how changes applied by concurrent transactions are visible to each other**(**isolation**). **DEFAULT, READ_UNCOMITTED, READ_COMITTED, REPEATABLE_READ, SERIALIZABLE**](https://www.baeldung.com/spring-transactional-propagation-isolation)
* [Explain the difference between **Dirty Read**, **Non-Repeatable read** and **Phantom Read**](https://www.baeldung.com/spring-transactional-propagation-isolation)
* [How will you **control the Atomicity of your transaction** by using different **propagation levels** such as  **REQUIRED, SUPPORTS, NOT_SUPPORTED, MANDATORY, NEVER, REQUIRES_NEW, NESTED**  ](https://www.baeldung.com/spring-transactional-propagation-isolation)
* [How will you implement **2nd level cache** for a JPA Entity with @Cacheable and below properties ](https://tcsglobal.udemy.com/course/hibernate-jpa-tutorial-for-beginners-in-100-steps/learn/lecture/7907642#overview)

        # Second Level Cache
        spring.jpa.properties.hibernate.cache.use_second_level_cache=true
        spring.jpa.properties.hibernate.cache.region.factory_class=org.hibernate.cache.ehcache.EhCacheRegionFactory
        spring.jpa.properties.javax.persistence.sharedCache.mode=ENABLE_SELECTIVE
        logging.level.net.sf.ehcache=debug

* [How does **1st Level cache work at the Transaction Level** in hibernate](https://tcsglobal.udemy.com/course/hibernate-jpa-tutorial-for-beginners-in-100-steps/learn/lecture/7907640#overview)
* [How will you **map associations in JPA** & Hibernate](https://thorben-janssen.com/ultimate-guide-association-mappings-jpa-hibernate/#Bidirectional_Many-to-One_Associations)

  * **Many to One**
    * **Unidirectional many-to-one** @ManyToOne -> foreign key is created in the "many" side of the relationship
    * **Unidirectional one-to-many**  @OneToMany -> foreign key is created in the "many" side of the relationship
    * **Bidirectional many-to-one** @ManyToOne @OneToMany(mappedBy = “order”) -> foreign key is created on the many side of the relationship
  * **Many to Many**
    * **Unidirectional many-to-many** @ManyToMany
    * **Bidirectional many-to-many** @ManyToMany
    @JoinTable & @ManyToMany(mappedby="")
  * **One to One**
    * **Unidirectional one-to-one** @OneToOne
    * **Bidirectional one-to-one** @OneToOne @OneToOne(mappedBy="")

* [What is the difference between **FetchType.EAGER** & **FetchType.LAZY**](https://thorben-janssen.com/ultimate-guide-association-mappings-jpa-hibernate/#Bidirectional_Many-to-One_Associations)
* [What are the different ways you can **map entities in hibernate**](https://thorben-janssen.com/ultimate-guide-association-mappings-jpa-hibernate/#Bidirectional_Many-to-One_Associations)
* [What is hibernate and what are the advantages of using it over jdbc](https://youtu.be/2sCAw1EbfEQ?t=104)
* [What is the **difference between JPQL and SQL Query**](https://tcsglobal.udemy.com/course/hibernate-jpa-tutorial-for-beginners-in-100-steps/learn/lecture/7907490#overview)
* [EntityManager **.persist(), .merge(), .flush() .detach(), .clear() .refresh()**](https://tcsglobal.udemy.com/course/hibernate-jpa-tutorial-for-beginners-in-100-steps/learn/lecture/7907480#overview)
* [What is **EntityManager** and how is it linked to the **PersistenceContext**](https://tcsglobal.udemy.com/course/hibernate-jpa-tutorial-for-beginners-in-100-steps/learn/lecture/7907486#overview)
* [**Inheritance Strategies** in JPA](https://thorben-janssen.com/complete-guide-inheritance-strategies-jpa-hibernate/)
  * **Mapped Super Class** -> Parent Abstract Class is annotated @MappedSuperClass and each concrete class will have it's own table
  * **Table Per Class** -> @Inheritance(strategy=InheritanceType.TABLE_PER_CLASS) Each Table will have own class
  * **Single Table** -> @Inheritance(strategy=InheritanceType.SINGLE_TABLE) @DiscriminatorColumn
  * **Joined** -> Maps each class of the inheritance hierarchy in it's own database table


* [Scenario where @Transactional annotation can be used in Spring Boot ](https://www.youtube.com/watch?v=95kxPSbHzVg)
* [How to configure Spring Data JPA for a non spring-boot project](https://www.baeldung.com/the-persistence-layer-with-spring-and-jpa)
* [Propagation and Isolation in Spring Transaction](https://www.baeldung.com/spring-transactional-propagation-isolation#1-required-propagation)
* [How will you implement Mongo DBRef with Spring Data JPA @DBRef annotation ](https://www.baeldung.com/spring-mongodb-dbref-annotation)


# Spring Cloud

#### [**Config Server**](https://www.baeldung.com/spring-cloud-configuration#:~:text=Spring%20Cloud%20Config%20is%20Spring's,be%20modified%20at%20application%20runtime.)
#### [**Eureka Server**](https://www.baeldung.com/spring-cloud-netflix-eureka#:~:text=With%20Netflix%20Eureka%2C%20each%20client,through%20a%20load%2Dbalancing%20algorithm.)
#### **API Gateway**
#### **Circuit Breaker**

#### **Distributed Tracing**
* [How will you use **zipkin** & **sleuth** to track api calls]()

#### **Log Aggregation**
* [How will you perform log aggregation with ELK **Elastisearch Logstash Kibana**](https://youtu.be/tljuDMmfJz8?t=6209)
* [How will you set up default user for Kibana](https://www.elastic.co/guide/en/elasticsearch/reference/current/built-in-users.html#:~:text=The%20Elastic%20bootstrap%20passwordedit&text=The%20bootstrap%20password%20is%20a,to%20the%20keystore%20during%20installation.)
* [How will you reset the *elastic* user's password in Kibana]
        
        .\elasticsearch-reset-password -u elastic




# Reactive Spring

* [How will you create a reactive REST API](https://www.youtube.com/watch?v=bXcFCgQsvAE&t=798)