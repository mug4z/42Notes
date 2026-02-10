## Key
- create a protected route to generate the key 
- using the user id in order to find the key faster.
- 

### backend
- [ ] **Créer table ApiKey dans Prisma**
  - [ ] Champs : id, key, owner, rateLimit, createdAt
  - [ ] Migration de la base de données
  
- [ ] **Plugin verifyApiKey** (vérification dans SQLite)
  - [ ] Middleware pour vérifier x-api-key header
  - [ ] Query Prisma pour valider la clé
  - [ ] Retour 401 si manquante, 403 si invalide

- [ ] **Plugin @fastify/rate-limit** (100/min)
  - [ ] Installation : `npm install @fastify/rate-limit`
  - [ ] Configuration avec Redis comme store
  - [ ] KeyGenerator basé sur API key
  - [ ] Message d'erreur 429 personnalisé

- [ ] **5 endpoints publics**
  - [ ] GET `/api/public/stats/leaderboard`
  - [ ] GET `/api/public/stats/user/:username`
  - [ ] GET `/api/public/games`
  - [ ] POST `/api/public/webhooks`
  - [ ] DELETE `/api/public/webhooks/:id`

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
