# Week 25th
## Algorithm
[Jewels and Stones](https://github.com/charleserious/leetcode/tree/master/JavaScript/Algorithms/JewelsAndStones)
There should be an elegant way for solving this simple problem.

## Review
**CSS should be separated into five types of categories**
1. Base
2. Layout
3. Module
4. State
5. Theme

- Base rules
> default rules. They are almost exclusively single element selectors include *attributes selector*, *pseudo-class selectors*, *child selectors*, *sibling selectors*.  

- Layout rules
> divide the page into sections. Layouts should hold one or more modules together.  

- Module rules
> reusable, modular parts of our design. things like *product lists*, *navigation*, *footer*, *gallery* etc.  

- State rules
> state describe how our modules or layouts will look when in particular state. hidden or expanded? active or inactive?   
> state also should describe how modules or layouts looks on screens that are bigger or smaller.   
> state also describing how a module might look in different views.  

- Theme rules
> theme similar to state rules in that they describe how modules or layouts might look.  

Above five simple rules, **KEEP IN MIND EVEYR TIME YOU TYPE STYLE SHEETS**.

## Technique
**Problem**
AngularJS input[date] directive with ngModel
I initially put a legal date value into this directive as model `$scope.chosenDate`, then I retrieve the data through `$scope.chosenDate` back with **undefined**, this is interesting.

**Solution**
Due to my `$scope.chosenDate` is today as `new Date()`, so I construct a new object for the  initial usage as default.
*still digging for why….*

## Share
### HTTP (Part 1)

#### Headers
- General headers
> Used in both client requests and server responses. Some may be more specific to either a client or server message.  
	1. Cache-Control
	2. Connection
	3. Date
	4. Progma
	5. Trailer
	6. Transfer-Encoding
	7. Upgrade: protocol/version
	8. Via
	9. Warning
- Request headers
> Client header data communicates the client’s configuration and preferred document formats to the server. Request headers are used in a client message to provide information about the client self.  
	1. Accept: type/subtype [media type some sort of  MIME ( Multipurpose Internet Mail Extensions) ?]
	2. Accept-Charset
	3. Accept-Encoding
	4. Accept-Language
	5. Authorization: scheme credentials
	6. Cookie
	7. Expect: indicates a client expectation about the server.
	8. From: email address
	9. Host: hostname:port
	10. If-Modified-Since
	11. If-Match
	12. If-None-Match
	13. If-Range
	14. If-Unmodified-Since
	15. Max-Forwards
	16. Proxy-Authorization
	17. Range
	18.  Referer
	19. TE: transfer codings
	20. User-Agent
- Response headers
> Server response headers are used in server responses to communicate information about the server and how it may handle requests.  
	1. Accept-Ranges
	2. Age
	3. ETag
	4. Location
	5. Proxy-Authenticate
	6. Retry-After
	7. Server
	8. Set-Cookie
	9. Vary
	10. WWW-Authenticate
- Entity headers
> Entity headers are used in both client requests and server responses. They supply information about the entity body in an HTTP message.  
	1. Allow
	2. Content-Encoding
	3. Content-Language
	4. Content-Length
	5. Content-Location
	6. Content-MD5
	7. Content-Range
	8. Content-Type
	9. Expires
	10. Last-Modified

#### Client Methods
- GET
- POST
- HEAD
- PUT
- LINK
- UNLINK
- DELETE
- OPTIONS
- TRACE

#### Server Response Codes
- 100 ~ 199
> Information  
	1. 100 Continue
	2. 101 Switching Protocols
- 200 ~ 299
> Client request successful  
	1. 200 OK
	2. 201 Created
	3. 202 Accepted
	4. 203 Non-Authoritative-Information
	5. 204 No Content
	6. 205 Reset Content
	7. 206 Partial Content
- 300 ~ 399
> Client request redirected, further action necessary  
	1. 300 Multiple Choices
	2. 301 Moved Permanently
	3. 302 Found
	4. 303 See Other
	5. 304 Not Modified
	6. 305 Use Proxy
	7. 307 Moved Terporarily
- 400 ~ 499
> Client request incomplete  
	1. 400 Bad Request
	2. 401 Unauthorized
	3. 402 Payment Required
	4. 403 Forbidden
	5. 404 Not Found
	6. 405 Method Not Allowed
	7. 406 Not Acceptable
	8. 407 Proxy Authentication Required
	9. 408 Request Timeout
	10. 408 Conflict
	11. 410 Gone
	12. 411 Length Required
	13. 412 Precondition Failed
	14. 413 Request Entity Too Large
	15. 414 Request URL Too Long
	16. 415 Unsupported Media Type
	17. 416 Request Range Not Satisfiable
	18. 417 Expectation Failed
- 500 ~ 599
> Server errors  
	1. 500 Internal Server Error
	2. 501 Not Implemented
	3. 502 Bad Gateway
	4. 503 Service Unavailable
	5. 504 Gateway Timeout
	6. 505 HTTP Version Not Support

#### Cookie
> Cookies allowed web servers to store state information in the browser. They often used to store session variables, user preferences, or user identity. Cookies are not part of the HTTP specification; however, they have become ubiquitous and are sometimes needed for proper interactions with most websites.  
> Cookies work in the following way: when a server program wishes to store state information in the client, the server issues a `Set-Cookie` header its response to the client, which contains the value it wishes to store. The client is expected to store the information from the `Set-Cookie` header, associated with the URL or domain that issues the cookie. In subsequent requests to that URL or domain, the client should include the cookie information using the `Cookie` header. The server or CGI program uses this information to return a document tailored to the specific client. The server can set an expiration date for the cookie, or just use it for a session that will not survive beyond the current instance of the browser.  

