# 🧪 Plan de Test – HEXED

> Cette branche contient la mise en place du **plan de test complet** pour le projet fil rouge 'HEXED'.  
> L'objectif est de définir la stratégie de tests pour garantir la fiabilité, la sécurité et la cohérence de l'application dès sa conception.

---

## 🎯 Objectif

L’application a pour but de devenir un site compagnon autour du jeu **Dead by Daylight**.  
Elle permettra aux utilisateurs de :

- Consulter les objets, personnages, compétences (via une API développée maison)
- Lire et poster des commentaires
- Aimer ou suivre les discussions
- Créer et publier leurs propres **tier lists**
- Explorer du contenu communautaire

Ce README documente la stratégie de test prévue pour l’ensemble de ces fonctionnalités.

---

## 🧱 Types de tests prévus

| Type de test        | Objectif                                                       |
|---------------------|----------------------------------------------------------------|
| Test unitaire       | Vérifier le comportement des fonctions/méthodes isolées       |
| Test d’intégration  | Tester les interactions entre les différents modules (ex : API + DB) |
| Test fonctionnel    | Vérifier que les fonctionnalités principales répondent aux besoins utilisateurs |
| Test d’acceptation  | Valider des parcours utilisateurs entiers                      |
| Test de sécurité    | Vérifier la gestion des accès, permissions et données sensibles |
| Test de performance | Simuler des appels massifs ou des scénarios à charge           |
| Test exploratoire   | Utiliser Postman / front pour tester manuellement des cas limites |

---

## 📋 Plan de test par fonctionnalité

### 🔐 Authentification & utilisateurs

| Fonctionnalité                         | Type de test       | Description                                                 | Priorité |
|---------------------------------------|--------------------|-------------------------------------------------------------|----------|
| Création de compte                    | Unitaire           | Données valides/invalides, mots de passe trop courts        | Haute    |
| Connexion                             | Intégration        | Connexion réussie, refusée, gestion du token                | Haute    |
| Accès à une route protégée sans token| Sécurité           | Doit retourner 401                                          | Haute    |
| Token expiré ou invalide              | Sécurité           | Accès refusé                                                | Haute    |

---

### 📚 API – Objets, personnages, perks

| Fonctionnalité              | Type de test     | Description                                              | Priorité |
|----------------------------|------------------|----------------------------------------------------------|----------|
| Récupération des données   | Fonctionnel      | Liste des personnages, objets, perks                     | Haute    |
| Détail d’une fiche         | Fonctionnel      | Infos complètes d’un personnage                          | Haute    |
| Filtrage / recherche       | Fonctionnel      | Par rôle, difficulté, nom                                | Moyenne  |
| Cas où un objet n'existe pas | Unitaire         | Retour d'erreur ou 404                                   | Moyenne  |

---

### 💬 Commentaires et likes

| Fonctionnalité              | Type de test     | Description                                               | Priorité |
|----------------------------|------------------|-----------------------------------------------------------|----------|
| Poster un commentaire      | Fonctionnel      | Utilisateur authentifié, contenu valide                   | Haute    |
| Commentaire vide ou invalide| Unitaire         | Rejeter la soumission                                     | Haute    |
| Liker un commentaire       | Intégration      | Incrémentation du compteur, un seul like par utilisateur  | Moyenne  |
| Suivre une discussion      | Intégration      | Ajouter à une liste personnelle                           | Moyenne  |
| Supprimer son commentaire  | Sécurité         | Vérifier qu’on ne peut supprimer que les siens           | Haute    |

---

### 🧩 Tier Lists

| Fonctionnalité                | Type de test     | Description                                              | Priorité |
|------------------------------|------------------|----------------------------------------------------------|----------|
| Création de tier list        | Fonctionnel      | Glisser-déposer, validation des données                  | Haute    |
| Publication                  | Intégration      | Sauvegarde en base, accessibilité publique               | Haute    |
| Affichage d’une tier list    | Fonctionnel      | Affichage propre, ordre correct                          | Moyenne  |
| Modification / suppression   | Sécurité         | Seul l’auteur peut modifier                              | Haute    |

---

## 🛠️ Outils de test envisagés

| Usage                     | Outil envisagé         |
|---------------------------|------------------------|
| Framework de test         | Jest (Node)            |
| Tests HTTP                | Supertest, Postman     |
| Linter / qualité de code  | ESLint / Prettier      |

---

## 📁 Structure du dossier `test/`

/test
├── README.md # Ce fichier
├── auth.test.js # Tests d'authentification
├── user.test.js # Création/gestion des utilisateurs
├── api/
│ ├── character.test.js # Tests des personnages
│ ├── item.test.js # Tests des objets
├── comment.test.js # Tests commentaires / likes
├── tierlist.test.js # Création et affichage de tier lists
└── setup.js # Configuration globale des tests

> Les fichiers de test seront complétés au fur et à mesure de l’avancement du projet.

## 🧪 Lancement futur des tests

```bash
# Installation des dépendances
npm install

# Lancer les tests
npm run test

# Avec couverture
npm run test -- --coverage
