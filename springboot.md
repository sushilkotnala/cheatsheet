# Spring Boot

For all Spring projects you should start with **[Spring Initializr](https://start.spring.io/)**

Parent entry added in the pom.xml when maven is choosen as build tool.
```maven
<parent>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-parent</artifactId>
	<version>2.3.3.RELEASE</version>
	<relativePath/> <!-- lookup parent from repository -->
</parent>
```
Dependency of **spring-boot-starter-web** is added by default.

```maven
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-web</artifactId>
</dependency>
```
Plugin for **sping-boot-maven-plugin** is added by default.
```maven
<build>
	<plugins>
		<plugin>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-maven-plugin</artifactId>
		</plugin>
	</plugins>
</build>
```
## Web application
Create a web application with ***@RestController*** annotation in class defination.
```java
@RestController
public class HelloController {

	@RequestMapping("/")
	public String index() {
		return "Greetings from Spring Boot!";
	}
}
```
Fagging the class with @RestController annotation means that the class is ready to handle the web requests.

*@RestController* does the functionality of *@Controller* and *@ResponseBody*, two annotation which help to respond with text to web request instead of view.

## Simple application
Simple application is created in SpringBoot using ***@SpringBootApplication*** annotation. 
The main method of this class is invoked while project startup.

```java
@SpringBootApplication
public class SimpleApplication {

	public static void main(String[] args) {
		SpringApplication.run(SimpleApplication.class, args);
	}
}	
```
**@SpringBootApplication** adds the following funtionality

 1. ***@Configuration*** tags the class as source of bean definations for application context.
 2. ***@EnableAutoConfiguration*** its starts adding beans automatically as per classpath.
 3. ***@ComponentScan*** looks for other components, configuration and services in specified packages, letting it find the controllers.


## Difference between @Component, @Service, @Repository

### @Components 
These are spring managed beans, these are registered by Spring at the start.
***@Service*** and ***@Repository*** are technically components only, but are used for different purpose.
***@Service*** is a pure bean used for business logic.
***@Repository*** is specific case of component, which catches persistence layer specific exception and retrows them as unified Spring specific unchecked exceptions.
> Check how to add bean into application context, specially the unified unchecked exception post processor.

# Spring Annotations
## DI related annotations
 1. ### _@Autowired_
	 @Autowired, marks a dependency which can be resolved and injected by Spring.
	 It can used with constructor, setters and field injections.
	 It has a boolean *required* which is true by default, if true it will throw exception if any of the dependency is not meet.
	 
	#### Constructor injection
	
	 ```java
	class Car {
	    Engine engine;

		 @Autowired
		 Car(Engine engine) {
		     this.engine = engine;
		 }
	 }
	```
	In constructor inject, all fields are mandatory.
	#### Setter injection
	```java
	class Car {
	    Engine engine;
	 
	    @Autowired
	    void setEngine(Engine engine) {
	        this.engine = engine;
	    }
	}
	```
	#### Field injection
	```java
	class Car {
	    @Autowired
	    Engine engine;
	}
	```
 2. ### _@Bean_
 @Bean marks a factory method which generated Spring beans.
```java
@Bean
Engine engine() {
    return new Engine();
}
```
 Spring calls these methods when a new instance of return type is required.
By default the bean name is same as that of factory method, but it can be changed using the name/ value attribute of @Bean.
```java
@Bean("engine")
Engine getEngine() {
    return new Engine();
}
```
*All the methods annotated with **@Bean** must be in the classes annotated with **@Configuration***

 3. ### _@Qualifier_

	@Qualifier annotation can be used with @Autowired in case of ambigous situations.
	#### Contructor
	```java
	@Autowired
	Biker(@Qualifier("bike") Vehicle vehicle) {
	    this.vehicle = vehicle;
	}
	```
	#### Setter
	```java
	@Autowired
	@Qualifier("bike")
	void setVehicle(Vehicle vehicle) {
	    this.vehicle = vehicle;
	}
	```
	#### Field injection
	```java
	@Autowired
	@Qualifier("bike")
	Vehicle vehicle;
	```

 4. ### _@Required_
	 @Required on setter marks the dependencies which we want to populate using xml. Otherwise, _BeanInitializationException_ will be thrown.
  
 5. ### _@Value_
	 It can used for injecting property values. It can pick values from external properties file.
	```java
	@Value("8")
	void setCylinderCount(int cylinderCount) {
	    this.cylinderCount = cylinderCount;
	}
	```
	Reading value from external properties file and injecting into property.
	> engine.fuelType=petrol
	```java
	@Value("${engine.fuelType}")
	String fuelType;
	```
 6. ### _@DependsOn_
	 It make Spring initilise the dependent beans first, this behaviour is default, but might be required in case of static blocks and static variables.
	 ``` java
	 @DependsOn("engine")
	class Car implements Vehicle {}
	```
	 Incase of factory method.
	 ```java
	 @Bean
	@DependsOn("fuel")
	Engine engine() {
	    return new Engine();
	}
	```
 7. ### _@Lazy_
It is used when we want to load the bean lazily, when actual required. By default, Spring loads all the depencencies and bean at the application start time and application context bootstraping, but there could be scenarios where we want to initilize the bean when they are actually required. This is done mostly in cases where the bean creation is costly.

This is annotation behaves differently depending on the place it is placed.

-   _@Bean_  annotated bean factory method, to delay the method call (hence the bean creation)
-   _@Configuration_  class and all contained  _@Bean_  methods will be affected
-   _@Component_  class, which is not a  _@Configuration_  class, this bean will be initialized lazily
-   _@Autowired_  constructor, setter, or field, to load the dependency itself lazily (via proxy)

	```java
	@Configuration
	@Lazy
	class VehicleFactoryConfig {
	 
	    @Bean
	    @Lazy(false)
	    Engine engine() {
	        return new Engine();
	    }
	}
	```
8. ### _@Lookup_
A method annotated with _@Lookup_ tells Spring to return an instance of the method’s return type when we invoke it.

9. ### _@Primary_
 Sometimes we have multiple beans of same type, although we can use qualifier to differentiate between the beans, but __@primary__ annotation provides as faility with which Spring can quickly use the most frequently used bean of that type.

```java
	@Component
	@Primary
	class Car implements Vehicle {}
	 
	@Component
	class Bike implements Vehicle {}
	 
	@Component
	class Driver {
	    @Autowired
	    Vehicle vehicle; // This will pick the bean with @primary annotation.
	}
	 
	@Component
	class Biker {
	    @Autowired
	    @Qualifier("bike")
	    Vehicle vehicle; //This will use the @Qualifier value.
	}
``` 


10. ### _@Scope_
We use _@Scope_ to define the scope of a _@Component_ class or a _@Bean_ definition. It can be either __singleton, prototype, request, session, globalSession__ or some custom scope.
```java
@Component
@Scope("prototype")
class Engine {}
```

## Context Configuration Annotations 

 1. ### _@Profile_
	 If you want to use some _*@Component*_ class and _*@Bean_* method, when a specific profile is active. We can configure the name of the profile with the _value_ argument of the annotation.
	```java
	@Component
	@Profile("sportDay")
	class Bike implements Vehicle {}
	```

 2. ### _@Import_
	 We can use specific *@Configuration* classes without component scanning the package with this annotation.
	```java
	@Import(VehiclePartSupplier.class)
	class VehicleFactoryConfig {}
	```
 3. ### _@ImportResource_
	 We can **import XML configurations** with this annotation. We can specify the XML file locations with the _locations_ argument, or with its alias, the _value_ argument.
	```java
	@Configuration
	@ImportResource("classpath:/annotations.xml")
	class VehicleFactoryConfig {}
	```
 4. ### _@PropertySource_
	 With this annotation, we can **define property files for application settings**.
	```java
	@Configuration
	@PropertySource("classpath:/annotations.properties")
	class VehicleFactoryConfig {}
	```
	_@PropertySource_ leverages the Java 8 repeating annotations feature, which means we can mark a class with it multiple times
	```java
	@Configuration
	@PropertySource("classpath:/annotations.properties")
	@PropertySource("classpath:/vehicle-factory.properties")
	class VehicleFactoryConfig {}
	```
 5. ### _@PropertySources_
	 This can used for specifing multiple _@PropertySource_ configuration.
	```java
	@Configuration
	@PropertySources({ 
	  @PropertySource("classpath:/annotations.properties"),
	  @PropertySource("classpath:/vehicle-factory.properties")
	})
	class VehicleFactoryConfig {}
	```

## Spring Boot annoations

 1. ### _@SpringBootApplication_
 2. ### _@EnableAutoConfiguration_
 3. ### Auto-Configuration Conditions
 
	 1. #### _@ConditionalOnClass_  and  _@ConditionalOnMissingClass_
	 2. #### _@ConditionalOnBean_  and  _@ConditionalOnMissingBean_
	 3. #### _@ConditionalOnProperty_
	 4. #### _@ConditionalOnResource_
	 5. #### _@ConditionalOnWebApplication_  and _@ConditionalOnNotWebApplication_
	 6. #### _@ConditionalExpression_
	 7. #### _@Conditional_

## Spring Bean annotations

## Common Spring data annotations
 1. ###  _@Transactional_
 2. ### _@NoRepositoryBean_
 3. ### _@Param_
 4. ### _@Id_
 5. ### _Transient_
 6. ### _@CreatedBy_,  _@LastModifiedBy_,  _@CreatedDate_,  _@LastModifiedDate_

## Spring Data JPA Annotations
 1. ### _@Query_
 2. ### _@Procedure_
 3. ### _@Lock_
 4. ### _@Modifying_
 5. ### _@EnableJpaRepositories_
 
## Spring Scheduling annotations
 1.	### _@EnableAsync_
 2.	### _@EnableScheduling_
 3.	### _@Async_
 4.	### _@Scheduled_
 5.	### _@Schedules_

