
### [**JUNIT and Mockito course**](https://tcsglobal.udemy.com/course/mockito-tutorial-with-junit-examples/learn/lecture/5678212#reviews)
### [**Spring Boot Testing course**](https://tcsglobal.udemy.com/course/learn-unit-testing-with-spring-boot/learn/lecture/9968158#overview)


## JUNIT
* assertEquals(), assertTrue(), assertThrows(), assertArrayEquals
* How will you test exceptions in Junit5 ``assertThrows(NullPointerException.class, () -> Arrays.sort(number));``
* What is the default naming convention for JUnit Tests methods
* How will you assert **equality between arrays** in Junit
* [How will you create **parameterized tests** using Junit 5](https://www.baeldung.com/parameterized-tests-junit-5)
* [How will you **introduce timeouts** in Junit 5](https://mkyong.com/junit5/junit-5-timeouts-examples/)
* [How will you create a **Junit Test Suite**](https://howtodoinjava.com/junit5/junit5-test-suites-examples/)
* [What is the need of writing JUNIT Test cases]


## MOCKITO

* [How will you **Mock Constructors** with Mockito](https://stackoverflow.com/questions/64905956/mockito-junit-5-mock-constructor)
* [How will you **mock private methods with PowerMock** (can't be done with Mockito)](https://www.baeldung.com/powermock-private-method)
* [How will you **mock static methods with Mockito**](https://www.baeldung.com/mockito-mock-static-methods)
* [How to **mock final methods with mockito**](https://www.baeldung.com/mockito-final)
* [Why can't we **mock private and static methods using Mockito**](https://www.softwaretestinghelp.com/mock-private-static-void-methods-mockito/)
* [What is the difference between **Mock** and **Spy(allows partial functionality to be mocked, rest of the functionality is same as the original object)** ``SpyTest``](https://tcsglobal.udemy.com/course/mockito-tutorial-with-junit-examples/learn/lecture/5678778#reviews)
* [How does **Mockito annotations @Mock @InjectMock @Captor** work](https://tcsglobal.udemy.com/course/mockito-tutorial-with-junit-examples/learn/lecture/5678772#overview)
* [Why do you need **hamcrest matchers** -> better readablity ``assertThat(scores, hasSize(4)``, How will you **match the elements within an array** ``HamcrestMatcherTest``](https://tcsglobal.udemy.com/course/mockito-tutorial-with-junit-examples/learn/lecture/5678770#overview)
* [How will you **verify how many times a method is invoked in a mocked object**, ``Mockito.verify()``](https://tcsglobal.udemy.com/course/mockito-tutorial-with-junit-examples/learn/lecture/5678764#overview)
* [What is **BDD** and **how can you implment BDD syntax with Mockito**](https://tcsglobal.udemy.com/course/mockito-tutorial-with-junit-examples/learn/lecture/5678762#overview)
* [How will you **make a mock object throw RunTimeException**](https://tcsglobal.udemy.com/course/mockito-tutorial-with-junit-examples/learn/lecture/5678760#overview)
* [What are **argument matcher** in Mockito: ``Mockito.when(list.get(anyInt())).thenReturn("hello")``](https://tcsglobal.udemy.com/course/mockito-tutorial-with-junit-examples/learn/lecture/5678760#overview)
* [What is the difference between **EasyMock**(no **nice mock behaviour **available) & **Mockito**(**nice mock feature is available**) framework](https://tcsglobal.udemy.com/course/mockito-tutorial-with-junit-examples/learn/lecture/5678760#overview)
* [what are **nice mocks** if we don't specify a behaviour for a method of a mock object, mockito returns default values, for example for a method which returns a list, it will return an empty list](https://tcsglobal.udemy.com/course/mockito-tutorial-with-junit-examples/learn/lecture/5678758#overview)
* [What are the advantanges of using mocks over stubs? Flexibility]((https://tcsglobal.udemy.com/course/mockito-tutorial-with-junit-examples/learn/lecture/5678758#overview))





## Spring Boot Testing

* [Spy](https://tcsglobal.udemy.com/course/learn-unit-testing-with-spring-boot/learn/lecture/9968318#overview)
* [How will you capture arguments that's passed to a method call](https://tcsglobal.udemy.com/course/learn-unit-testing-with-spring-boot/learn/lecture/9968310#overview)
* [What are some of the **best practices while writing unit tests**](https://tcsglobal.udemy.com/course/learn-unit-testing-with-spring-boot/learn/lecture/9968398#overview)
  * READABLE: Each test should be readable within 15 secs
  * FAST:
  * ISOLATED: Unit tests should not depends on external dependency like external systems & databases. Use mocks if required. Test should only fail if and only if there is an issue with dependency, not becasue of failure in other system
  * RUN OFTEN: CICD, run test while committing code
  * Load as minimum Spring Context as possible
  * Naming Convention of Test Methods
* [How will you test controller](https://tcsglobal.udemy.com/course/learn-unit-testing-with-spring-boot/learn/lecture/9968330#overview)
* [What is **test coverage** -> The percentage of the code executed while running the unit tests is know as test coverage, ideally test coverage should be 100%, i.e. all lines of the code should be executed. **Focus on coverage but focus on good asserts more**](https://tcsglobal.udemy.com/course/learn-unit-testing-with-spring-boot/learn/lecture/9968392#overview)
* [Explain some of the design patterns of testing](http://xunitpatterns.com/index.html)
* [What is the use of **JSONPath library**, what are the advantages of using it over  JSONAssert](https://tcsglobal.udemy.com/course/learn-unit-testing-with-spring-boot/learn/lecture/9968384#overview) [**JSONPath documentation...**](https://github.com/json-path/JsonPath)
* [How will you use **AssertJ** library to validate lists & String, what is the **advantages of using AssertJ(offers a fluent api) over Hamcrest**](https://tcsglobal.udemy.com/course/learn-unit-testing-with-spring-boot/learn/lecture/9968382#overview)
* [How will you use **Hamcrest** library to **validate Lists & Strings**](https://tcsglobal.udemy.com/course/learn-unit-testing-with-spring-boot/learn/lecture/9968380#overview)
* [How will you create tests for POST, validate the headers and result](https://tcsglobal.udemy.com/course/learn-unit-testing-with-spring-boot/learn/lecture/9968376#overview)
* [How will you create separate configuration for your tests](https://tcsglobal.udemy.com/course/learn-unit-testing-with-spring-boot/learn/lecture/9968374#overview)
  * Test Specific Properties using @TestPropertySource
  * Have a dedicated resources folder for your tests
* [How will you mock your beans within an **Integration Test with @SpringBootTest**](https://tcsglobal.udemy.com/course/learn-unit-testing-with-spring-boot/learn/lecture/9968370#overview)
* [How will you write integration tests using **``@SpringBootTest & TestRestTemplate``**](https://tcsglobal.udemy.com/course/learn-unit-testing-with-spring-boot/learn/lecture/9968368#overview)
* [What is the use of **@DataJpaTest** -> Launches inmemory database to test the application](https://tcsglobal.udemy.com/course/learn-unit-testing-with-spring-boot/learn/lecture/9968364#overview)
* [What is the difference between Mockito.mock() @Mock & @MockBean](https://www.baeldung.com/java-spring-mockito-mock-mockbean#:~:text=We%20can%20use%20the%20%40MockBean,new%20one%20will%20be%20added.)
* [how will do perform **testing of your Controller Class** using **@WebMvcTest** & MockMvc](https://tcsglobal.udemy.com/course/learn-unit-testing-with-spring-boot/learn/lecture/9968330#overview)
* [How does **``MockMvcResultMatchers.content().json()`` internally work**-> uses **JSONAssert.assertEquals()** (JSONAssert is used for testing Jsons, What is the difference between "strict" set to false from setting it to true)](https://www.baeldung.com/jsonassert)

* [What is the difference between @BeforeAll(-> executed once during class initialization)& @BeforeEach(-> executed before each test @LocalServerPort(-> used to get the local server port of randomPort)) annotation](https://youtu.be/Hh17JDpsKqc?t=604)
* [What is code coverage? !!!!Practical Pending!!!!](https://youtu.be/wL2DxBJDj_8?t=695)
  * Code coverage is a software metric used to measure how many lines of code were executed during a software test
* [Jacoco](https://www.baeldung.com/jacoco) Jacoco is a maven plugin that may be used to generate coverage reports
* [What is SonarQube !!!!Practical Pending!!!!](https://youtu.be/hyBznKcoKEg?t=66) SonarQube is an opensource platform developed by SonarSource for the following purposes: 
  1) continous inspection of code quality 
  2) to perform automatic inspection of code quality 
  3) to perform automatic reviews with static analysis of code to detect bugs, code smells, security vulnerabilities in 20 different programming language

  * Sonar may be used online with github repos
  * Or it may be used as an eclipse or intellij plugin 

