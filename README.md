# Mchichat

Application web sociale avec messagerie en temps réel, salons de discussion et partage de médias.

**Abdelmoughit Douimia · Master 1 Informatique · Université du Littoral Côte d’Opale**

J’ai participé à la conception et au développement de Mchichat dans le cadre du module **Conception – Web Services**. Réalisé en binôme, ce projet m’a permis de travailler sur une application complète : interface React, API REST, base de données relationnelle et échanges en temps réel.

## Fonctionnalités

- **Comptes et profils** : inscription, connexion, profil public, avatar, bannière et biographie.
- **Fil de publications** : publications, commentaires, mentions « J’aime » et partage de médias.
- **Amis** : recherche d’utilisateurs, demandes d’amitié et gestion des contacts.
- **Salons** : espaces publics ou privés, membres, invitations et demandes d’accès.
- **Messagerie** : conversations privées et de salon, modification et suppression de messages, notifications en temps réel.
- **Médias** : images, fichiers, messages vocaux et recherche de GIFs.
- **Services externes** : actualités, météo et localisation.
- **Administration** : statistiques, gestion des utilisateurs et des rôles.
- **Interface** : adaptation aux écrans mobiles, thème clair et thème sombre.

## Technologies

| Partie | Technologies |
| --- | --- |
| Interface | React 19, TypeScript, Vite 8, Tailwind CSS 4, React Router, TanStack Query |
| API | Node.js, Express 5, TypeScript, Prisma 6 |
| Données | MySQL |
| Temps réel | Socket.IO |
| Authentification | JWT, bcrypt, cookies HTTP Only |
| Validation et médias | Zod, Multer, Cloudinary, FFmpeg |
| Services externes | Giphy, NewsData.io, Open-Meteo, OpenStreetMap |
| Documentation | Swagger / OpenAPI |

## Organisation

| Dossier | Contenu |
| --- | --- |
| `frontend/src/pages` | Écrans de l’application |
| `frontend/src/features` | Authentification, publications, amis, messages et salons |
| `frontend/src/components` | Composants d’interface et navigation |
| `backend/src/modules` | Routes, contrôleurs, validation et logique métier par fonctionnalité |
| `backend/src/middlewares` | Authentification, rôles, fichiers et gestion des erreurs |
| `backend/prisma` | Modèle relationnel et configuration Prisma |

L’interface communique avec l’API via HTTP. Socket.IO transmet les événements liés aux messages et aux notifications. Prisma assure l’accès à MySQL ; les médias sont stockés sur Cloudinary.

## Installation locale

### Prérequis

- Node.js **22.12 ou supérieur** et npm.
- MySQL 8 et deux bases distinctes pour le développement et les migrations.
- Des identifiants Cloudinary, Giphy et NewsData.io.

FFmpeg est fourni par la dépendance `ffmpeg-static` lors de l’installation du backend.

```bash
git clone https://github.com/DOUIMIAGH/mchichat.git
cd mchichat
```

### 1. Base de données

Créer les bases avec un compte MySQL autorisé à modifier leur schéma :

```sql
CREATE DATABASE mchichat CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE DATABASE mchichat_shadow CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

### 2. Backend

```bash
cd backend
cp .env.example .env
npm ci
```

Renseigner les accès MySQL et les identifiants des services dans `.env`. Utiliser deux secrets JWT différents ; cette commande permet d’en générer un :

```bash
node -e "console.log(require('node:crypto').randomBytes(48).toString('hex'))"
```

Créer le schéma puis démarrer l’API :

```bash
npx prisma generate
npx prisma migrate dev --name init
npm run dev
```

### 3. Frontend

Dans un second terminal, depuis la racine du projet :

```bash
cd frontend
cp .env.example .env
npm ci
npm run dev
```

Sous Windows, la commande `copy .env.example .env` remplace `cp`.

| Service | Adresse locale |
| --- | --- |
| Application | http://localhost:5173 |
| API | http://localhost:5000/api/v1 |
| Documentation interactive | http://localhost:5000/api-docs |

Les fichiers `.env` restent locaux. Les exemples fournis contiennent uniquement des valeurs à renseigner.

## Compilation

```bash
# Depuis la racine
npm --prefix backend run build
npm --prefix frontend run build
```

Pour démarrer le backend compilé : `npm --prefix backend start`.
Pour prévisualiser le frontend : `npm --prefix frontend run preview`.

La configuration Netlify du frontend prend en charge les routes de l’application. En production, renseigner les URL publiques de l’API et de Socket.IO, les origines CORS autorisées et les variables du backend.

## Ce que ce projet m’a apporté

- Relier une interface React à une API structurée par fonctionnalités.
- Modéliser les utilisateurs, relations, salons, conversations et publications avec Prisma.
- Mettre en pratique l’authentification, la validation des données et les contrôles d’accès HTTP.
- Intégrer des échanges en temps réel et plusieurs services externes.
- Travailler en binôme avec Git et documenter l’installation d’une application web.

## Pistes d’amélioration

- Ajouter des tests automatisés des parcours d’authentification et de messagerie.
- Renforcer les contrôles d’accès aux canaux Socket.IO.
- Ajouter la pagination des conversations et des publications.
- Développer les outils de modération et la recherche globale.

## Contexte et crédits

Projet universitaire réalisé par **Abdelmoughit Douimia** et **Aya Touhaf**, sous l’encadrement de **Clément Fasquel** et **Axel Soupé**.

[Dépôt du travail en binôme](https://github.com/touhaf00/mchichat)
