
**Declared in AHTTPMessage**


The following sections are a listing of the part that will be probably affected by the refactor
## Request
Body derived from AHTTPMessage
HttpRequest.cpp 
- line 40
- line 92
### request manager
The following function will be affected
RequestManager.cpp
- SetBody 192, 194
- SetbodyWithSize line 212
- SetBodyWithChunks  line 228 ?
## Response
Body derived from AHTTPMessage
HttpResponse.cpp:
- Line 21
- line 112
HttpResponseError.cpp
- Line 13
- Line 27
- Line 32
- Line 42
- Line 43

### virtualServer
VirtualServer.cpp
- placeholderResponse line 140
- errorResponse line 145
- redirectResponse line 150
- deleteFile line 174
- servefile line 187, 192
- serveListing line 224
- buildResponse with the latters function.
## Next step
Delete the HttpBody object
- HttpBody.cpp 
- HttpBody.hpp
Applied the step below and adapt all the point mentioned earlier.
### New  body data structure
Put in HttpResponse
```cpp
struct {
	int fd;
	std::string strBody; 
	std::stringstream strbody; // alternate option for body in the form of string
	int type; // enum 1 FileDescriptor 2 String (or stringstream)
} body
```

### New constructors
HttpResponse
```cpp
HttpResponse::HttpResponse(httpCode_t codeHttp, mapHttpHeaders &map, int fdBody)
HttpResponse::HttpResponse(httpCode_t codeHttp, mapHttpHeaders &map, std::string strBody)
HttpResponse::HttpResponse(httpCode_t codeHttp, mapHttpHeaders &map, std::stringstream strBody)] // ?
```

HttpResponseError
If we go with this kind of constructor for HttpResponseError I guess we don't need to have the HttpResponseError class neither the HttpResponseRedirect.
```cpp
HttpResponseError::HttpResponseError(httpCode_t codeHttp, mapHttpHeaders &map, int fdBody)
HttpResponseError::HttpResponseError(httpCode_t codeHttp, mapHttpHeaders &map, std::string strBody)
```
## New methods
HttpResponse
```cpp
getBodyType()//  return the type of body. Fd or string(stream)

template< typename T> 
T &getBody() // return the body in the form FD or string (stream)
```

The object response will not put the Content-Length or Transfer-Encoding in the response header. The part of Benoit should do it.

### Logic out of HttpResponse object
Like mentioned earlier the goal of the new HttpResponse is to be the most straightforward as possible. 
I guess that the logic will be put in the buildresponse and ResponseManager/RequestManager. It is a proposition I'm open to suggestion.


## Update
- [X] Body removed from Ahttpmessage
- [X] Body removed from HTTPRequest
- [X] Body removed from HTTPResponse
- [X] Body class removed (HttpBody.hpp HttpBody.cpp)
- [ ] Struct added in httpResponse
	- [x] Add the new contructors
	- [ ] Test the new structure



