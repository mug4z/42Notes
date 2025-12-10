# Mini projet solo (idee projet 42): today -> 21/11/2025

- faites des branches /
- spec: generer nombre aleatoire -> button: fetch/add -> DB (table "Nombre") => (deux pages web: add / fetch (display))
- potentiellement: restreindre l'acces des pages: placeholder (auth / login) / boolean

- [ ] Continue the explication with the design pattern and architectures.
## Step

## Recherche

- [ ] Read some part of the handbook.
- [ ] Read some javascript.
- [ ] What the fuck is SQLLite.
- [ ] Package.json and use of npm

### Front End

- [x] faire un boutton qui creer une chiffre aleatoire
  - [x] Faire un placeholder qui permet d'afficher quelque chose dans la console quand on appuie dessus.
- [x] faire un bouton qui demande un chiffre aleatoire

### BackEnd
- [x] Setup the reverse proxy for backend.
- [x] access in service the test server through the port 3000
	- [x] Check fastify server listen
- [x] setup la base de donner. (SQLLIte)
	- [x]  Install avec npm https://www.npmjs.com/package/better-sqlite3
	 - [x] Setup la DB (creer la table numbers dans la DB PROTO).
	 - [x] Regarde avec fastify pour faire le backend -> better-sqlite3
- [x] faire une mini api pour aller checher un nombre et ajouter un nombre.
	- [x] addNbr
	- [x] getNbr
- [x] setup fastify
	- [x] setup the nodemon for hotreload
