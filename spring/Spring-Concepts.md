If you define a @Configuration with @EnableWebSecurity anywhere in your application it will switch off the default webapp security settings in Spring Boot 

If you add @EnableWebSecurity and also disable Actuator security, you will get the default form-based login for the entire application

spring-boot-starter-security : Default setting from spring security.

@EnableWebSecurity: Switch off the Boot default configuration. You will get the default form-based login for the entire application.

WebSecurityConfigurerAdapter: Provides way to customise default setting.


The auto configuration of Spring Boot automatically enables web security and retrieves all beans of the type WebSecurityConfigurerAdapter to customize the configuration if certain conditions are met (spring-boot-starter-security on the classpath etc.). The auto configuration for web security is enabled in the class 


```
| Annotation | Meaning                                             |
+------------+-----------------------------------------------------+
| @Component | generic stereotype for any Spring-managed component |
| @Repository| stereotype for persistence layer                    |
| @Service   | stereotype for service layer                        |
| @Controller| stereotype for presentation layer (spring-mvc)      |
| @Bean      | Explicit declaration of generic bean                |
```

@Service, @Controller, @Repository = {@Component + some more special functionality}


@Component Vs @Bean:
@Component (and @Service and @Repository) are used to auto-detect and auto-configure beans using classpath scanning. There's an implicit one-to-one mapping between the annotated class and the bean (i.e. one bean per class). Control of wiring is quite limited with this approach, since it's purely declarative.

@Bean is used to explicitly declare a single bean, rather than letting Spring do it automatically as above. It decouples the declaration of the bean from the class definition, and lets you create and configure beans exactly how you choose.


@Autowired Vs @Inject:
@Autowired is Spring's own (legacy) annotation. @Inject is part of a new Java technology called CDI that defines a standard for dependency injection similar to Spring. In a Spring application.
So in theory if you used @Inject you could replace spring with another DI framework e.g. Guice and inject your dependencies in the same way.


**Spring defines 5 types of scopes:** @Scope("prototype")

singleton,
prototype,
request,
session,
globalSession
