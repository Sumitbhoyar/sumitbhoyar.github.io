
# Clickjacking 

Click-jacking attacks trick web users into performing an action they did not intend, typically by rendering an invisible page element on top of the action the user thinks they are performing.

**Example**

     < body>
        < iframe src="www.kittens.com/vacuum-revenge">
        < /iframe>
        < div>
          < a href="https://www.facebook.com/sharer/sharer.php?u=http%3A%2F%2Fwww.buttholebalm.com&p[title]=Itchy"></a>
        < /div>
      < /body>

**Risk**

- Harvest login credentials, by rendering a fake login box on top of the real one.
- Trick users into turning on their web-cam or microphone, by rendering invisible elements over the Adobe Flash settings page.
- Spread worms on social media sites like Twitter and MySpace.
- Promote online scams by tricking people into clicking on things they otherwise would not.
- Spread malware by diverting users to malicious download links.
  
**Protection**

- X-Frame-Options
The X-Frame-Options HTTP header can be used to indicate whether or not a browser should be allowed to render a page in a < frame>, < iframe> or < object> tag.

There are three permitted values for the header:

DENY: The page cannot be displayed in a frame, regardless of the site attempting to do so.

SAMEORIGIN: The page can only be displayed in a frame on the same origin as the page itself.

ALLOW-FROM *uri*:	The page can only be displayed in a frame on the specified origins.

- Content Security Policy
The Content-Security-Policy HTTP header is part of the HTML5 standard, and provides a broader range of protection than the X-Frame-Options header Content-Security-Policy: frame-ancestors 'none' The page cannot be displayed in a frame, regardless of the site attempting to do so. Content-Security-Policy: frame-ancestors 'self' The page can only be displayed in a frame on the same origin as the page itself. Content-Security-Policy: frame-ancestors *uri* The page can only be displayed in a frame on the specified origins.
