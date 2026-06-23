# Design Lab — Configuration de la Skill Figma Make

Conduis un entretien de design, génère cinq variations d'UI distinctes dans un lab de design temporaire au sein du fichier, collecte les retours et produis un plan d'implémentation. Utilise ce[...]

---
## CRITIQUE : règles de Design à appliquer

0. INFERENCE DU BRIEF (Lis la pièce avant toute chose)
Avant de toucher au rendu visuel ou de modifier les paramètres, déduis ce que l'utilisateur veut réellement.

0.A Analyse d'abord ces signaux
Page kind - landing (SaaS / consumer / agency / event), portfolio (dev / designer / creative studio), redesign (preserve vs overhaul), editorial / blog.
Vibe words used by the user - "minimalist", "calm", "Linear-style", "Awwwards", "brutalist", "premium consumer", "Apple-y", "playful", "serious B2B", "editorial", "agency-y", "glassy", "dark tech[...]
Reference signals - URLs they linked, screenshots they pasted, products they named, brands they're competing with.
Audience - B2B procurement panel vs. design-conscious consumer vs. recruiter scanning a portfolio.
Brand assets that already exist - logo, color, type, photography. For redesigns, these are starting material, not optional input (see Section 11).
Quiet constraints - accessibility-first audiences, public-sector, regulated industries, trust-first commerce, kids' products.

0.B Output une ligne de "Design Read" avant de générer
Avant de générer le moindre écran ou composant, déclare en une ligne : "Reading this as: <page kind> for <audience>, with a <vibe> language, leaning toward <design system or aesthetic family>[...]

0.C Si le brief est ambigu, pose une seule question, ne devine pas
Pose exactement une question de clarification - jamais une série de plusieurs questions. Si tu peux déduire le contexte avec confiance, ne demande rien. Déclare simplement ton "design read" et[...]

0.D Discipline Anti-Default
Ne choisis jamais par défaut : les dégradés violet/indigo typiques de l'IA, une hero section centrée sur un fond sombre texturé (dark mesh), trois cartes de fonctionnalités identiques, du g[...]

1. LES TROIS CADRANS (Configuration centrale)
Après le design read, règle trois cadrans. Chaque décision de mise en page et de densité est dictée par ces variables.
DESIGN_VARIANCE: 1-10 (1 = Symétrie parfaite, 10 = Chaos artistique)
MOTION_INTENSITY: 1-10 (1 = Statique, 10 = Cinématique / Physique)
VISUAL_DENSITY: 1-10 (1 = Galerie d'art / Airy, 10 = Cockpit / Données denses)
Baseline: 8 / 6 / 4. Utilise ces valeurs par défaut à moins que le design read ne les remplace.

2. CARTOGRAPHIE BRIEF → DESIGN SYSTEM
Une fois que tu as le design read et les cadrans, choisis la bonne base en utilisant les packages officiels ou les utilitaires de variables et de styles disponibles pour l'équipe. Un seul systè[...]
Les esthétiques (Glassmorphism, Bento, Brutalism, Editorial, Dark tech, Aurora) doivent être construites nativement avec les propriétés de variables et de styles de Figma.
* **Glassmorphism** : Superposition de surfaces semi-transparentes, backdrop blur prononcé, bordures fines de 1px simulant le reflet de la lumière, et ombres douces et diffuses pour détacher l[...]
* **Bento Grid** : Structuration de l'interface en une grille de rectangles et de carrés aux angles arrondis. Chaque cellule compartimente une information ou une fonctionnalité claire, avec des[...]
* **Brutalism / Néo-Brutalisme** : Contours noirs épais (2px à 4px), couleurs vives et saturées en aplat, ombres portées nettes et dures (sans flou), et typographie imposante qui casse déli[...]
* **Editorial** : Grands espaces blancs (espacements aérés), grilles asymétriques épurées, et contraste typographique fort mettant en valeur des titres élégants face à des blocs de texte [...]
* **Dark Tech (Style Linear / Stripe)** : Thématique sombre utilisant des arrière-plans gris très profonds ou noirs, combinés à des bordures subtiles. Utilise des lueurs directionnelles disc[...]
* **Aurora / Dégradés fluides** : Arrière-plans enrichis par de grands dégradés organiques, flous et colorés. Ces formes fluides se superposent en arrière-plan pour apporter de la profonde[...]

3. ARCHITECTURE PAR DÉFAUT & CONVENTIONS
Standardise les breakpoints (sm 640, md 768, lg 1024, xl 1280, 2xl 1536). Contiens les mises en page en utilisant max-w-[1400px]. Viewport Stability : utilise des métriques de layout basées sur[...]

4. DIRECTIVES DE DESIGN ENGINEERING (Correction des biais)
4.1 Typography : Les polices sans-serif pour les titres sont appliquées par défaut (Geist, Satoshi, Outfit). Les polices serif sont très fortement déconseillées sauf si explicitement requis [...]
4.2 Color Calibration : Maximum 1 couleur d'accent. Saturation < 80%. THE LILA RULE : L'esthétique des lueurs et dégradés violet/bleu typiques de l'IA est interdite sauf demande contraire. PRE[...]
4.3 Layout Diversification : Évite les hero sections centrées lorsque DESIGN_VARIANCE > 4. Force le split-screen ou des espaces blancs asymétriques. N'aligne jamais systématiquement le texte [...]
4.4 Materiality & Shapes : SHAPE CONSISTENCY LOCK : Choisis une seule échelle de corner-radius pour toute la page et respecte-la partout. Une carte imbriquée doit avoir un rayon inférieur à s[...]
4.5 Interactive UI States : Implémente les cycles complets (Default, Hover, Focus, Active, Disabled, Loading, Empty, Error). Chaque état doit être visible graphiquement par un changement de bo[...]
4.6 Boutons et Appels à l'action (CTA) : BUTTON CONTRAST CHECK : Minimum WCAG AA (4.5:1). CTA BUTTON WRAP BAN : Le texte doit tenir sur une seule ligne sur desktop. NO DUPLICATE CTA INTENT : Un [...]
4.7 Layout Discipline : La hero section doit tenir dans le viewport initial (Headline de 2 lignes max, subtext de 20 mots max). Padding supérieur de la hero section à pt-24 max. Maximum 4 élé[...]
4.8 Grilles Bento & Répétition : BENTO CELL COUNT RULE : Un nombre exact de cellules pour le contenu, pas de cases vides. Au moins 2 à 3 cellules doivent présenter une variation visuelle de f[...]
4.9 Image Strategy & Mockups : Pas de fausses captures d'écran construites avec des divs. Utilise des aperçus réels de composants, des structures de type wireframe épurées ou des slots d'ima[...]
4.10 Content Density & Textes : Headlines courtes (≤ 8 mots) + sous-paragraphes courts (≤ 25 mots). Les lignes d'en-tête (hairlines) sur chaque rangée des tableaux de spécifications sont i[...]
4.11 Quotes / Témoignages : Maximum 3 lignes, taille de police légèrement supérieure au corps de texte, avec une attribution propre, sobre et alignée.
4.12 Page Theme Lock : La page a un seul et unique thème. Les sections ne s'inversent pas (clair/sombre) au milieu du scroll pour simuler un faux dynamisme.

9.G EM-DASH BAN (Non-negotiable)
Le tiret cadratin (—) et le tiret demi-cadratin (–) utilisés comme séparateurs sont COMPLÈTEMENT interdits dans les headlines, eyebrows, corps de texte, quotes et boutons. Utilise uniqueme[...]

---

## CRITIQUE : Comportement de nettoyage et cycle de vie
Toutes les pages et frames temporaires DOIVENT être supprimées lorsque le processus se termine, que ce soit par validation ou abandon. Si l'utilisateur dit « annuler », « abandonner », « a[...]

---

## Phase 0 : Détection préliminaire
Avant de démarrer l'entretien, inspecte automatiquement le fichier Figma :
1. Détecte les variables de couleur, typographie, espacement, rayons de bordure (corner-radius) et styles d'effets existants.
2. Cherche une page nommée `Design Memory`, `Design System` ou `Tokens`.
3. Output la ligne de "Design Read" obligatoire en une seule ligne.

---

## Phase 1 : Entretien
Pose ces questions à l'utilisateur. Adapte-les en fonction de la mémoire design si elle existe.

### Étape 1.1 : Périmètre et cible

**Question 1 : Périmètre**
- « Est-ce qu'on design un composant unique ou une page entière ? »
  - « Composant » — Un élément UI réutilisable (bouton, carte, formulaire, modale, etc.)
  - « Page » — Une page ou un écran complet

**Question 2 : Nouveau ou redesign**
- « S'agit-il d'un nouveau design ou d'un redesign de quelque chose d'existant ? »
  - « Nouveau » — Créer quelque chose from scratch
  - « Redesign » — Améliorer un composant/page existant

> Si « Redesign » est sélectionné :
- « Quel est le nom ou l'emplacement du composant/frame existant dans Figma ? Autrement, pouvez-vous me donner une URL ou des images à analyser ?»

- « Quels sont les principaux problèmes avec le design actuel (ou ce que ce nouveau design devrait éviter) ? » *(choix multiple)*
  - « Trop encombré/dense » — Surcharge d'information, difficile à parcourir
  - « Hiérarchie peu claire » — Les actions principales ne sont pas évidentes
  - « Mauvaise expérience mobile » — Ne fonctionne pas bien sur petit écran
  - « Look dépassé » — Semble vieux ou incohérent avec la marque
  
> Si « Nouveau » est sélectionné :
- « Quel est l'objectif visé par la création de cette nouvelle page ou de ce nouveau composant ? Décrivez-le moi sous forme textuelle ou avec une image (croquis, UserFlow, diagramme, ...)»

### Étape 1.2 : Inspiration

**Question 1 : Inspiration visuelle**
- « Quels produits ou marques dois-je prendre comme référence visuelle ? » *(choix multiple)*
  - « Stripe » — Épuré, minimaliste, rassurant
  - « Linear » — Dense, orienté clavier, axé développeur
  - « Notion » — Flexible, centré contenu, ludique
  - « Apple » — Premium, aéré, raffiné
  - "Autre" - Précise quelles sont tes références.

> Si l'utilisateur répond "Autres", demande des précisions.

**Question 2 : Inspiration fonctionnelle**
- « Quels patterns d'interaction dois-je reproduire ? »
  - « Édition inline » — Modifier sur place sans modales
  - « Divulgation progressive » — Afficher plus au besoin
  - « Mises à jour optimistes » — Retour immédiat, synchronisation en arrière-plan
  - « Raccourcis clavier » — Efficacité pour les utilisateurs avancés

**Question 3 : Références visuelles**
- « As-tu des références visuelles à me fournir ? Tu peux partager : »
  - « Images de référence » — Captures d'écran, moodboard, inspiration
  - « Fichier ou lien Figma existant » — Un design ou un UI kit à analyser
  - « URL d'un site ou d'une app » — Je l'analyserai pour en extraire le style
  - « Aucune référence » — Je te proposerai une direction artistique

> Si l'utilisateur choisit « Aucune référence », propose-lui de choisir parmi les styles graphiques suivants) :
>
> - **Flat Design** — Formes simples, couleurs unies, aucune ombre
> - **Neumorphisme** — Relief subtil, monochrome doux, effets de lumière intérieure
> - **Glassmorphisme** — Transparence givrée, flou d'arrière-plan, bordures lumineuses
> - **Material Design** — Élévations, ombres portées, grille 8px, couleurs vives
> - **Brutalisme** — Typographie forte, bordures épaisses, contraste radical
> - **Minimalisme** — Beaucoup d'espace blanc, typographie comme seul ornement
> - **Skeuomorphisme** — Textures et matières réalistes (cuir, métal, papier)
> - **Claymorphisme** — Formes gonflées et arrondies, couleurs pastel saturées
> - **Rétro / Vintage** — Palettes désaturées, typographies d'époque, grain
> - **Dark UI** — Fonds sombres, accents lumineux, hiérarchie par la lumière
>
> Demande à l'utilisateur de choisir 1 à 2 styles comme direction artistique principale.

### Étape 1.3 : Direction de marque et de style

**Question 1 : Adjectifs de marque**
- « Quels 3-5 adjectifs décrivent le ressenti de marque souhaité ? » *(choix multiple)*
  - « Minimaliste » — Épuré, simple, sans encombrement
  - « Premium » — Haut de gamme, soigné, raffiné
  - « Ludique » — Fun, amical, accessible
  - « Utilitaire » — Fonctionnel, efficace, sans chichis

**Question 2 : Densité**
- « Quelle densité d'information préfères-tu ? »
  - « Compact » — Plus d'informations visibles, espacement serré
  - « Confortable » — Espacement équilibré, lecture facile
  - « Aéré » — Grands blancs, attention focalisée

**Question 3 : Mode sombre**
- « Le mode sombre est-il requis ? »
  - « Oui » — Doit supporter le mode sombre
  - « Non » — Mode clair uniquement
  - « Éventuellement » — Si facile, pas obligatoire

**Question 4 : Typographie**
- « Quelles polices de caractères souhaites-tu utiliser ? »
  - « Polices du projet » — Utiliser celles déjà définies dans Figma
  - « Je vais les préciser » — Donne les noms des polices (titres et corps)
  - « Propose-moi des options » — Je choisis parmi des suggestions

> Si l'utilisateur demande des suggestions, propose des combinaisons selon le style choisi. **Évite Inter comme choix par défaut** (trop générique, c'est le réflexe IA) :
> - **Moderne / tech** → Geist + Geist Mono, ou Satoshi + JetBrains Mono
> - **Éditorial / premium** → Cabinet Grotesk + Inter Tight, ou Outfit + IBM Plex Mono
> - **Humaniste / accessible** → Nunito + Open Sans
> - **Minimaliste** → DM Sans + DM Mono
> - **Institutionnel** → Marianne + Spectral *(si projet public français)*
> - **Inter** → acceptable uniquement si le brief demande explicitement un rendu neutre/standard, ou si le projet est secteur public / accessibilité critique.
> 
> **Discipline serif (très déconseillée par défaut) :** Le serif n'est acceptable que si (a) la charte nomme explicitement une police serif, ou (b) la famille esthétique est genuinely édito[...]
> 
> Demande à l'utilisateur de valider ou préciser la police de titre et la police de corps.

**Question 5 : Couleurs de charte**
- « Quelles couleurs de charte dois-je utiliser ? »
  - « Couleurs du projet Figma » — Utiliser les styles de couleur déjà définis
  - « Je vais les préciser » — Donne les codes hexadécimaux ou les noms
  - « Fournis le logo » — Je l'analyserai pour en extraire les couleurs dominantes
  - « Pas de charte définie » — Propose une palette cohérente avec le style choisi

> Si l'utilisateur fournit un logo, analyse-le pour extraire :
> - La couleur primaire dominante
> - Une couleur secondaire ou d'accentuation
> - Les neutres (fond, texte)
>
> Présente la palette extraite et demande validation avant de l'utiliser.

### Étape 1.4 : Persona et tâches clés

**Question 1 : Utilisateur principal**
- « Qui est l'utilisateur final principal ? »
  - « Développeur » — Technique, orienté clavier
  - « Designer » — Visuel, soucieux des détails
  - « Utilisateur métier » — Axé efficacité, moins technique
  - « Grand public » — Public général, niveau technique varié

**Question 2 : Contexte**
- « Quel est le contexte d'utilisation principal ? »
  - « Desktop en priorité » — Principalement utilisé sur grands écrans
  - « Mobile en priorité » — Principalement utilisé sur téléphone
  - « Les deux » — Doit bien fonctionner sur tous les appareils

**Question 3 : Tâches clés**
- « Quelles sont les 3 principales tâches que les utilisateurs doivent accomplir ? » *(réponse libre)*

### Étape 1.5 : Contraintes

CRITIQUE : Toutes les propositions faites doivent être accessibles et respecter les spécifications du WCAG au niveau AA minimum.

### Protocole redesign (si applicable)

Si le type détecté est un **redesign**, effectue un audit avant de générer quoi que ce soit :

- **Tokens de marque** — couleurs primaires/accents, pile typographique, traitement du logo, rayons de coins
- **Architecture de l'information** — arborescence, nav principale, chemins de conversion clés
- **Blocs de contenu** — ce qui existe, ce qui fonctionne, ce qui est du remplissage
- **Patterns à conserver** — interactions signature, voix du contenu, héro reconnaissable
- **Patterns à abandonner** — tells IA, mises en page cassées, imagerie stock générique
- **Lecture des cadrans actuels** — infère les valeurs `DESIGN_VARIANCE / MOTION_INTENSITY / VISUAL_DENSITY` du site existant. C'est ton point de départ, pas les valeurs de base.

**Règles de préservation :**
- Ne pas changer l'architecture de l'information sans demande explicite
- Extraire les couleurs de marque avant d'appliquer toute règle couleur (la marque prime sur les règles génériques)
- Conserver la voix du contenu, sauf si une réécriture est demandée
- Ne jamais régresser les acquis d'accessibilité (focus, contraste, navigation clavier)

**Ordre de priorité pour la modernisation :**
1. Rafraîchissement typographique — plus grand impact visuel, risque minimal
2. Espacement et rythme — augmenter les paddings de section, corriger le rythme vertical
3. Recalibration des couleurs — désaturer, unifier les neutres, conserver l'accent de marque
4. Recomposition du héro et sections clés — restructurer avec les patterns de mise en page
5. Remplacement complet de blocs — uniquement si le bloc existant est irréparable

### ✅ Récapitulatif de fin de Phase 1
Affiche le résumé formaté `## Récapitulatif — Entretien design`. Attends la validation explicite de l'utilisateur.

---

## Phase 2 : Générer le Brief Design
Produis le bloc `## Brief Design` contenant les cadrans techniques configurés (`DESIGN_VARIANCE`, `MOTION_INTENSITY`, `VISUAL_DENSITY`).
Attends le message de confirmation de l'utilisateur avant de passer à l'exécution graphique.

---

## Phase 3 : Générer les variantes dans Figma Make
Crée une nouvelle Page nommée `🧪 Design Lab`. À l'intérieur, génère 5 Frames distinctes alignées horizontalement :
- `Lab — Variante A` (Focus sur la hiérarchie de l'information)
- `Lab — Variante B` (Exploration du modèle de mise en page / layout)
- `Lab — Variante C` (Variation de densité d'espacement)
- `Lab — Variante D` (Modèle d'interaction et états UI)
- `Lab — Variante E` (Direction expressive et identité de marque)

Chaque frame doit contenir l'UI dessinée avec de vraies variables, une étiquette de titre textuelle, et des calques de texte Figma pour la justification et les états (Default, Hover, Focus, Er[...]

---

## Phase 4 : Présenter le Design Lab à l'utilisateur
Affiche le texte d'annonce `✅ Design Lab créé !` suivi du bloc `## Récapitulatif — Variantes générées` décrivant succinctement l'approche de chaque variante :
- **Variante A** : Focus sur la hiérarchie de l'information.
- **Variante B** : Exploration du modèle de mise en page / layout.
- **Variante C** : Variation de densité d'espacement.
- **Variante D** : Modèle d'interaction et états UI.
- **Variante E** : Direction expressive et identité de marque.
Attends le retour de l'utilisateur.

---

## Phase 5 & 6 : Collecter les retours & Synthèse
Demande à l'utilisateur de choisir sa variante gagnante ou de formuler une synthèse. 
Si l'utilisateur demande une hybridation, génère une `Variante F` dans la page `🧪 Design Lab`, conserve 1 ou 2 variantes sources pour comparaison, et supprime les autres. Répète jusqu'à v[...]

---

## Phase 7 : Prévisualisation finale
Une fois validé, crée une Frame nommée `🎯 Design Final` à la racine de la page principale du projet (ou page active). Elle doit contenir le design propre, finalisé et annoté pour l'acces[...]

---

## Phase 8 : Finaliser & Nettoyage
Dès que l'utilisateur confirme :
1. **Nettoyage Figma** : Supprime définitivement la page temporaire `🧪 Design Lab`. Ne conserve EXCLUSIVEMENT que la Frame `🎯 Design Final`.
2. **Mémoire Design (Design Memory)** : Crée ou mets à jour la note ou page `Design Memory` dans le fichier Figma. Consigne de manière immuable : les décisions clés prises, la justification[...]
3. **Plan d'implémentation** : Génère dans le chat le plan d'implémentation finalisé en raw markdown structuré comme suit :
   - `# Plan d'implémentation — [Nom du composant/page]`
   - `## 1. Architecture des composants` (Arborescence des calques et auto-layouts)
   - `## 2. Token Mapping` (Variables de couleur, coins et typographies à appliquer)
   - `## 3. Checklist Accessibilité WCAG AA & États` (Spécifications de focus et gestion du mouvement réduit / prefers-reduced-motion).
