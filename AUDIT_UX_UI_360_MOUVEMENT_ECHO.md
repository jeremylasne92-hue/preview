# Audit UX/UI 360° — Mouvement ECHO

**Date :** 18 mars 2026
**Auditeur :** Lead UX/UI Auditor (Claude Code)
**Périmètre :** Repository `preview` — Site vitrine + Plateforme de streaming Mouvement ECHO
**Stack déclarée :** React + Tailwind CSS + Shadcn UI (frontend), FastAPI + MongoDB (backend)

---

## Constat préliminaire critique

> **Le repository ne contient actuellement aucun code applicatif.**

L'historique Git révèle :
1. `bbb6a77` — Scaffolding initial Next.js 16 via `create-next-app`
2. `dc32208` — Upload des documents associatifs (`.docx`, `.pdf`)
3. `8508b9b` → `66e4a17` — **Suppression systématique de tout le code** (app/, public/, package.json, configs)

**État actuel du repo :** 12 fichiers documentaires uniquement (Constitution, PRD Cognisphère, dossiers de candidature, comptabilité, SIRET, règlement intérieur).

**Conséquence :** Les fonctionnalités décrites en Phase 2 (authentification, grille d'épisodes, lecteur vidéo, routing protégé) **n'existent pas dans ce repository**. L'audit ne peut donc pas évaluer du code existant.

**Pivot stratégique :** Cet audit devient un **cahier de prescriptions architecturales** — un référentiel normatif complet pour construire le site correctement dès la première itération, en évitant la dette technique. Chaque recommandation est directement exploitable comme spécification.

---

## Partie 1 — Scorecard Radar

| # | Dimension | Score | Commentaire |
|---|-----------|-------|-------------|
| 1 | Design System & Cohérence visuelle | **0/10** | Aucun design system, aucun composant, aucune charte implémentée. Tout est à construire. |
| 2 | Parcours utilisateur (User Flows) | **0/10** | Aucune page, aucune route, aucun parcours existant. |
| 3 | Accessibilité (WCAG 2.2 AA) | **0/10** | Aucun markup sémantique, aucun attribut ARIA, aucune gestion du focus. |
| 4 | Responsive & Multi-device | **0/10** | Aucun layout implémenté. |
| 5 | Performance & Core Web Vitals | **1/10** | Le scaffolding Next.js 16 offrait SSR/code-splitting natif, mais le code a été supprimé. Le choix de Next.js reste pertinent. |
| 6 | SEO technique | **0/10** | Metadata par défaut ("Create Next App") dans le code supprimé. Aucun sitemap, robots.txt, Open Graph. |
| 7 | Sécurité frontend | **0/10** | Aucune implémentation d'auth, token, headers, CSP, validation. |

**Score global : 0,14 / 10** — Le projet est au stade de documentation, pas de développement.

> **Note importante :** Ces scores de 0 ne sont pas un jugement négatif sur le projet. Ils reflètent simplement l'absence de code. La documentation associative (Constitution, PRD Cognisphère, dossiers) témoigne d'une vision très structurée. L'enjeu est maintenant de traduire cette richesse en implémentation.

---

## Partie 2 — Parcours utilisateurs (Prescriptions)

Aucun parcours n'étant implémenté, voici les **flows cibles** à construire, avec les points de friction anticipés basés sur l'analyse des documents du projet et les standards du secteur streaming.

### Flow 1 : Découverte → Première visite

```
Landing Page (Hero)
    → 🟢 Vidéo teaser auto-play (muet) + CTA "Découvrir la série"
    → 🟢 Scroll : Présentation ECHO (Mission, Raison d'être — cf. doc "Présentation Mouvement site web")
    → 🟢 Section "La Websérie" avec aperçu Saison 1
    → 🟡 FRICTION ANTICIPÉE : Sans onboarding clair, le visiteur ne comprend pas
         s'il est sur un site associatif ou une plateforme de streaming
    → 🔴 RISQUE : Absence de hiérarchie visuelle entre contenu associatif et contenu série
    → Page Épisodes (grille)
```

**Prescription :** La landing page doit immédiatement clarifier la double nature du site (association + streaming) via un hero segmenté ou un parcours bifurqué ("Découvrir le mouvement" / "Regarder la série").

### Flow 2 : Inscription → Connexion

```
CTA "S'inscrire" (Header ou page épisode verrouillé)
    → 🟢 Formulaire inscription (email + mot de passe)
    → 🟡 FRICTION : Obligation d'inscription pour voir un épisode = barrière forte
         pour un public 25-55 ans à littératie numérique variée
    → 🟢 Email de confirmation
    → 🟢 Connexion
    → 🟢 Redirection vers le contenu demandé initialement
    → 🔴 RISQUE : Si pas de redirect post-login, l'utilisateur perd le contexte
```

**Prescription :**
- Permettre le visionnage du S01E01 sans inscription (hook d'engagement)
- Implémenter un redirect post-auth vers la page d'origine (`returnUrl`)
- Proposer une inscription simplifiée (email seul + magic link) en plus du classique

### Flow 3 : Navigation → Visionnage d'un épisode

```
Page d'accueil ou Menu
    → 🟢 Navigation vers "Épisodes"
    → 🟢 Grille avec vignettes, numéro d'épisode, titre, durée
    → 🟢 Clic sur un épisode
    → Page Épisode détail
        → 🟢 Lecteur vidéo
        → 🟡 FRICTION : Pas de bouton "Épisode suivant" automatique
        → 🟡 FRICTION : Pas d'indicateur de progression dans la saison
        → 🔴 RISQUE : Lecture vidéo sans contrôles accessibles (sous-titres, vitesse)
    → 🟢 Retour à la grille
```

**Prescription :**
- Auto-next avec countdown de 10s en fin d'épisode
- Progress bar par saison visible sur la grille
- Contrôles vidéo : sous-titres (FR obligatoire), vitesse, plein écran, PiP

### Flow 4 : Engagement associatif (post-visionnage)

```
Fin d'un épisode
    → 🟢 CTA contextuel lié à la thématique de l'épisode (cf. "ECHOLink")
    → 🟡 FRICTION : Transition abrupte fiction → engagement réel
    → Page "Agir" / ECHOLink
        → 🟢 Liste d'initiatives locales
        → 🔴 RISQUE : Si pas de géolocalisation, les initiatives semblent abstraites
    → 🟢 Retour à la série
```

**Prescription :** Créer une transition narrative douce entre l'épisode et le CTA d'engagement (ex: écran interstitiel avec citation du personnage + lien vers l'initiative réelle).

### Flow 5 : Pages institutionnelles

```
Menu → "À propos"
    → 🟢 Page structurée (La Graine, Germination, Enracinement, Émergence, etc.)
    → 🟡 FRICTION : Texte dense sans illustrations ni interactivité

Menu → "Contact"
    → 🟢 Formulaire de contact
    → 🔴 RISQUE : Pas de confirmation visuelle d'envoi
```

---

## Partie 3 — Constats détaillés par dimension

### 3.1 Design System & Cohérence visuelle

| # | Élément | Constat | Sévérité | Détail | Recommandation |
|---|---------|---------|----------|--------|----------------|
| 1 | Charte graphique | Aucun fichier de design tokens (couleurs, typographies, espacements) n'existe dans le repo | **Critique** | Le fichier `globals.css` supprimé ne contenait que les défauts Next.js (`--background: #ffffff`, `--foreground: #171717`) sans aucune couleur ECHO | Créer un fichier `tokens.ts` ou configurer `tailwind.config.ts` avec la palette ECHO (couleurs primaires/secondaires/accent dérivées de la charte graphique de l'association) |
| 2 | Shadcn UI | Déclaré dans la stack mais **jamais installé ni configuré** | **Critique** | Aucun dossier `components/ui/`, aucun `components.json`, aucune dépendance `@radix-ui/*` dans `package.json` | Initialiser Shadcn UI (`npx shadcn-ui@latest init`), configurer le thème ECHO, installer les composants nécessaires (Button, Card, Dialog, Input, Navigation, etc.) |
| 3 | Typographies | Seules Geist Sans/Mono (polices Next.js par défaut) étaient configurées | **Important** | Aucune police en lien avec l'identité ECHO. La websérie inspirée de Dante nécessite une typographie à forte personnalité | Choisir 2 polices : une display/titre (évoquant le narratif/littéraire) + une body lisible. Les déclarer via `next/font` pour le self-hosting optimal |
| 4 | Iconographie | Seuls les SVG par défaut Next.js (next.svg, vercel.svg, globe.svg) existaient dans `/public` | **Important** | Aucun système d'icônes cohérent | Adopter Lucide React (compatible Shadcn UI) + créer les icônes custom ECHO si nécessaire |
| 5 | Espacements | Aucune grille ni système de spacing défini | **Important** | Le code supprimé utilisait des valeurs ad hoc (py-32, px-16, gap-8) sans logique cohérente | Définir une échelle de spacing dans Tailwind config (4, 8, 12, 16, 24, 32, 48, 64, 96) et documenter les usages |

### 3.2 Parcours utilisateur

| # | Élément | Constat | Sévérité | Détail | Recommandation |
|---|---------|---------|----------|--------|----------------|
| 1 | Routing | Aucune route définie au-delà de `/` | **Critique** | L'App Router Next.js était en place mais avec une seule page | Implémenter l'arborescence : `/`, `/episodes`, `/episodes/[id]`, `/a-propos`, `/contact`, `/auth/login`, `/auth/register`, `/echolink` |
| 2 | Navigation | Aucun composant Header/Navbar | **Critique** | Pas de menu, pas de navigation | Créer un Header responsive avec : Logo ECHO, liens (Accueil, La Série, Épisodes, ECHOLink, À propos, Contact), bouton Auth |
| 3 | Footer | Inexistant | **Important** | Aucun footer avec mentions légales, liens sociaux, contact | Créer un Footer avec : liens légaux (CGU, Politique de confidentialité), réseaux sociaux, newsletter, copyright |
| 4 | Pages statiques | Le contenu existe dans les docs mais pas dans le site | **Important** | "Présentation Mouvement site web.pdf" contient un texte riche (La Graine, Germination, Enracinement...) jamais implémenté | Transposer le contenu du PDF en pages React structurées avec la métaphore de l'arbre comme fil narratif |

### 3.3 Accessibilité (WCAG 2.2 AA)

| # | Élément | Constat | Sévérité | Détail | Recommandation |
|---|---------|---------|----------|--------|----------------|
| 1 | Langue | `<html lang="en">` dans le layout supprimé — or le site est francophone | **Critique** | Mauvaise langue déclarée = lecteur d'écran avec prononciation incorrecte | Configurer `<html lang="fr">` dans `app/layout.tsx` |
| 2 | Skip navigation | Absent | **Critique** | Utilisateurs clavier ne peuvent pas sauter le menu | Ajouter un lien "Aller au contenu principal" en premier enfant du `<body>`, visible au focus (`sr-only focus:not-sr-only`) |
| 3 | Hiérarchie headings | Un seul `<h1>` placeholder ("Ready for your first task") | **Critique** | Aucune structure sémantique | Chaque page doit avoir exactement un `<h1>`, puis `<h2>` → `<h3>` sans saut de niveau. Documenter la convention |
| 4 | Contraste | Les CSS variables supprimées (#171717 sur #ffffff = ratio 12.6:1) étaient conformes AAA | **Mineur** | Bon point de départ, mais non testé avec les couleurs ECHO réelles | Valider chaque combinaison de couleurs ECHO avec un outil de contraste (minimum 4.5:1 pour texte, 3:1 pour grands textes) |
| 5 | Lecteur vidéo | Inexistant | **Critique** | Le lecteur vidéo est le coeur de la plateforme et doit être pleinement accessible | Utiliser un lecteur accessible (Vidstack, Plyr) avec : sous-titres, audio-description, contrôles clavier, ARIA live regions pour les changements d'état |
| 6 | Formulaires | Inexistants | **Important** | Aucun formulaire d'auth ou de contact | Tous les inputs doivent avoir un `<label>` associé, des messages d'erreur liés via `aria-describedby`, et un focus visible |

### 3.4 Responsive & Multi-device

| # | Élément | Constat | Sévérité | Détail | Recommandation |
|---|---------|---------|----------|--------|----------------|
| 1 | Breakpoints | Aucun breakpoint custom défini | **Critique** | Tailwind fournit des défauts (sm:640, md:768, lg:1024, xl:1280, 2xl:1536) mais aucune adaptation n'est codée | Adopter une approche mobile-first. Définir les breakpoints cibles : 375px (mobile), 768px (tablette), 1440px (desktop) |
| 2 | Grille épisodes | Inexistante | **Critique** | La grille de 33 épisodes (3 saisons) est le composant le plus critique pour le responsive | Implémenter avec CSS Grid : 1 colonne (mobile), 2 colonnes (tablette), 3-4 colonnes (desktop). Cards avec aspect-ratio 16/9 pour les vignettes |
| 3 | Lecteur vidéo | Inexistant | **Important** | Le lecteur doit fonctionner sur tous les devices | Utiliser un lecteur responsive natif (width: 100%, aspect-ratio: 16/9). Tester les contrôles tactiles (zones de tap >= 44x44px) |
| 4 | Navigation mobile | Inexistante | **Important** | Pas de menu hamburger ou drawer | Implémenter un Sheet/Drawer Shadcn UI pour la navigation mobile avec animation fluide |
| 5 | Typographie fluide | Non implémentée | **Mineur** | Les tailles de texte fixes ne s'adaptent pas | Utiliser `clamp()` pour la typographie fluide : `font-size: clamp(1rem, 2.5vw, 1.5rem)` ou les utilitaires Tailwind fluid |

### 3.5 Performance & Core Web Vitals

| # | Élément | Constat | Sévérité | Détail | Recommandation |
|---|---------|---------|----------|--------|----------------|
| 1 | Framework | Next.js 16 était configuré = bon choix pour SSR/SSG | **Info** | Next.js fournit code splitting, image optimization, font optimization nativement | Réinstaller Next.js et exploiter `next/image`, `next/font`, `next/script` systématiquement |
| 2 | Images/Vignettes | 33 épisodes × vignettes = risque LCP élevé sans optimisation | **Critique** | Aucune stratégie d'optimisation d'images | Utiliser `next/image` avec : format WebP/AVIF automatique, lazy loading (sauf above-the-fold), `sizes` et `srcset` adaptés, placeholder blur |
| 3 | Vidéos | Streaming de 33 épisodes = charge potentiellement énorme | **Critique** | Aucune stratégie de chargement vidéo | Utiliser HLS/DASH pour le streaming adaptatif. Ne jamais charger la vidéo entière en mémoire. Précharger uniquement le poster + premiers segments |
| 4 | Fonts | Geist était la seule police (bien optimisée via next/font) | **Important** | Si des polices custom ECHO sont ajoutées, elles doivent être self-hosted | Utiliser `next/font/local` pour les polices custom. Définir `font-display: swap`. Subsetter les polices aux caractères français |
| 5 | Bundle size | Le code supprimé était minimal (React + Next.js seulement) | **Important** | L'ajout de Shadcn UI, lecteur vidéo, auth va alourdir le bundle | Configurer le tree-shaking. Importer Shadcn UI composant par composant. Utiliser `next/dynamic` pour le lazy loading du lecteur vidéo |
| 6 | Core Web Vitals estimés | Impossible à mesurer (pas de code) | **Critique** | LCP, INP, CLS non mesurables | Objectifs cibles : LCP < 2.5s, INP < 200ms, CLS < 0.1. Monitorer avec `web-vitals` + Next.js Analytics |

### 3.6 SEO technique

| # | Élément | Constat | Sévérité | Détail | Recommandation |
|---|---------|---------|----------|--------|----------------|
| 1 | Metadata | `title: "Create Next App"`, `description: "Generated by create next app"` — placeholder non modifié | **Critique** | Aucune balise SEO exploitable | Configurer la Metadata API Next.js avec : titre dynamique par page, description unique (max 160 car.), keywords pertinentes |
| 2 | Open Graph | Absent | **Critique** | Le partage social est crucial pour une websérie virale | Ajouter `openGraph` dans chaque page : `og:title`, `og:description`, `og:image` (vignette épisode), `og:type: video.episode` pour les épisodes |
| 3 | Sitemap | Absent | **Important** | Google ne peut pas indexer correctement le site | Utiliser `next-sitemap` ou la génération native Next.js (`app/sitemap.ts`) pour générer automatiquement le sitemap avec toutes les pages et épisodes |
| 4 | robots.txt | Absent | **Important** | Aucune directive pour les crawlers | Créer `app/robots.ts` ou `public/robots.txt` : autoriser le crawl général, bloquer `/auth/*`, `/api/*` |
| 5 | Données structurées | Absentes | **Important** | Les épisodes sont un cas d'usage parfait pour Schema.org | Implémenter JSON-LD pour : `Organization` (ECHO), `TVSeries`, `TVSeason`, `TVEpisode` avec `VideoObject`. Cela active les rich snippets Google |
| 6 | URLs | Aucune route définie | **Important** | Structure URL non planifiée | Convention : `/episodes/saison-1/episode-1-titre-slug` — URLs lisibles, hiérarchiques, en français |

### 3.7 Sécurité frontend

| # | Élément | Constat | Sévérité | Détail | Recommandation |
|---|---------|---------|----------|--------|----------------|
| 1 | Authentification | Inexistante | **Critique** | Aucun système d'auth implémenté | Utiliser NextAuth.js v5 (Auth.js) avec session côté serveur. Stocker les tokens en cookies `httpOnly` + `Secure` + `SameSite=Strict`. **Ne jamais stocker de JWT dans localStorage** |
| 2 | Headers de sécurité | Non configurés | **Critique** | Aucun header CSP, HSTS, X-Frame-Options | Configurer dans `next.config.ts` les headers : `Content-Security-Policy`, `Strict-Transport-Security`, `X-Content-Type-Options: nosniff`, `X-Frame-Options: DENY`, `Referrer-Policy: strict-origin-when-cross-origin` |
| 3 | Variables d'environnement | Aucun `.env` | **Critique** | Les clés API, URL backend, secrets doivent être protégés | Créer `.env.local` (gitignored). Préfixer `NEXT_PUBLIC_` uniquement pour les variables côté client non sensibles. Valider la présence des variables au build |
| 4 | Protection XSS | Non implémentée | **Important** | React échappe par défaut le JSX, mais `dangerouslySetInnerHTML` est un risque | Ne jamais utiliser `dangerouslySetInnerHTML` sans sanitization (DOMPurify). Valider les inputs côté serveur avec Zod |
| 5 | CSRF | Non implémenté | **Important** | Les formulaires POST sont vulnérables sans token CSRF | NextAuth.js inclut une protection CSRF native. Pour les API custom, utiliser le pattern `SameSite cookie` + `Origin header validation` |
| 6 | Rate limiting | Non implémenté | **Important** | Les endpoints d'auth sont vulnérables au brute force | Implémenter un rate limiter côté API (FastAPI) : 5 tentatives/min pour login, 3 tentatives/heure pour register |

---

## Partie 4 — Plan d'action priorisé

### P0 — Bloquants (à faire immédiatement)

| # | Action | Dimension | Effort | Fichier(s) |
|---|--------|-----------|--------|------------|
| 1 | Réinstaller Next.js 16 + TypeScript + Tailwind CSS 4 | Tous | Quick Win | `package.json`, configs |
| 2 | Initialiser Shadcn UI avec thème ECHO | Design System | Quick Win | `components.json`, `tailwind.config.ts`, `globals.css` |
| 3 | Créer le Design System : tokens couleurs, typographie, espacements | Design System | Moyen | `tailwind.config.ts`, `tokens.ts` |
| 4 | Implémenter le layout principal : Header, Footer, navigation | Parcours UX | Moyen | `app/layout.tsx`, `components/Header.tsx`, `components/Footer.tsx` |
| 5 | Créer l'arborescence des pages (routes App Router) | Parcours UX | Moyen | `app/*/page.tsx` |
| 6 | Configurer `<html lang="fr">` | Accessibilité | Quick Win | `app/layout.tsx` |
| 7 | Configurer les headers de sécurité | Sécurité | Quick Win | `next.config.ts` |

### P1 — Importants (Phase 3 prioritaire)

| # | Action | Dimension | Effort | Fichier(s) |
|---|--------|-----------|--------|------------|
| 8 | Implémenter l'authentification (NextAuth.js v5) | Sécurité, Parcours UX | Chantier | `app/api/auth/`, `middleware.ts` |
| 9 | Créer la grille d'épisodes responsive | Responsive, Parcours UX | Moyen | `app/episodes/page.tsx`, `components/EpisodeCard.tsx` |
| 10 | Intégrer le lecteur vidéo accessible | Accessibilité, Performance | Chantier | `app/episodes/[id]/page.tsx`, `components/VideoPlayer.tsx` |
| 11 | Configurer la Metadata API + Open Graph par page | SEO | Moyen | Chaque `page.tsx`, `app/layout.tsx` |
| 12 | Implémenter les données structurées JSON-LD | SEO | Moyen | `components/JsonLd.tsx`, pages épisodes |
| 13 | Créer le sitemap dynamique + robots.txt | SEO | Quick Win | `app/sitemap.ts`, `app/robots.ts` |
| 14 | Ajouter skip navigation + focus visible | Accessibilité | Quick Win | `app/layout.tsx`, `globals.css` |
| 15 | Optimiser les images avec `next/image` | Performance | Moyen | Tous les composants avec images |

### P2 — Améliorations (Phase 3 secondaire)

| # | Action | Dimension | Effort | Fichier(s) |
|---|--------|-----------|--------|------------|
| 16 | Implémenter l'auto-next entre épisodes | Parcours UX | Moyen | `components/VideoPlayer.tsx` |
| 17 | Créer les pages institutionnelles (À propos avec métaphore de l'arbre) | Parcours UX, SEO | Moyen | `app/a-propos/page.tsx` |
| 18 | Intégrer ECHOLink (CTA post-épisode) | Parcours UX | Chantier | `app/echolink/page.tsx`, `components/EngagementCTA.tsx` |
| 19 | Configurer le monitoring Core Web Vitals | Performance | Quick Win | `app/layout.tsx`, instrumentation |
| 20 | Implémenter le streaming adaptatif (HLS) | Performance | Chantier | Backend + `components/VideoPlayer.tsx` |
| 21 | Typo fluide avec `clamp()` | Responsive | Quick Win | `globals.css` |
| 22 | Rate limiting sur les endpoints auth | Sécurité | Moyen | Backend FastAPI |

---

## Partie 5 — Quick Wins (Top 10, < 1h chacun)

Ces actions ont le meilleur ratio impact/effort et sont réalisables immédiatement.

| # | Action | Impact | Temps estimé |
|---|--------|--------|--------------|
| 1 | **`<html lang="fr">`** — Corriger la langue du document | Accessibilité, SEO | 1 min |
| 2 | **Réinstaller le framework** — `npx create-next-app@latest . --typescript --tailwind --eslint --app --src-dir` | Tous | 5 min |
| 3 | **Initialiser Shadcn UI** — `npx shadcn-ui@latest init` + configurer le thème | Design System | 15 min |
| 4 | **Headers de sécurité** — Ajouter CSP, HSTS, X-Frame-Options dans `next.config.ts` | Sécurité | 15 min |
| 5 | **Metadata de base** — Titre, description, Open Graph dans `app/layout.tsx` | SEO | 15 min |
| 6 | **robots.txt + sitemap** — Créer `app/robots.ts` et `app/sitemap.ts` | SEO | 15 min |
| 7 | **Skip navigation** — Lien "Aller au contenu" + styles focus | Accessibilité | 15 min |
| 8 | **Palette de couleurs ECHO** — Configurer les tokens dans `tailwind.config.ts` | Design System | 30 min |
| 9 | **Structure de routing** — Créer les dossiers `app/episodes/`, `app/a-propos/`, `app/contact/`, `app/auth/` avec pages placeholder | Parcours UX | 30 min |
| 10 | **`.env.local` + `.gitignore`** — Créer le fichier d'environnement et s'assurer qu'il est ignoré par Git | Sécurité | 5 min |

**Temps total estimé : ~2h30 pour poser des fondations solides.**

---

## Partie 6 — Recommandations stratégiques pour la Phase 3

### Recommandation 1 : Construire un Design System ECHO avant de coder les pages

**Justification :** Le projet a une identité narrative forte (métaphore de l'arbre, inspiration dantesque, transmedia). Sans design system formalisé, chaque développeur (humain ou IA) interprétera différemment les intentions visuelles, créant une dette de cohérence impossible à rattraper.

**Actions concrètes :**
- Définir les design tokens dans `tailwind.config.ts` : palette primaire (verts/terres pour la nature ?), secondaire, accent, neutres, sémantiques (success/warning/error)
- Documenter les composants Shadcn UI customisés dans un Storybook ou une page `/design-system`
- Créer les variantes : boutons (CTA primaire, secondaire, ghost), cards (épisode, initiative, info), typographie (display, heading, body, caption)
- **Fichiers à créer :** `tailwind.config.ts`, `lib/design-tokens.ts`, `components/ui/` (via Shadcn)

### Recommandation 2 : Adopter une architecture "Feature-based" avec Server Components

**Justification :** Next.js 16 avec App Router encourage les React Server Components (RSC). Avec 33 épisodes, des données dynamiques (progression, favoris) et du contenu statique (pages institutionnelles), la stratégie de rendu est critique pour la performance.

**Actions concrètes :**
- Pages institutionnelles (À propos, Contact) → Server Components statiques (SSG)
- Grille d'épisodes → Server Component avec revalidation (ISR, `revalidate: 3600`)
- Lecteur vidéo → Client Component isolé (`"use client"`) lazy-loaded
- Auth → Server Actions + middleware Next.js pour la protection des routes
- **Structure recommandée :**
  ```
  app/
  ├── (marketing)/          # Groupe : pages statiques
  │   ├── a-propos/
  │   ├── contact/
  │   └── echolink/
  ├── (streaming)/           # Groupe : plateforme vidéo
  │   ├── episodes/
  │   │   ├── page.tsx       # Grille (Server Component)
  │   │   └── [slug]/
  │   │       └── page.tsx   # Page épisode (Server + Client hybrid)
  │   └── layout.tsx         # Layout streaming avec sidebar saison
  ├── auth/
  │   ├── login/
  │   └── register/
  └── layout.tsx             # Layout racine
  ```

### Recommandation 3 : Stratégie de test progressive

**Justification :** Le projet est développé via Claude Code, ce qui accélère la production mais rend les tests encore plus critiques — le code généré doit être validé systématiquement.

**Actions concrètes :**
- **Unitaires (Vitest)** : Tester les utils, les hooks custom, les fonctions de formatage
- **Composants (Testing Library)** : Tester les interactions clés (formulaire auth, navigation épisodes, contrôles vidéo)
- **E2E (Playwright)** : Tester les 5 parcours utilisateur décrits en Partie 2
- **Accessibilité (axe-core + Playwright)** : Scanner automatiquement chaque page pour les violations WCAG
- **Visuels (Chromatic ou Percy)** : Détecter les régressions visuelles sur les 3 breakpoints
- **Budget :** Commencer par Vitest + Testing Library (P1), ajouter Playwright en P2

### Recommandation 4 : Monitoring performance continu

**Justification :** Une plateforme de streaming a des exigences de performance supérieures à un site vitrine classique. Le LCP (chargement du lecteur vidéo ou de la première vignette) est le métrique le plus critique.

**Actions concrètes :**
- Intégrer `web-vitals` dans `app/layout.tsx` pour le reporting côté client
- Configurer Vercel Analytics ou SpeedCurve pour le monitoring continu
- Définir des budgets de performance : bundle JS < 200KB gzipped, LCP < 2.5s, INP < 200ms
- Tester systématiquement sur connexion 3G throttled (simuler le public à littératie numérique variée)

### Recommandation 5 : Internationalisation préparée dès le départ

**Justification :** Bien que le public soit "majoritairement francophone", le document "Candidature Émergence IDF 2026" et l'ambition transmedia suggèrent une expansion future. Préparer l'i18n dès maintenant coûte presque rien, le retrofit coûte très cher.

**Actions concrètes :**
- Utiliser `next-intl` ou le support i18n natif de Next.js
- Externaliser tous les textes dans des fichiers JSON (`messages/fr.json`)
- Ne pas hardcoder les textes dans les composants
- Préparer la structure de routing : `app/[locale]/` (même si seul `fr` est actif au lancement)

---

## Annexe — Documents analysés dans le repository

| Fichier | Contenu pertinent pour l'audit |
|---------|-------------------------------|
| `Présentation Mouvement site web.pdf` | Texte fondateur (La Graine → La Fructification) — à transposer en pages web |
| `PRD COGNISPHERE_v1.3.docx` | PRD de la plateforme Cognisphère (non lisible en binaire, à consulter manuellement) |
| `Description ECHOLink.docx` | Description du système ECHOLink (non lisible en binaire, à consulter manuellement) |
| `Constitution_ECHO_v1.docx` | Constitution de l'association |
| `Candidature Émergence IDF 2026 - Cognisphère.docx` | Dossier de candidature — confirme l'ambition de scaling |
| `Règlement Intérieur - Mouvement ECHO - Officiel.pdf` | Règlement interne |

---

## Conclusion

**L'état actuel du repository est un point zéro.** Il n'y a pas de code à auditer, mais il y a une vision associative remarquablement structurée dans les documents. Le défi de la Phase 3 n'est pas technique — Next.js 16 + Shadcn UI + FastAPI est une stack solide — le défi est de **traduire fidèlement l'univers narratif ECHO en expérience numérique** tout en respectant les standards d'accessibilité, de performance et de sécurité.

Les 10 Quick Wins (~2h30 de travail) posent les fondations. Les 5 recommandations stratégiques structurent le développement. Le plan d'action priorisé (22 actions) constitue la feuille de route complète de la Phase 3.

**Prochaine étape recommandée :** Exécuter les Quick Wins 1 à 3 (réinstaller le framework, initialiser Shadcn UI, configurer la langue et les tokens) pour disposer d'une base de code fonctionnelle sur laquelle itérer.
