RFC 2388 

man page curl in order to send file with POST
https://curl.se/docs/manpage.html#-F
NGINX n'est pas fait pour faire un POST directement il le transfere a un CGI.

https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/POST
https://datatracker.ietf.org/doc/html/rfc2388

PHP, python ont des CGI qui parse le body du formulaire envoyer par le POST.

https://www.rfc-editor.org/rfc/rfc9110.html#section-9.3.3 -> Response to POST requests contain a Content-Location header that has the same value as the POST's target URI

## Planifications
- Check how we upload files with post request using NC
Test: CGI verifier si la lib cgi verifie le content_length en ecrivant un content lenght plus petit que le body.
