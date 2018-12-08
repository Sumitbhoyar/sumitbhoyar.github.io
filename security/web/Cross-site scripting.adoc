# Cross-site scripting 

Cross-site scripting (XSS) vulnerabilities permit a malicious user to execute arbitrary chunks of JavaScript when other users visit your site.

XSS is the most common publicly reported security vulnerability, and part of every hacker’s toolkit.

**Risk**

- Spreading worms on social media sites. Facebook, Twitter and YouTube have all been successfully attacked in this way.
- Session hijacking. Malicious JavaScript may be able to send the session ID to a remote site under the hacker’s control, allowing the hacker to impersonate that user by hijacking a session in progress.
- Identity theft. If the user enters confidential information such as credit card numbers into a compromised website, these details can be stolen using malicious JavaScript.
- Denial of service attacks and website vandalism.
- Theft of sensitive data, like passwords.
- Financial fraud on banking sites.

**Example**

    < script> upvote()< /script>

**Prevention**

- Escape Dynamic Content
- Whitelist Values: a handful of valid values
- Implement a Content-Security Policy:  
By setting a content security policy in the response header, you can tell the browser to never execute inline JavaScript, and to lock down which domains can host JavaScript for a page

> < meta http-equiv="Content-Security-Policy" content="script-src 'self'
> https://apis.google.com">

By whitelisting the URIs from which scripts can be loaded, you are implicitly stating that inline JavaScript is not allowed.

- Sanitize HTML:
If your site stores and renders rich content, you need to use a HTML sensitization library to ensure malicious users cannot inject scripts in their HTML submissions.