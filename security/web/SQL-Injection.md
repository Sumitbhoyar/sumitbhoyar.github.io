# SQL Injection

SQL injection is a type of injection attack. Injection attacks occur when maliciously crafted inputs are submitted by an attacker, causing an application to perform an unintended action. 

**Example**

Code:

    SELECT * FROM users WHERE email = ' " +email + "' AND pass  = ' " +pass+ " ' 

Input:

    ' or 1=1 --

Generated query:

    SELECT * FROM users WHERE email = 'user@email.com' AND pass  = ' ' or 1=1 -- ' LIMIT 1

**Risk**

- Extract sensitive information, like Social Security numbers, or credit card details.
- Enumerate the authentication details of users registered on a website, so these logins can be used in attacks on other sites.
- Delete data or drop tables, corrupting the database, and making the website unusable.
- Inject further malicious code to be executed when users visit the site.


**Prevention**

- Parameterized Statements
- Object Relational Mapping
- Escaping Inputs
- Sanitizing Inputs

