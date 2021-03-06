
# Cross Site scripting - CSRF

Cross-site request forgery (CSRF) vulnerabilities can be used to trick a user’s browser into performing an unwanted action on your site.

A CSRF attack occurs when a user is tricked into interacting with a page or script on a third-party site that generates a malicious request to your site.
All your server will see is an HTTP request from an authenticated user. However, an attacker takes control over the form of the data sent in the request to cause mischief.

## Risk

Any function that your users can perform deliberately is something they can be tricked into performing inadvertently using CSRF. In the most malign cases, CSRF attacks can spread themselves as a worm.

- Steal confidential data.
- Manipulate online surveys.
- Spread worms on social media.
- Install malware on mobile phones.

## Prevention

Server-side actions can also be triggered by forged HTTP requests, unless you explicitly put in protective measures. A CSRF attack occurs when a malicious actor tricks a victim into clicking on a link, or running some code, that triggers a forged request. (This malicious code is typically hosted on a website owned by the attacker, on another domain – hence the “cross-domain” denomination.)

Protecting against CSRF (commonly pronounced “sea-surf”) requires two things: ensuring that GET requests are side-effect free, and ensuring that non-GET requests can only be originated from your client-side code.

#### REST: 
Representation State Transfer (REST) is a series of design principles that assign certain types of action (view, create, delete, update) to different HTTP verbs. REST insists that GET requests are used only to view resources. Keeping your GET requests side-effect free will limit the harm that can be done by maliciously crafted URLs–an attacker will have to work much harder to generate harmful POST requests.

#### Anti-Forgery Tokens: 
Even when edit actions are restricted to non-GET requests, you are not entirely protected. POST requests can still be sent to your site from scripts and pages hosted on other domains. In order to ensure that you only handle valid HTTP requests you need to include a secret and unique token with each HTTP response, and have the server verify that token when it is passed back in subsequent requests that use the POST method (or any other method except GET, in fact.)

This is called an anti-forgery token. Each time your server renders a page that performs sensitive actions, it should write out an anti-forgery token in a hidden HTML form field. This token must be included with form submissions, or AJAX calls. The server should validate the token when it is returned in subsequent requests, and reject any calls with missing or invalid tokens.

#### Ensure Cookies are sent with the SameSite Cookie Attribute:
The Set-Cookie header to help prevent CSRF, and it quickly became supported by the other browser vendors. The Same-Site cookie attribute allows developers to instruct browsers to control whether cookies are sent along with the request initiated by third-party domains.

Setting a Same-Site attribute to a cookie is quite simple:

    Set-Cookie: CookieName=CookieValue; SameSite=Lax;
    Set-Cookie: CookieName=CookieValue; SameSite=Strict;

#### Include Addition Authentication for Sensitive Actions:
