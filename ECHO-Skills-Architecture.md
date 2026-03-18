# Architecture Skills & Workflows - Projet Mouvement ECHO

*Document de curation et d'automatisation pour Claude Code*
*Date : 18 mars 2026*

---

## PARTIE 1 - Synthese du projet ECHO

### Comprehension globale

**Mouvement ECHO** est une association loi 1901 (SIREN 933 682 510, active depuis le 01/09/2024, siege a Bougival 78380) portant un ecosysteme transmedia structure autour de 3 piliers :

**1. INFORMER - La Serie ECHO**
- Webserie sociale, educative et transmedia de 33 episodes (3 saisons x 11), inspiree de La Divine Comedie de Dante
- Saison 1 "L'Enfer" (Antithese) : decryptage des vices et dysfonctionnements systemiques
- Saison 2 "Le Purgatoire" (These) : exploration de solutions tangibles
- Saison 3 "Le Paradis" (Synthese) : vision d'une societe reformee
- Format 40-60 min par episode, melant fiction, realite et documentaire
- Bande-annonce prevue mars 2026, diffusion S1 sept 2026 - fev 2027
- Personnages ancres dans les 7 peches capitaux de Dante (Sacha, Akou, Eva, Lily, collegues)

**2. FEDERER - Le Mouvement ECHO**
- Association qui federe l'ECHOSystem : partenaires experts, financiers, audiovisuels, educatifs
- Systeme d'adhesions et de communaute (Discord collaboratif)
- Valeurs : Cooperation, Responsabilite, Respect, Integrite, Innovation
- 13 regles ECHO regissant le fonctionnement interne

**3. AGIR - Les Plateformes**
- **ECHOLink** : plateforme d'action collaborative avec 3 fonctionnalites : enigmes/apprentissage, hubs de projets geolocalises, systeme economique alternatif (troc, monnaie virtuelle)
- **Cognisphere** : OS d'apprentissage augmente par IA avec tuteur IA socratique, memorisation espacee (courbe Ebbinghaus), apprentissage social collaboratif (Focus Camps, binomes d'etude)

### Gouvernance (Constitution ECHO v1)
L'association adopte un modele de gouvernance horizontale inspire de la sociocratie, Frederic Laloux (organisations Teal), Elinor Ostrom (gouvernance des communs) et les traditions africaines de dialogue circulaire (palabre).

**Structure en 14 cercles** : ECHOmovie (serie), ECHOcommunaute, ECHOpartenariat, ECHOnomie (admin/finance), ECHOcommunication, ECHOnet (infra numerique), ECHOtech, ECHOacademy, ECHOsocial, ECHOCognisphere, ECHOsound, ECHOood (documentaire), ECHOallies, ECHOlearn.

**Conseil Oecumenique (ECHOC)** : 13 membres, decisions par consentement, representant legal tournant (mandat 18 mois).

**Phases de croissance** : La Graine (5 membres) → La Germination (7-9) → L'Enracinement (13) → L'Emergence (25) → Les Branches (50) → La Floraison (100+) → La Fructification (11+ salaries).

### Stack technique identifie
- **Site web** : Next.js (projet actuel)
- **Cognisphere (PRD v1.3)** : Electron + React + TypeScript (desktop), React Native (mobile), Python + LLM local (Mistral 7B) + Whisper + LanceDB, SQLite, CRDT sync, architecture local-first
- **ECHOLink** : React + Tailwind + Shadcn UI (frontend), FastAPI + MongoDB (backend)
- **Algorithme cle** : FSRS-5 (repetition espacee), matching study buddies, graphe de connaissances D3.js
- **Securite** : AES-256 chiffrement, X25519+AES-GCM transit, architecture zero-data-server
- **Outils** : Claude Code comme collaborateur technique principal, Discord, Google Drive

### Equipe
- Cofondateurs : Eddyason Koffi, Jeremy Lasne (representant legal, gardien de la raison d'etre)
- Deborah Prevaud (chargee de developpement), Clement Grandmontagne (co-realisateur), Thierry Korutos-Chatam (partenariats)
- ~15 membres actifs : developpeurs web, data analyst, ingenieur IA, community manager, scenaristes, monteur
- Budget : financement par partenariats, crowdfunding, subventions, monetisation YouTube

### Modele economique Cognisphere
- **FREE** (0EUR) : 100 cards, 3 mind maps, 1 device
- **PRO** (9EUR/mois) : Illimite, multi-device, Palais Mental 3D, scheduling complet
- **TEAM** (15EUR/user/mois) : Admin panel, SLA 99.9%
- Cible : 50 000 utilisateurs, 5% conversion = 2 500 Pro = ~22 500EUR MRR

### Urgences operationnelles identifiees
1. Site web a finaliser (prevu 01/03/2026 - en retard)
2. Bande-annonce en production (mars 2026)
3. Plateforme ECHOLink a developper
4. Cognisphere MVP desktop a livrer (cible mai 2026, candidature Emergence IDF 2026)
5. Gestion administrative de l'association (comptabilite, adhesions, RGPD)
6. Prototype mobile Cognisphere (Phase 1 : companion review-only)

---

## PARTIE 2 - Audit des skills existants

### Etat des lieux

| Emplacement | Skill | Utilite ECHO | Recommandation | Justification |
|---|---|---|---|---|
| `/home/claude/.claude/skills/session-start-hook/` | startup-hook-skill | Partiel | **Conserver** | Utile pour initialiser les sessions Claude Code sur le web, installer les dependances automatiquement. Pertinent pour le workflow dev Next.js/FastAPI |
| `/mnt/skills/user/` | *(vide - repertoire inexistant)* | N/A | **A creer** | Le repertoire n'existe pas encore. Il faudra le creer pour accueillir les skills valides |

**Constat** : L'environnement est quasi-vierge. Un seul skill systeme est present (session-start-hook). Il n'y a aucun skill utilisateur installe. Tout est a construire.

---

## PARTIE 3 - Proposition des 50 Skills

### Note importante sur l'ecosysteme des skills Claude Code

Les "skills" Claude Code sont des fichiers `SKILL.md` contenant des instructions structurees que Claude Code lit pour executer des taches specifiques. Il n'existe pas de marketplace centralisee. Les skills sont :
- **Crees sur mesure** pour un projet (fichiers SKILL.md dans `.claude/skills/`)
- **Partages via GitHub** par la communaute (repos a cloner)
- **Fournis par des serveurs MCP** (Model Context Protocol) pour des integrations externes

La proposition ci-dessous combine ces 3 sources. Chaque skill est un fichier SKILL.md a creer dans `/mnt/skills/user/` ou `.claude/skills/`.

---

### DOMAINE 1 : Administration Associative Loi 1901 (12 skills)

> **Domaine prioritaire.** Ces skills couvrent la gestion quotidienne, juridique et financiere du Mouvement ECHO en tant qu'association loi 1901. Ils tiennent compte de la gouvernance sociocratique par cercles definie dans la Constitution ECHO v1.

#### Skill A1 - governance-circles-manager
- **Source** : Custom SKILL.md
- **Domaine** : Gouvernance / Organisation
- **Cas d'usage ECHO** : Gestion operationnelle des 14 cercles sociocratiques de l'association. Suivi de la composition de chaque cercle (premier lien, second lien, membres), facilitation des processus de decision par consentement, mitose obligatoire au-dela de 12 membres, animation du Conseil Oecumenique (ECHOC, 13 membres). Gestion des mandats tournants du representant legal (18 mois) et du facilitateur. Tenue du registre des decisions du ECHOC
- **Priorite** : P0 Indispensable
- **Synergies** : meeting-notes-ag, member-registry, document-generator-asso

#### Skill A2 - member-registry
- **Source** : Custom SKILL.md
- **Domaine** : Administration / Membres
- **Cas d'usage ECHO** : Registre officiel des adherents conforme aux obligations loi 1901. Inscription, demission, radiation, cotisations annuelles. Suivi du statut (membre actif, bienfaiteur, partenaire, fondateur). Historique des contributions et engagements par cercle. Alertes pour cotisations en retard. Export pour declarations et AG. Respect des phases de croissance (La Graine → La Fructification)
- **Priorite** : P0 Indispensable
- **Synergies** : governance-circles-manager, financial-tracker-asso, cerfa-fiscal-receipts

#### Skill A3 - financial-tracker-asso
- **Source** : Custom SKILL.md
- **Domaine** : Administration / Comptabilite
- **Cas d'usage ECHO** : Comptabilite conforme aux obligations des associations loi 1901 (plan comptable associatif). Suivi des recettes (cotisations, dons, subventions, crowdfunding, mecenat) et depenses. Rapprochement bancaire mensuel. Budget previsionnel annuel. Generation du bilan financier et compte de resultat pour l'AG. Suivi par cercle (ECHOnomie). Seuils d'alerte pour le commissaire aux comptes si >153 000EUR de subventions
- **Priorite** : P0 Indispensable
- **Synergies** : member-registry, cerfa-fiscal-receipts, grant-manager

#### Skill A4 - cerfa-fiscal-receipts
- **Source** : Custom SKILL.md
- **Domaine** : Administration / Fiscalite
- **Cas d'usage ECHO** : Generation de recus fiscaux Cerfa n°11580*04 (dons) et Cerfa n°11580*03 (mecenat) conformes aux articles 200 et 238 bis du CGI. Verification de l'eligibilite de l'association a emettre des recus fiscaux (interet general, gestion desinteressee). Numerotation sequentielle, archivage 6 ans, envoi automatique aux donateurs. Suivi du montant total des dons pour les declarations fiscales de l'association
- **Priorite** : P0 Indispensable
- **Synergies** : financial-tracker-asso, member-registry, document-generator-asso

#### Skill A5 - meeting-notes-ag
- **Source** : Custom SKILL.md
- **Domaine** : Administration / Reunions
- **Cas d'usage ECHO** : Gestion complete des Assemblees Generales (ordinaires et extraordinaires) et reunions du ECHOC. Convocations avec ordre du jour (15 jours avant), feuilles de presence, verification du quorum, proces-verbaux conformes, registre des deliberations. Gestion des votes par consentement (specifique ECHO). Preparation du rapport moral et du rapport financier pour l'AGO. Archivage des PV au siege social
- **Priorite** : P0 Indispensable
- **Synergies** : governance-circles-manager, document-generator-asso, member-registry

#### Skill A6 - prefecture-declarations
- **Source** : Custom SKILL.md
- **Domaine** : Administration / Juridique
- **Cas d'usage ECHO** : Declarations obligatoires a la prefecture des Yvelines (siege a Bougival 78380). Declaration de modification (changement de bureau, de siege, d'objet). Publication au Journal Officiel. Mise a jour du RNA (Repertoire National des Associations). Suivi du SIRET (933 682 510 00013) et des obligations INSEE. Declaration de changement de representant legal lors des mandats tournants (tous les 18 mois)
- **Priorite** : P0 Indispensable
- **Synergies** : governance-circles-manager, association-legal-advisor-asso

#### Skill A7 - association-legal-advisor-asso
- **Source** : Custom SKILL.md
- **Domaine** : Administration / Juridique
- **Cas d'usage ECHO** : Conseil juridique specialise loi 1901. Verification de conformite des statuts et du reglement interieur avec la legislation en vigueur. Obligations employeur si salaries (phase La Fructification : CSE obligatoire a 11+ salaries). Responsabilite du president et des dirigeants. Assurance responsabilite civile. Conventions de mise a disposition de locaux. Droit du benevole (loi du 23 mai 2006). Articulation avec la gouvernance horizontale specifique ECHO (pas de president permanent)
- **Priorite** : P0 Indispensable
- **Synergies** : prefecture-declarations, rgpd-compliance-asso, volunteer-manager

#### Skill A8 - volunteer-manager
- **Source** : Custom SKILL.md
- **Domaine** : Administration / Ressources Humaines
- **Cas d'usage ECHO** : Gestion des benevoles du Mouvement ECHO (~15 membres actifs). Lettre de mission pour chaque benevole. Valorisation comptable du benevolat (methode du cout de remplacement, utile pour les dossiers de subvention). Planning des disponibilites. Suivi des heures par cercle. Remboursement de frais (justificatifs, bareme kilometrique). Contrat de benevolat (non obligatoire mais recommande). Couverture assurance. Attestation de benevolat pour les benevoles
- **Priorite** : P1 Important
- **Synergies** : member-registry, governance-circles-manager, financial-tracker-asso

#### Skill A9 - grant-manager
- **Source** : Custom SKILL.md
- **Domaine** : Administration / Subventions
- **Cas d'usage ECHO** : Gestion complete du cycle de vie des subventions. Veille des appels a projets (Emergence IDF 2026, FDVA, FONJEP, Region IDF, collectivites). Constitution des dossiers Cerfa n°12156*06 (demande de subvention). Budget previsionnel par action. Convention d'objectifs et de moyens. Reporting et bilan d'utilisation obligatoire. Suivi des echeances et relances. Pipeline des demandes en cours (soumis, accorde, refuse, a reporter)
- **Priorite** : P0 Indispensable
- **Synergies** : financial-tracker-asso, document-generator-asso, association-legal-advisor-asso

#### Skill A10 - partnership-crm
- **Source** : Custom SKILL.md
- **Domaine** : Administration / Partenariats
- **Cas d'usage ECHO** : CRM dedie aux partenaires de l'ECHOSystem (experts, financiers, audiovisuels, educatifs). Fiche partenaire avec : contact, type de partenariat, conventions signees, historique des echanges, valeur apportee. Pipeline de prospection. Modeles de conventions de partenariat. Suivi des engagements reciproques. Mapping partenaires par cercle (ECHOpartenariat). Gestion de l'axe France-Afrique (polycentricite de la gouvernance)
- **Priorite** : P1 Important
- **Synergies** : grant-manager, contract-templates-asso, volunteer-manager

#### Skill A11 - document-generator-asso
- **Source** : Custom SKILL.md
- **Domaine** : Administration / Documents
- **Cas d'usage ECHO** : Generation de tous les documents officiels de l'association. Modeles : attestation de domiciliation, attestation d'adhesion, lettre de mission benevole, convention de partenariat, rapport moral annuel, rapport d'activite, budget previsionnel, bilan financier, compte de resultat, PV d'AG, PV de ECHOC, convocations, courrier prefecture. Format PDF avec en-tete ECHO et mentions legales obligatoires
- **Priorite** : P0 Indispensable
- **Synergies** : Tous les skills du domaine Administration

#### Skill A12 - rgpd-compliance-asso
- **Source** : Custom SKILL.md
- **Domaine** : Administration / Conformite
- **Cas d'usage ECHO** : Conformite RGPD specifique aux associations. Registre des traitements (membres, donateurs, benevoles, newsletter). Politique de confidentialite conforme. Durees de conservation (3 ans apres dernier contact pour prospects, duree de la relation + 5 ans pour membres). Droit d'acces, rectification, effacement, portabilite. Base legale par traitement (consentement, interet legitime, obligation legale). DPO si traitements sensibles. Formation des benevoles a la protection des donnees
- **Priorite** : P0 Indispensable
- **Synergies** : member-registry, association-legal-advisor-asso, document-generator-asso

---

### DOMAINE 2 : Developpement Web Frontend (8 skills)

#### Skill 1 - nextjs-app-builder
- **Source** : Custom SKILL.md
- **Domaine** : Frontend
- **Cas d'usage ECHO** : Construction des pages du site web ECHO (accueil, episodes, mouvement, ECHOSystem, ECHOLink). Generation de composants Next.js App Router avec TypeScript
- **Priorite** : P0 Indispensable
- **Synergies** : tailwind-component-designer, shadcn-ui-integrator

#### Skill 2 - tailwind-component-designer
- **Source** : Custom SKILL.md
- **Domaine** : Frontend / Design
- **Cas d'usage ECHO** : Design system coherent pour le site web et ECHOLink. Creation de composants UI respectant la charte ECHO (fond sombre, accents bleu/rouge)
- **Priorite** : P0 Indispensable
- **Synergies** : nextjs-app-builder, shadcn-ui-integrator

#### Skill 3 - shadcn-ui-integrator
- **Source** : Custom SKILL.md
- **Domaine** : Frontend / UI
- **Cas d'usage ECHO** : Integration des composants Shadcn UI (formulaires d'adhesion, cartes de projets, tableaux de bord). Configuration theme sombre ECHO
- **Priorite** : P0 Indispensable
- **Synergies** : tailwind-component-designer, form-builder

#### Skill 4 - responsive-layout-architect
- **Source** : Custom SKILL.md
- **Domaine** : Frontend
- **Cas d'usage ECHO** : Layouts responsive pour le site web et ECHOLink (mobile-first, essentiel pour la communaute). Grilles adaptatives pour la carte de projets collaboratifs
- **Priorite** : P1 Important
- **Synergies** : nextjs-app-builder, tailwind-component-designer

#### Skill 5 - interactive-map-builder
- **Source** : Custom SKILL.md
- **Domaine** : Frontend / Geo
- **Cas d'usage ECHO** : Carte interactive des projets collaboratifs ECHOLink (hubs locaux, departementaux, regionaux). Integration Leaflet/Mapbox avec geolocalisation
- **Priorite** : P1 Important
- **Synergies** : nextjs-app-builder, api-endpoint-designer

#### Skill 6 - video-player-integrator
- **Source** : Custom SKILL.md
- **Domaine** : Frontend / Media
- **Cas d'usage ECHO** : Lecteur video custom pour les 33 episodes de la serie ECHO. Integration YouTube/Vimeo embed avec metadonnees, chapitres, et indices visuels
- **Priorite** : P1 Important
- **Synergies** : nextjs-app-builder, content-management-skill

#### Skill 7 - animation-motion-designer
- **Source** : Custom SKILL.md
- **Domaine** : Frontend / UX
- **Cas d'usage ECHO** : Animations immersives pour le site ECHO (transitions entre sections Enfer/Purgatoire/Paradis, effets de parallaxe, animations du logo ECHO). Framer Motion / GSAP
- **Priorite** : P2 Utile
- **Synergies** : nextjs-app-builder, tailwind-component-designer

#### Skill 8 - pwa-offline-builder
- **Source** : Custom SKILL.md
- **Domaine** : Frontend / Mobile
- **Cas d'usage ECHO** : Transformer ECHOLink et Cognisphere en PWA pour un acces offline aux flashcards et contenus d'apprentissage. Service workers, cache strategies
- **Priorite** : P2 Utile
- **Synergies** : nextjs-app-builder, cognisphere-learning-engine

---

### DOMAINE 2 : Developpement Backend (7 skills)

#### Skill 9 - fastapi-backend-architect
- **Source** : Custom SKILL.md
- **Domaine** : Backend
- **Cas d'usage ECHO** : Architecture API REST pour ECHOLink et Cognisphere. Endpoints pour adhesions, projets collaboratifs, systeme de points, enigmes. Structure FastAPI avec routers modulaires
- **Priorite** : P0 Indispensable
- **Synergies** : mongodb-schema-designer, auth-system-builder

#### Skill 10 - mongodb-schema-designer
- **Source** : Custom SKILL.md
- **Domaine** : Backend / Data
- **Cas d'usage ECHO** : Modelisation MongoDB pour : membres/adherents, episodes/metadonnees, projets collaboratifs, systeme de points/monnaie virtuelle, flashcards Cognisphere, progression apprentissage
- **Priorite** : P0 Indispensable
- **Synergies** : fastapi-backend-architect, api-endpoint-designer

#### Skill 11 - auth-system-builder
- **Source** : Custom SKILL.md
- **Domaine** : Backend / Securite
- **Cas d'usage ECHO** : Authentification des membres du Mouvement ECHO. JWT + OAuth2, gestion des roles (adherent, benevole, partenaire, admin). Inscription via formulaire d'adhesion
- **Priorite** : P0 Indispensable
- **Synergies** : fastapi-backend-architect, rgpd-compliance-checker

#### Skill 12 - api-endpoint-designer
- **Source** : Custom SKILL.md
- **Domaine** : Backend
- **Cas d'usage ECHO** : Design et documentation d'API RESTful pour toutes les fonctionnalites ECHO. OpenAPI/Swagger auto-genere. Versionning d'API
- **Priorite** : P1 Important
- **Synergies** : fastapi-backend-architect, nextjs-app-builder

#### Skill 13 - websocket-realtime-handler
- **Source** : Custom SKILL.md
- **Domaine** : Backend / Realtime
- **Cas d'usage ECHO** : Communication temps reel pour la resolution collaborative d'enigmes ECHOLink et les Focus Camps Cognisphere. Notifications push aux membres
- **Priorite** : P2 Utile
- **Synergies** : fastapi-backend-architect, nextjs-app-builder

#### Skill 14 - file-upload-media-handler
- **Source** : Custom SKILL.md
- **Domaine** : Backend / Media
- **Cas d'usage ECHO** : Upload et traitement de contenus pour Cognisphere (PDF, videos YouTube, podcasts). Extraction de texte, transcription, structuration automatique du contenu
- **Priorite** : P1 Important
- **Synergies** : fastapi-backend-architect, cognisphere-learning-engine

#### Skill 15 - fsrs5-spaced-repetition-engine
- **Source** : Custom SKILL.md
- **Domaine** : Backend / Algorithme
- **Cas d'usage ECHO** : Implementation de l'algorithme FSRS-5 (Free Spaced Repetition Scheduler) pour Cognisphere. Modele DSR (Difficulty-Stability-Retrievability), extensions pour contexte temporel, graphe de dependances, detection de leeches. Grades Again/Hard/Good/Easy, gestion fatigue cognitive
- **Priorite** : P1 Important
- **Synergies** : mongodb-schema-designer, electron-desktop-builder

---

### DOMAINE 3 : Design & UI (4 skills)

#### Skill 16 - design-system-manager
- **Source** : Custom SKILL.md
- **Domaine** : Design
- **Cas d'usage ECHO** : Gestion du design system ECHO : palette de couleurs (noir, bleu ECHO, rouge ECHO), typographies, espacements, composants reutilisables. Tokens CSS/Tailwind
- **Priorite** : P0 Indispensable
- **Synergies** : tailwind-component-designer, shadcn-ui-integrator

#### Skill 17 - dark-theme-architect
- **Source** : Custom SKILL.md
- **Domaine** : Design / UX
- **Cas d'usage ECHO** : L'identite visuelle ECHO est fondamentalement sombre (fond noir avec accents). Ce skill gere le theme sombre natif et les variantes par saison (rouge Enfer, violet Purgatoire, dore Paradis)
- **Priorite** : P1 Important
- **Synergies** : design-system-manager, tailwind-component-designer

#### Skill 18 - icon-illustration-curator
- **Source** : Custom SKILL.md
- **Domaine** : Design / Assets
- **Cas d'usage ECHO** : Curation et integration des icones pour le site web et les plateformes. Icones personnalisees pour les sections (ECHOSystem, episodes, enigmes). Lucide Icons / custom SVG
- **Priorite** : P2 Utile
- **Synergies** : design-system-manager, nextjs-app-builder

#### Skill 19 - accessibility-auditor
- **Source** : Custom SKILL.md
- **Domaine** : Design / Accessibilite
- **Cas d'usage ECHO** : Audit et correction d'accessibilite WCAG pour le site web et ECHOLink. La serie vise toutes les classes sociales : l'accessibilite web est indispensable pour l'inclusivite
- **Priorite** : P1 Important
- **Synergies** : nextjs-app-builder, tailwind-component-designer

---

### DOMAINE 4 : Contenu & Redaction (5 skills)

#### Skill 20 - content-writer-fr
- **Source** : Custom SKILL.md
- **Domaine** : Contenu
- **Cas d'usage ECHO** : Redaction de contenus en francais pour le site web, articles de blog, descriptions d'episodes, biographies de personnages, pages du Mouvement. Ton aligne avec les valeurs ECHO
- **Priorite** : P0 Indispensable
- **Synergies** : seo-optimizer, social-media-content-creator

#### Skill 21 - seo-optimizer
- **Source** : Custom SKILL.md
- **Domaine** : Contenu / SEO
- **Cas d'usage ECHO** : Optimisation SEO du site web ECHO pour les requetes cibles (webserie engagee, action collective, serie Dante moderne, etc.). Meta tags, structured data, sitemap
- **Priorite** : P1 Important
- **Synergies** : content-writer-fr, nextjs-app-builder

#### Skill 22 - email-template-builder
- **Source** : Custom SKILL.md
- **Domaine** : Contenu / Communication
- **Cas d'usage ECHO** : Templates d'emails pour : confirmation d'adhesion, newsletters mensuelles, relances benevoles, invitations aux evenements, notifications de nouveaux episodes
- **Priorite** : P1 Important
- **Synergies** : content-writer-fr, member-management-skill

#### Skill 23 - document-generator
- **Source** : Custom SKILL.md
- **Domaine** : Contenu / Admin
- **Cas d'usage ECHO** : Generation de documents officiels : attestations de don (cerfa), conventions de partenariat, dossiers de subvention, comptes-rendus d'AG, rapports d'activite
- **Priorite** : P1 Important
- **Synergies** : association-legal-advisor, financial-tracker

#### Skill 24 - multilingual-translator
- **Source** : Custom SKILL.md
- **Domaine** : Contenu / i18n
- **Cas d'usage ECHO** : Traduction FR/EN/langues africaines pour le deploiement intercontinental de la serie (diffusion Afrique prevue 2027). Sous-titrage, localisation du site web
- **Priorite** : P2 Utile
- **Synergies** : content-writer-fr, nextjs-app-builder

---

### DOMAINE 5 : Video & Transmedia (4 skills)

#### Skill 25 - screenplay-formatter
- **Source** : Custom SKILL.md
- **Domaine** : Video / Ecriture
- **Cas d'usage ECHO** : Formatage de scenarios aux normes professionnelles (format Courier 12pt, INT/EXT, dialogues). Assistance a la reecriture des 11 episodes de la saison 1 en cours de finalisation
- **Priorite** : P1 Important
- **Synergies** : content-writer-fr, storyboard-assistant

#### Skill 26 - storyboard-assistant
- **Source** : Custom SKILL.md
- **Domaine** : Video / Pre-production
- **Cas d'usage ECHO** : Assistance au decoupage technique (pilote en cours). Description structuree des plans, mouvements de camera, notes de mise en scene pour le co-realisateur Clement
- **Priorite** : P2 Utile
- **Synergies** : screenplay-formatter

#### Skill 27 - transmedia-narrative-planner
- **Source** : Custom SKILL.md
- **Domaine** : Transmedia
- **Cas d'usage ECHO** : Planification de la narration transmedia : liens entre episodes TV, enigmes ECHOLink, comptes reseaux sociaux des personnages, QR codes physiques, events IRL. Matrice de coherence narrative
- **Priorite** : P0 Indispensable
- **Synergies** : social-media-content-creator, enigma-designer

#### Skill 28 - enigma-designer
- **Source** : Custom SKILL.md
- **Domaine** : Transmedia / Gamification
- **Cas d'usage ECHO** : Conception d'enigmes integrees aux episodes (indices visuels dissimules, QR codes, chasse au tresor nationale). Coherence entre enigmes virtuelles et physiques
- **Priorite** : P1 Important
- **Synergies** : transmedia-narrative-planner, interactive-map-builder

---

### DOMAINE 6 : Gestion de Projet (5 skills)

#### Skill 29 - project-tracker
- **Source** : Custom SKILL.md
- **Domaine** : Gestion de projet
- **Cas d'usage ECHO** : Suivi des taches et jalons du projet ECHO. Roadmap par sprint, suivi de l'avancement (bande-annonce, site web, scenarios, ECHOLink). Dashboard de progression
- **Priorite** : P0 Indispensable
- **Synergies** : meeting-notes-generator, team-coordination-skill

#### Skill 30 - meeting-notes-generator
- **Source** : Custom SKILL.md
- **Domaine** : Gestion de projet
- **Cas d'usage ECHO** : Generation automatique de comptes-rendus de reunions d'equipe (Discord, visios). Extraction des decisions, actions, et responsables
- **Priorite** : P1 Important
- **Synergies** : project-tracker, team-coordination-skill

#### Skill 31 - team-coordination-skill
- **Source** : Custom SKILL.md
- **Domaine** : Gestion de projet / RH
- **Cas d'usage ECHO** : Coordination des ~15 membres benevoles. Attribution des taches selon competences et centres d'interet (regle ECHO n°11). Suivi de l'engagement et relances
- **Priorite** : P1 Important
- **Synergies** : project-tracker, member-management-skill

#### Skill 32 - onboarding-guide
- **Source** : Custom SKILL.md
- **Domaine** : Gestion de projet / RH
- **Cas d'usage ECHO** : Parcours d'onboarding pour les nouveaux benevoles : presentation du projet, lecture du reglement interieur, signature, acces Discord/Drive, attribution des premieres taches
- **Priorite** : P2 Utile
- **Synergies** : team-coordination-skill, document-generator

#### Skill 33 - risk-analyzer
- **Source** : Custom SKILL.md
- **Domaine** : Gestion de projet / Strategie
- **Cas d'usage ECHO** : Identification et suivi des risques projet : retards de production, depart de benevoles, problemes de financement, risques juridiques. Matrice probabilite/impact
- **Priorite** : P2 Utile
- **Synergies** : project-tracker, financial-tracker

---

### DOMAINE 7 : Conformite & Juridique (4 skills)

#### Skill 34 - rgpd-compliance-checker
- **Source** : Custom SKILL.md
- **Domaine** : Conformite / RGPD
- **Cas d'usage ECHO** : Verification de la conformite RGPD pour le site web, ECHOLink et Cognisphere. Politique de confidentialite, consentement cookies, registre de traitements, DPO. Indispensable pour la collecte de donnees des adherents
- **Priorite** : P0 Indispensable
- **Synergies** : auth-system-builder, association-legal-advisor

#### Skill 35 - association-legal-advisor
- **Source** : Custom SKILL.md
- **Domaine** : Juridique
- **Cas d'usage ECHO** : Assistance juridique pour association loi 1901 : statuts, reglement interieur (deja redige), declarations prefecture, obligations comptables, recu fiscal (articles 200/238 CGI), contrats de benevoles
- **Priorite** : P0 Indispensable
- **Synergies** : rgpd-compliance-checker, document-generator

#### Skill 36 - intellectual-property-advisor
- **Source** : Custom SKILL.md
- **Domaine** : Juridique / PI
- **Cas d'usage ECHO** : Protection de la propriete intellectuelle : depot de marque ECHO, droits d'auteur sur les scenarios/episodes, licences Creative Commons pour les contenus educatifs, droits a l'image des acteurs
- **Priorite** : P1 Important
- **Synergies** : association-legal-advisor, screenplay-formatter

#### Skill 37 - contract-template-generator
- **Source** : Custom SKILL.md
- **Domaine** : Juridique / Contrats
- **Cas d'usage ECHO** : Modeles de contrats : conventions de partenariat ECHOSystem, contrats de cession de droits, autorisations de tournage, CGU des plateformes ECHOLink/Cognisphere
- **Priorite** : P1 Important
- **Synergies** : association-legal-advisor, document-generator

---

### DOMAINE 8 : Communication & Community Management (5 skills)

#### Skill 38 - social-media-content-creator
- **Source** : Custom SKILL.md
- **Domaine** : Communication / Social
- **Cas d'usage ECHO** : Creation de contenu pour les reseaux sociaux (Instagram, YouTube, TikTok, X). Publications des personnages fictifs (strategie transmedia), teasers d'episodes, behind-the-scenes
- **Priorite** : P0 Indispensable
- **Synergies** : content-writer-fr, transmedia-narrative-planner

#### Skill 39 - community-moderation-guide
- **Source** : Custom SKILL.md
- **Domaine** : Communication / Communaute
- **Cas d'usage ECHO** : Regles et outils de moderation pour le Discord ECHO et les futurs espaces communautaires ECHOLink. Gestion des conflits, charte de bonne conduite, signalement
- **Priorite** : P1 Important
- **Synergies** : social-media-content-creator, member-management-skill

#### Skill 40 - newsletter-architect
- **Source** : Custom SKILL.md
- **Domaine** : Communication / Email
- **Cas d'usage ECHO** : Conception et envoi de newsletters periodiques aux adherents et partenaires. Actualites du projet, avancement de la serie, prochains evenements, appels a benevoles
- **Priorite** : P1 Important
- **Synergies** : email-template-builder, content-writer-fr

#### Skill 41 - press-kit-generator
- **Source** : Custom SKILL.md
- **Domaine** : Communication / Presse
- **Cas d'usage ECHO** : Generation de dossiers et communiques de presse pour les medias. Pitch journaliste, visuels HD, biographies, synopsis, contacts. Indispensable pour la diffusion de la bande-annonce
- **Priorite** : P1 Important
- **Synergies** : content-writer-fr, document-generator

#### Skill 42 - event-planner
- **Source** : Custom SKILL.md
- **Domaine** : Communication / Evenements
- **Cas d'usage ECHO** : Planification des evenements ECHO : projections/cine-debats, ateliers, enigmes urbaines, conferences. Check-lists, planning, communication, logistique
- **Priorite** : P2 Utile
- **Synergies** : project-tracker, social-media-content-creator

---

### DOMAINE 9 : Donnees & Analytics (3 skills)

#### Skill 43 - analytics-dashboard-builder
- **Source** : Custom SKILL.md
- **Domaine** : Analytics
- **Cas d'usage ECHO** : Tableaux de bord pour suivre les KPIs du projet : nombre d'adherents, vues des episodes, engagement communautaire, progression des projets ECHOLink, metriques Cognisphere
- **Priorite** : P1 Important
- **Synergies** : mongodb-schema-designer, nextjs-app-builder

#### Skill 44 - member-management-skill
- **Source** : Custom SKILL.md
- **Domaine** : Donnees / CRM
- **Cas d'usage ECHO** : Gestion des adherents du Mouvement ECHO : inscriptions, cotisations, roles (benevole/partenaire/expert), suivi de l'engagement, historique des contributions
- **Priorite** : P0 Indispensable
- **Synergies** : auth-system-builder, financial-tracker

#### Skill 45 - financial-tracker
- **Source** : Custom SKILL.md
- **Domaine** : Donnees / Finance
- **Cas d'usage ECHO** : Suivi comptable de l'association : recettes (adhesions, dons, subventions, crowdfunding), depenses, budget previsionnel, bilan annuel. Generation de documents comptables conformes
- **Priorite** : P0 Indispensable
- **Synergies** : member-management-skill, association-legal-advisor

---

### DOMAINE 10 : Automatisation & DevOps (5 skills)

#### Skill 46 - ci-cd-pipeline-builder
- **Source** : Custom SKILL.md
- **Domaine** : DevOps
- **Cas d'usage ECHO** : Pipeline CI/CD pour le site web et les plateformes. Tests automatises, build Next.js, deploiement Vercel/VPS. Lint, type-check, preview deployments
- **Priorite** : P0 Indispensable
- **Synergies** : nextjs-app-builder, test-automation-skill

#### Skill 47 - test-automation-skill
- **Source** : Custom SKILL.md
- **Domaine** : DevOps / QA
- **Cas d'usage ECHO** : Tests automatises pour le site web et les API. Tests unitaires (Vitest), tests d'integration, tests E2E (Playwright) pour les parcours critiques (adhesion, inscription ECHOLink)
- **Priorite** : P1 Important
- **Synergies** : ci-cd-pipeline-builder, fastapi-backend-architect

#### Skill 48 - electron-desktop-builder
- **Source** : Custom SKILL.md
- **Domaine** : DevOps / Desktop
- **Cas d'usage ECHO** : Build et packaging de l'app desktop Cognisphere en Electron + React + TypeScript. Auto-updater avec rollout progressif (10%→50%→100%), canaux Stable/Beta/Canary. PyInstaller pour le backend Python local (LLM, Whisper, LanceDB)
- **Priorite** : P0 Indispensable (pour Cognisphere MVP)
- **Synergies** : ci-cd-pipeline-builder, fsrs5-spaced-repetition-engine

#### Skill 49 - docker-deployment-manager
- **Source** : Custom SKILL.md
- **Domaine** : DevOps / Infra
- **Cas d'usage ECHO** : Containerisation du backend FastAPI + MongoDB. Docker Compose pour l'environnement de dev, deploiement production
- **Priorite** : P1 Important
- **Synergies** : fastapi-backend-architect, ci-cd-pipeline-builder

#### Skill 50 - crdt-sync-engine
- **Source** : Custom SKILL.md
- **Domaine** : DevOps / Data Sync
- **Cas d'usage ECHO** : Implementation du moteur de synchronisation CRDT (Conflict-free Replicated Data Types) pour Cognisphere. Sync bidirectionnelle desktop/mobile, verification d'integrite du graphe post-sync (DFS cycle detection), resolution auto des noeuds orphelins et doublons semantiques
- **Priorite** : P1 Important (Phase 2 Cognisphere)
- **Synergies** : electron-desktop-builder, fsrs5-spaced-repetition-engine

#### Skill 51 - backup-recovery-skill
- **Source** : Custom SKILL.md
- **Domaine** : DevOps / Securite
- **Cas d'usage ECHO** : Strategies de sauvegarde pour la base MongoDB (donnees adherents, projets, progression Cognisphere). Backups automatiques, plan de reprise d'activite
- **Priorite** : P2 Utile
- **Synergies** : docker-deployment-manager, mongodb-schema-designer

#### Skill 52 - monitoring-alerting-skill
- **Source** : Custom SKILL.md
- **Domaine** : DevOps / Monitoring
- **Cas d'usage ECHO** : Supervision des services en production. Alertes en cas de panne du site web, des API, ou des plateformes. Uptime monitoring, logs centralises
- **Priorite** : P2 Utile
- **Synergies** : ci-cd-pipeline-builder, docker-deployment-manager

---

## PARTIE 4 - Workflows Automatises

### Workflow 0 : Cycle de Gouvernance Mensuel (ECHOC)
- **Processus automatise** : Reunion mensuelle du Conseil Oecumenique et suivi des decisions
- **Declencheur** : 3 jours avant la date de reunion mensuelle du ECHOC
- **Etapes** :
  1. Preparation → `governance-circles-manager` → Collecte des remontees de chaque cercle (premier/second liens)
  2. Convocation → `document-generator-asso` → Envoi de l'ordre du jour avec 3 jours de preavis
  3. Reunion → `meeting-notes-ag` → Prise de notes, gestion du processus de consentement, enregistrement des objections
  4. PV → `document-generator-asso` → Generation du PV de reunion du ECHOC, archivage au registre
  5. Diffusion → `governance-circles-manager` → Transmission des decisions aux cercles concernes
  6. Suivi → `governance-circles-manager` → Mise a jour du tableau de suivi des decisions, assignation aux cercles
- **Benefice** : Gouvernance horizontale fluide malgre la complexite du modele sociocratique
- **Prerequis** : ECHOC constitue (phase L'Enracinement, 13 membres minimum)

### Workflow 0b : Preparation et Tenue de l'Assemblee Generale
- **Processus automatise** : Cycle complet de l'AG annuelle obligatoire
- **Declencheur** : 2 mois avant la date d'AG prevue
- **Etapes** :
  1. Convocation → `document-generator-asso` → Envoi convocations avec ordre du jour (15 jours avant minimum)
  2. Rapport moral → `governance-circles-manager` → Compilation du bilan d'activite de chaque cercle
  3. Rapport financier → `financial-tracker-asso` → Generation du bilan, compte de resultat, budget previsionnel N+1
  4. Feuille de presence → `member-registry` → Generation de la feuille de presence, verification quorum
  5. Votes → `meeting-notes-ag` → Gestion des votes (approbation comptes, renouvellement mandats, modifications statuts)
  6. PV → `document-generator-asso` → Redaction du PV d'AG, signature, archivage
  7. Declarations → `prefecture-declarations` → Si modifications (bureau, statuts) : declaration en prefecture + publication JO
  8. Diffusion → `document-generator-asso` → Envoi du PV aux membres absents
- **Benefice** : AG conforme juridiquement, preparee en 1 semaine au lieu de 1 mois
- **Prerequis** : Registre des membres a jour, comptabilite cloturee

### Workflow 0c : Gestion des Cotisations et Recus Fiscaux
- **Processus automatise** : Cycle annuel de collecte des cotisations et emission des recus
- **Declencheur** : Date anniversaire d'adhesion de chaque membre + cycle annuel en janvier
- **Etapes** :
  1. Appel → `member-registry` → Envoi des appels a cotisation avec montant et echeance
  2. Suivi → `financial-tracker-asso` → Enregistrement des paiements recus, lettrage comptable
  3. Relance → `member-registry` → Relance automatique a J+15, J+30, J+45
  4. Recu fiscal → `cerfa-fiscal-receipts` → Generation du Cerfa pour les dons et la part exceeding la cotisation
  5. Radiation → `member-registry` → Si impaye apres 3 relances : proposition de radiation au ECHOC
  6. Bilan → `financial-tracker-asso` → Synthese annuelle des cotisations percues/impayees pour l'AG
- **Benefice** : Zero cotisation oubliee, recus fiscaux conformes envoyes automatiquement
- **Prerequis** : Montant des cotisations defini par l'AG, eligibilite fiscale verifiee

### Workflow 0d : Demande de Subvention
- **Processus automatise** : Constitution et suivi d'un dossier de subvention complet
- **Declencheur** : Identification d'un appel a projets (Emergence IDF 2026, FDVA, etc.)
- **Etapes** :
  1. Eligibilite → `grant-manager` → Analyse des criteres, verification de la compatibilite avec ECHO
  2. Dossier Cerfa → `grant-manager` → Remplissage du Cerfa n°12156*06
  3. Budget action → `financial-tracker-asso` → Budget previsionnel detaille par poste
  4. Pieces jointes → `document-generator-asso` → Statuts, RI, dernier PV AG, dernier bilan, SIRET, RIB
  5. Valorisation benevolat → `volunteer-manager` → Calcul et attestation de la valeur du benevolat
  6. Lettre → `document-generator-asso` → Lettre de sollicitation signee du representant legal
  7. Soumission → `grant-manager` → Depot + ajout au pipeline de suivi
  8. Suivi → `grant-manager` → Relances, reponse, convention, reporting final si accorde
- **Benefice** : Dossier complet et professionnel en 2 jours, suivi sans perte
- **Prerequis** : Comptabilite a jour, AG tenue, SIRET actif

### Workflow 0e : Declaration de Changement en Prefecture
- **Processus automatise** : Modification officielle de l'association (changement de representant legal tous les 18 mois, etc.)
- **Declencheur** : Decision du ECHOC (mandat tournant) ou de l'AG (modification statuts/siege)
- **Etapes** :
  1. Decision → `meeting-notes-ag` → Extraction de la decision du PV (ECHOC ou AG)
  2. Formulaire → `prefecture-declarations` → Remplissage Cerfa n°13971*03 (modification) ou e-modification via le compte asso
  3. Pieces → `document-generator-asso` → PV de decision, nouveaux statuts si besoin, liste des dirigeants
  4. Depot → `prefecture-declarations` → Envoi en prefecture ou via le compte asso en ligne
  5. JO → `prefecture-declarations` → Publication au Journal Officiel si modification des statuts ou du siege
  6. Mise a jour → `member-registry` → Actualisation des informations internes (representant, siege, etc.)
  7. INSEE → `prefecture-declarations` → Verification mise a jour du SIRET si changement de siege
- **Benefice** : Conformite legale assuree malgre les mandats tournants specifiques a ECHO
- **Prerequis** : Acces au compte asso en ligne, PV de decision

### Workflow 1 : Onboarding Nouveau Membre
- **Processus automatise** : Inscription d'un nouvel adherent, de la candidature a l'integration complete
- **Declencheur** : Formulaire d'adhesion soumis sur le site web
- **Etapes** :
  1. Formulaire soumis → `auth-system-builder` → Creation du compte utilisateur
  2. Paiement cotisation → `financial-tracker` → Enregistrement du paiement + generation recu
  3. Verification RGPD → `rgpd-compliance-checker` → Consentements enregistres
  4. Email de bienvenue → `email-template-builder` → Envoi avec lien Discord + reglement interieur
  5. Fiche membre → `member-management-skill` → Ajout au registre des adherents
  6. Onboarding → `onboarding-guide` → Parcours d'integration declenche
- **Benefice** : Un nouveau membre est operationnel en 24h au lieu de plusieurs jours de suivi manuel
- **Prerequis** : Site web avec formulaire d'adhesion, passerelle de paiement, compte email ECHO

### Workflow 2 : Publication d'Episode
- **Processus automatise** : Publication d'un episode de la serie, du master final a la diffusion multi-canal
- **Declencheur** : Validation du montage final par le realisateur
- **Etapes** :
  1. Metadonnees → `content-writer-fr` → Redaction description, synopsis, credits
  2. SEO → `seo-optimizer` → Optimisation titre, tags, structured data
  3. Publication site → `nextjs-app-builder` → Mise a jour de la page episodes
  4. Reseaux sociaux → `social-media-content-creator` → Posts sur tous les comptes (y compris personnages)
  5. Newsletter → `newsletter-architect` → Envoi aux adherents
  6. Enigmes → `enigma-designer` → Activation des enigmes liees a l'episode
  7. Cognisphere → `spaced-repetition-engine` → Ajout des thematiques de l'episode aux playlists d'apprentissage
- **Benefice** : Diffusion coherente et simultanee sur tous les canaux en quelques heures
- **Prerequis** : Comptes reseaux sociaux configures, site web fonctionnel, ECHOLink operationnel

### Workflow 3 : Gestion Mensuelle de l'Association
- **Processus automatise** : Taches administratives recurrentes mensuelles
- **Declencheur** : 1er du mois (automatique)
- **Etapes** :
  1. Comptabilite → `financial-tracker` → Rapprochement des recettes/depenses du mois
  2. Adhesions → `member-management-skill` → Verification des cotisations, relance des retards
  3. Relances → `email-template-builder` → Envoi automatique des relances de cotisation
  4. Reporting → `analytics-dashboard-builder` → Generation du tableau de bord mensuel
  5. Reunion → `meeting-notes-generator` → Preparation de l'ordre du jour de la reunion mensuelle
- **Benefice** : Le representant legal peut piloter l'administratif en 2h/mois au lieu de 2 jours
- **Prerequis** : Base de donnees membres, integration comptable

### Workflow 4 : Creation de Projet Collaboratif ECHOLink
- **Processus automatise** : Soumission, validation et publication d'un projet citoyen sur ECHOLink
- **Declencheur** : Soumission d'un projet par un membre via ECHOLink
- **Etapes** :
  1. Soumission → `fastapi-backend-architect` → Enregistrement en base avec statut "en attente"
  2. Verification → `content-writer-fr` → Relecture automatique de la description
  3. Geolocalisation → `interactive-map-builder` → Placement sur la carte
  4. Validation expert → `team-coordination-skill` → Notification a un partenaire expert pour evaluation
  5. Publication → `nextjs-app-builder` → Affichage sur la carte ECHOLink
  6. Communication → `social-media-content-creator` → Annonce du nouveau projet
- **Benefice** : Un projet soumis peut etre visible en 48h avec validation qualite
- **Prerequis** : Plateforme ECHOLink operationnelle, reseau de partenaires experts

### Workflow 5 : Demande de Subvention / Partenariat
- **Processus automatise** : Constitution d'un dossier de financement complet
- **Declencheur** : Identification d'un appel a projets ou d'un potentiel partenaire
- **Etapes** :
  1. Veille → `content-writer-fr` → Analyse de l'appel a projets et criteres d'eligibilite
  2. Dossier → `document-generator` → Generation du dossier avec : presentation ECHO, budget, impact attendu
  3. Juridique → `association-legal-advisor` → Verification des pieces administratives (SIRET, statuts, RI)
  4. Financier → `financial-tracker` → Extraction des donnees comptables et previsionnel
  5. Relecture → `content-writer-fr` → Relecture et amelioration du dossier
  6. Suivi → `project-tracker` → Ajout au pipeline de suivi des demandes
- **Benefice** : Dossier de subvention complet en 1 jour au lieu d'1 semaine
- **Prerequis** : Documents administratifs a jour, comptabilite tenue

### Workflow 6 : Cycle d'Apprentissage Cognisphere
- **Processus automatise** : Import de contenu jusqu'a la memorisation durable
- **Declencheur** : Import d'un nouveau contenu par un utilisateur (video YouTube, PDF, article)
- **Etapes** :
  1. Import → `file-upload-media-handler` → Extraction et transcription du contenu
  2. Structuration → `cognisphere-learning-engine` (= spaced-repetition-engine) → Identification des concepts cles
  3. Flashcards → generation automatique de fiches question/reponse
  4. Quiz → generation de QCM adaptatifs
  5. Planning → `spaced-repetition-engine` → Calcul du calendrier de revision optimal
  6. Rappels → `email-template-builder` → Notifications push/email de rappel de revision
  7. Visualisation → `analytics-dashboard-builder` → Mise a jour du cerveau de connaissances 3D
- **Benefice** : Apprentissage actif et retention a long terme sans effort de planification
- **Prerequis** : Plateforme Cognisphere developpee, tuteur IA integre

### Workflow 7 : Campagne de Crowdfunding
- **Processus automatise** : Lancement et suivi d'une campagne de financement participatif
- **Declencheur** : Decision de lancer une campagne (ex: financement du tournage S1)
- **Etapes** :
  1. Page campagne → `content-writer-fr` → Redaction du pitch et description des contreparties
  2. Visuels → `design-system-manager` → Creation des visuels de campagne alignes ECHO
  3. Lancement → `social-media-content-creator` → Annonce sur tous les canaux
  4. Suivi → `financial-tracker` → Suivi en temps reel des contributions
  5. Relances → `newsletter-architect` → Emails de relance aux contacts + newsletter progression
  6. Remerciements → `email-template-builder` → Emails de remerciement + recus fiscaux
  7. Bilan → `document-generator` → Rapport de campagne pour les contributeurs
- **Benefice** : Campagne professionnelle geree par une equipe reduite
- **Prerequis** : Compte sur plateforme de crowdfunding, visuels du projet

### Workflow 8 : Veille Strategique & Partenariale
- **Processus automatise** : Identification continue d'opportunites et d'acteurs alignes avec ECHO
- **Declencheur** : Hebdomadaire (chaque lundi)
- **Etapes** :
  1. Veille web → recherche d'appels a projets culturels/educatifs/ESS
  2. Veille partenaires → identification d'associations, ONG, experts alignes avec les thematiques ECHO
  3. Synthese → `content-writer-fr` → Resume des opportunites identifiees
  4. Priorisation → `risk-analyzer` → Evaluation opportunite/effort pour chaque piste
  5. Action → `project-tracker` → Ajout des actions au backlog (contact, candidature, relance)
- **Benefice** : Aucune opportunite de financement ou de partenariat ne passe inapercue
- **Prerequis** : Acces internet, liste de sources de veille configuree

---

## PARTIE 5 - Plan d'Implementation

### Vague 1 : Administration & Fondations (Semaines 1-4)
**Objectif** : Mettre en place la gestion associative et poser les bases techniques

**Bloc A - Administration associative (prioritaire)**

| # | Skill | Justification |
|---|---|---|
| A1 | `governance-circles-manager` | Gestion des cercles et du ECHOC - coeur de la gouvernance ECHO |
| A2 | `member-registry` | Registre des adherents - obligation legale loi 1901 |
| A3 | `financial-tracker-asso` | Comptabilite associative - obligation legale |
| A4 | `cerfa-fiscal-receipts` | Recus fiscaux - indispensable pour les dons et mecenat |
| A5 | `meeting-notes-ag` | PV de reunions et AG - obligation legale |
| A6 | `prefecture-declarations` | Declarations prefecture - obligation legale (mandats tournants) |
| A7 | `association-legal-advisor-asso` | Conseil juridique loi 1901 |
| A9 | `grant-manager` | Dossiers de subvention (Emergence IDF 2026 en cours) |
| A11 | `document-generator-asso` | Generation de tous les documents officiels |
| A12 | `rgpd-compliance-asso` | Conformite RGPD des donnees membres/donateurs |

**Bloc B - Site web (en parallele)**

| # | Skill | Justification |
|---|---|---|
| 1 | `nextjs-app-builder` | Site web ECHO - priorite absolue (deja en retard) |
| 2 | `tailwind-component-designer` | Design system pour le site |
| 3 | `shadcn-ui-integrator` | Composants UI du site |
| 4 | `design-system-manager` | Charte graphique coherente |
| 5 | `content-writer-fr` | Contenu du site web |

**Workflows activables** : Gouvernance ECHOC, AG, Cotisations/Recus, Demande Subvention, Declaration Prefecture, Onboarding (partiel)

**Dependances** : Les skills A1-A3 sont prerequis pour tout le reste de l'administration. Le bloc B peut avancer en parallele du bloc A.

---

### Vague 2 : Production & Partenariats (Semaines 5-12)
**Objectif** : Administration avancee, plateformes fonctionnelles, production de contenu

**Bloc A - Administration avancee**

| # | Skill | Justification |
|---|---|---|
| A8 | `volunteer-manager` | Gestion des benevoles (plannings, valorisation, remboursements) |
| A10 | `partnership-crm` | CRM partenaires de l'ECHOSystem |
| 28 | `intellectual-property-advisor` | Protection des creations (depot marque ECHO) |
| 29 | `contract-template-generator` | Conventions partenariat, cession droits, CGU |

**Bloc B - Backend & Plateformes**

| # | Skill | Justification |
|---|---|---|
| 11 | `fastapi-backend-architect` | Backend des plateformes |
| 12 | `mongodb-schema-designer` | Modelisation des donnees |
| 13 | `api-endpoint-designer` | APIs pour ECHOLink et Cognisphere |
| 22 | `video-player-integrator` | Lecteur video pour les episodes |
| 23 | `interactive-map-builder` | Carte des projets ECHOLink |
| 24 | `file-upload-media-handler` | Import de contenus Cognisphere |
| 25 | `fsrs5-spaced-repetition-engine` | Moteur d'apprentissage Cognisphere |

**Bloc C - Communication & Contenu**

| # | Skill | Justification |
|---|---|---|
| 15 | `social-media-content-creator` | Communication pour la bande-annonce |
| 16 | `transmedia-narrative-planner` | Coherence transmedia |
| 17 | `seo-optimizer` | Referencement du site |
| 18 | `email-template-builder` | Communications automatisees |
| 19 | `newsletter-architect` | Newsletter periodique |
| 20 | `project-tracker` | Suivi de la production S1 |
| 21 | `screenplay-formatter` | Reecriture des scenarios S1 |
| 26 | `dark-theme-architect` | Theme sombre par saison |
| 27 | `accessibility-auditor` | Accessibilite du site |
| 30 | `press-kit-generator` | Dossier de presse bande-annonce |

**Workflows activables** : Publication d'Episode, Campagne Crowdfunding, Cycle Cognisphere, Veille Partenariale

**Dependances** : Skills 11-13 sont la base du backend. Le skill A10 enrichit le workflow de subvention.

---

### Vague 3 : Optimisation (Semaines 13-20)
**Objectif** : Fonctionnalites avancees, automatisation complete, scalabilite

| # | Skill | Justification |
|---|---|---|
| 31 | `enigma-designer` | Enigmes transmedia |
| 32 | `responsive-layout-architect` | Optimisation mobile |
| 33 | `animation-motion-designer` | Animations immersives |
| 34 | `websocket-realtime-handler` | Temps reel pour Focus Camps |
| 35 | `pwa-offline-builder` | Mode offline Cognisphere |
| 36 | `community-moderation-guide` | Moderation communaute |
| 37 | `meeting-notes-generator` | Comptes-rendus reunions |
| 38 | `team-coordination-skill` | Coordination equipe |
| 39 | `onboarding-guide` | Parcours nouveaux benevoles |
| 40 | `analytics-dashboard-builder` | Tableaux de bord KPIs |
| 41 | `document-generator` | Documents officiels |
| 42 | `multilingual-translator` | Traduction FR/EN/Afrique |
| 43 | `press-kit-generator` | (deja en vague 2) |
| 44 | `event-planner` | Evenements ECHO |
| 45 | `storyboard-assistant` | Pre-production episodes |
| 46 | `test-automation-skill` | Tests automatises |
| 47 | `docker-deployment-manager` | Containerisation |
| 48 | `backup-recovery-skill` | Sauvegardes |
| 49 | `monitoring-alerting-skill` | Supervision production |
| 50 | `risk-analyzer` | Gestion des risques |
| 51 | `icon-illustration-curator` | Assets visuels |

**Workflows activables** : Tous les workflows, y compris Veille Strategique et Projet Collaboratif ECHOLink

---

### Resume du plan

```
VAGUE 1 (S1-S4)                    VAGUE 2 (S5-S12)              VAGUE 3 (S13-S20)
Admin Asso + Fondations             Production & Partenariats      Optimisation
10 skills admin + 5 site web        4 admin + 7 backend + 10 comm  20 skills avances
Gouvernance, AG, Compta, RGPD       Benevoles, CRM, PI, Contrats   Scale + DevOps
6 workflows admin                   4 workflows prod               Tous workflows
```

**Total : 12 skills Administration Associative (A1-A12) + 52 skills techniques = 64 skills**

### Contrainte rappellee
**Aucune installation ou suppression ne sera effectuee sans validation explicite de Jeremy.** Ce document est une proposition. L'execution attend votre approbation.
