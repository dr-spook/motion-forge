# Styles : le langage visuel

Un style (`styles/<id>.json`, choisi par `video.json.style`) est **un jeu complet de tokens** : couleurs, polices,
graisses, rayon, ombre, lueur, mouvement, texture. On remplace le jeu entier, jamais une couleur au cas par cas dans
une scène. `brand.colors` et `brand.font` surchargent les tokens correspondants ; le reste du style tient.

Sommaire : 1. Discipline commune · 2. paper · 3. dark-saas · 4. kinetic-mono · 5. glow-neon · 6. noir ·
7. Associations typographiques · 8. Blueprints dark-SaaS → blocs · 9. Profils et leurs styles

État : 8 styles dans `styles/<id>.json` (`mf styles`) ; en cas d'écart avec ce texte, le fichier JSON fait foi. Les
5 premiers sont décrits ci-dessous ; `minimal`, `pastel` et `flat` sont les styles par défaut des profils
saas-minimal, saas-pastel et illustration-flat (§ 9).

**Style et profil.** Le style est le langage visuel (tokens) ; le profil (`profiles/<id>.json`) est un **goût mesuré**
sur des références : un style par défaut, une vie continue des scènes (`vie` : poussée de caméra et flottement) et
les seuils de rythme de `mf qa`. `mf ref variant --profile <id>` rend le même film dans un autre profil : la marque
garde son accent, le fond et le texte suivent le profil (`--keep-brand` pour tout garder).

## 1. Discipline commune

- **Une couleur par rôle** : `--mf-accent` = mot clé, trait de pic, bouton final, curseur. Rien d'autre n'est en
  accent. Les couleurs sémantiques (vert/rouge) ne vivent que dans les graphiques ; les couleurs de marques tierces
  que dans leurs tuiles.
- Texte secondaire en `--mf-muted` **plein** ; jamais l'encre avec de l'opacité (le contraste s'effondre).
- **Grain** : rend la dérive de caméra lisible et casse les bandes de dégradé en H.264. 4–6 % sur fond sombre,
  3–6 % sur fond clair, statique ou très lent, jamais dans une couche mise à l'échelle avec des points < 2,5 px.
- **Vignette** : statique, seulement sur fonds sombres (0,3–0,45) ; sur fond clair, 0,06–0,12 au plus ou rien.
- **Lueur** (`--mf-glow`) : fonds sombres uniquement, sur **le rôle accent seulement** (bouton, curseur, point de
  lumière), jamais sur un texte à lire ni sur une capture. Une lueur se gagne : un événement l'allume.
- Fond clair : pas de flash blanc (il ne monte nulle part ; fais un creux sombre de 6–10 % sur 3–4 images), pas de
  sortie floue (elle grise l'image), pas de fondu entre deux scènes claires sans fond commun dessous.
- Une ombre unique par style, réservée aux objets « posés » (captures, cartes, appareils) ; le texte n'a jamais
  d'ombre (le contour d'un sous-titre est une aide de lecture, pas une ombre).
- Rayon : un seul rayon de carte par film (`--mf-radius`), pastilles en `pill`, plein cadre à 0.

## 2. `paper` — éditorial, chaleureux, humain

- **Tokens** : fond `#F3EFE6` · encre `#141414` · muted `#6A665E` · accent `#FF4F1F` · surface `#FFFFFF` · ligne
  `#141414` · rayon 22 · ombre douce double · glow `none` · grain 0,06 · vignette 0 · `snap` back.out(1.7),
  transition 0,55 s, stagger 0,05 s.
- **Humeur** : papier, beaucoup d'air, cartes blanches aux ombres douces qui arrivent en volant, une idée par image.
- **Quand** : launch pour indépendants, fondateurs, cibles non techniques ; explainer ; bibliothèque et docs.
- **À faire** : mot clé dans une petite boîte d'accent aux angles nets (texte couleur fond), trait fin effilé sous
  LE mot des 3–4 pics ; vraies interfaces posées sur le papier ; mises en page côte à côte aux marges égales ;
  deux mondes possibles (pivot sur un noir de marque, retour au papier pour la solution).
- **À éviter** : boîte noire pour le mot clé, gros encadré, mot géant ; décor sans sens (barres grises « pour
  remplir ») ; ligne du décor qui traverse une phrase ; flou de sortie ; accent ailleurs que sur les 4 rôles.
- **Typo** : Space Grotesk 700 en display, Inter 500 en texte, JetBrains Mono pour chiffres et code, Instrument
  Serif italique pour une emphase de contraste (une fois par film).

## 3. `dark-saas` — scène noire, UI convoquée de l'obscurité

- **Tokens** : fond `#06070A` · encre `#F4F6FA` · muted `#8B93A7` · accent `#7C5CFF` · surface `#11131A` · ligne
  `#2A2F3D` · rayon 20 · ombre `0 50px 120px rgba(0,0,0,.6)` + filet 6 % · glow `0 0 80px rgba(124,92,255,.45)` ·
  grain 0,04 · vignette 0,35 · `snap` back.out(1.4), transition 0,5 s, stagger 0,045 s.
- **Humeur** : une pièce noire au sol lumineux ; le produit apparaît comme invoqué, capable, rapide, un peu
  cinématographique.
- **Quand** : outil de dev, produit IA, SaaS, démo de fonctionnalité, project pour une CLI ou une web-app.
- **À faire** : noir spatial (presque noir, pas ardoise bleue) + grain/étoiles fines + **lueur violette faible au
  bas du cadre** ; grande typo blanche cinétique comme temps forts (ouverture et fin) ; **un** bouton CTA en
  dégradé cyan → bleu → magenta qui **déclenche** une transformation visible (le dégradé est le rôle « action » de
  l'accent, nulle part ailleurs) ; objets héros **grands** à leur image la plus visible ; transitions majeures en
  flou de vitesse, traînée, ruée d'échelle ou balayage blanc ; cartes qui dérivent en parallaxe dont l'une devient
  le héros.
- **À éviter** : fond à lignes néon horizontales persistantes ; flash plein écran coloré inexpliqué ; beige, orange
  chaud, grand dégradé violet-bleu en fond ; petites cartes UI lointaines ; mise en page de site web à plat ; décor
  plus fort que le produit ; serif ou fonte fantaisie.
- **Typo** : Space Grotesk 700 display (très grand), Inter 500 pour les libellés UI (petits mais nets), JetBrains
  Mono pour prompts et terminal.

## 4. `kinetic-mono` — la typographie est l'image (cible)

- **Cible** : fond `#000000`–`#050505` · encre `#FFFFFF` · muted `#8A8A8A` · accent : l'**inversion** (bloc blanc,
  texte noir) ou un seul accent vif si la marque l'impose · glow none · grain 0–0,03 · vignette 0.
- **Humeur** : manifeste, terminal, affiche qui bouge. Rien d'autre que des lettres et du rythme.
- **Quand** : `opener`, project CLI minimaliste, sting, phrase-clé d'un cinematic.
- **À faire** : phrase héros à 9–15 % de la hauteur ; une ou deux lignes courtes ; frappe caractère par caractère,
  remplacement de mot (balayer puis retaper), interlettrage serré **statique** + lettres qui convergent par `x` ;
  masques et inversions comme seules « couleurs ».
- **À éviter** : fond décoratif, couleur, plus de 3 états avant la tenue finale, tween de `letterSpacing`, texte
  compressé, ligne entière révélée d'un coup.
- **Typo** : JetBrains Mono 500–700 pour la frappe ; Space Grotesk 700 pour la phrase finale ; pas de serif.

## 5. `glow-neon` — énergie nocturne, lumière méritée (cible)

- **Cible** : fond `#05060B` · encre `#F5F7FF` · muted `#8C93B0` · accent cyan `#22D3EE` (magenta `#E879F9` seulement
  dans le dégradé du CTA) · glow sur l'accent, rayon ≤ 80 px, alpha ≤ 0,45 · grain 0,04 · vignette 0,4.
- **Humeur** : outil IA, sortie de version, film musical à forte énergie.
- **Quand** : cinematic sur un beat rapide (> 115 BPM), annonce, teaser ; jamais pour un explainer.
- **À faire** : la lueur naît d'un événement (un clic, un drop) et retombe ; une seule teinte de lueur à la fois ;
  traînées de vitesse sur les gestes rapides ; anneaux et orbites déterministes.
- **À éviter** (règles anti-« motion IA ») : dégradés arc-en-ciel, chrome lumineux, particules gratuites, texte
  courant qui brille, néons permanents en fond, deux couleurs pour le même rôle.
- **Typo** : Space Grotesk 700 display, Inter 500, JetBrains Mono pour les badges et compteurs.

## 6. `noir` — cinéma, contraste, lenteur maîtrisée (cible)

- **Cible** : fond `#0B0B0C` · encre `#EDEAE4` · muted `#7D7A74` · accent chaud unique (terre cuite `#C25B28` ou or
  pâle) · glow none ou point de lumière très doux · grain 0,06–0,08 · vignette 0,45.
- **Humeur** : film de marque, citation, acte de pivot, bande-annonce.
- **Quand** : cinematic posé (< 100 BPM), quote, ouverture ou fermeture d'un launch, acte sombre d'un explainer.
- **À faire** : grands aplats de noir, une flaque de lumière derrière le sujet, serif italique pour le mot qui
  compte, mouvements lents (dérive 1–2 %/s) cassés par de rares gestes nets, tenue finale qui respire.
- **À éviter** : UI chargée, plusieurs couleurs, whips à chaque coupe, lueurs saturées, texte petit sur grain fort.
- **Typo** : Instrument Serif (display, italique pour l'emphase) + Inter 500 ; JetBrains Mono pour une date ou un
  chiffre isolé.

## 7. Associations typographiques

| Style | Display | Texte | Mono | Emphase |
|---|---|---|---|---|
| paper | Space Grotesk 700 | Inter 500 | JetBrains Mono | boîte d'accent ; Instrument Serif italique (1×) |
| dark-saas | Space Grotesk 700 | Inter 500 | JetBrains Mono | accent + glow du CTA |
| kinetic-mono | Space Grotesk 700 | — | JetBrains Mono 500–700 | inversion noir/blanc |
| glow-neon | Space Grotesk 700 | Inter 500 | JetBrains Mono | accent cyan qui s'allume |
| noir | Instrument Serif 400 | Inter 500 | JetBrains Mono | italique serif |

Deux graisses par film (texte / fort) plus le display ; hero ≥ 2× le texte ; display à −0,02 em ; chiffres en
`tabular-nums`. Si `brand.font` existe, il remplace le display (combat l'empreinte « police par défaut »).

## 8. Blueprints dark-SaaS → blocs motion-forge

Choisis seulement les modules qui correspondent aux capacités **vérifiées** du produit (faits). Sans capture, des
cartes UI abstraites et des pastilles de texte, et le film se présente comme « niveau style », pas comme un
enregistrement fidèle. Logo inconnu : marque géométrique simple, signalée comme provisoire.

| Module | Motif | Blocs |
|---|---|---|
| 1. Promesse cinétique | noir, grande phrase saisie à mi-frappe, noms qui se remplacent par flou horizontal, logo, balayage | `kinetic-type`, `typewriter-opener`, `logo-wordmark` |
| 2. Invocation | carte de prompt inclinée, grande ; le prompt se tape ; le CTA dégradé luit ; le curseur clique ; étincelles | `cursor-demo`, `terminal-type` (CLI) |
| 3. Champ de résultats | cartes UI qui flottent en profondeur, une grande carte traverse, l'amas se résout en un canevas | `ui-float`, `screen-showcase` |
| 4. Plateforme / local | une fenêtre monte du bas, le titre se tape au-dessus, pastilles de plateformes, poussée jusqu'au grand | `screen-showcase` + `kinetic-type` |
| 5. Écosystème | grand nœud circulaire entré sur une courbe, pastilles de fournisseurs autour ; le nœud reste grand | `ui-float`, `feature-grid` |
| 6. Anneau de capacités | anneau de badges en orbite, texte central après lisibilité de l'anneau, échanges de profondeur | `ui-float`, `feature-grid` |
| 7. Export | titre + CTA d'export cliqué, le texte s'efface en traînée, un dossier apparaît, les formats jaillissent | `cursor-demo` → `ui-float` |
| 8. Revendication finale | un mot seul, un second le rejoint, la phrase passe par 2–4 états, tenue ≥ 1 s | `kinetic-type` → `cta-end` |

Presets de durée : **sting** 8–12 s (3–4 modules : 0–2,5 promesse · 2,5–5 CTA · 5–8,5 résultat · 8,5–12 final) ;
**standard** 30–36 s (6–8 modules : 0–5,5 promesse + logo · 5,5–9,5 invocation · 9,5–14,5 résultats · 14,5–17
plateforme · 17–20,5 écosystème · 20,5–24,5 anneau · 24,5–30,5 export · 30,5–36 final) ; **étendu** 45–60 s (même
grammaire, + flux produit, cas d'usage, preuve). Chaîne de cause à effet de préférence : promesse → prompt → clic
→ résultat → intégrations → export → revendication.

Contrôle de style dark-saas : scène noire présente ; lueur basse discrète ; pas de fond néon dominant ; typo
cinétique à l'ouverture ou à la fin (idéalement les deux) ; un CTA dégradé qui transforme ; objets héros assez
grands ; aucun flash coloré inexpliqué ; chaque scène a une image héros lisible.

## 9. Profils et leurs styles

| Profil | Style | Vie (poussée · flottement) | Signature mesurée sur les références |
|---|---|---|---|
| saas-minimal | `minimal` | 8 % · 1,6 % | blanc, encre noire fine, halo bleu ; caméra qui plonge |
| saas-pastel | `pastel` | 9 % · 2 % | blanc cassé, aplats doux, coins ronds, cartes volantes |
| illustration-flat | `flat` | 6 % · 1,6 % | aplats francs sans contour, objets qui se construisent |
| mono-glow | `glow-neon` | 8 % · 1,4 % | une teinte + lueur, capitales grasses |
| saas-gradient | `dark-saas` | 6 % · 1,2 % | dégradés doux, UI en perspective |
| affiche-editoriale | `paper` | 5 % · 0,8 % | N&B + un rouge, grille d'affiche |
| geometrique-minimal | `kinetic-mono` | 2 % · 0 | primitives noires, capitales espacées |

Nouvelle référence : `mf ref measure <video>` (profil le plus proche), puis `mf ref add <video> --profile <id>`
(les seuils s'élargissent pour l'inclure, jamais ne se resserrent sans `--recalibrate`). Le fichier vidéo n'est pas
copié, seules ses mesures et son empreinte sont gardées.

