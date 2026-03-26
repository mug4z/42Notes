
## Key
- using the user id in order to find the key faster.
- Schema must contain the x-api-key. 

Create the structure
1. Routes -> ok
2. Schemas -> ok
3. Controllers -> ok
4. Models -> ok

### backend
- [X] **Créer table ApiKey dans Prisma**
  - [X] Champs : id, key, owner, rateLimit, createdAt
  - [X] Migration de la base de données
- [x] create a protected route to generate the key ✅ 2026-02-12
  - [x] Add the route in the user.routes.ts -> /api/user/generatekey ✅ 2026-02-11
  - [X] Add a schemas
  - [X] Add a Controllers
  - [X] Add a Models
  - [x] Add the key into the Database with hash. ✅ 2026-02-12
  - [x] Si deja ajouter alors update. ✅ 2026-02-15
  - [x] Test si le hash est bien ajouter en DB. ✅ 2026-02-15
  - [x] Add the middle ware to check the validity of the key. ✅ 2026-02-15
  
- [x] **Plugin verifyApiKey** (vérification dans SQLite)
  - [x] Middleware pour vérifier x-api-key header ✅ 2026-02-15
  - [x] Query Prisma pour valider la clé ✅ 2026-02-15
  - [x] Retour 401 si manquante, 403 si invalide

- [ ] **Plugin @fastify/rate-limit** (100/min)
  - [x] Installation : `npm install @fastify/rate-limit` ✅ 2026-02-19
  - [ ] Configuration avec Redis comme store
  - [ ] KeyGenerator basé sur API key
  - [ ] Message d'erreur 429 personnalisé

- [ ] **5 endpoints publics**
- [x] pas besoin de faire du CRUD ✅ 2026-02-17
  - [x] GET `/api/public/stats/leaderboard` ✅ 2026-02-17
  - [x] GET `/api/public/stats/user/:username` ✅ 2026-02-17
  - [x] GET `/api/public/games` ✅ 2026-02-17
  - [x] POST `/api/public/webhooks` ✅ 2026-02-17
  - [x] DELETE `/api/public/webhooks/:id` ✅ 2026-02-17

- [ ] **Schémas JSON pour Swagger**
  - [ ] Définir schema pour chaque endpoint
  - [ ] Description, tags, paramètres
  - [ ] Response codes (200, 401, 403, 404, 429)
  - [ ] Exemples de réponses

- [ ] **Configuration Swagger UI**
  - [ ] Installation : `npm install @fastify/swagger @fastify/swagger-ui`
  - [ ] Config dans server.ts
  - [ ] securitySchemes pour API key
  - [ ] Route `/api/docs` accessible

- [ ] **Endpoint admin pour générer les clés**
  - [ ] POST `/api/admin/api-keys` (JWT admin requis)
  - [ ] Génération clé sécurisée (crypto.randomUUID x2)
  - [ ] Stockage dans SQLite via Prisma
  - [ ] Return de la clé générée

### Tests
- [ ] Tests unitaires des endpoints
- [ ] Test du rate limiting (dépasser la limite)
- [ ] Test de validation API key
- [ ] Test des erreurs (401, 403, 429)
- [ ] Script bash de tests manuels

### Documentation
- [ ] Swagger UI fonctionnel sur `/api/docs`
- [ ] Tous les endpoints documentés
- [ ] Exemples de requêtes/réponses
- [ ] README avec instructions d'utilisation

### Sécurité
- [ ] API keys stockées dans SQLite (table ApiKey)
- [ ] Redis utilisé pour cache rate limiting uniquement
- [ ] Validation HTTPS pour webhooks
- [ ] Logs des requêtes API
- [ ] Gestion propre des erreurs


Source
https://www.reddit.com/r/node/comments/14hd7ku/how_do_i_issue_api_keys_for_my_users/
https://www.freecodecamp.org/news/best-practices-for-building-api-keys-97c26eabfea9
https://developer.mozilla.org/en-US/docs/Web/API/Crypto/randomUUID
https://developer.mozilla.org/en-US/docs/Web/API/Window/btoa
https://nodejs.org/api/crypto.html#cryptocreatehmacalgorithm-key-options
https://github.blog/engineering/behind-githubs-new-authentication-token-formats/
https://nodejs.org/api/crypto.html#cryptocreatehashalgorithm-options