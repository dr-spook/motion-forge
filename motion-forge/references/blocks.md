# Catalogue des blocs (généré par `mf blocks --md` — ne pas éditer à la main)

Sommaire : tableau · bar-chart · chapter-card · code-card · cta-end · cursor-demo · feature-grid · highlight-zoom · kinetic-type · list-steps · logo-wordmark · metric-counter · quote-card · screen-showcase · split-compare · terminal-type · title-slam · typewriter-opener · ui-float

| Bloc | Catégorie | Énergie | Durée | Sémantique | Rôle |
|---|---|---|---|---|---|
| `bar-chart` | data | 3 | 2.5–9 s | compare, count, prove | Histogramme de 3 à 6 barres qui poussent en cascade (verticales en paysage, horizontales en portrait), valeurs qui comptent, maximum en accent. |
| `chapter-card` | transition | 3 | 1.5–4 s | sequence, transition, explain | Carte de chapitre d'explainer : grand numéro qui roule depuis le précédent, titre qui suit, points de progression des N chapitres. |
| `code-card` | code | 2 | 3–10 s | explain, demo, focus | Extrait de code en carte : coloration par regex, révélation ligne à ligne, puis une bande de surbrillance glisse sur les lignes clés et estompe le reste. |
| `cta-end` | cta | 2 | 2.5–8 s | end, brand | Carte de fin : nom de marque qui se lève lettre à lettre, commande ou URL tapée dans une pastille, anneau de pouls discret. |
| `cursor-demo` | showcase | 3 | 3–10 s | demo, focus, sequence | Démo guidée sur capture : un grand curseur suit une trajectoire lissée (Catmull-Rom, forme fermée), clique avec onde, et la caméra zoome en le suivant. |
| `feature-grid` | list | 3 | 3–10 s | list, explain, prove | Grille de 2 à 4 cartes de fonctionnalités : construction en cascade, puis un cadre lumineux voyage de carte en carte (jamais statique). |
| `highlight-zoom` | showcase | 3 | 2.5–8 s | focus, prove, demo | Capture avec zone d'intérêt : le reste s'assombrit (spotlight), un cadre se pose sur la région, puis la caméra pousse dedans ; étiquette en surimpression. |
| `kinetic-type` | title | 5 | 1.5–7 s | reveal, problem, explain | Typographie cinétique : gros mots qui claquent un par un (calés sur les mots horodatés si présents), secousse d'impact, accent *mot*, poussée caméra. |
| `list-steps` | list | 2 | 3–12 s | sequence, list, explain | Étapes numérotées en frise verticale : la ligne de progression se trace, chaque nœud s'allume quand la ligne l'atteint, puis l'étape courante est cerclée. |
| `logo-wordmark` | brand | 3 | 2–6 s | brand, reveal, end | Révélation de marque : les lettres s'assemblent depuis des décalages seedés avec un ressort closed-form, point d'accent qui tombe, logo optionnel. |
| `metric-counter` | data | 3 | 2.5–8 s | count, prove | Chiffre clé qui compte en forme fermée (préfixe, suffixe, décimales) avec une sparkline qui se trace au même instant ; l'unité se pose quand le chiffre s'arrête. |
| `quote-card` | emphasis | 2 | 3–9 s | quote, prove, focus | Citation en grand, révélée ligne à ligne ; un surligneur balaie le passage *clé* pendant que le reste s'estompe ; ligne d'auteur. |
| `screen-showcase` | showcase | 3 | 2–9 s | demo, prove, focus | Capture d'écran réelle dans un cadre flottant : bascule 3D d'entrée, pan lent, légende optionnelle. |
| `split-compare` | compare | 3 | 3–9 s | compare, prove | Avant / après dans le même cadre : un volet clipPath et sa poignée, pilotés par une seule progression (révèle, s'arrête, pousse, revient). |
| `terminal-type` | code | 3 | 3–12 s | demo, prove, sequence | Fenêtre de terminal : commandes tapées caractère par caractère (cadence déterministe), sorties ligne à ligne, défilement sans interpolation, curseur à clignotement fini. |
| `title-slam` | title | 4 | 1.2–6 s | reveal, brand, problem | Titre cinétique : mots révélés par masque avec rebond, barre d'accent, poussée caméra continue. |
| `typewriter-opener` | opener | 1 | 2.5–9 s | reveal, brand, problem | Ouverture noire premium : curseur qui clignote (fini), puis texte blanc tapé caractère par caractère (événements du planificateur ou cadence cps). |
| `ui-float` | showcase | 3 | 3–10 s | demo, prove, reveal | UI flottante dark SaaS : fenêtre produit (capture ou squelette) et 3 panneaux en profondeur, parallaxe en orbite lente, lueur d'horizon, un panneau devient héros. |

## bar-chart

- `title` (text, optionnel, ≤ 52 car.) — *mot* = accent
- `items` (list, ≤ 6 items) — 3 à 6 objets {label (≤ 14 car.), value}
- `unit` (text, optionnel, ≤ 6 car.) — suffixe des valeurs (%, ms, k…)
- `decimals` (number, optionnel)
- SFX auto : tick@0.5s, pop@1.5s
- ⚠ Les barres ne rebondissent pas (les données ne sont pas des ressorts) : ease power3.out uniquement.
- ⚠ Libellés > 14 caractères : coupés en paysage à 6 barres ; abrège.
- ⚠ Valeurs négatives non gérées : utilise une base 0 et des valeurs positives.

## chapter-card

- `index` (number) — numéro du chapitre (1…total)
- `total` (number) — nombre total de chapitres (≤ 9)
- `title` (text, ≤ 40 car.)
- `kicker` (text, optionnel, ≤ 20 car.)
- SFX auto : whoosh@0s, tick@0.45s
- ⚠ Le numéro d'abord, le titre ensuite : jamais simultanés (la hiérarchie s'effondre).
- ⚠ ≤ 2,5 s en général : une transition plus longue que le contenu vole la vedette.
- ⚠ total > 9 : les points deviennent illisibles en 9:16.

## code-card

- `code` (code) — ≤ 14 lignes, ≤ 52 caractères par ligne de préférence
- `language` (text, optionnel, ≤ 14 car.)
- `filename` (text, optionnel, ≤ 36 car.)
- `highlight` (list, optionnel, ≤ 4 items) — numéros de lignes (à partir de 1) visités dans l'ordre par la bande
- SFX auto : tick@0.45s
- ⚠ Au-delà de 14 lignes la police devient illisible en 9:16 : montre l'extrait utile, pas le fichier.
- ⚠ La coloration est une regex simple (chaînes, nombres, mots-clés, appels) : pas d'analyse syntaxique, évite les gabarits imbriqués.
- ⚠ La bande s'arrête sur chaque ligne surlignée puis glisse (jamais de saut) : 0,8 s minimum par ligne.

## cta-end

- `brand` (text, ≤ 22 car.)
- `command` (text, ≤ 44 car.) — commande (npx …, brew …) ou URL ; tapée dans la pastille
- `tagline` (text, optionnel, ≤ 60 car.)
- `note` (text, optionnel, ≤ 40 car.) — ex. « Gratuit · open source · local »
- SFX auto : whoosh@0.05s, key@0.9s
- ⚠ Une seule action : une commande OU une URL, jamais les deux.
- ⚠ Commande > 32 caractères en 9:16 : la police de la pastille rétrécit, préférer une URL courte.
- ⚠ Garder ≥ 1,5 s après la frappe pour que la commande soit lisible avant la coupe.

## cursor-demo

- `capture` (capture) — capture réelle (mf capture)
- `points` (list, ≤ 8 items) — [{x, y, click?}] en fractions 0–1 de l'image ; 2 à 5 points conseillés
- `label` (text, optionnel, ≤ 44 car.)
- `aspect` (number, optionnel) — largeur/hauteur de la capture
- SFX auto : whoosh@0s, click@1.6s
- ⚠ Chaque clic doit déclencher une réponse visible dans la capture suivante : sinon le curseur semble cliquer dans le vide.
- ⚠ Un mouvement de curseur par idée dite : trop de points = démo d'enregistrement d'écran.
- ⚠ Les SFX de clic du bloc ne couvrent que le premier clic : ajoute les autres dans scene.sfx (mêmes instants que le planning).

## feature-grid

- `heading` (text, optionnel, ≤ 48 car.) — *mot* = accent
- `items` (list, ≤ 4 items) — 2 à 4 objets {title (≤ 28 car.), body (≤ 90 car.)}
- SFX auto : whoosh@0.25s, tick@1.2s
- ⚠ Titres de carte ≤ 28 caractères, corps ≤ 90 : au-delà la carte déborde en 16:9 à 4 colonnes.
- ⚠ Le cadre lumineux a besoin d'au moins 0,9 s par carte : compte durée ≥ 1,4 + 0,9 × nombre de cartes.
- ⚠ 4 cartes en 9:16 = cartes basses : garde des corps courts (≤ 60 car.).

## highlight-zoom

- `capture` (capture) — capture réelle (mf capture)
- `rect` (list, ≤ 4 items) — [x, y, w, h] en fractions 0–1 de l'image
- `label` (text, optionnel, ≤ 40 car.)
- `aspect` (number, optionnel) — largeur/hauteur de la capture (1.6 = 16:10) — sert à caler la région sans mesurer
- SFX auto : whoosh@1.3s
- ⚠ aspect doit correspondre à l'image réelle, sinon le cadre tombe à côté de la région.
- ⚠ Région minuscule (< 8 % de largeur) : le zoom plafonne à ×3 pour rester net ; recadre la capture.
- ⚠ La cible elle-même n'est ni recolorée ni agrandie à part : seul le reste s'assombrit.

## kinetic-type

- `text` (text, ≤ 72 car.) — 3 à 9 mots ; *mot* = accent. Si timing/words.json couvre la scène, chaque mot claque à son start
- `kicker` (text, optionnel, ≤ 32 car.)
- `align` (text, optionnel) — auto (gauche en 16:9, centré ailleurs) | left | center
- SFX auto : impact@0.12s
- ⚠ Plus de 9 mots : le dernier claque trop tard, découpe en deux scènes.
- ⚠ Avec des mots horodatés, le nombre de mots du slot doit égaler celui de la scène, sinon le texte transcrit est affiché (accents perdus sauf correspondance exacte).
- ⚠ Un mot de plus de 14 lettres réduit toute la taille : préférer des mots courts en 9:16.

## list-steps

- `title` (text, optionnel, ≤ 44 car.) — *mot* = accent
- `items` (list, ≤ 5 items) — 2 à 5 chaînes (≤ 46 car.)
- SFX auto : tick@0.5s
- ⚠ Le nœud apparaît quand la ligne l'atteint, jamais avant : la frise montre la progression, pas une liste.
- ⚠ ≥ 0,7 s par étape, sinon l'activation se lit comme un clignotement.
- ⚠ Étapes > 46 caractères : passent sur deux lignes et serrent la frise en 9:16.

## logo-wordmark

- `brand` (text, ≤ 18 car.)
- `logo` (image, optionnel) — PNG/SVG carré, fond transparent
- `tagline` (text, optionnel, ≤ 48 car.)
- SFX auto : whoosh@0.1s, pop@1.15s
- ⚠ Le ressort est le seul élément élastique : le slogan entre en pur ease-out, sinon deux rebonds se disputent.
- ⚠ Nom de plus de 12 lettres en 9:16 : la taille baisse fortement, prévoir un logo + nom court.
- ⚠ Même seed → mêmes trajectoires : change le seed de la spec pour varier l'assemblage.

## metric-counter

- `value` (number) — valeur finale, ex. 12480 ou 99.9
- `prefix` (text, optionnel, ≤ 4 car.)
- `suffix` (text, optionnel, ≤ 6 car.) — unité, posée à la fin du comptage (%, ms, k…)
- `label` (text, ≤ 56 car.)
- `decimals` (number, optionnel)
- `points` (list, optionnel, ≤ 24 items) — série de nombres pour la sparkline (≥ 3)
- `delta` (text, optionnel, ≤ 28 car.) — ex. « +38 % en 30 jours »
- SFX auto : tick@0.5s, impact@1.9s
- ⚠ Le chiffre doit venir d'un fait sourcé (facts.json) : jamais inventé.
- ⚠ Chiffre + préfixe + suffixe > 9 caractères : la taille est réduite automatiquement, mieux vaut abréger (12,4 k).
- ⚠ La sparkline et le comptage démarrent au même instant (0,5 s) : ne pas les décaler, sinon « chiffre puis graphe décoratif ».

## quote-card

- `quote` (text, ≤ 170 car.) — *passage surligné* (un seul, ≤ 6 mots)
- `author` (text, ≤ 40 car.)
- `role` (text, optionnel, ≤ 48 car.)
- SFX auto : whoosh@1s
- ⚠ Un seul passage surligné : surligner partout revient à ne rien surligner.
- ⚠ Citation réelle et attribuée uniquement (jamais de témoignage inventé).
- ⚠ Au-delà de 140 caractères en 9:16, la taille descend sous le confort de lecture mobile.

## screen-showcase

- `capture` (capture) — PNG/JPG d'une vraie page (mf capture)
- `caption` (text, optionnel, ≤ 56 car.)
- `pan` (text, optionnel) — down | up | left | right | none
- `url` (text, optionnel, ≤ 48 car.) — affichée dans la barre du navigateur
- SFX auto : whoosh@0s
- ⚠ Capture plus haute que large pour un pan vertical lisible.
- ⚠ Ne jamais montrer de données personnelles réelles : masque d'abord (mf capture le fait).

## split-compare

- `before` (text) — chemin d'image (même cadrage que after) ou texte court
- `after` (text) — chemin d'image ou texte court ; *mot* = accent en mode texte
- `before_label` (text, optionnel, ≤ 16 car.)
- `after_label` (text, optionnel, ≤ 16 car.)
- `caption` (text, optionnel, ≤ 56 car.)
- SFX auto : whoosh@0.5s
- ⚠ Les deux images doivent avoir exactement le même cadrage : le volet ne compare que le contenu.
- ⚠ En 9:16 le volet devient vertical (avant en haut, après en bas) : prévois des captures lisibles en bande.
- ⚠ Mode texte : 40 caractères max par côté, sinon la taille chute.

## terminal-type

- `lines` (list, ≤ 16 items) — objets {cmd: "npx mf make"} ou {out: "✓ rendu 16:9"} ; ✓ = ligne de succès (seule couleur sémantique) ; finir par … pour une pause
- `title` (text, optionnel, ≤ 40 car.)
- `cps` (number, optionnel) — caractères/s des commandes (humain : 14–24)
- `prompt` (text, optionnel, ≤ 4 car.)
- SFX auto : key@0.45s
- ⚠ Une seule couleur sémantique : la ligne ✓ finale. Pas de terminal arc-en-ciel.
- ⚠ Lignes très longues → police réduite pour tout le terminal : coupe les sorties à ~48 caractères.
- ⚠ Si la durée est trop courte pour tout taper, la cadence est accélérée uniformément (vérifie la lisibilité).

## title-slam

- `title` (text, ≤ 48 car.) — 2 à 6 mots ; *mot* = accent
- `kicker` (text, optionnel, ≤ 32 car.)
- `align` (text, optionnel) — center | left
- SFX auto : impact@0.12s
- ⚠ Plus de 6 mots = lecture impossible en < 2 s : découpe en deux scènes.
- ⚠ L'accent *mot* sur un seul mot, jamais deux.

## typewriter-opener

- `text` (text, ≤ 48 car.) — une phrase forte, ≤ 2 lignes en 16:9
- `events` (list, optionnel) — [{t, i}] : t secondes relatives au début de scène, i index du caractère (Array.from(text)) — produit par le planificateur Python d'ouverture ; les SFX de frappe doivent utiliser les mêmes t
- `cps` (number, optionnel) — caractères/s si events absent (doctrine : 10–16)
- `hold_cursor` (bool, optionnel) — le curseur reste et clignote après la frappe
- SFX auto : key@0.9s
- ⚠ Pas de sous-titres sur ce bloc : le texte tapé EST le sous-titre (désactive captions sur cette plage ou laisse le bloc les masquer).
- ⚠ Style noir conseillé (#000–#050505) : un fond coloré casse la doctrine noir-blanc.
- ⚠ Les clics de frappe ne tombent jamais sur les espaces ni pendant la tenue : génère-les depuis events.
- ⚠ Texte > 24 caractères en 9:16 : passe sur 3–4 lignes, la hauteur descend vers 7 % de l'image.

## ui-float

- `capture` (capture, optionnel) — capture réelle du produit ; sinon squelette d'interface
- `panels` (list, ≤ 3 items) — 1 à 3 objets {title (≤ 22 car.), value (≤ 12 car.)}
- `heading` (text, optionnel, ≤ 44 car.) — *mot* = accent
- SFX auto : whoosh@0s, riser@1s
- ⚠ Orbite de faible amplitude et déphasage de 90° entre axes : plus grand, c'est un manège ; en phase, c'est un balancier.
- ⚠ Les panneaux ne doivent pas cacher l'information clé de la capture : place-la au centre-haut.
- ⚠ Style sombre recommandé (dark-saas, glow-neon) : sur paper la lueur d'horizon disparaît.
