

#### **Explain the Life Cycle of a Spring Bean**
The lifecycle of any object means when & how it is born, how it behaves throughout its life, and when & how it dies. Similarly, the bean life cycle refers to when & how the bean is instantiated, what action it performs until it lives, and when & how it is destroyed. <br/>
Bean life cycle is managed by the spring container. When we run the program then, the following happens:
1. the spring container gets started. 
2. the container creates the instance of a bean as per the request
3. the dependencies are injected. 
4. the bean is destroyed when the spring container is closed. 
It is possible to execute custom code on bean instantiation and before the bean is destroyed.


