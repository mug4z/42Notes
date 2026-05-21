# Informations
## Goal
Store an initial password in file encrypted and being capable of generating a new one time password every time it is requested.
It is aimed to implement a  [TOTP](https://datatracker.ietf.org/doc/html/rfc6238)(Time-based One-Time Password) 

## Programm arguments 
- `-g`, receive a hexadecimal key of at least 64 characters. store it in a file **ft_otp.key** which is encrypted.
- `-k`, generate a new temporary password based on the key given as argument and prints it on the std out.

## Algorithms

Use the  [**HTOP algorithm**](https://datatracker.ietf.org/doc/html/rfc4226#autoid-1)  and the TOTP. The temporary password should always on the same format **6 digits**.


## Technical research
### HOTP Notations and Symbols

 Symbol  Represents
   -------------------------------------------------------------------
   C       8-byte counter value, the moving factor.  This counter
           MUST be synchronized between the HOTP generator (client)
           and the HOTP validator (server).

   K       shared secret between client and server; each HOTP
           generator has a different and unique secret K.

   T       throttling parameter: the server will refuse connections
           from a user after T unsuccessful authentication attempts.

   s       resynchronization parameter: the server will attempt to
           verify a received authenticator across s consecutive
           counter values.


### Generating HOTP Value

- use hmac-sha-1, [python library ](https://docs.python.org/3/library/hmac.html)
## Sources
https://datatracker.ietf.org/doc/html/rfc6238#autoid-1
https://datatracker.ietf.org/doc/html/rfc4226#section-5.3

#security #cryptography #htop #TOTP
#cyberpiscine