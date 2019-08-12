# Logging

Logging refers to the recording of activity. Logging is a common issue for development teams. Several frameworks ease and standardize the process of logging for the Java platform. 

### Functionality overview
Logging is broken into three major pieces: the Logger, Formatter and the Handler (Appender).

##### Logger

A Logger is an object that allows the application to log without regard to where the output is sent/stored. The application logs a message by passing an object or an object and an exception with an optional severity level to the logger object under a given a name/identifier.
```concept
LOGGER LOGGER = LOGGER.GETLOGGER(MYCLASS.CLASS.GETNAME());
```

##### Logging Events
Loggers provide several methods for triggering log events. However, before you can log an event, you need to assign a level. Log levels determine the severity of the log and can be used to filter the event or send it to a different Appender.
```concept
LOGGER.LOG(LEVEL.WARNING, “THIS IS A WARNING!”);
LOGGER.WARNING(“THIS IS A WARNING!”);
```

##### Formatters or renderers

A Formatter is an object that formats a given object. Mostly this consists of taking the binary object and converting it to a string representation.

##### Appenders or handlers

Appenders listen for messages at or above a specified minimum severity level. The Appender takes the message it is passed and posts it appropriately. Message dispositions include:

- display on the console
- write to a file or syslog
- append to a database table
- distribute via Java Messaging Services
- send via email
- write to a socket
- discard to the “bit-bucket” (/dev/null)

The more common approach is to add an Appender using the configuration file. With java.util.logging, Appenders are defined in a comma-separated list. This example adds both the console and a log file as destinations.

```concept
HANDLERS=JAVA.UTIL.LOGGING.CONSOLEHANDLER, JAVA.UTIL.LOGGING.FILEHANDLER
```

##### Types of Appenders
**ConsoleAppender**:
simply displays log entries in the console. The ConsoleAppender is used as the default Appender for many logging frameworks and comes preconfigured with basic settings. 

**FileAppenders**
FileAppenders write log entries to files. FileAppenders are responsible for opening and closing files, appending entries to files, and locking files to prevent data corruption or overwriting.



### Logging in Java
Java contains the Java Logging API. This logging API allows you to configure which message types are written. Individual classes can use this logger to write messages to the configured log files.

The java.util.logging package provides the logging capabilities via the Logger class.

### Components
```
 |Logger| ---->   |Handler|  ----->   |External System|
     |           _____|______           * Disk
     |          |            |          * Survillence System
 |Filter|   |Filter|   |Formatter|      * etc 
```

All logging is done via a **Logger** instance. Loggers gather the data to be logged into a LogRecord. The LogRecord is then forwarded to a Handler. The **Handler** determines what to do with the LogRecord. For instance, the LogRecord can be written to **External System** like disk, or sent over the network to a surveillance system.

Both Logger's and Handler's can pass the LogRecord through a **Filter** which determines whether the LogRecord should be forwarded or not.

A Handler can also use a **Formatter** to format the LogRecord as a string before it is sent to the external disk or system.

### Logger Hierarchy
The Logger instances are organized into a hierarchy. A Logger further down in the hierarchy will forward messages logged to it, to its ancestors in the hierarchy. Thus, log levels and messages can be filtered or switched on and off for entire branches of the Logger hierarchy at a time.

The name indicates a hierarchy of Loggers. Each . (dot) in the name marks a level in the hierarchy.

These levels are different from the log levels of the messages logged.

When a message is passed to a Logger, the message is passed through the Logger's Filter, if the Logger has a Filter set. The Filter can either accept or reject the message. If the message is accepted, the message is forwarded to the Handler's set on the Logger. If no Filter is set, the message is always accepted.

If a message is accepted by the Filter, the message is also forwarded to the Handler's of the parent Logger's. However, when a message is passed up the hierarchy, the message is not passed through the Filter's of the parent Logger's. The Filter's are only asked to accept the message when the message is passed directly to the Logger, not when the message comes from a child Logger.

Example:
```
Logger logger      = Logger.getLogger("");
Logger logger1     = Logger.getLogger("1");
Logger logger1_2   = Logger.getLogger("1.2");

logger1.addHandler  (new ConsoleHandler());
logger1_2.addHandler(new ConsoleHandler());

logger1.setFilter(new Filter() {
    public boolean isLoggable(LogRecord record) {
    return false;
    }
    });

logger     .info("msg:");
logger1    .info("msg: 1");
logger1_2  .info("msg: 1.2");
```

Output
```
14-01-2012 11:33:21 java.util.logging.LogManager$RootLogger log
INFO: msg:
14-01-2012 11:33:21 logging.LoggingExamples main
INFO: msg: 1.2
14-01-2012 11:33:21 logging.LoggingExamples main
INFO: msg: 1.2
14-01-2012 11:33:21 logging.LoggingExamples main
INFO: msg: 1.2
```

Notice how the first message is still logged once, and the third message still logged three times, once by each Logger in the hierarchy.

The second message, however, the message sent to the middle Logger is not logged at all. The Filter set on the middle Logger which always return false (meaning it never accepts any messages), filters out all messages logged via this Logger. Thus, the second message is never logged, nor propagated up the Logger hierarchy.

Notice though, that the message propagated up the hierarchy from the Logger named 1.2 is still logged by the middle Logger, and still forwarded up to the root Logger. The Filter set on the middle Logger does not touch propagated messages.

### Logging Frameworks
Logging in Java requires using one or more logging frameworks. These frameworks provide the objects, methods, and configuration necessary to create and send log messages. Java provides a built-in framework in the java.util.logging package. There are also many third-party frameworks including Log4j, Logback, and tinylog. You can also use an abstraction layer, such as SLF4J and Apache Commons Logging, which decouples your code from the underlying logging framework so you can switch between logging frameworks on the fly.

### Abstraction Layers
Abstraction layers such as SLF4J decouple the underlying logging framework from your application, allowing you to change logging frameworks on demand. The abstraction layer provides a generic API and determines which logging framework to bind to at runtime based on the frameworks available on the application’s classpath. If a framework is not available on the classpath, the abstraction layer effectively disables log calls. Abstraction layers are useful for when you plan on upgrading or switching frameworks down the road, or if you are developing a library for use in other projects.

### Configuration

##### java.util.logging
java.util.logging stores its configuration in a file called logging.properties. It uses the Properties format to store settings as key/value pairs. When Java is installed, it adds a global configuration file to the lib folder of the Java installation directory. However, you can specify your own configuration file by setting the java.util.logging.config.file property when running a Java program. This lets you create and store logging.properties files with individual projects.

```
# DEFAULT FILE OUTPUT IS IN USER'S HOME DIRECTORY.
JAVA.UTIL.LOGGING.FILEHANDLER.PATTERN = %H/JAVA%U.LOG
JAVA.UTIL.LOGGING.FILEHANDLER.LIMIT = 50000
JAVA.UTIL.LOGGING.FILEHANDLER.COUNT = 1
JAVA.UTIL.LOGGING.FILEHANDLER.FORMATTER = JAVA.UTIL.LOGGING.XMLFORMATTER
```

###### Log4j
Log4j supports multiple different configuration file formats including XML, JSON, and YAML. When your Java application starts, Log4j searches for a log4j2.<format> file in the project directory. If it doesn’t find one, it will default to console output. You can find configuration examples in the Log4j documentation.
      
##### Logback
Logback uses a logback.xml file, which has an XML syntax similar to Log4j. You can also provide a logback.groovy file, which uses the Groovy format instead of XML. 
      

