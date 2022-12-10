# Spring Cloud Examples

## Table of Contents
* [Spring Cloud Stream Examples](#spring-cloud-stream-examples)


### Spring Cloud Stream Examples:

Spring Cloud Stream comes with two programming models: one older and nowadays deprecated model based on the use of annotations 
(for example, *@EnableBinding , @Output , and @StreamListener* ) 
and one newer model based on writing functions.To implement a publisher, we only need to implement the *java.util.function.Supplier* functional interface as a Spring Bean. 
For example, the following is a publisher that publishes messages as a String:
```java
    @Bean
    public Supplier<String> publisher() {
      return () -> "Bye!";
  }
```
A subscriber is implemented as a Spring Bean implementing the *java.util.function.Consumer* functional interface. For example, the following is a
subscriber that consumes messages as Strings:
```java
   @Bean
   public Consumer<String> subscriber() {
     return s -> System.out.println("Hi! ..." + s);
   }
```
To make Spring Cloud Stream aware of these functions we need to declare them using the *spring.cloud.function.definition* configuration property. For example, for the two functions defined previously, this would look as follows:
```java 
spring.cloud.function:
definition: publisher;subscriber
```
Finally, we need to tell Spring Cloud Stream what destination to use for each function. To connect our two functions so that our *subscriber* consumes messages from our *publisher*, we can supply the following configuration:
```java
spring.cloud.stream.bindings:
publisher-out-0:
destination: subscriber-in
subscriber-in-0:
destination: publisher-out
```
