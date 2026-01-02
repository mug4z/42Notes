**Authentication** describes who is allowed to access the service. On the other hand, **authorization**
defines what actions can be performed by the user once authenticated.


use the fastify plugin modules.
https://assets.roadmap.sh/guest/jwt-authentication-74ksi.png
https://datatracker.ietf.org/doc/html/rfc7519

https://fastify.dev/docs/latest/Reference/Plugins/#create-a-plugin
https://fastify.dev/docs/latest/Reference/TypeScript/#plugins

TODO
Voir comment on fait un plugin en typescript

Problem was that the secret need to be a string but I;m trying to get the secret from env
found solution there -> https://ssojet.com/jwt-validation/validate-jwt-using-hs512-in-fastify/

## Register

pbkdf2 -> https://mojoauth.com/hashing/pbkdf2-in-nodejs/
