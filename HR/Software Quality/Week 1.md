# Data Life Cycle
- Data has three known states:
	- Data in transit
	- Data in rest
	- Data in use
# S-SDLC
- Secure Software Development Life Cycle
- Common security activities
	- Vulnerability analysis
	- Threat modeling
	- Penetration testing
	- Code analysis
	- White / Black / Gray testing
# Vulnerability, Threat and Risk
- **Vulnerability:** A flaw of weakness in system security procedures, design, implementation, or internal controls that could be exercised and result in a security breach or a violation of the system's security
- **Threat:** Any circumstance or event with the potential to adversely impact an information system through unauthorized access, destruction, disclosure, modification of data, and/or denial of service
- **Risk:** A measure of the extent to which an entity is threatened by a potential circumstance or event
	- `Risk = Chance * Damage`
	- Good to mention **whose** risk it is
# Client-Server model of web
- TCP connection is established, the browser sends a HTTP request asking the web server to provide the wanted document
- The server sends a reply containing the page contents, and (optionally) closes the connection
- The **browser** is **always** the initiating party, the server never "calls back"
- This means that HTTP is a client/server protocol
	- The client will typically be a browser, but can be any program that is capable of sending HTTP requests
# HTTP Versions
- Version 1.0
	- `GET`, `POST`, `HEAD`
- Version 1.1
	- `PUT`, `DELETE`
	- Persistent connections
- Version 2
	- Request multiplexing
		- Asynchronous requests and response
		- Possible to send multiple requests at the same time using a single connection
	- Server push
		- The server tries to predict the resources that will be requested and proactively pushes these resources to the client cache
- Version 3
	- Based on Quick UDP Internet Connections
	- Different network layer structure
	- Native and standard encryption
		- No more HTTP and HTTPS, every HTTP communication is encrypted
# Requests and Responses
- HTTP is line-oriented, just like many other internet protocols
	- Communication takes place using strings of characters, seperated by carriage return and line feed
# GET Request
- Request line
	- Method token
		- `GET`, `POST`, `PUT`, etc.
	- Request URI
		- `/`
	- HTTP Version
		- `HTTP/1.0`
- Request header lines
	- Host
	- Accept:
		- Types of data that we expect to get back
	- Language
	- User-Agent
- Client is free to resend a GET request
- Any parameters are encoded as part of the URL
##  GET Response
- Status line
	- HTTP Version
	- Status code
	- Status message
- Request header lines
	- Content-Length
		- Bytes
	- Content-Type
- Content
# POST Request
```
POST /login.php HTTP/1.0
Host: www.example.com
Pragma: no-cache
Referer: http://www.example.com/login.php
Content-type: application/x-www-form-urlencoded
Content-length: 49

username=jdoe&password=Password123&login=Log+in
```
- Should be used when the action about to be taken has side effects on the server
	- Something is permanently changed
- Cannot be resent by the browser without first asking the user for permission to do so
- Any parameters are "hidden"
- The parameters are encoded as you are used to, but they are hidden in the request rather than being part of the URL
	- URL Encoding refers to the escaping of certain characters by encoding the, using a percent sign followed by two hexadecimal digits
## Security Concern
- As all requests originate on the client-side, that is, on computers of which the user has full control, nothing stops the attacker from **replacing** the browser with something completely different
# Proxy
- There are freely available programs that will aid them in manipulating all data that gets sent to the server
# Referer header
- A referer header us sent by most browsers on most requests
	- The header contains the URL of the document from which the request originated
# Cache
- Local cache
	- Stored in memory or disk on the local machine
- Shared (proxy) cache
	- Typically a server in the LAN
- Some documents should not be cached
	- Banking information
	- live-data
- Cache is handled by HTTP headers
# Cookies
- HTTP is a stateless protocol
	- No ties connecting different requests from the same client
	- Nothing is remembered about a client between requests
- We would like to have state between requests
- Cookies are introduced as an extension to HTTP to give us just the state
- This information is passed back by the client on each subsequent request
- HTTP headers are used for both setting and returning cookie
- When the server wants a cookie from a client it sends a `Set-Cookie` header
	- `Set-Cookie: Customer="79"; Version="1"; Path="/"; Max-Age=1800`
## Drawbacks
- Cookies may be limited in size, so space consuming states cannot be safely represented using cookies
- Cookies are handles on the client-side, so we have to keep making sure that a misbehaving user doesn't change the state to his own liking
# Sessions
- Sessions are server-side collection of variables that make up the state
- How to associate a set of data on the server to the correct client?
	- **Session ID**
	- The common approach is to have the client pass a session ID on each request
## Session hijacking
- Many web sites use a **session-based log-in**, in which a session is initiated once the user has given a valid username and password
- The attacker would not need to know the password of the victim, as the session ID works as a "short-time password" or a **proof of successful authentication** after a user has logged in
- How would the attacker gain access to the session ID?
	- Guess it
	- Calculate it
	- Brute-force it
	- Find it by trial and error
	- Cross-side scripting
	- Packet sniffing
# HTTPS
- Encrypted communication
- Secure Socket Layer - SSL
- Transport Layer Security - TLS
- Encryption only protects the network connection between the client and the server
- When HTTPS is used, the clients will always verify the server's certificate