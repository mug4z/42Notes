Terminology:
- .key -> private key.
- .pem -> public key.
- .cert or .crt -> signed certificate.
- .csr -> certificate signing request.

Create a private key, local CA
`openssl genrsa  -out myCA.key 2048 `

Create a root certificate
`openssl req -x509 -new -nodes -key myCA.key -sha256 -days 1825 -out myCA.pem -subj '/CN=localhost'`

https://docs.nginx.com/waf/configure/secure-mtls/
# Source
[[Security-Source]]