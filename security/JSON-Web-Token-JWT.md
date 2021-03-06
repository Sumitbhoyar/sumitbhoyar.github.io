**JSON Web Token (JWT)**
-------------------------

**A JSON Web Token (JWT)** is a JSON object is safe way to represent a set of information between two parties. 

This information can be verified and trusted because it is digitally signed.

**When should you use JSON Web Tokens?**

- Authentication: This is the most common scenario for using JWT. Once the user is logged in, each subsequent request will include the JWT, allowing the user to access routes, services, and resources that are permitted with that token. Single Sign On is a feature that widely uses JWT nowadays, because of its small overhead and its ability to be easily used across different domains.

- Information Exchange: JSON Web Tokens are a good way of securely transmitting information between parties. Because JWTs can be signed—for example, using public/private key pairs—you can be sure the senders are who they say they are. Additionally, as the signature is calculated using the header and the payload, you can also verify that the content hasn't been tampered with.

**What is the JSON Web Token structure?**

JSON Web Tokens consist of three parts separated by dots (.), which are:

Header.
Payload.
Signature

Therefore, a JWT typically looks like xxxxx.yyyyy.zzzzz

- **Header**

> The header typically consists of two parts: the type of the token, which is JWT, and the hashing algorithm being used, such as HMAC SHA256 or RSA.

- **Payload**

> The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional metadata. 


- **Signature**

> To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.
```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```
The signature is used to verify that the sender of the JWT is who it says it is and to ensure that the message wasn't changed along the way.


***How does JWT protect our data?***

- Client requests to server.
- Server asks authenticate user.
- Server sends JWT to client. It will have Header.Payload.Signature.  Signature has hashed header and payload along with secret.
- Client sends this JWT token along with each request. When server gets the request along with token, it will decrypt the signature using signature secret. If it can then token is valid and is not tampered.
If it cannot then it is possible attack and server denies the request.

**Implementation using spring security**

https://medium.com/@nydiarra/secure-a-spring-boot-rest-api-with-json-web-token-reference-to-angular-integration-e57a25806c50

https://github.com/nydiarra/springboot-jwt

http://www.baeldung.com/spring-security-oauth-jwt


References:

https://medium.com/vandium-software/5-easy-steps-to-understanding-json-web-tokens-jwt-1164c0adfcec


https://jwt.io/introduction/
