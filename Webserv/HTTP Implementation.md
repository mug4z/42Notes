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
  - [x] Consider that LogManager.hpp may not be accessible in current structure.

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
- [x] Constructor avec http request en entrer
- [x] int status
- [x] Besoin du coter server
	- [x] getter de location ?
- [x]  constructor avec code error
	- [x] Prendre le `getErrorPage` ?


## Next Thing to implement
1. Clean the code.
	1. AHttpMessage -> OK voir avec Ben pour fonction utils range de chiffre
	2. Request -?
	3. Response
2. lire RFC 9112 chapter 5 -8.
### Ideas
Request : rendre 505 si la version d'http est mauvaise ?
Request / Response / AHttpMessage : faire des checker pour les data members ?

## Ce qui  rest a faire
- Check si un body est present dans la request. -> OK
- Les conditions pour qu'un body soit present dans la response. -> OK
- Avoir la taille correct du body de la response. -> OK
- Ajouter des check syntaxique pour:
	- startline -> OK
	- Method -> OK
	- location -> OK
	- httpVersion -> OK
	- statusCode -> OK
	- statusMessage -> OK
	- Headers values -> encore check pour transfer-encoding
	- errorCode -> OK
- Faire en sorte que la gestion des erreur soit correct.(Le bon code en fonction du probleme) -> OK
- Verifier que GET fonctionne comme specifier dans la rfc 9110 
- Implementer les methodes
	- POST
	- DELETE
- Faire en sorte que les request et response fonctionne en chuncked.(Donc la requete n'arrive pas d'un coup).
## Ce qui  rest a faire V2
- Refactor le code pour cette histoire de poll.
	- lecture de fichier:
		- HttpResponseError.cpp:23
		- Vue comment est fait le response on me passe le stream directement et je le remplis.
- Ajouter des check syntaxique pour:
	- Headers values -> encore check pour transfer-encoding
-  Implementer les methodes
	- POST
	- DELETE
	- Faire un check de method pour s'assurer que la methode est autoriser au globale et pour la ressource.
-  Faire en sorte que les request et response fonctionne en chuncked.(Donc la requete n'arrive pas d'un coup).
## Ce qui  rest a faire V3
- POST
- CGI
- Organiser le Body pour le type le set a CGI.

## V1.1
- setter return bool et font les checks donc valide si tout est bon
	- setter startline
		- Method -> OK
		- Location -> OK
		- HTTP Version -> OK
	- setter headers
		- Check value to make sure that only visible US-Ascii is set -> OK
		- Check if Host exists -> OK
		- Check if map empty -> OK
		- Check if the value is empty -> OK
		- Check if the key is empty -> OK
	- setter body
- Add the HTTP error code to use -> OK 
- Change the workflow of the response builder
- Access log. -> OK
	- Format la request comme le mettre dans le access log avec l'operateur <<
	- request 
		- startline + header sans \n
	- response

## Response class
faire les prototype pour 
	- HttpResponseError -> OK
	- HttpResponseRedirect -> OK
	- Response(HttpCode,header,body) -> OK
- Faire le generateur de html d'erreur -> OK
- A faire
	- le Response(httpCode, header, body)
## V2
- Request :
	- Check if a body is sent in a request.

## Suite des operations

- se renseigner sur POST avec des tests,
- se renseigner sur CGI et son fonctionement,
- se mettre d'accord sur le format du body dans la request et la response,
- une fois le format du body ok refactor time.,
- faire des test avec le serveur pour ajuster les messages de log