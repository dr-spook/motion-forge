# Direction : la doctrine de mise en scène

À charger avant d'écrire le moindre `scenes[]`, puis à relire avant `mf make`. Ce fichier dit **comment un film
bouge** ; `storyboard.md` dit comment l'écrire dans `video.json`, `styles.md` à quoi il ressemble.

Sommaire : 1. L'idée qui bouge · 2. Les gestes du monde · 3. Le test du diaporama · 4. Lois de mise en scène · 5. Règles anti-« motion
IA » · 6. Courbe d'énergie · 7. Passages de relais · 8. Caméra · 9. Typographie en mouvement · 10. Couleur et accent ·
11. Son et image

## 1. L'idée qui bouge (à écrire avant le storyboard)

Un film de motion design se résume à une transformation : sous nos yeux, une chose en devient une autre, et ce
changement est l'argument. Avant de choisir le moindre bloc, écris-la en une ligne en tête du storyboard :

> « On voit **A** devenir **B** ; c'est la preuve que **<promesse>**. »

- VoxText : une bulle vocale de quatre minutes se défait en lignes de texte ; lire va plus vite qu'écouter.
- Facturo : une pile de factures froissées se range dans un tableau qui se remplit seul ; facturer ne demande plus
  d'y penser.
- Une CLI de release : un historique de commits illisible se trie en trois colonnes ; une commande suffit.

Si la ligne ne vient pas, le film n'a pas encore d'idée. Cherche dans le quotidien de la cible un objet qui peut
changer d'état (une bulle, une pile, une file d'attente, une horloge, un tiroir qui déborde) ; les
objets-métaphores de `world.md` § 3 bis en sont une réserve prête à l'emploi.

## 2. Les gestes du monde

Le film bouge avec les actions réelles du `world` (`world.md` § 3). Les ranger par intention aide à choisir :

| Intention | Actions | Exemple |
|---|---|---|
| Faire naître | `enter`, `type`, `words`, `assemble`, `draw` | le titre se tape ; le logo se trace |
| Transformer | `morph`, `rewrite`, `set` (prop), `count` | la bulle devient du texte ; le prix roule |
| Déplacer, relier | `move`, `orbit`, `click` (curseur) | le fichier glisse dans l'appli ; le curseur clique |
| Envahir, basculer | `flood`, caméra (poussée, panoramique, cran) | la couleur de la marque gagne tout l'écran |
| Faire vivre | `pulse`, `press`, `drift` | le bouton bat ; tout dérive doucement |

- Chaque moment a un **geste principal**, celui qui porte l'idée, et un **geste d'appoint** (caméra, son, dérive)
  qui le soutient. Apparaître en fondu n'est pas un geste.
- Un film garde **deux ou trois transformations-signatures** et les fait revenir avec un sens nouveau : la bulle
  qui se défait au début revient à la fin sous forme de coche. On retient un motif, pas un catalogue.

## 3. Le test du diaporama (avant le rendu, puis avant la livraison)

Un film raté ressemble à une présentation : des écrans qui se succèdent, un titre et trois points, des fondus.
Six vérifications, dont quatre se lisent directement sur la planche de `mf board` :

1. **Sans le son**, la planche raconte-t-elle l'histoire ? Montre-la muette : la personne doit pouvoir la
   résumer en une phrase (« l'appli a transformé le vocal en texte »).
2. **La fin d'une scène n'est pas son début** : chaque scène se termine dans un état visiblement différent de celui
   où elle commence. « Quelque chose est apparu » ne compte pas.
3. **Pas de trou** : aucune zone rouge sur la planche (plus de 1,5 s sans changement visible). Une capture ou une
   icône continue de vivre après son arrivée : dérive, curseur, zoom.
4. **Un seul monde** : les scènes se passent le relais (un objet de la scène précédente change de rôle) au lieu de
   repartir d'un écran vide.
5. **Des compositions qui changent** : jamais deux fois de suite la même mise en page (titre centré, carte au
   milieu).
6. **Des fondus comptés** : deux au plus dans tout le film ; une transition se justifie par ce qui bouge.

Un « non » aux points 1, 2 ou 3 bloque le rendu : on retravaille la mise en scène, jamais le seuil. Signes qui
annoncent un échec : un plan rédigé comme une liste de pages, des icônes posées sans trajectoire, la même courbe
d'accélération partout.

Contrat motion-forge : un bloc **change d'état visible pendant toute sa durée** (jamais plus de 1,5 s d'immobilité ;
`mf qa` la mesure), et un fondu seul n'est pas un mouvement.

## 4. Lois de mise en scène (chiffrées)

1. **Le monde est un lieu, la caméra une piste à part** : on se déplace dans un décor, on ne change pas d'écran.
2. **Deux vitesses, aucune tenue figée** : gestes de 0,04 à 0,2 s ; dérives de toute la durée du plan
   (1 à 10 %/s, linéaires) ; la zone 0,3–0,9 s est réservée à la caméra et au curseur, courbe très asymétrique
   (70–90 % du trajet dans le premier tiers).
3. **L'objet-pont change de rôle** ; à défaut, le vecteur de sortie (direction, vitesse, courbe) fixe l'entrée.
4. **Trop grand et flou, puis posé** : ×1,1 (plan entier) à ×3–6 (objet venu de la caméra), flou 6–12 px, posé en
   1 à 9 images, puis recul lent. Jamais un fondu à taille finale.
5. **Le calage se choisit mot par mot** : l'image devance le mot-image de 0,1 à 0,6 s, chaque silence > 0,4 s est
   une action muette (table « Ancrer sur les mots » de `storyboard.md`).
6. **La coupe franche se mérite** : voix narrative 0 à 4 coupes, aux changements d'acte ; voix jouée : coupe sur le
   premier mot de chaque idée ; 0 à 2 fondus par film.
7. **La métaphore se joue sur le verbe** : « tombe » = chute + contact à ±0,1 s de la syllabe ; au moins 3 verbes
   joués physiquement par film.
8. **Une ou deux signatures répétées 4 à 8 fois** ; un registre de texte = un seul mouvement ; le mécanisme du logo
   ou un objet de l'accroche revient à l'identique à la fin (la rime).
9. **Trois niveaux de profondeur** : avant-plan flou coupé par le bord, sujet net, fond ; parallaxe 2:1 à 3:1.
10. **La fin rassemble le film**, puis un curseur arrive d'un seul mouvement courbe (0,4–0,5 s `power3.out`), clique
    directement (pas d'hésitation), 2 à 3 s de tenue vivante, sortie en iris ou au noir.

Rythme : **un événement (arrivée, geste, clic, changement d'état, cran) toutes les 0,5 à 1 s, toutes les 0,1 à 0,3 s
dans l'accroche**. Le nombre de plans ne discrimine pas (2,8 à 8,3 plans/10 s chez les références) ; les événements,
si. Jamais la même mise en page plus de 3 s.

| Mouvement | Durée | Courbe (token de style) |
|---|---|---|
| Apparition | 0,06–0,2 s | `easeOut` (expo.out) ; `snap` pour petits objets |
| Cran / whip | 0,08–0,15 s | expo.inOut, flou 6–12 px au milieu |
| Changement de scène | 0,3–0,9 s | sortie power2.in, entrée expo.out, chevauchement 0,2–0,3 s |
| Dérive | durée du plan | linéaire, 2–5 % d'échelle/s ou 10–30 px/s |
| Vie d'une tenue | boucle 1–2 s | sine.inOut, 1–3° ou 2–6 px, répétitions finies |
| Sortie | ≈ 1/2 de l'entrée | power3.in ; la sortie est toujours plus légère que l'entrée |

## 5. Règles anti-« motion IA »

- **Un seul accent** ; **une seule chose bouge à la fois** (sauf transformation continue pilotée) ; **un seul système
  de formes** du début à la fin, des transformations plutôt que des coupes.
- Ressorts amortis (rapport d'amortissement ≥ 0,72) : léger dépassement, jamais de rebond de dessin animé. En tokens :
  `snap` (back.out ≤ 1,7) réservé aux petits objets (pastilles, puces, lettres) ; jamais sur un bloc de texte, une
  capture, un panneau ou la caméra. Pas de mouvement linéaire visible hors dérives.
- Interdits : dégradés arc-en-ciel, particules gratuites, chrome lumineux, emoji, lorem ipsum, flips 3D gratuits,
  texte flou mis à l'échelle (ne jamais agrandir une copie floue : fondre seulement le remplissage).
- Texte assez grand pour un téléphone ; zone sûre 9:16 décidée au storyboard (le texte utile dans le carré central).
- Combattre l'empreinte : police de marque si `brand.font` existe ; pas de mises en page verticales surchargées.
- « Mieux vaut aucun mouvement qu'un mauvais mouvement » : pas d'effet ajouté sans rôle.

## 6. Courbe d'énergie d'un film

Chaque bloc annonce son intensité dans `block.json` (`energy`, de 1 calme à 5 explosif). Trace la courbe du film
avant de choisir les blocs ; ce sont les écarts qui se ressentent, pas le niveau moyen.

| Moment | Intensité | Cadence |
|---|---|---|
| Accroche (0–3 s) | 4–5 | un changement toutes les 0,1–0,3 s |
| Problème | 3–4, en montée | plus nerveuse que la solution (mesuré sur nos références : 9,3 contre 5,4 plans/10 s) |
| Bascule | 1, puis 5 | 0,6–1,5 s presque vides (un mot, du noir), puis le basculement |
| Démonstration | 3, stable | une idée par scène, portée par des gestes d'interface |
| Preuve | 4, au sommet | un chiffre qui roule ou qui fonce vers la caméra |
| Fin | 3, puis 2 | un clic, 2–3 s de tenue vivante, la sortie |

Trois ou quatre sommets suffisent. Deux scènes à 5 d'affilée s'écrasent l'une l'autre ; plus de 6 s à 2 endort.
Le soulagement de la solution vient du contraste avec la nervosité du problème.

## 7. Passages de relais (éléments partagés)

- À chaque couture, un objet de la scène N **survit et prend un autre rôle** en N+1 (la bulle porte ses mots dans
  l'aplat, le bouton porte son libellé dans la page). Écris-le dans le storyboard : « objet → nouveau rôle ».
- À défaut, **le vecteur** : même direction, même flou, chevauchement 0,1–0,3 s. Un zoom garde le signe de
  d(échelle)/dt de part et d'autre.
- Morph : rétrécir 2 à 4 fois plus vite qu'on ne s'étend. Jamais deux copies du même objet à l'écran.
- La couture tombe **au sommet du flou** d'un mouvement ; aucun élément ne naît ni ne meurt dans les 2 images autour.
- Une coupe ne tombe jamais sur une image vide : la scène entrante est visible dès sa première image.
- Aplat (flood) : cercle né de l'objet source, qui doit couvrir le coin le plus lointain (×1,05) en 0,3–0,35 s.

Dans `video.json`, la couture passe par `transition_in` :

| Valeur | Usage | Quota |
|---|---|---|
| `cut` | défaut ; continuité portée par les blocs (même objet, même vecteur) | coupes « franches » (changement de monde) 0–4 en voix narrative |
| `push`, `rise`, `wipe` | vecteur de sortie repris à l'entrée, même direction tout l'acte | libre si motivé |
| `zoom` | plongée dans l'objet-pont (mot, pastille, zéro) | 1–3 |
| `iris` | pivot ou sortie de fin | 1–2 |
| `fade` | jamais entre deux idées ; seulement respiration voulue | 0–2 par film |

## 8. Caméra

Deux façons de filmer ; tranche par type :
- **Caméra active (launch, project, cinematic, style)** : la caméra ne s'arrête jamais (dérive + crans datés vers ce qui
  arrive), zooms francs, whips flous. Énergie, événements.
- **Caméra par soustraction (explainer long, voix posée)** : « mouvement par soustraction ». Une seule courbe d'échelle par scène,
  1,00→1,04–1,06 (ou l'inverse), `sine.inOut`, sans x/y/rotation/flou ; une tenue peut être immobile si la caméra
  respire. Le spectateur écoute : le décor ne doit pas l'arracher au propos.

Communes aux deux :
- Jamais d'aller-retour sur le décor ; un zoom franc dans un seul sens est bienvenu. Zoom interpolé en espace
  logarithmique ; jamais zoom avant puis arrière dos à dos.
- La caméra isole **le sujet de la phrase** ; l'ensemble ne se montre que quand il a du sens.
- Une dérive ne se lit que sur un fond texturé (grain, trame de points) ; un aplat la cache.
- Textures fines hors des couches mises à l'échelle (points ≥ 2,5 px, pas ≥ 32 px), sinon le rendu « grouille ».
- La dernière clé d'une courbe tombe **après** la fin de scène, sinon les 0,8 s finales ralentissent jusqu'à l'arrêt.
- Flou de sortie seulement sur fond sombre ; sur fond clair il grise l'image (fondre, ne pas flouter).

## 9. Typographie en mouvement

- **Sous-titres** (`captions`) : en bas au centre, mot par mot (gris → encre sur le mot dit, runtime `MF.captions`),
  morceaux de `captionChars` signes au plus (42 en 16:9, 22 en 9:16), ≥ 0,7 s à l'écran, ≤ 17 signes/s, rien
  d'autre dans leur bande. Variante posée (phrase entière, sans animation, sans ponctuation) : à préférer pour un
  explainer > 90 s où le karaoké fatigue.
- **Un mot clé par phrase**, dans l'accent (`*mot*` dans les slots qui l'acceptent), arrivé 0 à 2 images avant le
  mot dit. Les pics (3–4 par film) : un trait fin sous LE mot, jamais un gros encadré ni deux accents.
- Le texte à l'écran est une **réécriture** de la voix (≤ 12 mots, souvent 2 à 6), jamais la phrase recopiée en même
  temps que le sous-titre. Certaines phrases n'ont volontairement aucun texte.
- 2 ou 3 « moments typographiques » par film où la phrase est l'image (`title-slam`, `kinetic-type`, `quote-card`).
- Révélation par masque (montée de 105 % dans un `overflow:hidden`), décalage ≈ 50 ms par mot (token `stagger`).
- Jamais de tween de `letterSpacing`, `width`, `height`, `top`, `left` : découpe en lettres et anime leur `x`.
- Titre ≤ 6 mots (lu en < 2 s) ; chiffres en `tabular-nums` ; display à −0,02 em ; un niveau hero par écran.
- Lisibilité vérifiée sur la planche à 360–390 px de large : ce qui ne se lit pas là n'existe pas.

## 10. Couleur et accent

- **Une couleur par rôle, jamais deux pour le même rôle** : accent = mot clé, trait de pic, bouton final, curseur.
  Une seconde couleur seulement pour le négatif (rouge de douleur), ou un accent par acte (sombre/clair).
- Les couleurs de marques tierces n'existent qu'à l'intérieur de leurs logos ou tuiles d'outils.
- Couleurs sémantiques (vert/rouge) seulement dans les graphiques et les états, jamais dans un titre.
- Texte secondaire en `--mf-muted` plein, jamais l'encre + opacité (contraste qui s'effondre).
- Deux mondes possibles : la douleur sur un fond, la solution sur un autre, la bascule au pivot dit « on change
  d'acte » sans un mot. Sinon un seul fond tout le film, le rythme vient du texte.
- Aucun flash plein écran coloré non motivé.

## 11. Son et image (réconciliation par type)

Deux principes opposés : « l'image ne bouge jamais pour le son » et « chaque scène sur un temps, le drop sur le moment
clé ». Les deux sont vrais, pas pour le même film :

| Type | Horloge | Règle |
|---|---|---|
| launch, project, explainer | **la voix** (`words.json`) | l'image se cale sur les mots ; les SFX se calent sur les **gestes** visuels ; la musique s'adapte (`music.drop_at` sur le premier mot de la solution) et ne dicte aucune coupe |
| cinematic, style (sans voix) | **la musique** (`mf music`) | scènes et coupes sur la grille de temps, drop sur la révélation clé ; une révélation peut glisser de ≤ 0,15 s (≤ 0,10 s pour un petit élément) pour tomber sur un temps |
| opener | **la frappe** | un clic par caractère visible, rien pendant les tenues |
| remake | **la référence** | temps de coupe de la référence ; jamais sa musique ni sa voix |

- SFX : sec, ≤ 1 par image, jamais deux sons empilés au même instant ; un seul son **signature** sur le moment clé.
  Clic sur les clics, pop sur ce qui atterrit, whoosh court sur les transitions (riser avant, rien sur le point
  d'impact), frappe : sous une voix, un seul tapis clavier coupé à la longueur de la frappe ; sans voix, clic par
  caractère, gain et hauteur légèrement variés. Pas de « ding » final ni d'impact lourd gratuit.
- Les SFX se placent par leur **pic mesuré** (c'est ce que fait `mf audio`) ; les poser dans les respirations de
  ~0,3 s entre phrases, sinon la voix les masque.
- Musique : tension jusqu'au pivot prise dans une partie **pleine** du morceau, 2 à 3 dB sous l'élan au plus ;
  impact grave au pivot ; l'élan revient sur le drop ; `duck_db` ≈ −9 sous la voix ; fondu de 2,5 s sur la carte de
  fin ; mix final −14 LUFS (`mf audio`). Jamais de musique générée.

