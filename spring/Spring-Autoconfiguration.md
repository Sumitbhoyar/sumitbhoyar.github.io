**Spring Auto-configuration**
-----------------------------

Spring Boot auto-configuration attempts to automatically configure your Spring application based on the jar dependencies that you have added. For example, If HSQLDB is on your classpath, and you have not manually configured any database connection beans, then we will auto-configure an in-memory database.

Spring Boot looks at a) Frameworks available on the CLASSPATH b) Existing configuration for the application. Based on these, Spring Boot provides basic configuration needed to configure the application with these frameworks. This is called Auto Configuration.

All auto configuration logic is implemented in spring-boot-autoconfigure.jar.

You need to opt-in to auto-configuration by adding the @EnableAutoConfiguration or @SpringBootApplication annotations to one of your @Configuration classes.

Auto-configuration is **noninvasive**, at any point you can start to define your own configuration to replace specific parts of the auto-configuration. For example, if you add your own DataSource bean, the default embedded database support will back away.

@ConditionalOnClass({ DataSource.class, EmbeddedDatabaseType.class }) : This configuration is enabled only when these classes are available in the classpath.

@ConditionalOnMissingBean : This bean is configured only if there is no other bean configured with the same name.

Disabling specific auto-configuration

@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})

Existing example in Spring Boot

When we use Spring MVC, we need to configure component scan, dispatcher servlet, a view resolver, web jars(for delivering static content) among other things.


Debugging Auto Configuration

logging.level.org.springframework: DEBUG
Spring Boot Actuator


Resources

http://www.springboottutorial.com/spring-boot-auto-configuration
https://docs.spring.io/spring-boot/docs/current/reference/html/using-boot-auto-configuration.html

