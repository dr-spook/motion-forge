# Monde : mettre en scène un film continu (`video.json` → `world`)

Les films produit de référence coupent très peu (0 à 2 coupes par 10 s) : ce sont des **mondes qui se
transforment**, pas des suites de pages. `world` décrit ce monde ; les `scenes` (blocs) restent possibles par-dessus,
comme moments préfabriqués. Un film peut n'avoir **que** un monde (`"scenes": []`).

Sommaire : 1. Structure · 2. Objets · 3. Actions · 3 bis. Objets-métaphores · 3 ter. Formes et morph de tracés · 4. Caméra et vie continue · 5. Règles qui font la qualité · 6. Principes de composition · 7. Profil, planche et contrôle du rythme · 8. Exemples · 9. Pièges

## 1. Structure

```json
"world": {
  "background": { "kind": "solid | gradient | glow", "colors": ["#E3E8FF", "#FFE9DE"], "angle": 160 },
  "drift": 0.008,
  "camera": [ { "at": "s:3.w2-0.2", "dur": 0.9, "zoom": 1.8, "x": 0.66, "y": 0.5, "ease": "expo.inOut" } ],
  "objects": [ { "id": "titre", "kind": "text", "text": "…", "actions": [ … ] } ]
}
```

- Coordonnées `x`, `y` : fraction du cadre (0–1), centre de l'objet. Tailles `size`, `w`, `h` : en **u** (1 % du
  petit côté du format), donc elles suivent le format.
- **Valeur par format** pour tout nombre de position ou de taille : `"x": {"16:9": 0.66, "9:16": 0.7}` (clé
  `default` en repli). C'est ainsi qu'un même monde se recompose en 9:16 sans recadrage.
- `at` accepte les ancres de phrase (`"s:3"`, `"s:3.w2-0.2"`, `"s:3.end"` ; syntaxe : `storyboard.md` § 7) : le film
  suit la voix verrouillée et survit à l'édition des autres phrases. L'ancienne forme `w:N` reste lue.
- Couleurs : jetons de style (`fg`, `bg`, `accent`, `muted`, `surface`, `line`) ou `#hex`.

## 2. Objets (`kind`)

| kind | Champs utiles | Usage |
|---|---|---|
| `text` | `text` (`*mot*` = accent), `size`, `font` (display/body/mono/serif), `weight`, `color`, `w` (largeur → retour à la ligne), `align` | la phrase dite, un titre, un compteur |
| `shape` | `shape` (forme nommée, `line` ou `path`), `w`, `h`, `fill`/`color`, `d` (path), `text` (libellé, ex. bouton) | bouton, pastille, soulignement, connecteur, illustration flat |
| `prop` | `prop` (battery, clock, calendar, notifs, price, strike), `value`, `w`, `label`… (§ 3 bis) | objet-métaphore : une idée lisible sans un mot |
| `card` | `src` (capture → fenêtre avec barre), ou `text`, `w`, `fill` | fenêtre d'app, carte |
| `image` | `src`, `w`, `h`, `shape: circle` (avatar), `shadow` | photo, logo PNG, avatar |
| `svg` | `src` (fichier .svg, nettoyé à la compilation), `w`, `color` ; ses éléments à `id` sont des **pièces** animables (`part`) | logo vectoriel, illustration, icône, logo-reveal |
| `cursor` | `size`, `color` | le curseur qui clique |

Communs : `layer` (`back` / `mid` / `front`, parallaxe 0,6 / 1 / 1,5 sous la caméra), `rotate`, `glow`, `shadow`,
`visible`, `drift` (`{"x","y","scale","rotate"}` par seconde : la tenue ne fige jamais).
Un objet qui a une action `enter`, ou qui est la cible d'un `morph`, commence invisible.

## 3. Actions (`do`)

| do | Paramètres | Effet |
|---|---|---|
| `enter` | `from` rise/drop/pop/blur/left/right/scale/fade/fly/tilt | apparition (`tilt` : bascule en perspective, carte qui se redresse) |
| `exit` | `to` (mêmes valeurs) | sortie, plus légère que l'entrée |
| `move` | `x`, `y`, `scale`, `rotate`, `rotateX`, `rotateY`, `opacity` | déplacement (courbe `expo.inOut` par défaut) ; `rotateX`/`rotateY` inclinent l'objet en perspective (UI 2,5D) |
| `type` | `cps` (caractères/s, défaut 14) | frappe caractère par caractère, curseur texte qui clignote un nombre fini de fois |
| `words` | `stagger` | mot à mot, chaque mot monte net depuis un flou |
| `assemble` | `stagger` | les lettres arrivent de tout le cadre et convergent pour former la phrase (marque, révélation) |
| `rewrite` | `text` | le texte se réécrit en place (brouillage seedé, déterministe) |
| `count` | `value`, `decimals`, `prefix`, `suffix` | le nombre du texte roule jusqu'à `value` |
| `draw` | `stagger` | les tracés de l'objet (path, line, svg) se dessinent |
| `morph` | `to` (id d'objet) | l'objet devient un autre : il vole vers sa place et sa taille, l'autre prend le relais |
| `morph` (tracé) | `to` (forme nommée ou pièce du SVG) ou `d`, `fill`, `part`, `shapeIndex` | la forme elle-même se transforme (§ 3 ter) |
| `set` (prop) | `value` | l'état de l'objet-métaphore glisse vers `value` (§ 3 bis) |
| `orbit` | `cx`, `cy`, `r` (fraction du petit côté), `angle` (°), `turns` | trajectoire circulaire |
| `flood` | `to` (couleur), `target` (objet d'origine) ou `x`, `y` | aplat qui envahit le fond en cercle depuis un point |
| `pulse` / `press` | `scale`, `target` | battement / appui |
| `click` (cursor) | `target` | le curseur arrive en courbe, clique, onde, la cible réagit |

`dur` et `ease` sont optionnels partout (durées par défaut raisonnables). Sur un objet `svg`, `part: "<id>"`
applique `enter`, `exit`, `pulse`, `draw` ou `morph` à une seule pièce du fichier : l'illustration se construit morceau
par morceau. Une entrée de pièce ne cache que la pièce, pas l'objet.

## 3 bis. Objets-métaphores (`kind: "prop"`)

Un objet-métaphore dit une idée sans phrase : le temps qui file, l'énergie qui s'épuise, le chaos qui se range. Son
état est **un seul nombre**, initialisé par `value` et déplacé par l'action `set` (`{"at", "do": "set", "value", "dur",
"ease"}`) ; plusieurs `set` s'enchaînent. Toutes les autres actions (enter, move, pulse, exit…) s'appliquent aussi.

| prop | État (`value`) | Ce qui se voit | Champs utiles |
|---|---|---|---|
| `battery` | niveau 0–1 (défaut 1) | jauge pleine → ambre → rouge ; éclair pendant une recharge | `w` (22), `fill` (couleur pleine), `label` (`""` masque le %) |
| `clock` | heure décimale (défaut 9 ; 17.5 = 17 h 30) | aiguilles ; 9 → 19 en 1,5 s = le temps s'emballe | `w` (22), `label` |
| `calendar` | jour 1–31 (défaut 1) | l'anneau saute de jour en jour, les jours franchis se barrent | `w` (30), `label` (mois), `color` (croix) |
| `notifs` | chaos 1 → 0 (défaut 1) | cartes éparpillées et agitées → pile rangée | `items` (≤ 8 titres), `w` (38), `spread` (0,2–1,5) |
| `price` | prix (défaut 0) | étiquette qui roule jusqu'au prix et se balance à chaque changement | `w` (26), `prefix`, `suffix` (`" €"`), `decimals`, `label`, `fill` |
| `strike` | trait 0–1 (défaut 0) | le mot se barre à la main et pâlit | `text` (requis), `size`, `fill` (couleur du trait) |

Un chiffre illustratif (prix, pourcentage) reste soumis à la loi « vérité d'abord » : sans fait, écris « exemple » dans
le `label`. La valeur est une fonction pure du temps (comme la caméra) : aucun risque à rembobiner.

## 3 ter. Formes et morph de tracés

Formes nommées (`shape` ou cible de morph) : `circle`, `rect`, `pill`, `triangle`, `diamond`, `hexagon`, `star`,
`heart`, `check`, `cross`, `arrow`, `drop`, `blob`, `bolt`. Toutes sont des tracés pleins : **n'importe laquelle peut
devenir n'importe quelle autre**. `shape: "path"` est un trait (`color`) ; avec `fill`, un tracé plein.

- Forme → forme : `{"do": "morph", "to": "heart", "fill": "#E5484D", "dur": 0.8}` (couleur optionnelle, enchaînable).
- Tracé libre : `"d": "M0 0 L…"` dans le repère de la boîte de l'objet (pixels de `w` × `h`).
- Logo-reveal avec un SVG à pièces nommées : le fichier contient la forme de départ et la forme d'arrivée,
  `{"do": "morph", "part": "seed", "to": "tile"}` ; la forme cible est masquée automatiquement. Puis `enter` sur
  la lettre (`part: "mark"`), `draw` sur un contour (`part: "ring"`). Modèle : `examples/metaphors-demo/assets/facturo-logo.svg`.
- `mf lint` refuse une forme inconnue, une pièce absente du fichier (avec la liste des pièces), un groupe `<g>` comme
  pièce à morpher, une `line` à morpher. `shapeIndex` (entier) corrige un morph qui se tord.

## 3 quater. Personnages (marionnette découpée)

Un personnage 2D se joue avec les primitives ci-dessus : SVG à pièces nommées (`part`) pour les expressions et la
bouche, objets séparés superposés (`layer`) pour un bras ou un accessoire qui tourne (`move`), un PNG par pose
relayé par `morph` vers un autre objet. La bouche « parle » par une alternance de `morph` ancrée sur les mots de ses
répliques (`s:N.wK`). Pas de squelette, de cycle de marche ni de synchro labiale : `apports.md` § 5 (dont les droits).

## 4. Caméra et vie continue

Clés `{at, dur, zoom, x, y, rotate, target}` : la caméra amène le point (`x`, `y`) ou l'objet `target` au centre, au
zoom voulu ; zoom interpolé en logarithme ; parallaxe par calque. `world.drift` ajoute une poussée continue (0,005 à
0,012 = +0,5 à +1,2 %/s) : le monde respire même pendant une tenue. Jamais un zoom avant puis arrière dos à dos
sans raison ; une plongée dans un mot (zoom 1,6–2,2 sur le mot clé) est un temps fort, une ou deux fois par film.

**Vie continue (par défaut)** : caméra portée légère (`world.float`, amplitude 0,015 du cadre), flottement borné de
chaque objet sans `drift`, taches du fond `glow` qui dérivent, halo d'accent qui suit le caret pendant une frappe.
`"float": false` pour un plan volontairement fixe (affiche, opener noir). C'est ce qui a fait passer la démo de 41 % à
21 % d'images figées (mesure des références) : la vie n'est pas un effet ajouté, c'est l'état normal du monde.

## 4 bis. Son du monde (automatique)

Chaque geste notable pose un son, calé pour que son pic tombe sur l'image où le geste se voit (`mf audio` aligne le
pic) : `type` → une touche par lettre (instants identiques à ceux du runtime, donc chaque son tombe sur sa lettre) ;
`click`, `press` → clic ; `enter` `pop`/`scale` → pop, `drop` → tic à l'atterrissage ; `flood`, `assemble` →
whoosh ; `morph` → pop léger ; `set` d'un calendrier, d'une horloge ou d'un prix → un tic par jour barré, heure
passée ou chiffre qui change (10 tics/s au plus) ; batterie rechargée à plein → ding ; `strike` → trait.
Caméra : whoosh sur un mouvement vif et ample (zoom ×1,3 ou plus en 0,15 à 1 s). Muets par défaut : fondus,
sorties, `move`, `pulse`, `words`, `rewrite`, `draw`, `orbit` — un monde qui sonne à chaque mouvement devient une
mitraillette.

Réglages : `world.sfx: "off"` coupe tout ; sur une action, `"sfx": false` (muet), `"sfx": "ding"` (autre son, même
instant) ou `"sfx": {"kind": "impact", "gain_db": -3, "at": 0.2}` (`at` = décalage depuis le début de l'action) ; sur
une clé de caméra, `"sfx": false` ou un nom. Un son nommé sur un geste muet par défaut se pose à son début. Usage :
un seul accent par temps fort (le logo qui se pose, le chiffre final), pas un son de plus sur chaque geste.
Les événements sont listés dans `build/<fmt>/mf-manifest.json` (`source: "world"`) ; `mf audio` les mixe avec la voix
et la musique et rapporte les sons écartés (deux sons identiques à moins de 80 ms).

## 5. Règles qui font la qualité (mesurées sur les références)

- **Un objet persiste et change de rôle** au lieu d'être remplacé : le bouton devient la fenêtre (`morph`), le titre
  monte et rétrécit pour laisser la place (`move`), la fenêtre sert d'origine à l'aplat (`flood`).
- **~1 événement par seconde** dans un film produit (0,9–1,3 mesuré) : une action notable par seconde environ.
- **Aucune tenue figée** : donne un `drift` aux objets qui restent longtemps, et un `world.drift` léger.
- **La phrase dite peut être l'image** : `type` ou `words` sur la phrase, puis les objets naissent autour.
- Le curseur clique sur quelque chose qui **répond** (press, morph, flood), jamais dans le vide.
- Une seule chose importante bouge à la fois ; les orbites et dérives sont du décor, pas le sujet.

## 6. Principes de composition

- **Le contraste crée la tension** : grand/petit, plein/vide, clair/sombre, calme/rapide. Un film sans contraste ne
  retient pas le regard ; prévois au moins un renversement fort (fond qui bascule par `flood`, objet qui passe de
  minuscule à plein cadre, silence visuel avant la révélation).
- **La composition varie dans le temps** : chaque moment clé est une image forte en soi, et la suivante est
  différente (position du sujet, échelle, densité). Le profil fixe la durée maximale d'une même mise en page.
- **L'idée avant le style** : un style frame vaut par le concept qu'il montre ; si la planche est belle mais ne dit
  rien, reprends l'idée qui bouge (`direction.md` § 1) avant de retoucher le look.
- **Du mystère à la certitude** : un film commercial peut ouvrir dans l'ambiguïté (une forme, un mot, une question)
  et finir dans la certitude (le produit, la marque, l'action). La marque arrive tard et reste.
- **Naissance, vie, mort** : chaque objet entre (`enter`, `type`, `assemble`, `morph`), vit pendant sa présence
  (flottement, dérive, réaction) et sort ou se transforme. Un objet qui apparaît puis ne fait plus rien est un défaut.
- **La typographie joue** : le texte peut être l'acteur principal (frappe, convergence, réécriture, plongée).

## 7. Profil, planche et contrôle du rythme

`video.json.profile` nomme le profil visé (`profiles/<id>.json`) : saas-minimal, saas-pastel, saas-gradient,
mono-glow, affiche-editoriale, illustration-flat, geometrique-minimal. Ses seuils ont été mesurés sur des vidéos de
référence. `mf qa` mesure le rendu (images figées, tenue figée max, événements/s, coupes/10 s, même mise en page max) :
FAIL sur les images figées et les tenues, WARN sur le reste. Un WARN « événements/s » se corrige dans la spec : ajoute
une action notable (réaction à un clic, pulse, rewrite, entrée d'un objet) là où le rapport montre un creux.
Mesure isolée : `python3 py/mf_rhythm.py --video out/16x9.mp4 --profile saas-minimal`, ou `mf ref measure <video>`
pour classer tous les profils. Le profil apporte aussi une **vie continue** des scènes (`vie` : poussée de caméra
linéaire et flottement sinusoïdal sur chaque scène, surchargée par `video.json.life`, coupée par `"life": false`) :
sur Facturo elle fait passer les images figées de 48 % à 13–25 % selon le profil. C'est un remède de direction, pas
un réglage de seuil.

**Avant de rendre : `mf board`.** La planche « design board » (`video/qa/board-<format>.png`) montre une image par
moment clé (fin d'un geste important), numérotée et légendée à partir des actions, sous une frise du rythme
**prévu** : un trait par départ d'action, en rouge les creux de plus de 1,5 s sans aucun départ, et la cible du
profil. Lis-la pour chaque format : elle révèle avant rendu les objets oubliés à l'écran, les traits parasites, les
creux et une composition qui ne change pas. `"board": [{"at", "label"}]` dans la spec impose ses propres moments.
`mf board --video` refait la planche à partir du rendu. `mf snapshot` sans `--at` prend ces mêmes moments.

**Prévu n'est pas mesuré.** La frise compte des départs d'actions ; `mf_rhythm` mesure ce qui change à l'écran. Un geste
trop petit dans le cadre ne compte pas comme événement : sur la démo métaphores, 2,4 départs/s prévus donnaient
0,58 événement/s mesuré en 16:9, corrigé en **agrandissant les gestes** (caméra qui plonge sur la commande tapée,
logo révélé par un recul depuis ×2, objets plus grands) → 1,17. Ne baisse jamais un seuil de profil pour faire passer
un film : les seuils viennent des références.

## 8. Exemples

`examples/world-demo/video.json` (10 s, 16:9 + 9:16, sans voix) : frappe de la phrase → plongée de caméra dans le mot
accent + soulignement tracé → le titre monte → bouton → clic du curseur → le bouton devient une fenêtre d'app →
trois pastilles de formats en orbite → aplat d'accent depuis la fenêtre → compteur → marque mot à mot.
Pars de ce fichier, remplace le contenu, garde la grammaire.

`examples/metaphors-demo/video.json` (12 s, 16:9 + 9:16, profil saas-minimal, QA rythme OK dans les deux formats) :
notifications en chaos → elles se rangent sur le côté pendant que le calendrier se barre, que l'horloge s'emballe et que
la batterie se vide → plongée vers la batterie → la batterie grandit au centre → « Relancer à la main » se barre →
commande tapée en gros plan → recharge, étiquette de prix → aplat sombre → logo révélé (point → tuile, F, anneau) et
marque assemblée. Montre les 6 props, le morph de pièce et la planche.

## 9. Pièges

- `type` réserve la place de la phrase finale : une phrase centrée se tape depuis sa gauche finale. Pour une phrase
  qui pousse depuis le centre, préfère `words`.
- `type` suppose une seule ligne (pas de `w`) ; pour un texte long, `words` avec `w`.
- `morph` déforme le contenu pendant le vol : il est fait pour une forme simple → une fenêtre/carte, pas texte → texte
  (pour ça : `rewrite`).
- Un objet hors cadre au repos (y > 1) ne se voit pas ; un `move` vers y = 1,1 est une sortie propre.
- `notifs` en chaos occupe une grande partie du cadre (`spread`) : range-les (`set` 0) ou déplace-les avant d'amener
  d'autres objets.
- Un geste qui ne compte pas à la mesure est presque toujours un geste trop petit : grossis-le (caméra, `scale`).
- Deux compteurs qui tournent en même temps donnent deux trains de tics entrelacés : `mf audio` écarte ceux à moins
  de 80 ms ; si le résultat bourdonne, coupe l'un des deux (`"sfx": false` sur son `set`).
- `mf lint` contrôle les références (`target`, `to`), les usages (`click` réservé au curseur, `type` au texte) et
  les ancres ; `mf snapshot --at …` montre les états clés avant tout rendu.
