Question ?:
- La game session peut avoir plusieur Game ?
- Pourquoi pas mettre le game id dans le profile du player ?
- Pourquoi faire un game session par player ?
- Pour le rematch pas trop compris l'histoire du player B is slower.
- Est ce que se serait pas mieux si la game se fait une fois que tout le monde a accepter de rematch ?
- websocket: true -> header 


Reponse:
- La game session peut avoir plusieur Game ?
	- Non c'est l'inverse la game a plusieur game session.
	- La table game reste apres la partie pour l'historique.
	- La table game et lier a la table user par le userID.
	- La table game session est lier a la table user par le userID
- Pourquoi pas mettre le game id dans le profile du player ?
	- Sert pas a grand chose vue qu'on a la table Game.
- Pourquoi faire un game session par player ?
	- GameSession -> gameConnection 
	- token expire_at et consumed at -> remove, JWT token prend le relai au niveau de la secu.
- Pour le rematch pas trop compris l'histoire du player B is slower.
	- Logique si le rematche est pas possible, le user est remis dans la queue.
	- La websocket est garder mais on recreer une game dans la DB.
- Est ce que se serait pas mieux si la game se fait une fois que tout le monde a accepter de rematch ?
	- OUI
- websocket: true -> header 
	- Pas un header mais specification dans fastify route.


Note:
- Faire une table gameStats,garde des stats sur les game. Les donner les plus courante ne devrait pas ce recalculer a chaque fois.
- Essayer de faire uniquement la table game.
- Queue matchmaking serait mis dans le cache du serveur (Theo regarde)

A faire:
- se renseigner sur les websockets
- 28-game-proto exemple de ce qu'a fait Theo.
