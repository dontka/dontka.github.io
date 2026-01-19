# Plan de développement SCHOR – Parcours intégral A → Z
(Langue Français)
Ce document réinterprète `schor.txt` en un plan de réalisation exhaustif pour une application web premium (PHP 8.1+ PDO, MySQL 8, Bootstrap 5, JS moderne) couvrant front public, espace admin complet, portail utilisateur avancé et stack de collecte type KoboToolbox.

---

## Phase A – Cadre stratégique & gouvernance
- **Vision** : rappeler la mission SCHOR (consultance scientifique, data, orientation humanitaire) et aligner les parties prenantes (PME, ONG, universités, autorités, startups, chercheurs, particuliers).
- **Backlog** : dériver les 13 blocs front/admin/utilisateur listés dans `schor.txt` en épics, définir périmètre MVP vs évolutions.
- **Organisation** : RACI, rituels agiles (sprints 2 semaines), outils (Jira/Linear, Figma, Notion, GitHub).
- **Branding** : charte graphique premium, ton éditorial, guidelines UI/UX inspirés de design GitHub-like.

## Phase B – Découverte produit & UX premium
1. **Recherche utilisateur** : ateliers métiers, interviews pour prioriser usages (collecte terrain, consultance, formation, publications, appui recherche).
2. **Information architecture** : cartographie complète : Accueil, Missions/Pourquoi SCHOR, Collecte & Analyse, Conseils & Orientation, Publications, Formation & Sensibilisation, Appui recherche/Données, Footer enrichi, Dashboard admin, modules utilisateur.
3. **User flows & maquettes** : prototypes interactifs (hero dynamique, CTA flottant, timeline, carrousel témoignages, FAQ), maquettes responsive (desktop/tablette/mobile) avec animations et transitions prévues.

## Phase C – Architecture fonctionnelle & technique
- **Stack** : PHP ≥ 8.1 (PDO, namespaces PSR-4), Apache/Nginx, MySQL 8, Composer, Node/Yarn (build Sass/JS), Redis (cache/queue), Mailhog/SMTP, GitHub Actions CI.
- **Organisation du code** : structure `app/` (Controllers, Models, Services, Repositories, Middleware, Views), `bootstrap/`, `routes/web.php`, `routes/api.php`.
- **Router & contrôleurs** : FastRoute, base controller (PSR-7 Request/Response, helpers JSON/HTML, validation, pagination).
- **Conteneur & services** : PHP-DI, services notifications (email/SMS/in-app), stockage fichiers, jobs asynchrones (Redis queue + workers), import/export, analytics.
- **Observabilité** : Monolog (canaux app/security/sync), intégration Sentry/ELK, métriques Prometheus.

## Phase D – Base de données & migrations
1. **Modèle conceptuel** : utilisateurs, rôles, organisations, formulaires, sections/questions, soumissions, médias, rendez-vous/événements, formations, partenaires, publications, notifications, logs/audit, widgets, projets/business plans, tickets/support.
2. **Conception logique** : contraintes FK, index, partitionnement tables volumineuses (soumissions, logs), champs audit (created_at/by, updated_at/by), soft deletes.
3. **Migrations & seeds** : scripts init dans `database/migrations`, seeds rôles (admin, analyste, consultant, collecteur, partenaire, utilisateur avancé), seeds contenus de démonstration (missions, publications, formations, FAQ).

## Phase E – Noyau applicatif & services transverses
- **MVC interne** : couche modèles PDO réutilisable, repositories typés, services métiers.
- **Middleware** : auth session + token, CSRF, rate limiting, locale, RBAC fin (politiques par module), journaux d’accès.
- **API REST** : endpoints `/api/v1` pour formulaires, soumissions, publications, rendez-vous, formations, notifications; conventions JSON:API, pagination cursor, filtres génériques.
- **Sécurité fondamentale** : Argon2id, politiques mot de passe, rotation session, CSP stricte, headers sécurité, sanitisation/validation Respect\Validation.
- **Intégrations** : Email, stockage des médias, Google analytics privacy-first, analyses statistiques.

## Phase F – Front public Moderne, premium et dynamique
1. **Accueil** : hero scientifique, slogan, CTA flottant, barre de recherche, timeline,Statistiques, carrousel témoignages, section Actualités dynamique, animations CSS/GSAP.
2. **Nos Missions / Pourquoi SCHOR** : cartes objectifs (accessibilité, transparence, innovation, formation, appui recherche) + section “Pour qui ?” (PME, ONG, chercheurs, autorités, startups, personnes physiques).
3. **Collecte & Analyse** : visuels data, graphiques Chart.js, CTA “Demander une analyse” + upload dataset.
4. **Conseils & Orientation** : formulaire prise de rendez-vous, FAQ, témoignages.
5. **Publications & Ressources** : blog/rapports/études, filtres catégories, moteur de recherche.
6. **Formation & Sensibilisation** : calendrier ateliers/webinaires, CTA inscription, espace universités.
7. **Appui à la recherche / Données** : mise en avant datasets, services data, partenariats.
8. **Footer enrichi** : liens rapides, contacts, réseaux sociaux, mini KPI, newsletter, mentions légales.
9. **Techniques UI/UX** : Bootstrap 5 + Sass modulaire, composants réutilisables, SEO schema.org, Morphisme, OG tags, accessibilité AA, tests Lighthouse, Navigation fluide, Mise en page épurée et structurée, Thème clair et sombre, code couleur: #002f6cff et #ff7f00ff , Police système : `-apple-system, BlinkMacSystemFont, "Segoe UI", ...`


## Phase G – Modules Admin (12 blocs complets)
1. Tableau de bord synthétique : stats temps réel (soumissions, formations, rendez-vous), graphiques, notifications, widgets personnalisables, accès rapide.
2. Gestion utilisateurs & rôles : CRUD, import/export, activation/désactivation, 2FA optionnelle, historique connexions, audit.
3. Publications & ressources : workflow draft → review → publish, éditeur WYSIWYG, aperçu, notifications ciblées.
4. Données collectées : mapping formulaires, validation, visualisation tableaux/graphes, export multi-format, logs d’accès.
5. Rendez-vous / événements : calendrier (FullCalendar), prise de RDV, invitations email/SMS, ICS.
6. Formations : création sessions, inscriptions, suivi assiduité, certificats.
7. Partenaires / organisations : fiches complètes, documents, KPI, suivi collaborations.
8. Notifications / messages : segmentation audiences, templates, campagnes email/SMS/in-app, historique.
9. Paramètres du centre : branding, politiques sécurité, accès API, quotas.
10. Logs d’activité & audit : recherches multi-filtres, alertes anomalies, export CSV/JSON.
11. Support / FAQ admin : base de connaissances interne, tickets, tutoriels.
12. Recherche globale & widgets : moteur FULLTEXT + filtres, favoris, quick actions drag & drop.

## Phase H – Espace utilisateur avancé (15 blocs)
1. Inscription / Connexion / Reset mot de passe (validation email, 2FA optionnelle).
2. Onboarding & tutoriels (checklist, NPS).
3. Dashboard personnel : widgets custom, stats projets/soumissions/notifs.
4. Gestion projets : création, collaboration, versioning, export PDF/Docx.
5. Publications & ressources personnalisées.
6. Gestion données : upload datasets, suivi analyses, visualisation interactive.
7. Rendez-vous & calendrier : demandes consultance, sync ICS.
8. Formations : inscriptions, progression, certificats.
9. Partenaires & documents partagés.
10. Notifications / messages : inbox, filtres, ciblage.
11. Paramètres profil & sécurité.
12. Logs activité utilisateur.
13. Support / FAQ contextualisée.
14. Recherche globale (contenus, projets, formations, publications).
15. Widgets personnalisables (drag & drop, favoris).

## Phase I – Collecte & synchronisation type KoboToolbox
Implémentation d'une stack complète de collecte de données offline-first, synchronisation et analyse, inspirée de KoboToolbox/ODK.

### **1. Infrastructure de collecte (Collecteurs terrain)**
- **Application mobile-like** : interface optimisée pour appareils mobiles (faible bande passante, écrans petits).
- **Mode offline natif** : formulaires téléchargés, réponses stockées localement en SQLite/IndexedDB, synchronisation au retour connexion.
- **Gestion fichiers médias** : photos, audio, vidéo compressées localement, upload chunked avec retry automatique.
- **Géolocalisation** : capture GPS optionnelle (lat/lon/alt/accuracy), markers sur carte, historique traces.
- **Validation en temps réel** : contraintes type (min/max, regex, skip logic) appliquées côté client.
- **Métadonnées d'audit** : device ID, collecteur ID, timestamp, versioning offline UUID → submission ID.

### **2. Synchronisation & résolution conflits**
- **Manifest pull** : collecteur récupère list formulaires + versions, métadonnées (création date, questions, champs obligatoires).
- **Push différé** : file d'attente locale, retry exponentiel, marquage sync_status (pending → synced).
- **Versioning** : if form_version_updated → notification collecteur, re-download, merge réponses existantes.
- **Résolution conflits** : last-write-wins ou merge intelligent (médias + réponses texte disjoints).
- **Compression** : export JSON compressé gzip, signatures HMAC-SHA256 pour intégrité.

### **3. Flux réception au serveur**
- **API collecteurs** : endpoints `/api/v1/submissions/` avec auth token (issued par admin).
- **Validation qualité** : vérification schéma, type données, contraintes, images taille, coordonnées valides.
- **Enrichissement** : reverse geocoding GPS, extraction métadonnées fichiers, hachage données sensibles.
- **Stockage sécurisé** : chiffrement champs PII (AES-256), audit trail changements, soft deletes.
- **Acknowledge & feedback** : ACK immédiat, notifications anomalies, quotas (max 100MB/jour/collecteur).

### **4. Gestion formulaires & versions**
- **Versionning formulaires** : tracking modifications questions (add/remove/rename), déploiement progressif.
- **Déploiement** : admin publie version 1.0, collecteurs reçoivent manifest, update optionnel vs forcé.
- **Compatibilité** : server accepte réponses versions N-2, migration données anciennes questions archivées.
- **Rollback** : restauration version antérieure, re-activation pour collecteurs actifs.

### **5. Tableaux de bord temps réel (Analystes/Admin)**
- **Submission tracker** : vue live (auto-refresh 10s) soumissions entrantes, statut sync, anomalies détectées.
- **Géovisualisation** : cluster map, heatmaps soumissions par zone, drill-down détails.
- **Quality monitoring** : graphiques taux complétude, durée remplissage, drop-off questions, outliers détectés.
- **Performance collector** : statistiques par collecteur (count, avg_time, error_rate), leaderboards, incitations.
- **Alerting** : notifications anomalies (image corrompue, GPS hors bounds, réponse impossible), escalade.

### **6. Exports & intégrations**
- **Multi-formats** : CSV (wide + long format), XLS avec styles, JSON (flat + nested), GeoJSON pour GPS.
- **Filtres avancés** : par plage dates, collecteurs, zones géo, statut, complétude, mots-clés.
- **Exports planifiés** : jobs asynchrones (Redis queue), email automatique, upload vers Google Drive/OneDrive, webhooks.
- **Intégrations** : import vers Power BI/Tableau, export Kobo/ODK Central, API webhooks pour 3e systèmes.

### **7. Analytics & reporting**
- **Rapports dynamiques** : générateur visual (filtres, agrégations, calculs, pivots), exports PDF/PPTX.
- **Analyses prédéfinies** : répartitions réponses (pie/bar charts), cross-tabulations, analyses texte (word clouds).
- **Time series** : courbes soumissions par jour, tendances réponses, comparaisons périodes.
- **Données sensibles** : anonymisation avant export (hash IDs, masquage noms), conformité RGPD, audit traces.

### **8. Sécurité & gouvernance collecte**
- **RBAC collecteurs** : roles (collecteur_basique, senior_collecteur, superviseur), permissions per formulaire/zone.
- **Credentials & tokens** : auth tokens révocables (exp 90j), device tokens, audit logins échoués.
- **Données sensibles** : PII flagging (phone, email, ID), chiffrement stockage/transit, purges programmées.
- **Conformité** : RGPD (right to delete submissions), audit trail complet, backups chiffrés, disaster recovery.

### **9. Scaling & optimisation**
- **Indexation** : full-text search sur réponses texte (MySQL FULLTEXT ou Elasticsearch).
- **Partitionnement** : tables soumissions partitionnées par date (hebdo/mensuel), archivage données anciennes.
- **Caching** : Redis cache formulaires (5min), réponses agrégées (15min), invalidation events.
- **Monitoring** : métriques soumissions/sec, latence API, storage usage, alertes seuils dépassés.


## Phase J – Sécurité, conformité & observabilité
- RBAC granulaire couvrant modules front/admin/utilisateur.
- Chiffrement données sensibles (OpenSSL), stockage fichiers chiffrés, rotation clés.
- CSRF, CSP, protections XSS/SQLi, scans dépendances, tests intrusion périodiques.
- RGPD : consentement, droit à l’oubli, registre traitements, anonymisation datasets.
- Backups automatisés (base + médias), PRA/PCA, plan de reprise.
- Audit trail (events user_login, form_submission, data_export, rendez-vous, formation, publication).

## Phase K – Qualité, tests & automatisation
- **Tests unitaires** (PHPUnit) sur services/repositories, **tests fonctionnels** (Pest/Behat) pour parcours clés (collecte, admin, utilisateur), **tests API** (Postman/Newman), **performance** (k6).
- **Lint/format** : PHP-CS-Fixer, ESLint/Prettier, Stylelint.
- **CI/CD** : GitHub Actions/GitLab CI (lint, tests, build assets, packaging), sécurité (Dependabot).
- **Environnements** : dev (Docker Compose), staging, préprod, prod avec données anonymisées.

## Phase L – Livraison, déploiement & exploitation
- Pipelines automatisés (Capistrano/Deployer ou Actions vers VPS/containers), migrations & seeds orchestrées.
- Health checks applicatifs, monitoring uptime, alerting.
- Observabilité complète : logs centralisés, dashboards Grafana, alertes Prometheus.
- Documentation runbooks (opérations, incidents, déploiements), guides utilisateur/admin.

## Phase M – Formation, adoption & support
- Sessions formation internes (admin, analystes, collecteurs) + contenus e-learning.
- Guides pas-à-pas, vidéos, FAQ intégrée, support omnicanal.
- Boucle feedback (surveys in-app, NPS), roadmap publique, amélioration continue.
