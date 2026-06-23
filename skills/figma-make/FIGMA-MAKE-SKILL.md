# Skill Figma · Make

## Titre
Figma Make — Skill d'automatisation pour Figma

## Bref résumé
Cette skill facilite l'automatisation de tâches Figma depuis Make (Integromat) :
- extraction de frames
- export d'images
- création et mise à jour de composants
- mise à jour de texte
- déclenchement de workflows via webhooks

---

## Table des matières
1. Manifest (exemple YAML)
2. Installation
3. Utilisation (exemples)
4. Erreurs courantes & dépannage
5. Bonnes pratiques
6. Contribution
7. Licence
8. Design Lab — Configuration (guide complet)

---

## 1. Manifest (exemple YAML)
```yaml
name: figma-make-skill
id: com.votreorg.figma_make_skill
version: 0.1.0
author: Votre Nom <votre@exemple.com>
description: >-
  Intégration Make pour automatiser opérations Figma : extraction/export,
  création/mise à jour de composants et hooks d'événements.
platforms:
  - make
auth:
  type: oauth2
  authorizationUrl: https://www.figma.com/oauth
  tokenUrl: https://www.figma.com/api/oauth/token
  scopes:
    - file_read
    - file_write
    - images:read
    - teams:read
triggers:
  - id: file_updated
    title: On File Updated
    description: Déclenché lorsqu'un fichier Figma est modifié (via webhook).
actions:
  - id: export_frame
    title: Export Frame
    description: Exporte une frame en PNG/JPEG/SVG
    inputs:
      - name: file_key
        type: string
        required: true
      - name: node_id
        type: string
        required: true
      - name: format
        type: string
        enum: [png, jpg, svg]
        default: png
    outputs:
      - name: image_url
        type: string
  - id: create_component
    title: Create Component
    description: Crée un composant basé sur une sélection
    inputs:
      - name: file_key
        type: string
        required: true
      - name: selection_node_ids
        type: array
        items: string
    outputs:
      - name: component_id
        type: string
webhooks:
  - id: webhook_file_events
    description: Webhook pour événements de fichier
rate_limits:
  calls_per_minute: 60
endpoints:
  base: https://api.figma.com/v1
  examples:
    export_image: /images/:file_key?ids=:node_id&format=:format
permissions:
  - read:files
  - write:files
```

---

## 2. Installation
1. Créez une application OAuth dans Figma et récupérez client_id / client_secret.
2. Configurez la connexion OAuth dans Make (ou votre plateforme Make-compatible) en utilisant les URLs indiquées.
3. Enregistrez les webhooks (endpoint public) pour recevoir les événements file_updated.

---

## 3. Utilisation (exemples)
- Exporter une frame en PNG
  - Action: Export Frame
  - Inputs: file_key, node_id, format=png
  - Résultat: image_url utilisable dans Make

- Créer un composant automatiquement à partir d'une sélection
  - Action: Create Component
  - Inputs: file_key, selection_node_ids
  - Résultat: component_id

---

## 4. Erreurs courantes & dépannage
- 401 Unauthorized : vérifier token OAuth et scopes.
- 429 Rate limit : appliquer backoff et limiter fréquence des appels.
- Node not found : s'assurer que node_id est correct et appartient au file_key fourni.

---

## 5. Bonnes pratiques
- Réutiliser les webhooks pour éviter le polling intensif.
- Mettre en cache les métadonnées de fichiers (versions, nodes) quand possible.
- Prévoir des retries exponentiels pour appels réseau.

---

## 6. Contribution
- Forkez le dépôt, créez une branche feature/xxx, ouvrez une PR.
- Tests: inclure fixtures Figma (IDs factices) et mocks pour l'API.

---

## 7. Licence
MIT

---

# Design Lab — Configuration de la Skill Figma Make

Ce guide décrit le flux complet pour lancer un "Design Lab" dans Figma via la skill.
Il contient : règles de critique, phases du processus (0 à 8), script d'entretien, et format du plan d'implémentation.

### Objectif
- Conduire un entretien de design
- Générer 5 variations UI temporaires dans Figma
- Collecter des retours et produire un plan d'implémentation

---

## Règles essentielles (CRITIQUE)
0. Inference du brief
- Lire le brief et les éléments liés avant toute génération.
- Analyser : type de page (landing, portfolio, redesign...), mots-clés stylistiques, audience, assets existants, contraintes spécifiques.

0.B Design Read (obligatoire)
- Avant tout rendu, afficher une ligne :
  "Reading this as: <page kind> for <audience>, with a <vibe> language, leaning toward <design system or aesthetic family>."

0.C Clarification
- Si le brief est ambigu, poser exactement une question de clarification.

0.D Discipline anti-default
- Éviter les choix par défaut trop génériques (ex : dégradés violet/indigo IA, hero centrée sombre, glassmorphism générique, Inter + slate-900).

---

## 1. Les trois cadrans (configuration)
Après le Design Read, définir :
- DESIGN_VARIANCE: 1-10 (défaut 8)
- MOTION_INTENSITY: 1-10 (défaut 6)
- VISUAL_DENSITY: 1-10 (défaut 4)

Ces valeurs dictent mise en page, mouvement et densité visuelle.

---

## 2. Cartographie Brief → Design System
- Choisir un seul système (Glassmorphism, Bento, Brutalism, Editorial, Dark Tech, Aurora).
- Construire l'esthétique via les variables & styles Figma (couleurs, typographie, rayons, effets).

Descriptions rapides :
- Glassmorphism : surfaces semi-transparentes, backdrop blur, bordures 1px, ombres douces.
- Bento Grid : grille modulée en rectangles/carrés, cellules de tailles variées.
- Brutalism : contours épais (2-4px), aplats saturés, typographie imposante.
- Editorial : grands espaces blancs, grille asymétrique, contraste typographique.
- Dark Tech : thèmes sombres, bordures subtiles, micro-accents lumineux.
- Aurora : grands dégradés organiques et flous en arrière-plan.

---

## 3. Architecture par défaut & conventions
- Breakpoints: sm 640, md 768, lg 1024, xl 1280, 2xl 1536.
- Max width: 1400px.
- Viewport stability: min-h: 100dvh.
- Préférer une structure Grid (émulation CSS Grid en auto-layout).

---

## 4. Directives de design engineering (règles clés)
- Typography: sans-serif pour titres par défaut (Geist, Satoshi, Outfit). Serifs déconseillées sauf cas luxe/édition.
- Color Calibration: 1 couleur d'accent max, saturation < 80%. "Lila rule" interdit les dégradés violet/bleu IA par défaut.
- Layout: éviter hero centrée si DESIGN_VARIANCE > 4; favoriser split-screen ou grilles asymétriques.
- Shape consistency: une seule échelle de corner-radius pour tout le projet.
- Interactive states: implémenter Default, Hover, Focus, Active, Disabled, Loading, Empty, Error.
- CTA: contraste WCAG AA (4.5:1), texte sur une seule ligne sur desktop, pas de CTAs dupliquées pour une même intention.
- Hero: headline ≤ 2 lignes, subtext ≤ 20 mots, max 4 éléments textuels, padding top ≤ pt-24.
- Bento rules: pas de cellules vides; 2-3 cellules doivent varier visuellement.
- Image strategy: utiliser aperçus réels ou wireframes, ratio constantes (16:9 ou 4:3).
- Copy: headlines ≤ 8 mots, paragraphs ≤ 25 mots; éviter tournures pompeuses IA.
- Quotes: ≤ 3 lignes, attribution sobre.
- Page theme lock: un seul thème par page (pas d'inversions clair/sombre en scroll).

Non négociable : EM-DASH BAN — utiliser uniquement des tirets réguliers (-) ou des hyphens.

---

## Comportement de nettoyage
- Toute page/frame temporaire DOIT être supprimée à la fin du processus (validation ou abandon).
- Si l'utilisateur demande d'annuler, supprimer immédiatement les éléments temporaires.

---

## Phase 0 : Détection préliminaire (automatique)
Avant l'entretien :
1. Détecter les styles Figma : couleurs, typographie, espacement, corner-radius, effets.
2. Chercher une page nommée "Design Memory", "Design System" ou "Tokens".
3. Afficher la ligne de Design Read.

---

## Phase 1 : Entretien (script)
Poser les questions suivantes (adapter selon Design Memory si présent).

Étape 1.1 — Périmètre et cible
- Périmètre : composant unique ou page complète ?
- Nouveau ou redesign ?
  - Si redesign : préciser l'emplacement/URL du composant et les principaux problèmes (trop dense, hiérarchie faible, mauvaise mobile, look dépassé).
  - Si nouveau : quel objectif ? (décrire / fournir croquis, userflow, diagramme)

Étape 1.2 — Inspiration
- Références visuelles : Stripe, Linear, Notion, Apple, ou autre (préciser).
- Patterns d'interaction : édition inline, divulgation progressive, mises à jour optimistes, raccourcis clavier.
- Références : images, fichier Figma, URL, ou aucune (dans ce cas proposer styles : Flat, Neumorphisme, Glassmorphism, Material, Brutalisme, Minimalisme, Skeuomorphisme, Claymorphisme, Rétro, Dark UI).

Étape 1.3 — Direction de marque & style
- Adjectifs de marque (3-5) : Minimaliste, Premium, Ludique, Utilitaire, etc.
- Densité : Compact / Confortable / Aéré
- Mode sombre : Oui / Non / Éventuellement
- Typographie : utiliser polices du projet, préciser, ou demander suggestions (éviter Inter par défaut). Propositions selon style inclues.
- Couleurs : utiliser styles Figma, ou fournir codes hex / logo pour extraction.

Étape 1.4 — Persona et tâches clés
- Utilisateur principal : Développeur, Designer, Utilisateur métier, Grand public
- Contexte : Desktop, Mobile, Les deux
- Tâches clés : lister 3 tâches principales

Étape 1.5 — Contraintes
- Toutes les propositions doivent respecter WCAG AA minimum.

---

## Protocole redesign (si applicable)
Audit préalable : tokens, architecture de l'information, blocs de contenu, patterns à conserver/abandonner, lecture des cadrans actuels.

Règles de préservation :
- Ne pas changer l'architecture sans demande explicite.
- Extraire les couleurs de marque avant d'appliquer des règles générales.
- Conserver la voix du contenu sauf demande de réécriture.
- Ne pas régresser l'accessibilité.

Ordre de priorité pour la modernisation :
1. Typographie
2. Espacement et rythme
3. Recalibration des couleurs
4. Recomposition du hero et sections clés
5. Remplacement complet de blocs (si nécessaire)

---

## Phases 2 → 8 (processus de production)
Phase 2 — Générer le Brief Design
- Produire le bloc "## Brief Design" avec les cadrans configurés (DESIGN_VARIANCE, MOTION_INTENSITY, VISUAL_DENSITY).
- Attendre confirmation avant exécution graphique.

Phase 3 — Générer les variantes dans Figma
- Créer une page nommée "🧪 Design Lab".
- Ajouter 5 frames alignées horizontalement :
  - Lab — Variante A (hiérarchie)
  - Lab — Variante B (layout)
  - Lab — Variante C (densité d'espacement)
  - Lab — Variante D (interactions & états)
  - Lab — Variante E (direction expressive)
- Chaque frame : variables réelles, titre, calques de texte pour justification et états (Default, Hover, Focus, Error).

Phase 4 — Présentation
- Annoncer : ✅ Design Lab créé !
- Fournir "## Récapitulatif — Variantes générées" décrivant chaque variante.

Phase 5 & 6 — Retours et synthèse
- L'utilisateur choisit une variante ou propose une hybridation.
- Si hybridation : créer Variante F, conserver 1-2 sources pour comparaison, supprimer autres.

Phase 7 — Prévisualisation finale
- Créer une frame "🎯 Design Final" à la racine de la page principale (ou page active).
- Ajouter annotations d'accessibilité et résumé "## Récapitulatif — Design final".

Phase 8 — Finaliser & nettoyage
- Après confirmation :
  1. Supprimer la page temporaire "🧪 Design Lab".
  2. Conserver uniquement "🎯 Design Final".
  3. Créer/mettre à jour la page "Design Memory" avec décisions, mapping des variables, et arbitrages d'accessibilité.
  4. Générer le plan d'implémentation (voir modèle ci-dessous).

---

## Modèle de Plan d'implémentation (sortie finale)
Fournir en raw markdown structuré :

# Plan d'implémentation — [Nom du composant/page]

## 1. Architecture des composants
- Arborescence des calques et auto-layouts

## 2. Token Mapping
- Variables de couleur
- Rayons (corner-radius)
- Typographies et échelles (h1, h2, body, etc.)

## 3. Checklist Accessibilité WCAG AA & États
- Spécifications de focus
- Gestion prefers-reduced-motion
- États visuels (Default, Hover, Focus, Active, Disabled, Loading, Empty, Error)

---

## Prochaines actions possibles
- Je peux lancer la création automatisée dans un fichier Figma (nécessite URL du fichier et token/API).
- Je peux ouvrir une PR pour modifier ou déplacer ce fichier dans le repo.
- Autres demandes : préciser.

---

*Fichier mis à jour pour améliorer la lisibilité : sections clarifiées, table des matières ajoutée, listes et blocs de code formatés.*
