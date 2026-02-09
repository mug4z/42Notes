Terminology:
- .key -> private key.
- .pem -> public key.
- .cert or .crt -> signed certificate.
- .csr -> certificate signing request.

The CN (Common Name) is important while creating a certificate and private key.


Create a private key, local CA
`openssl genrsa  -out myCA.key 2048 `

Create a root certificate
`openssl req -x509 -new -nodes -key myCA.key -sha256 -days 1825 -out myCA.pem -subj '/CN=localhost'`


Create dhparam
```
sudo openssl dhparam -out ./dhparam.pem 4096
```

https://docs.nginx.com/waf/configure/secure-mtls/

Must follow.
https://docs.nginx.com/nginx/admin-guide/security-controls/securing-http-traffic-upstream/#prerequisites
SSL for nginx.
https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-nginx-in-ubuntu-20-04-1

Next Steps
- [ ] Use this doc https://docs.nginx.com/nginx/admin-guide/security-controls/securing-http-traffic-upstream/#prerequisites
- [ ]  create a CA and make the certification accordindly.
- [ ] If doesn't work use the 
## Question ?
Diffie-Hellman (DH) group
https://en.wikipedia.org/wiki/Forward_secrecy
https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange
https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security
	


# Source
https://cipherlist.eu/
[[Security-Source]]