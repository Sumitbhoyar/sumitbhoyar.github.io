
# Basic points to remember

### Can you provide a high level overview of the “access control security” in a recent application you had worked?
Access controls are security features that control how users and systems communicate and interact with other systems and resources.
Single sign-on (SSO) is a session/user authentication process that permits a user to enter one name and password in order to access multiple applications. The process authenticates the user for all the applications they have been given rights to and eliminates further prompts when they switch applications during a particular session. For example, SiteMinder, TivoliAccessManager (i.e. TAM), etc provides SSO. 
In one of my application, SiteMinder is configured to intercept the calls to authenticate the user. 
Once the user is authenticated, a HTTP header “SM_USER” is added with the 
authenticated user name. For example “123”. The user header is passed to 
Spring 3 security. 
SiteMinder authenticates the user and adds the SM_USER HTTP header to the application. It removes all the “SM” headers and add them after authenticating the user. This prevents amy malicious headers being injected via the browser with plugins like “Firefox Modify headers”.
The “Security.jar” is a custom component that knows how 
to retrieve user roles for a given user like 123 from a database or LDAP 
server. This custom component is responsible for creating a UserDetails 
Spring object that contains the roles as authorities. Once you have the 
authorities or roles for a given user, you can restrict your application 
URLs and functions to provide proper access control.
The Spring security in this scenario will only be used for authorization.

### What are the different layers of security?
1. **Application-Layer Security**: For example, Spring 3 Security, JAAS (Java Authentication and Authorization) that provides a set of APIs to provide authentication and authorization (aka access control), etc. Spring security tackles security at the JEE level (e.g. URLs, Controller methods, service methods, etc)
2. **Transport-Layer Security**: Java Secure Sockets Extension (JSSE) provides a framework and an implementation for a Java version of the Secure Sockets Layer (SSL) and Transport Layer Security (TLS) protocols and includes functionality for data encryption, server authentication, message integrity, and optional client authentication to enable secure Internet communications. (TLS) 1.0 / (SSL) 3.0, is the mechanism to provide private, secured and reliable communication over the internet between the client and the server. It is the most widely used protocol that provides HTTPS for internet communications between the client (web browsers) and web servers.
3. **Message-Layer Security**: In message-layer security, security information is contained within the SOAP message and/or SOAP message attachment, which allows security information to travel along with the message or attachment. For example, the credit card number is signed by a sender and encrypted for a particular receiver to decrypt. Java Generic Security Services (Java GSS-API) is a token-based API used to securely exchange messages between communicating applications. The GSS-API offers application programmers uniform access to security services on top of a variety of underlying security mechanisms, including Kerberos. The advantage of this over point to point transport layer security is that the security stays with the message over all hops and after the message arrives at its destination. So, it can be used with intermediaries over multiple hops and protocols (e.g. HTTP, JMS, etc). The major disadvantage is that it is more complex to implement and requires more processing.

### What do you understand by the terms trusstores and keystores in Java?
You generally need a truststore that points to a file containing trusted certificates, no matter whether you are implementing the server or the client side. You may or may not need a keystore. The keystore points to a file containing private key. You need a keystore if
1) you are implementing the server side of the protocol, or
2) you are implementing the client side and you need to authenticate yourself to the server.
The keystore will be used for encrypting/signing some thing with your private key while the trust stores will be used mostly to authenticate remote servers. You can use the command line based “keytool” application that is shipped with your JDK to work with keystores/trustores and certificates.

### What is a one-way SSL? What is 2-way SSL?
**One way SSL** just means that the server does not validate the identity of the client. The client generates a random key, encrypts it so that only the server can decrypt it, and sends it to the server. The server and client now have a shared secret that can be used to encrypt and validate the communications in both directions.
In **two-way SSL** authentication, the SSL client application verifies the identity of the SSL server application, and then the SSL server application verifies the identity of the SSL-client application. Two-way SSL authentication is also referred to as client authentication because the application (e.g. RESTful Web service client) acting as an SSL client presents its certificate to the SSL server after the SSL server authenticates itself to the SSL client.

### What are some of the things you will keep in mind to write a more secured Java applications?
1. States are problematic from a security point of view due to sharing the state between the client and server. There are methods around this problem using encryption and other techniques, but again can complicate your solution. But favor stateless services where possible.
2. Favoring immutable objects where applicable. String class was intentionally made immutable in Java for security reasons.
3. Perform proper input validation to prevent any rogue characters. Both client side and server side validation.
4. Always use Prepared or Callable statements. Stay away from ordinary statements.
5. When using third-party frameworks, heed the warnings and best practices recommended by documentation.
6. Handle exceptions properly, and don’t let internal details like server names, database table names, etc to be displayed on the screen. Show generic exceptions where applicable like “An error has occurred, please contact support”
7. Encrypt all sensitive information including the passwords in the .properties files.
8. Subject your application to PEN testing before deploying to production.

### What is declarative and programmatic security?
**Declarative Security** - Declarative security specifies an application's security requirements by using either deployment descriptors or annotations.

**Programmatic Security** - Programmatic security implements an application's security within the application code.

### What are the key characteristics of application security?
Following are the key characteristics of application security.
**Authentication** - Authentication is the means by which a user or client proves to a server that it is authorized to access a specific resource and vice-versa.

**Authorization** - Authorization is the means by which a server determines if a user has permissions to access a specific resource or data.

**Data Integrity** - Data integrity means that the data that is exchanged by a client and server is not modified by an unauthorized third party.

**Confidentiality or Data privacy** - This ensures that information is send to only those users or clients that are authorized to access the data.

**Non-repudiation** - This means that you can prove that a transaction or action has occurred. So a user who has performed a certain action, cannot deny doing so.


### What are Realms, Users, Groups and Roles?
**Realms** - Realms are security domains or protection spaces setup for web or application servers. Each realm has its own authentication scheme and contains a collection of Users and Groups.

**Users** - Users are individual or application entities defined in an identity store that access the application resources.

**Group** - Groups are abstract entities defined in Java EE that contains a set of users having common traits.

**Roles** - Roles are are abstract entities defined in Java EE that has permissions to access a set of secured resources in an application. Users or Groups are mapped to Roles.

### What are the authentication mechanisms used to secure web applications?
Http Basic authentication
Form-based authentication
Digest authentication

### What are the Security risks? 
There are two classes of security problems: **nuisances** and **security breaches**. A nuisance attack merely prevents you from getting your work done - for example it may cause your computer to crash. Security breaches are more serious: your files could be deleted, your private data could be read, or a virus could infect your machine.
If you are the victim of a security breach, any data stored on your machine may be read or corrupted by a bad guy. If you've got important company secrets on your computer, maybe you should surf the net on another machine.