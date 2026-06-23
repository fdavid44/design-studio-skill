# Skill Figma · Figma Make

## Titre
Figma Make — Skill d'automatisation native pour Figma

## Bref résumé
Cette skill facilite l'automatisation et l'orchestration d'actions directement dans Figma via Figma Make (automations, plugins et webhooks) :
- création d'un "Design Lab" temporaire dans un fichier Figma
- génération de variantes UI
- export d'images et d'assets
- création et mise à jour de composants
- collecte de retours et génération d'un plan d'implémentation

---

## Qu'est-ce que Figma Make ?
Figma Make est la plateforme d'automatisation native dans l'écosystème Figma (automations, plugins, webhooks et intégrations). Elle permet d'exécuter des workflows et scripts qui interagissent avec les fichiers Figma — par exemple créer des pages/frames, modifier des composants, exporter des images, ou écouter des événements de fichier — sans sortir de Figma.

Points clés :
- Exécutable depuis Figma (automations ou plugins) ou depuis des services externes via l'API et webhooks.
- Utilise les APIs et webhooks officiels de Figma pour lire/écrire la structure du fichier et exporter ressources.
- Authentification : tokens Figma (PAT) ou OAuth apps enregistrées dans le tableau de bord développeur Figma selon le mode d'exécution.

---

## Table des matières
1. Manifest (exemple YAML)
2. Installation & permissions (Figma Make)
3. Utilisation (exemples)
4. Erreurs courantes & dépannage
5. Bonnes pratiques
6. Contribution
7. Licence
8. Design Lab — Configuration (guide complet)

---

## 1. Manifest (exemple YAML)
Remplace le champ `platforms` par `figma_make` pour indiquer que la skill cible l'automatisation native de Figma.

```yaml
name: figma-make-skill
id: com.votreorg.figma_make_skill
version: 0.1.0
author: Votre Nom <votre@exemple.com>
description: >-
  Automatisation native pour Figma via Figma Make : création de pages lab,
  génération de variantes, export d'assets, et gestion de webhooks.
platforms:
  - figma_make
auth:
  type: oauth2  # ou token selon le mode d'exécution (plugin vs serveur)
  authorizationUrl: https://www.figma.com/oauth
  tokenUrl: https://www.figma.com/api/oauth/token
  scopes:
    - files:read
    - files:write
    - images:read
triggers:
  - id: file_updated
    title: On File Updated
    description: Déclenché lorsqu'un fichier Figma est modifié (via webhook ou automation).
actions:
  - id: create_design_lab
    title: Create Design Lab
    description: Crée une page "🧪 Design Lab" et 5 variantes dans le fichier Figma cible
    inputs:
      - name: file_id
        type: string
        required: true
      - name: options
        type: object
    outputs:
      - name: lab_page_id
        type: string
  - id: export_frame
    title: Export Frame
    description: Exporte une frame en PNG/JPEG/SVG via l'API Figma
    inputs:
      - name: file_id
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
webhooks:
  - id: webhook_file_events
    description: Webhook pour événements de fichier (modification, version, etc.)
rate_limits:
  calls_per_minute: 60
endpoints:
  base: https://api.figma.com/v1
permissions:
  - files:read
  - files:write
  - images:read
```

---

## 2. Installation & permissions (Figma Make)
Selon le mode d'exécution, deux approches :

A. Exécution depuis Figma (plugin / automation)
- Créer un plugin ou une automation Figma qui contient la logique de la skill.
- Déployer le plugin/automation via le tableau de bord développeur Figma ou en tant que plugin d'équipe.
- Les utilisateurs exécutent la skill directement dans le fichier Figma (permissions gérées par Figma).

B. Exécution depuis un service externe (serveur)
- Enregistrer une application OAuth dans le panneau développeur Figma pour obtenir client_id / client_secret, ou utiliser un token personnel (PAT) pour appels serveur.
- Abonner un webhook pour surveiller les événements de fichier (modification, publication de version).
- Le serveur reçoit les événements, appelle l'API Figma pour lire/écrire le fichier, puis exécute la logique (création de pages, export d'images, etc.).

Notes de sécurité
- Stocker les tokens de façon sécurisée (secrets, vault).
- Respecter les quotas API et implémenter retries/backoff.

---

## 3. Utilisation (exemples)
- Créer un Design Lab dans un fichier Figma
  - Action: Create Design Lab
  - Inputs: file_id, options (noms des variantes, styles de base)
  - Résultat: lab_page_id contenant les 5 frames

- Exporter une frame en PNG via l'API Figma
  - Action: Export Frame
  - Inputs: file_id, node_id, format=png
  - Résultat: image_url (hôte par Figma ou transféré vers votre stockage)

- Synchroniser tokens (colors/typography) depuis Figma vers un repo ou un design system externe
  - Lire les styles Figma via l'API
  - Mapper et pousser vers destination (JSON, tokens, fichier)

---

## 4. Erreurs courantes & dépannage
- 401 Unauthorized : vérifier token OAuth / PAT et scopes.
- 403 Forbidden : vérifier les permissions du plugin / de l'app.
- 429 Rate limit : appliquer backoff et limiter la fréquence des appels.
- Node not found : s'assurer que node_id appartient bien au file_id fourni.
- Webhook non reçu : vérifier endpoint public, certificats, et configuration du webhook dans Figma.

---

## 5. Bonnes pratiques
- Exécuter d'abord les actions sur un fichier de test.
- Versionner les modifications critiques (Utiliser des noms/versions de pages temporaires).
- Nettoyer automatiquement les pages/frames temporaires après validation ou abandon.
- Fournir des messages clairs dans Figma (annotations) pour que les designers comprennent les changements automatisés.

---

## 6. Contribution
- Forkez le dépôt, créez une branche feature/xxx, ouvrez une PR.
- Tests: inclure fixtures Figma (IDs factices) et mocks pour l'API.

---

## 7. Licence
MIT

---

# Design Lab — Configuration de la Skill Figma Make

(Ce guide a été mis à jour pour préciser que la skill cible Figma Make — la plateforme d'automatisation native de Figma.)

[Le reste du guide "Design Lab" est inchangé mais reste adapté pour une exécution via Figma Make — création de la page `🧪 Design Lab`, génération de 5 variantes, collecte des retours et plan d'implémentation.]
