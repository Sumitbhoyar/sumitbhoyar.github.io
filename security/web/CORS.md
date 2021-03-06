# Cross-Origin Resource Sharing (CORS)

Cross-Origin Resource Sharing (CORS) is a technique for relaxing the same-origin policy, allowing Javascript on a web page to consume a REST API served from a different origin.

Cross-origin resource sharing (CORS) is a standard for accessing web resources on different domains. CORS allows web scripts to interact more openly with content outside of the original domain, leading to better integration between web services.

In cases where cross-domain scripting is desired, CORS allows web developers to work around the same-origin policy. CORS adds HTTP headers which instruct web browsers on how to use and manage cross-domain content. The browser then allows or denies access to the content based on its security configuration.

## Step-by-step, here’s how CORS works:

1. A user opens a resource on a webpage which references another domain. This is usually a JavaScript file, but can include fonts and CSS resources.
2. The user’s browser creates a connection to the second domain, adding an “Origin” HTTP header to the request which contains the first domain.
3. The second domain replies with an “Access-Control-Allow-Origin” HTTP header which lists the domains allowed to make CORS requests. A wildcard (“*”) allows all domains to make requests.
4. If the first domain is allowed to make the request, the second domain responds with the requested content.
5. The Access-Control-Allow-Origin header is defined in the second domain’s server configuration. If the header doesn’t contain wildcards and the first domain isn’t explicitly included, the browser displays an error message.

## Pre-Flight Request
Most servers will allow GET requests but may block requests to modify resources on the server. Servers don't just blindly block such requests though; they have a process in place that first checks and then communicates to the client (your web browser) which requests are allowed.
When a request is made using non GET methods, a standard preflight request will be made before the original request.

Preflight requests use the OPTIONS header. The preflight request is sent before the original request, hence the term "preflight." The purpose of the preflight request is to determine whether or not the original request is safe (for example, a DELETE request). The server will respond to the preflight request and indicate whether or not the original request is safe. If the server specifies that the original request is safe, it will allow the original request. Otherwise, it will block the original request.

## Examples
**Direct GET Request**

    GET /greeting/ HTTP/1.1
    User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_5) AppleWebKit/536.30.1 (KHTML, like Gecko) Version/6.0.5 Safari/536.30.1
    Accept: application/json, text/plain, */*
    Referer: http://foo.client.com/
    Origin: http://foo.client.com

**GET Request Response**

    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8
    Date: Wed, 20 Nov 2013 19:36:00 GMT
    Server: Apache-Coyote/1.1
    Content-Length: 35
    Connection: keep-alive
    Access-Control-Allow-Origin: http://foo.client.com
    [response payload]


**PreFlight Request**

    OPTIONS /resource/12345
    User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_5) AppleWebKit/536.30.1 (KHTML, like Gecko) Version/6.0.5 Safari/536.30.1
    Access-Control-Request-Method: DELETE
    Access-Control-Request-Headers: origin, x-requested-with, accept
    Origin: http://foo.client.com

**PreFlight Response**

    HTTP/1.1 200 OK
    Date: Wed, 20 Nov 2013 19:36:00 GMT
    Server: Apache-Coyote/1.1
    Content-Length: 0
    Connection: keep-alive
    Access-Control-Allow-Origin: http://foo.client.com
    Access-Control-Allow-Methods: POST, GET, OPTIONS, DELETE
    Access-Control-Max-Age: 86400


## Enabling Cross Origin Requests for a RESTful Web Service
**Controller level**

    @CrossOrigin(origins = "http://localhost:9000")
    @GetMapping("/greeting")
	
**Global Configuration**

    @Bean
    public WebMvcConfigurer corsConfigurer() {
    	return new WebMvcConfigurerAdapter() {
    		@Override
    		public void addCorsMappings(CorsRegistry registry) {
    			registry.addMapping("/greeting").allowedOrigins("http://localhost:9000");
    			//registry.addMapping("/**");
    		}
    	};
    }

## References:
https://www.keycdn.com/support/cors

https://spring.io/understanding/CORS

https://spring.io/blog/2015/06/08/cors-support-in-spring-framework

https://enable-cors.org/server.html
