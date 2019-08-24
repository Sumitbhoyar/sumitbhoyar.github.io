# Security Principles

### Principle of Least Privilege:
Applications should ensure that each process or software component can access and affect only the resources it needs. Apply “levels of clearance” as appropriate, in the same way that only certain bank employees have access to the vault. Applying restricted privileges can help mitigate a lot of the risk around injection attacks.

### Password Hashing
Storing unencrypted passwords is a major security flaw in itself. Applications should store user passwords as strong, one-way hashes, preferably salted. This mitigates the risk of malicious users stealing credentials, or impersonating other users.

### Third Party Authentication
It is often worth considering out-sourcing the authentication workflow of your application entirely. Facebook, Twitter, and Google all provide mature OAuth APIs, which can be used to let users log into your website using their existing accounts on those systems. This saves you as an application developer from rolling your own authentication, and assures your users that their passwords are only stored in a single location.

### HTTP-only Cookies
A session-hijacking attack can use malicious JavaScript to steal the cookie containing the user’s session ID. There is rarely a good reason to read or manipulate cookies in client-side JavaScript, so consider marking cookies as HTTP-only, meaning that cookies will be received, stored, and sent by the browser, but cannot be modified or read by JavaScript.

### Content Security Policy
The web’s security model is rooted in the same origin policy. 
Code from https://mybank.com should only have access to https://mybank.com’s data, and https://evil.example.com should certainly never be allowed access. Each origin is kept isolated from the rest of the web, giving developers a safe sandbox in which to build and play. 