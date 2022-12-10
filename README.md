# spring-cloud-configs
This repository was created for saving some configurations that are used in my projects with spring cloud.

## Table of contents
* [Spring Cloud Stream Configurations ](#spring-cloud-stream-configs)

### Spring Cloud Stream Examples:

Spring Cloud Stream comes with two programming models: one older and nowadays deprecated model based on the use of annotations 
(for example, @EnableBinding , @Output , and @StreamListener ) 
and one newer model based on writing functions.To implement a publisher, we only need to implement the java.util.function.Supplier functional interface as a Spring Bean. 
For example, the following is a publisher that publishes messages as a String:

```java
    @Bean
    public Supplier<String> myPublisher() {
      return () -> new Date().toString();
  }
```
