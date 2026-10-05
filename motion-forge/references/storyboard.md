# Storyboard : du brief au `video.json`

Le storyboard s'écrit **avant** toute animation ; `video.json` en est la traduction mécanique. Corriger une ligne
de storyboard coûte dix fois moins qu'un rendu.

Sommaire : 1. La chaîne · 2. Brief du réalisateur · 3. Le plan des moments · 4. Fiches de scène · 5. Choisir les blocs ·
6. Règles de timing · 7. Ancrer sur les mots · 8. Exemple complet (35 s, CLI fictive)

## 1. La chaîne (ordre imposé)

brief → `facts.json` (`mf scan`, faits de l'utilisateur en `source: "user"`) → script validé (G2, `script.md`) →
voix → `timing/words.json` (`mf align`) → plan des moments → fiches de scène → `scenes[]` → `mf lint` → `mf snapshot` (G3).
Toute modification de la voix invalide les ancres : relance `mf align`, puis `mf lint`. Une seule source de durée :
`words.json` (ou la grille musicale en cinematic). **Ne calcule jamais une somme de durées de tête** : `mf lint` et
`mf-manifest.json` font foi.

## 2. Brief du réalisateur (premier livrable, puis STOP pour accord)

```
BRIEF — <titre>
Durée / format maître / déclinaisons : 35 s · 16:9 · 9:16 (même timeline, recomposé, jamais rogné)
Sujet + promesse en une ligne : …           Public : …           Canal : landing / LinkedIn / README
Style de référence NOMMÉ : « lancement Linear », « docs Stripe », « bumper Apple » (jamais « moderne premium »)
Style motion-forge : dark-saas | paper | kinetic-mono | glow-neon | noir   Accent : #……
L'idée qui bouge : « On voit A devenir B ; c'est la preuve que … » (direction.md § 1)
États datés : 0–2,5 s accroche (type) → 2,5 s la forme devient l'écran 1 → … → preuve avec un vrai chiffre (f-0xx)
              → logo + URL (retour à l'état 0 si boucle)
Calques : fond (texture) / sujet / UI / texte / curseur / avant-plan flou
Plan sonore : voix (fichier | kokoro | aucune) · musique (fichier, drop sur …) · SFX (liste courte) · ou silence
Faits mobilisés : f-001, f-004, … ; données d'illustration étiquetées « Exemple »
Sortie attendue : 6 à 10 moments + liste de calques + plan sonore
```

## 3. Le plan des moments

Avant les scènes, découpe le film en **moments** : un moment, c'est un changement qu'on veut faire voir. Pour
chacun, remplis une ligne :

| Colonne | Ce qu'on y écrit |
|---|---|
| Quand | ancres de début et de fin (`s:N`, `s:N.wK`), ou secondes |
| À quoi il sert | accroche, problème, bascule, démonstration, preuve, fin |
| Ce qui change | l'état de départ et l'état d'arrivée, nommés tous les deux |
| Qui le porte | l'objet principal qui fait le changement |
| Où l'on regarde | caméra et profondeur (poussée, panoramique, calques) |
| Ce qui est écrit | rien, un sous-titre, un mot mis en avant, un chiffre |
| Ce qu'il faut | capture, SVG, icône, rien |
| Le piège | ce qui ferait de ce moment une diapositive, en une phrase |

Si « ce qui change » se résume à « apparaît », le moment est à réécrire. La colonne « le piège » se remplit
toujours : un piège qu'on n'a pas nommé finit à l'écran.

## 4. Fiches de scène

Une fiche par scène, assez précise pour qu'un autre puisse la construire sans te poser de question. Exemple réel
(VoxText, 9:16) :

```
s04 · « Appui long, Partager, VoxText. » · s:4-0.35 → s:5-0.1 · démonstration · cursor-demo · énergie 3
Départ      : « Lis-le. » monte et s'efface pendant que le téléphone se lève sur ressort
Changements : s:4.w0 le doigt se pose sur la bulle (anneau) → s:4.w2 la feuille de partage monte
              → s:4.w3 tap sur l'icône, halo violet
Arrivée     : l'icône VoxText éclairée, la caméra s'est rapprochée d'elle
Caméra      : montée sur ressort, puis légère poussée vers l'icône
Écrit       : une pastille par geste (1 Appui long · 2 Partager · 3 VoxText) + sous-titres
Son         : deux taps, un souffle à la montée de la feuille
Relais      : la bulle sur laquelle on appuie est celle de l'accroche
Faits       : f-003           Piège : trois captures fixes enchaînées sans doigt
```

Chaque fiche répond à trois questions : **le décor** (jamais un fond vide), **le sujet** (un seul à la fois, qui
laisse la place quand il a fini), **le texte** (les sous-titres et au plus un mot mis en avant). Recopie aussi les
`pitfalls` de chaque bloc choisi (lus dans son `block.json`) et vérifie-les sur les images de contrôle.

## 5. Choisir les blocs (sémantique → bloc)

Pour chaque phrase du script, demande-toi ce qu'elle fait, puis prends le bloc fait pour ça (`semantics` dans
`block.json` ; liste à jour : `mf blocks`).

| La phrase… | Sémantique | Blocs |
|---|---|---|
| ouvre, nomme la cible, claque une promesse | reveal, problem | `title-slam`, `kinetic-type`, `typewriter-opener` |
| nomme la marque | brand | `logo-wordmark` |
| montre le produit qui marche | demo | `screen-showcase`, `cursor-demo`, `ui-float`, `terminal-type` |
| montre du code / une config | explain, demo | `code-card`, `terminal-type` |
| pointe un détail précis | focus | `highlight-zoom`, `screen-showcase` (pan) |
| donne un chiffre | count, prove | `metric-counter`, `bar-chart` |
| oppose avant/après, A/B | compare | `split-compare`, `bar-chart` |
| énumère sans ordre | list | `feature-grid`, `list-steps` |
| décrit des étapes | sequence | `list-steps`, `cursor-demo` |
| cite quelqu'un ou une phrase-clé | quote | `quote-card`, `kinetic-type` |
| change de chapitre | transition | `chapter-card` |
| conclut, appelle à l'action | end | `cta-end` |

- Chaque scène a **une seule mission à l'image** (accrocher, montrer, prouver, comparer, conclure) ; deux
  missions font deux scènes.
- Les bornes de chaque bloc font foi (`duration.min/max`, `max_chars` des slots) ; au-delà de six mots, un titre
  se répartit sur deux scènes.
- Varie les blocs : pas trois fois le même d'affilée, et aucun ne dépasse le tiers des scènes d'un film qui en
  compte six ou plus.
- Une phrase qui précise la précédente fait évoluer ce qui est déjà à l'écran au lieu d'ajouter un élément.
- Un mot de bascule (« Stop. », « Mais… ») commence une scène neuve : coupe juste avant lui.
- On choisit un bloc pour ce que la phrase fait, jamais pour son allure ; l'intensité (`energy`) sert ensuite à
  dessiner la courbe (`direction.md` § 6).

## 6. Règles de timing

- Débit français : **2,6 à 2,8 mots/s** (≈ 160 mots/min), silences compris hors gag et pivot. 35 s ≈ 60–70 mots.
- **Accroche ≤ 3 s** : la cible ou sa douleur est nommée et montrée avant 3 s ; première composition ≤ 3 s.
- Scène ≥ `duration.min` du bloc et ≥ 1,2 s ; une composition nouvelle toutes les 1 à 4 s ; jamais la même mise en
  page plus de 3 s ; un événement toutes les 0,5–1 s.
- Tout texte reste lisible ≥ 1,5 s après sa pose complète (2 s pour un nom + une fonction).
- Chaque silence > 0,4 s est une étape avec action muette (gag de 2–3 s, pivot de 0,6–1,5 s).
- **Bande de protection** : aucun événement ancré à moins de 0,5–0,7 s de la fin de sa scène (la transition
  l'avalerait) ; avance-le ou passe-le à la scène suivante.
- **CTA** : carte de 3 à 6 s, dont 2 à 3 s de tenue vivante après le clic ; `end` de la dernière scène =
  `s:<dernière phrase>.end+3` à `+4`, et `"duration": "voice+3"` à `"voice+4"` (même valeur : la voix fixe la durée).
- Logo complet jamais avant 5 s, sauf s'il est un objet du récit qui se transforme aussitôt.

## 7. Ancrer sur la voix (`s:N`)

Audio d'abord : on n'ancre que sur une voix **verrouillée** (`mf voice lock`, après écoute) et on lit d'abord sa carte,
`qa/voice-board.png` (`mf voice board`) : chaque phrase y porte son ancre `s:N` et chaque mot son index `wK`.

Syntaxe : `"s:3"` = début du premier mot de la phrase 3 (phrases comptées depuis 0) ; `"s:3.end"` = fin de son dernier
mot ; `"s:3.w2"` = début de son mot 2 (mots comptés depuis 0 dans la phrase) ; `"s:3.w2.end"` = fin de ce mot ;
`+0.3` / `-0.3` = décalage en secondes. Une fois `words.json` présent, plus aucune seconde tapée à la main dans
`start`, `end`, `sfx[].at`, `at` du monde ou `music.drop_at`.

Pourquoi des phrases : une ancre `s:N` survit à l'édition des **autres** phrases (ajouter un mot à la phrase 0 ne
déplace pas la scène ancrée en `s:4`). L'ancienne forme `w:N` (index global du mot) reste lue mais glisse d'un mot à
chaque mot ajouté avant elle : `mf anchors --to-sentence` convertit une spec, `mf anchors` liste ce que chaque ancre
désigne.

| Type d'événement | Écart image / voix | Ancre typique |
|---|---|---|
| Mot-image (objet, métaphore, chiffre) | image 0,1–0,6 s avant | `s:N.wK-0.3` |
| Texte mot à mot | 0–0,1 s avant | automatique (captions, slots) |
| Titre de chapitre, logo, pilier | 0,5–2 s avant | `s:N-0.8` |
| Impact (contact, clic) | sur la syllabe accentuée ±0,1 s | `s:N.wK+0.1` |
| Changement de scène | premier mot de l'idée ±0,1 s, ou dans le silence d'avant | `s:N-0.15` |

- Une scène commence là où la précédente finit : `end` de N = `start` de N+1, mêmes ancres.
- Une idée = une phrase : si une scène doit couper au milieu d'une phrase, c'est souvent le texte qu'il faut couper
  (deux phrases), avant le verrou.
- Les phrases à réécouter (cadre rouge sur la carte, flags de `words.json`) se vérifient à l'oreille avant d'y
  ancrer une coupe.
- Avant voix : écris le storyboard en phrases (`s:N`), pas en secondes ; les temps viennent de la voix verrouillée.
- Le texte change après le verrou : `mf voice --unlock`, nouvelle voix, `mf align`, écoute, `mf voice lock`, puis
  `mf anchors --rebase` (recale les ancres des phrases inchangées ; celles d'une phrase réécrite sont listées).

## 8. Exemple complet : « notch », CLI fictive, film projet de 35 s

Faits (`facts.json`, extrait) : f-001 name `notch` (package.json:2) · f-002 tagline « Ton changelog s'écrit tout
seul » (README.md:3) · f-003 command `notch release` (README.md:14) · f-004 feature « classe feat / fix / breaking
(Conventional Commits) » (src/classify.ts:12) · f-005 feature « chaque entrée renvoie vers son commit »
(src/render.ts:40) · f-006 command `npm i -g notch` (README.md:9). Le « 300 commits » est un scénario et les
« 40 s » n'ont pas de fait : tous deux portent l'étiquette **Exemple** à l'écran.

Idée qui bouge : « on voit un `git log` interminable devenir un seul CHANGELOG propre ; c'est la preuve qu'une commande suffit. »
Phrases (carte `mf voice board` après `mf voice lock`, temps indicatifs) : s:0 « Vendredi, dix-huit heures. » ·
s:1 « Tu dois publier… » · s:2 « Et le changelog ? » · s:3 « Trois cents commits… » (fin 7,00 ; gag 7,0–9,4) ·
s:4 « Stop. » (9,40) · s:5 « Avec notch, une seule commande… » (11,20 ; w2 = « une », 11,90) · s:6 « Fonctionnalités… »
(15,40) · s:7 « Trois cents commits, triés… » (19,80) · s:8 « Et chaque ligne… » (22,75) · s:9 « notch. » (25,20) ·
s:10 « Ton changelog… » · s:11 « Installe-le en une ligne. » (28,10 ; fin 29,45).

| # | Ancres | Rôle | Qui porte → ce qui change | Bloc | Transition | Piège |
|---|---|---|---|---|---|---|
| s01 | 0 → s:1 | accroche | « Vendredi, 18 h » se tape mot à mot, *18 h* passe à l'accent | kinetic-type | — | titre posé |
| s02 | s:1 → s:3 | accroche | le terminal tape `git tag v2.0.0`, puis `cat CHANGELOG.md` → vide | terminal-type | push | capture figée |
| s03 | s:3 → s:4-0.15 | douleur + gag | `git log` défile, accélère, ne finit jamais (silence 7,0–9,4) | terminal-type | cut (raccord) | log qui défile sans fin visible |
| s04 | s:4-0.15 → s:5-0.6 | pivot | « Stop. » claque sur noir, tout s'arrête | title-slam | cut (franche) | — |
| s05 | s:5-0.6 → s:5.w2 | marque | le mot-marque s'assemble, son point devient un curseur | logo-wordmark | iris | logo en signature |
| s06 | s:5.w2 → s:6 | solution | `notch release` se tape, la sortie monte ligne à ligne | terminal-type | zoom | texte qui apparaît d'un bloc |
| s07 | s:6 → s:7 | preuve | les lignes deviennent des cartes triées dans 3 colonnes | feature-grid | rise | 3 cartes qui fondent ensemble |
| s08 | s:7 → s:8 | preuve | « 40 s » roule depuis 0, étiquette Exemple | metric-counter | rise | chiffre posé en fondu |
| s09 | s:8 → s:9-0.4 | preuve | capture de la page de release, pan vers un lien de commit | screen-showcase | rise | capture posée sans geste |
| s10 | s:9-0.4 → s:11-0.3 | marque (rime) | le logo de s05 rejoué à l'identique + tagline | logo-wordmark | zoom | — |
| s11 | s:11-0.3 → s:11.end+4 | CTA | carte de fin : la commande se tape dans la pastille, anneau de pouls | cta-end | cut (raccord) | carte tenue ≥ 2 s |

Contrôles : 1 coupe franche (s04, changement d'acte), 2 zooms, 1 iris, 0 fondu ; terminal-type 3 fois sur 11
(≤ 1/3) mais jamais 3 de suite ; douleur plus rapide (4 scènes en 10,6 s) que la solution (7 scènes en 22,9 s) ;
rime s05 = s10 ; durée `voice+4` ≈ 33,5 s (affichée par `mf lint`).

```json
{
  "version": "0.2",
  "type": "project",
  "title": "notch, lancement",
  "seed": 7,
  "fps": 30,
  "formats": ["16:9", "9:16"],
  "gif": true,
  "language": "fr",
  "style": "dark-saas",
  "brand": {"name": "notch", "font": "Space Grotesk"},
  "facts": "facts.json",
  "timing": "timing/words.json",
  "script": [{"text": "Vendredi, dix-huit heures. Tu dois publier la version deux.", "role": "hook"}, {"text": "Et le changelog ? Trois cents commits à relire, à la main.", "role": "diagnosis"}, {"text": "Stop.", "role": "other"}, {"text": "Avec notch, une seule commande lit tes commits et rédige le changelog.", "role": "solution", "facts": ["f-001", "f-003"]}, {"text": "Fonctionnalités, correctifs, ruptures : chaque commit trouve sa place.", "role": "proof", "facts": ["f-004"]}, {"text": "Trois cents commits, triés en quarante secondes.", "role": "proof"}, {"text": "Et chaque ligne renvoie vers son commit.", "role": "proof", "facts": ["f-005"]}, {"text": "notch. Ton changelog s'écrit tout seul.", "role": "cta", "facts": ["f-002"]}, {"text": "Installe-le en une ligne.", "role": "cta", "facts": ["f-006"]}],
  "voice": {"source": "kokoro"},
  "music": {"file": "assets/music.mp3", "drop_at": "s:5", "duck_db": -9, "gain_db": -2},
  "captions": {"enabled": true, "position": "bottom"},
  "duration": "voice+4",
  "scenes": [
    {"id": "s01-hook", "block": "kinetic-type", "start": 0, "end": "s:1", "slots": {"text": "Vendredi, *18 h*"}},
    {"id": "s02-tag", "block": "terminal-type", "start": "s:1", "end": "s:3", "transition_in": "push", "slots": {"lines": [{"cmd": "git tag v2.0.0"}, {"cmd": "cat CHANGELOG.md"}, {"out": "(vide)"}]}, "sfx": [{"kind": "key", "at": "s:1"}]},
    {"id": "s03-gag", "block": "terminal-type", "start": "s:3", "end": "s:4-0.15", "transition_in": "cut", "slots": {"lines": [{"cmd": "git log --oneline"}]}, "sfx": [{"kind": "riser", "at": "s:3.end"}]},
    {"id": "s04-stop", "block": "title-slam", "start": "s:4-0.15", "end": "s:5-0.6", "transition_in": "cut", "slots": {"title": "*Stop.*"}, "sfx": [{"kind": "impact", "at": "s:4"}]},
    {"id": "s05-logo", "block": "logo-wordmark", "start": "s:5-0.6", "end": "s:5.w2", "transition_in": "iris", "facts": ["f-001"], "slots": {"brand": "notch"}},
    {"id": "s06-release", "block": "terminal-type", "start": "s:5.w2", "end": "s:6", "transition_in": "zoom", "facts": ["f-003"], "slots": {"lines": [{"cmd": "notch release"}, {"out": "✓ 300 commits lus"}, {"out": "✓ CHANGELOG.md écrit"}]}, "sfx": [{"kind": "key", "at": "s:5.w4"}, {"kind": "ding", "at": "s:5.w11"}]},
    {"id": "s07-tri", "block": "feature-grid", "start": "s:6", "end": "s:7", "transition_in": "rise", "facts": ["f-004"], "slots": {"items": [{"title": "Fonctionnalités", "body": "Les nouveautés, rangées par commit."}, {"title": "Correctifs", "body": "Chaque bug corrigé, avec son lien."}, {"title": "Ruptures", "body": "Ce qui casse, signalé en premier."}]}, "sfx": [{"kind": "pop", "at": "s:6"}, {"kind": "pop", "at": "s:6.w1"}, {"kind": "pop", "at": "s:6.w2"}]},
    {"id": "s08-chrono", "block": "metric-counter", "start": "s:7", "end": "s:8", "transition_in": "rise", "slots": {"value": 40, "label": "pour 300 commits", "suffix": "s", "delta": "Exemple"}},
    {"id": "s09-liens", "block": "screen-showcase", "start": "s:8", "end": "s:9-0.4", "transition_in": "rise", "facts": ["f-005"], "slots": {"capture": "assets/captures/release.png", "caption": "Chaque ligne → son commit", "pan": "down", "url": "notch.dev/releases/v2.0.0"}},
    {"id": "s10-rime", "block": "logo-wordmark", "start": "s:9-0.4", "end": "s:11-0.3", "transition_in": "zoom", "facts": ["f-002"], "slots": {"tagline": "Ton changelog s'écrit tout seul", "brand": "notch"}},
    {"id": "s11-cta", "block": "cta-end", "start": "s:11-0.3", "end": "s:11.end+4", "transition_in": "cut", "facts": ["f-006"], "slots": {"command": "npm i -g notch", "brand": "notch"}, "sfx": [{"kind": "click", "at": "s:11.w3"}]}
  ]
}
```

Les slots et les SFX de cet exemple sont valides pour les blocs réels (vérifié avec `mf lint`) ; les durées dépendent de ta vraie voix : si `mf lint` signale une scène plus courte que le minimum du bloc, déplace l'ancre ou fusionne la scène. La musique `assets/music.mp3` est à fournir (CC0 ou sous licence). `mf blocks --slots` et `references/blocks.md` font foi pour les slots ; les SFX disponibles sont listés par `mf sfx` (impact, whoosh, click, key, pop, riser, ding, swoosh-down, tick) et un fichier `assets/sfx/<kind>.wav` en ajoute.

