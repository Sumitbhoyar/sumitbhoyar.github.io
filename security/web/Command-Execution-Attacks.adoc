# Command Execution Attacks

If an attacker can execute arbitrary code on your servers, your systems are almost certainly going to be compromised. 

Command injection vulnerabilities often occur in older, legacy code, such as CGI scripts.

**Example** 
google.com && cat /etc/passwd


**Risk**

- After gaining access, an attacker will attempt to escalate their privileges on the server, install malicious scripts, or make your server part of a botnet to be used at a later date.

**Prevention**

- Try to Avoid Command Line Calls Altogether: 
- Use APIs wherever possible – only use shell commands where absolutely necessary. This will reduce the number of attack vectors in your application, and will also simplify your codebase.
- Escape Inputs Correctly
- Restrict the Permitted Commands. 
- Perform Thorough Code Reviews
- Run with Restricted Permissions
