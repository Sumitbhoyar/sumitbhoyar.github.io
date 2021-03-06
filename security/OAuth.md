**OAuth 2.0**
--------------

The OAuth 2.0 authorization framework enables a third-party application to obtain limited access to an HTTP service, either on behalf of a resource owner or by allowing the third-party application to obtain access on its own behalf.

**Roles**

- **Resource owner (a.k.a. the User)** - An entity capable of granting access to a protected resource. When the resource owner is a person, it is referred to as an end-user.
- **Resource server (a.k.a. the API server)** - The server hosting the protected resources, capable of accepting and responding to protected resource requests using access tokens.
- **Client** - An application making protected resource requests on behalf of the resource owner and with its authorization. The term client does not imply any particular implementation characteristics (e.g. whether the application executes on a server, a desktop, or other devices).
- **Authorization server** - The server issuing access tokens to the client after successfully authenticating the resource owner and obtaining authorization.
- **Access token**- represents a user’s permission for the client to access their data.

The OAuth 2.0 specification describes five **grants** (“methods”) for a client application to acquire an access token which can be used to authenticate a request to an API endpoint.

1. **Authorization code grant:** 
The client will redirect the user to the authorization server having "response_type" with the value "code".
The user will then be asked to login to the authorization server and approve the client.
If the user approves the client they will be redirected from the authorisation server back to the client (specifically to the redirect URI) with authorization code.
The client will now send a POST request to the authorization server with grant_type value of "authorization_code", client_id and client_secret.
The authorization server will respond with access_token.

2. **Implicit grant:**
It is intended to be used for user-agent-based clients (e.g. single page web apps).
The client will redirect the user to the authorization server with response_type with the value "token"
The user will then be asked to login to the authorization server and approve the client.
If the user approves the client they will be redirected back to the authorization server with token_type with the value "Bearer"

3. **Resource owner credentials/Password grant**
First party clients both on the web and in native device applications.
The client then sends a POST request with grant_type with the value "password", client_id , client_secret, username, password.
The authorization server will respond with access_token.

4. **Client credentials grant**
This grant is suitable for machine-to-machine authentication where a specific user’s permission to access data is not required.
The client sends a POST request with grant_type with the value "client_credentials", client_id  and client_secret.
The authorization server will respond with access_token.

5. **Refresh token grant**


[[ https://raw.githubusercontent.com/Sumitbhoyar/notes/master/security/WhichGrant.png ]]






