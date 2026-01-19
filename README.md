# Plan de développement SCHOR

Ce document décrit étape par étape la construction de l’application web SCHOR, une plateforme de collecte, d’analyse et de consultance scientifique inspirée des usages de KoboToolbox, développée en **PHP (PDO)** avec **MySQL**. Chaque section précise les objectifs, dépendances et livrables pour faciliter l’exécution A → Z.

## 1. Vision & cadrage
- **Objectifs** : centraliser la collecte de données terrain, offrir de la consultance scientifique et assurer le suivi des formations.
- **Personae** : équipes internes SCHOR, partenaires externes, collecteurs terrain, administrateurs, décideurs.
- **Cas d’usage clés** : formulaires dynamiques, import/export Kobo/ODK, analyse statistique, gestion des rendez-vous, formations, publications.
- **Livrable** : cahier des charges validé + maquettes UX haute fidélité.

## 2. Prérequis techniques
- **Stack** : PHP ≥ 8.1, Apache/Nginx, MySQL 8, Composer, Node/Yarn pour pipelines front, Git.
- **Normes** : PSR-12, MVC modulaire, Twig/Blade ou moteur interne, Bootstrap 5 + charting (Chart.js).
- **Environnement** : `.env` versionné en exemple, configuration PDO centralisée, docker-compose optionnel pour CI.

## 3. Architecture fonctionnelle
- **Front public** : accueil, missions, data, conseils, publications, formations, appui à la recherche, footer enrichi.
- **Espace admin** : dashboard synthétique, gestion multi-modules (utilisateurs, publications, données, rendez-vous, formations, partenaires, notifications, paramètres, logs, support).
- **Espace utilisateur avancé** : inscription, connexion, dashboard perso, projets (business plan), widgets personnalisables.
- **Flux data** : synchronisation formulaires Kobo-like (JSON/XLSForm), uploads CSV, API REST interne.

## 4. Conception base de données
- **Étape 4.1** : Modélisation entités (utilisateurs, rôles, organisations, formulaires, soumissions, sessions de formation, rendez-vous, publications, notifications, logs).
- **Étape 4.2** : Définir contraintes (FK, index, clés uniques, audit trail).
- **Étape 4.3** : Scripts migration initiaux (SQL) + seed de rôles/par défaut.
- **Livrables** : diagramme conceptuel + scripts versionnés (`database/migrations`).

## 5. Mise en place de l’environnement
- **5.1** Installer dépendances (Composer, npm), configurer autoload PSR-4.
- **5.2** Configurer `config/database.php` (PDO, pooling, retry).
- **5.3** Intégrer container d’injection (ex. PHP-DI) + router (FastRoute).
- **5.4** Mettre en place monolog + gestion d’erreurs (Whoops en dev).

## 6. Framework interne & fondations
- **6.1** Créer noyau MVC (Request/Response, Middleware, Controller abstrait, View renderer).
- **6.2** Gestion authentification : sessions sécurisées, hashing Argon2id, CSRF, RBAC.
- **6.3** Services transverses (file storage, notifications, file import/export, jobs asynchrones via queue ou cron).
- **6.4** Normes API : endpoints RESTful pour formulaires et données collectées (JSON:API).

## 7. Développement Front public
1. **Accueil premium** : hero scientifique, CTA flottant, timeline, carrousel témoignages.
2. **Sections missions/data/conseils/publications/formations** : composants réutilisables, contenus dynamiques depuis CMS interne.
3. **Footer modernisé** : liens rapides, contacts, réseaux, widgets statistiques.
4. **SEO & accessibilité** : balises méta, schémas structurés, tests Lighthouse.

## 8. Modules Admin (12 blocs)
1. **Dashboard** : stats temps réel (soumissions, formations, rendez-vous) + notifications.
2. **Utilisateurs & rôles** : CRUD, import CSV, export, activation 2FA.
3. **Publications** : workflow (draft → review → publish), éditeur WYSIWYG, aperçu.
4. **Données collectées** : mapping formulaires Kobo, validation, visualisation (tableaux, graphiques), export CSV/XLS/JSON.
5. **Rendez-vous / événements** : calendrier (FullCalendar), invitations email/SMS.
6. **Formations** : création sessions, suivi inscriptions, statistiques d’assiduité.
7. **Partenaires / organisations** : fiches, documents, KPI.
8. **Notifications / messages** : ciblage (segment utilisateurs), templates, historique.
9. **Paramètres centre** : branding, sécurité (politiques mots de passe, IP whitelist), accès API.
10. **Logs & audit** : journal des actions, exports, alertes anomalies.
11. **Support/FAQ interne** : base de connaissance, tickets internes.
12. **Recherche globale & widgets** : moteur unifié (MySQL FULLTEXT + filtres), favoris personnalisés.

## 9. Espace utilisateur avancé
- **9.1** Parcours onboarding (inscription/connexion, reset mot de passe).
- **9.2** Dashboard personnel : widgets custom, stats projets.
- **9.3** Gestion projets (business plan) : génération documents, commentaires collaboratifs.
- **9.4** Accès publications, datasets, formulaires assignés, calendrier partagé.

## 10. Collecte et synchronisation type KoboToolbox
- **10.1** Concepteur de formulaires web (drag & drop, types de questions, validation).
- **10.2** Import XLSForm/Kobo JSON, conversion en schéma interne.
- **10.3** API mobile/offline : endpoints pour collecteurs, stockage local, sync différée.
- **10.4** Gestion soumissions : contrôle qualité, géolocalisation, pièces jointes.
- **10.5** Automatisation analyses : scripts statistiques (PHP + Python via CLI si nécessaire), dashboards data.

## 11. Sécurité & conformité
- **11.1** RBAC granulaires, journalisation complète, traçabilité.
- **11.2** Validation côté serveur + côté client, sanitisation, Content Security Policy.
- **11.3** Chiffrement données sensibles (OpenSSL), stockage fichiers chiffrés.
- **11.4** Backups automatisés (base + fichiers), plan PRA/PCA.
- **11.5** Conformité RGPD (consentement, droit à l’oubli, registre traitements).

## 12. Tests & qualité
- **12.1** Tests unitaires PHPUnit (services, repositories).
- **12.2** Tests fonctionnels Behat/Pest + scénarios utilisateurs.
- **12.3** Tests API (Postman/Newman) + performance (k6).
- **12.4** Intégration CI (GitHub Actions/GitLab CI) : lint, tests, build assets.

## 13. Livraison & déploiement
- **13.1** Pipelines : staging → préprod → prod, avec migrations automatisées.
- **13.2** Déploiement continu (Capistrano/Deployer) ou conteneurs Docker/Kubernetes.
- **13.3** Surveillance : logs centralisés (ELK), métriques (Prometheus/Grafana), alertes.
- **13.4** Documentation utilisateurs & runbooks support.

## 14. Formation & adoption
- **14.1** Sessions de formation pour équipe interne + collecteurs terrain.
- **14.2** Guides pas-à-pas, vidéos, FAQ intégrée.
- **14.3** Boucle de feedback continue (in-app surveys, NPS).

## Démarrage technique rapide

1. **Prérequis** : PHP ≥ 8.1, Composer, Node 18+, MySQL 8, Redis (optionnel pour la queue).
2. **Installation** :
   ```bash
   composer install
   copy .env.example .env  # Windows PowerShell: use `copy`, on *nix use `cp`
   php -S localhost:8000 -t public
   ```
   ```bash
   npm install
   npm run dev
   ```
3. **Structure** :
   - `public/index.php` : front controller PSR-4.
   - `bootstrap/app.php` : chargement Dotenv + boot Router.
   - `routes/web.php` / `routes/api.php` : front, admin, portail utilisateur, health-check.
   - `resources/views` : layout premium (Bootstrap 5) inspiré du plan SCHOR.
   - `app/` : Controllers, Services, Repositories, Policies, Middleware prêts pour les 13 blocs fonctionnels décrits.
4. **Étapes suivantes** :
   - Brancher PDO + migrations `database/migrations`.
  
## Commandes utiles

- Lancer les migrations locales :

```powershell
composer migrate
# ou
php bins/console migrate
```

Si la base de données est refusée, vérifiez que MySQL est démarré et que les variables DB dans `.env` sont correctes.

   - Implémenter authentification (sessions + tokens API).
   - Industrialiser les modules Phase H/I (Dashboard admin, builder Kobo, widgets utilisateur).
