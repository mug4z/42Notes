# Modules Checklist,

   Major Modules,

---

 Framework Frontend & Backend,

- [ ] Frontend : React (composants, routing, state management),
- [ ] Backend : Fastify (serveur, plugins, routes),
- [ ] Communication Frontend ↔ Backend fonctionnelle,
- [ ] Build de production opérationnel,

---

 Real-time (WebSockets),

- [ ] Connexion WebSocket établie côté client,
- [ ] Connexion WebSocket établie côté serveur,
- [ ] Mises à jour en temps réel propagées entre clients,
- [ ] Gestion de la déconnexion gracieuse,
- [ ] Gestion de la reconnexion,
- [ ] Broadcasting efficace des messages,
- [ ] Tests de charge / stress basiques,

---

 Public API,

- [ ] Authentification par API key sécurisée,
- [ ] Rate limiting implémenté,
- [ ] Documentation de l'API (Swagger / autre),
- [ ] `GET /api/{resource}` (lecture),
- [ ] `POST /api/{resource}` (création),
- [ ] `PUT /api/{resource}` (modification),
- [ ] `DELETE /api/{resource}` (suppression),
- [ ] Au moins 5 endpoints distincts,
- [ ] Réponses d'erreur standardisées,

---

 User Management & Auth,

- [ ] Création de compte (inscription),
- [ ] Connexion / Déconnexion,
- [ ] Mise à jour des informations de profil,
- [ ] Upload d'avatar,
- [ ] Avatar par défaut si aucun fourni,
- [ ] Ajout d'amis,
- [ ] Affichage du statut en ligne des amis,
- [ ] Page de profil avec informations personnelles,
- [ ] Protection des routes privées,

---

 Jeu en ligne (Pong),

- [ ] Règles du jeu claires et documentées,
- [ ] Conditions de victoire / défaite définies,
- [ ] Matchs en direct jouables (2 joueurs),
- [ ] Interface de jeu 2D (ou 3D),
- [ ] Système de matchmaking / lobby,
- [ ] Score affiché en temps réel,
- [ ] Fin de partie correctement gérée,

---

 Remote Players,

- [ ] Deux joueurs sur deux machines distinctes peuvent jouer,
- [ ] Latence réseau gérée correctement,
- [ ] Déconnexion pendant une partie gérée,
- [ ] Logique de reconnexion implémentée,
- [ ] Expérience utilisateur fluide malgré la distance,

---

 Minor Modules,

---

 ORM (Base de données),

- [ ] ORM configuré (Prisma),
- [ ] Schéma de base de données défini,
- [ ] Migrations versionnées,
- [ ] Seed de données de test,
- [ ] Requêtes via ORM (pas de SQL brut),

---

 Statistiques & Historique,

- [ ] Statistiques par joueur (victoires, défaites, ranking, niveau),
- [ ] Historique des matchs (1v1, dates, résultats, adversaires),
- [ ] Affichage des succès / achievements,
- [ ] Progression du joueur visible,
- [ ] Leaderboard intégré et fonctionnel

---

Framework de test
- [ ] 
