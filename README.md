## Zuul Eureka and Cloud Configuration

#### Prerequisites

+ [Java 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 
+ [Gradle](https://gradle.org/)

#### Run
+ Start each component in this order - waiting on the previous component to be completely started:
  + eureka component 

     `cd components/eureka && ./gradlew clean bootrun`

  + cloud-config component _(wait for eureka to start)_
     
     `cd components/cloud-config && ./gradlew clean bootrun`

  + zuul component _(wait for cloud-config to start)_
     
     `cd components/zuul && ./gradlew clean bootrun`

  + netflix-protected _(wait for cloud-config to start)_

     `cd components/netflix-protected && ./gradlew clean bootrun`

#### Verification
+ start all of the components
+ hit the zuul endpoint that should call through to the netflix-protected api, expect output that reads `hello world!`
  `curl http://localhost:8080/netflix-protected/hello`

#### Useful endpoints

 + __eureka registry__ --> http://localhost:8282
 
 + __netflix-protected without zuul__ --> http://localhost:8181/hello
 
 + __netflix-protected with zuul__ --> http://localhost:8080/netflix-protected/hello
 
 + __zuul cloud-config__ --> http://localhost:9999/zuul/default
 
 + __netflix-protected cloud-config__ --> http://localhost:9999/netflix-protected/default
