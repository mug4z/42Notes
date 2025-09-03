* Any external library and Boost libraries are forbidden.

- HTTP Hypertext Transfer Protocol.
- client-server communication occurs through HTTP.
- compatible with firefox and/or chrome
- telnet
- Uniform Resource Identifier (URI)
- Uniform Resource Locator (URL)

## First things first.
- read rfc and perform tests with telnet and NGINX.

## Recherche 
- hypertext ?
- websocker en cpp98
- http response status codes.
- NGINX
- CGI 
- non-blocking server ?

## Requirements
What you have to do
- IN -> config file or use a default path.
- server remain non-blocking
- Properly handle client disconnection when necessary.
- poll (or equivalent)
	- use only 1 for all the I/O operations between client and server.
	- never do a read/write without going through it.
- You can use macro and define like FD_SET, FD_CLR, FD_ISSET, FD_ZERO
- The webserver should work with standard webrowser (firefox, chrome)
- NGINX is HTTP 1.1 compliant.
- The http status code must be accurate.
- 

Forbidden:
- use execve another web server
- check the value of errno after performing a read / write.
- not required to use poll()(or equivalent) before reading the config file.
- a request to the server should never hang indefiniely
