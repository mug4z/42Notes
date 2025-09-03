l
# Goal
- Handle the HTTP messages as iostream.
- Check the parsing and validity of the HTTP message.

## Classes
https://github.com/jart/cosmopolitan/blob/master/net/http/parsehttpmessage.c 
Parser de message en c a voir pour s'inspirer.
### Headers
- contient les headers sous forme de map
- check la validiter des headers ?
### Body

### Message
- get body
- get fieldline (headers)
- get startline
- get httpVersion.

#### Request
 - [ ] Header
	 - [x] getter
	 - [x] setter
	 - [x] operator<<
		 - [x] Must check the issue with operator<<
 - [x] Getter
 - [x] Setter
 - [x] Parse Startline
 - [x] Getter
	 - [x] method
	 - [x] location
 - [x] Setter 
	 - [x] method
	 - [x] location
 - [ ] Operator=
 - [x] get location 
 - [x] get method
 - [ ] copy constructor
 - [ ] Ajouter les logs au bon endroit 
 - [ ] Gestion des erreurs.
	 - [ ] L'objet request a un nouveau flag qui est set si il y a un probleme.
	 - [ ] Le status est set dans le headers et dans le body.
 - [ ] operator<<
## Review
Functional

  - [x] HttpHeader::setHeaders() should clear existing setters first (NULL from default constructor) 

Structural

  - [x] AHttpMessage class should ideally have member variables that are inherited by HttpRequest & HttpResponse (such as m_startLine, m_headers & m_body) along with getters/setters.
  - [x] Protected members -> Private members when not inherited (may require using getters for copy constructors or '=' operators)
  - [ ] Consider that LogManager.hpp may not be accessible in current structure.

Optimizations
- [x] Change istream to string stream.
  - [x] HttpBody::setBody() : use string stream method to simplify (not reading char by char) 
 - [x]  HttpHeader::setHeaders() : colon char check can be simplified through splitting the  key/values by first ':' and then adding the ':' char to invalid character set.
 - [x] HttpHeader::isContainspace : should also consider other whitespaces, not just ' '.
 - [x] Copy constructors can utilise '=' operator for simplification.

Other
 - [x] Remove comments from Makefile
  
- [x] suprimer  le constructor de AHttpMessage. utiliser les valeur deriver dans le constructeur de request.

#### Response
- [ ] Constructor avec http request en entrer
- [ ] int status
- [ ] Besoin du coter server
	- [ ] getter de location ?
- [ ]  constructor avec code error
	- [ ] Prendre le `getErrorPage` ?


### HTTP error
