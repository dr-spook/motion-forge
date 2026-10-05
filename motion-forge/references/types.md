# Types : les 7 films de motion-forge

`video.json.type` choisit une recette : durée, arc, blocs, style, son, portes, pièges et commandes. Tout type passe
par la porte de vérité (`script.md` § 4) et par `review.md`. Portes : G1 captures · G2 script · G3 styleframes.

Sommaire : launch · project · opener · cinematic · style · explainer · remake · tableau récapitulatif

## launch — film de lancement (produit, offre, fonctionnalité)

- **Durée** : 30–60 s (cible 40–50 s) ; 16:9 maître, 9:16 recomposé.
- **Arc** : accroche datée → gag muet 2–3 s → diagnostic (3 douleurs) → pivot sur noir → marque → solution par
  gestes → preuve chiffrée → carte de fin un bouton (`script.md` § 3).
- **Blocs** : `kinetic-type` / `title-slam` → `screen-showcase`, `cursor-demo`, `ui-float` → `metric-counter` →
  `logo-wordmark` → `cta-end`. Un objet de l'accroche revient à la fin.
- **Style** : `paper` (éditorial, deux mondes papier/noir) ou `dark-saas` (produit tech).
- **Son** : voix + musique tension → silence au pivot → élan avec `music.drop_at` sur le premier mot de la
  solution + SFX sur les gestes + un son signature.
- **Portes** : G1 (si on montre l'interface), G2, GV (écoute de la voix), G3, + musique (2–3 options).
- **Pièges** : logo en ouverture ; offre détaillée (prix, étapes) ; chiffre sans fait ; capture posée sans geste ;
  interface dessinée de mémoire (celle de l'an dernier) ; même rythme douleur et solution.
- **Commandes** : `mf init` → `mf capture --url <site> --routes /,/pricing` → **G1** → script → **G2** → `mf voice`
  → `mf align` → **GV** `mf voice lock` → `mf voice board` → `mf music --file assets/music.mp3` → scènes → `mf lint` → `mf snapshot --at <images clés>` →
  **G3** → `mf make` → `review.md`.

## project — film d'un dépôt de code (README, page projet, annonce)

- **Durée** : 20–45 s ; `gif: true` pour une boucle muette de README (`out/readme.gif`, 8–15 s, lisible sans son).
- **Arc** : douleur de développeur → la commande → la sortie réelle → la preuve → l'installation.
- **Blocs** : `terminal-type`, `code-card`, `screen-showcase` (si web-app), `feature-grid`, `list-steps`,
  `metric-counter`, `cta-end` (commande d'installation). Exemple complet : `storyboard.md` § 8.
- **Style** : `dark-saas` (outil), `kinetic-mono` (CLI minimaliste), `paper` (bibliothèque, docs).
- **Son** : voix courte ou aucune ; clavier en tapis unique sous la voix ; musique légère.
- **Portes** : G1 (planche de captures ou sorties de terminal réelles), G2, GV, G3.
- **Pièges** : faits pris dans le README au lieu du code ; commande qui n'existe pas (`kind: command` obligatoire) ;
  sortie de terminal inventée sans « Exemple » ; chemins, jetons ou `.env` visibles ; GIF qui saute à la boucle
  (finir sur l'état 0 avec la même vitesse).
- **Commandes** : `mf init` → `mf scan --repo .` (relis `facts.json`) → si `type: web-app` : `mf capture --url
  http://localhost:<port> --routes <suggested_routes>` → **G1** → script → **G2** → `mf voice` → `mf align` →
  **GV** `mf voice lock` → `mf voice board` → scènes → `mf lint` → `mf snapshot` → **G3** → `mf make`.

## opener — ouverture noire, texte blanc tapé

- **Durée** : trois préréglages de `mf opener` (court ≈ 3 s, standard ≈ 5,4 s par défaut, lent ≈ 7 s).
- **Déroulé** : un instant de noir, la phrase qui s'écrit lettre après lettre, au moins une seconde de tenue, puis
  la coupe vers le film (ou le retour au noir). Pour remplacer un mot (effacer puis retaper), `mf opener` ne suffit
  pas : enchaîne deux scènes `typewriter-opener`.
- **Blocs** : `typewriter-opener` (et `kinetic-type` pour le mot remplacé).
- **Style** : `noir` (défaut de `mf opener`) ou `kinetic-mono` ; `dark-saas` quand l'opener précède un film
  dark-saas, en restant plus sobre que lui.
- **Son** : la frappe seule, un son par lettre qui s'affiche, chacun un peu différent du précédent pour ne pas
  sonner mécanique (−18 à −12 dB en crête) ; le silence partout ailleurs (noir, tenue, espaces, sortie).
- **Portes** : G2 (deux ou trois phrases courtes proposées ; la plus nette gagne).
- **Pièges** : une phrase trop longue pour la durée (au-delà d'environ 16 lettres/s, raccourcis-la plutôt que
  d'accélérer) ; une ligne qui s'affiche d'un coup ; une première image qui n'est pas noire ; un flash de couleur ;
  un texte plus petit que 9 % de la hauteur ; plus de trois états à l'écran.
- **Commandes** : `mf opener --text "…" --preset 5.4 --style dark-saas` (écrit une spec complète ; préréglages dans
  `mf opener --help`) → relis `video.json` → `mf lint` → `mf make`. Cadence par défaut : 14 lettres/s (12 pour une
  phrase dense, 14–16 pour un nom court).

## cinematic — film musical, sans voix ou presque

- **Durée** : 15–60 s.
- **Arc** : montée → **drop sur la révélation clé** (aplat, logo, grand plan) → pic → relâchement → tenue finale.
- **Blocs** : `title-slam`, `kinetic-type`, `ui-float`, `highlight-zoom`, `split-compare`, `logo-wordmark`,
  `chapter-card` ; rien de bavard.
- **Style** : `noir` ou `glow-neon` ; `dark-saas` pour un produit.
- **Son** : la musique est l'horloge. Pas d'alignement : `voice.source: "none"`, pas de `timing`, ancres en
  **secondes** sur la grille (durée d'un temps = 60 / BPM). `music.drop_at` en secondes = le moment clé. Une
  révélation peut glisser de ≤ 0,15 s pour tomber sur un temps.
- **Spec** : `"motion_blur": { "enabled": true, "subframes": 6, "shutter": 0.5 }` (6–8 sous-images pour les
  mouvements rapides, 4 laisse des fantômes ; obturateur 0,5 = 180°, 1,0 bave). Le flou ne traverse jamais une
  coupe franche ; aucun texte à lire ne doit être flouté.
- **Portes** : G2 (les états de texte), G3, musique.
- **Pièges** : grille automatique fausse de 1–2 temps (cherche le drop par l'énergie, `mf music`) ; tout sur chaque
  temps (punch de caméra minuscule par temps, plus marqué après le drop seulement) ; zoom avant puis arrière.
- **Commandes** : `mf init` → `mf music --file song.mp3` (BPM, drop proposé) → scènes en secondes → `mf lint` →
  `mf snapshot --at <temps forts>` → **G3** → `mf make`.

## style — création dans le langage d'une référence

- **Durée** : sting 8–12 s · standard 30–36 s · étendu 45–60 s (même grammaire, pas de diaporama).
- **Arc** : choisi parmi des modules (promesse cinétique, invocation, champ de résultats, écosystème, anneau de
  capacités, export, revendication finale : `styles.md` § blueprints). Choisis ceux qui correspondent aux
  capacités **réelles**.
- **Méthode** : prends la grammaire, jamais le contenu ni les logos. Extrais une image toutes les 0,5 s de la
  référence, écris un guide de style (hex de la palette, typo, durées de plan, transitions, caméra, texture,
  entrées/sorties de texte), puis choisis ou dérive un `style`. Attends l'accord avant de construire.
- **Blocs** : selon les modules ; **Style** : celui qui colle au guide ; **Son** : musique + SFX, voix optionnelle.
- **Portes** : G3 renforcée (styleframes comparées aux images de référence côte à côte).
- **Pièges** : présenter le résultat comme une copie (on reprend un langage visuel, pas des images) ; copier
  la typo ou le texte de la référence ; objets héros minuscules ; fond plus fort que le produit.
- **Commandes** : `mf remake analyze --ref ref.mp4` (planches et coupes, pour lecture seulement) → guide de style →
  `mf init` → scènes → `mf lint` → `mf snapshot` → **G3** → `mf make`.

## explainer — explication longue, voix posée, chapitres

- **Durée** : 60–180 s ; 13 phrases ≈ 95 s.
- **Arc** : question ou chiffre d'ouverture → 3 à 5 chapitres (`chapter-card`, puis affirmation → exemple → à
  retenir) → récapitulatif → CTA. Coupe aux paragraphes de sens, pas « une phrase = un nouvel élément ».
- **Blocs** : `chapter-card`, `kinetic-type`, `list-steps`, `code-card`, `bar-chart`, `split-compare`,
  `quote-card`, `highlight-zoom`, `screen-showcase`. Rotation : même bloc jamais 3 fois de suite, ≤ 1/3 du film ;
  chaque chapitre a sa couleur de fond et son motif, dans la même grammaire.
- **Style** : `paper` (clair dominant, un acte sombre pour le contraste) ; caméra par soustraction
  (`direction.md` § 8).
- **Son** : voix d'abord ; SFX ≤ 0,4 par seconde, aucun sur les révélations continues ni les citations ; musique
  très basse ou absente.
- **Alignement** : `mf align` découpe déjà la voix en segments ≤ 75 s (`--chunk-sec`) ; écoute chaque phrase
  signalée dans `flags` (cadre rouge de `mf voice board`) avant d'y ancrer une coupe.
- **Présentateur filmé : non pris en charge** (aucun bloc ne l'accueille). Dis-le, propose la voix seule ; les règles
  ci-après valent pour le jour où un bloc existera : fps du rush = fps du film,
  durée calée à l'image près sur la voix ; zone du visage mesurée, aucun texte ni fond de carte n'y entre ; le
  présentateur se pose en pastille dans le tiers inférieur, figée, mais il parle toujours ; il ouvre en plan
  moyen sur la première phrase puis se réduit ; jamais deux scènes de suite sans lui ; échange en 3 temps
  (l'ancien panneau sort, il se déplace, le nouveau entre).
- **Portes** : G2, GV, pilote (obligatoire), G3 par chapitre.
- **Pièges** : scène tout-texte sans dessin de soutien (ajoute un schéma au trait) ; même mise en page partout ;
  sous-titre karaoké fatigant (préférer la phrase posée) ; texte d'écran qui recopie le sous-titre.
- **Commandes** : `mf init` → (`mf scan`, `mf capture`) → script → **G2** → `mf voice` → `mf align` → **GV** `mf voice lock` → `mf voice board` → scènes → `mf lint` → pilote → `mf snapshot` → **G3** → `mf make`.

## remake — refaire une vidéo existante pour sa marque

- **Porte des droits, d'abord** : uniquement une vidéo dont l'utilisateur détient les droits ou a l'autorisation
  explicite. Sinon, propose le type `style`. Jamais la musique, la voix, les images ni les photos de personnes de la
  référence ; pas de faux co-marquage ; légende honnête (pas de « fait en 15 minutes ») ; créditer l'original.
- **Durée** : celle de la référence ; **Arc** : celui de la référence, contenu échangé selon des règles écrites
  (marque, accent, textes vrais, chiffres d'exemple étiquetés).
- **Méthode** : `mf remake analyze --ref ref.mp4` → coupes, planches, spec de plans. Les bornes sont souvent fausses
  de quelques images, et la plupart des « coupes » sont des mouvements continus (≈ 10–15 vraies coupes pour 60 s).
  Associe chaque plan à un bloc, ancres en secondes sur les temps de coupe de la référence.
- **Contrôle** : `mf compare --a ref.mp4 --b out/16x9.mp4` (écart moyen par image, recherche d'un décalage de
  ±2 images, SSIM/PSNR). On corrige un écart à la fois, en commençant par le premier ou le plus gros ; un
  échantillon sert à trouver où ça cloche, seule la comparaison complète valide. Regarde chaque raccord juste avant,
  pendant et juste après.
- **Ce qu'on promet** : une reconstruction ressemble à la référence, elle ne la duplique pas. Décris le résultat
  comme « proche de l'original », jamais comme « identique » ou « au pixel près ».
- **Son** : morceau libre de droits étiré de ≤ 8 % et coupé sur les mesures pour que les drops tombent aux temps de
  la référence ; SFX aux instants d'impact de la référence.
- **Portes** : droits, G3 (côte à côte), rapport de comparaison.
- **Commandes** : droits → `mf remake analyze --ref ref.mp4` → spec → `mf lint` → `mf snapshot` → **G3** →
  `mf make` → `mf compare --a ref.mp4 --b out/16x9.mp4` → corrections.

## Récapitulatif

| Type | Durée | Horloge | Style par défaut | Portes |
|---|---|---|---|---|
| launch | 30–60 s | voix | paper / dark-saas | G1 · G2 · G3 · musique |
| project | 20–45 s | voix | dark-saas | G1 · G2 · G3 |
| opener | 3,0 / 5,4 / 7,0 s (presets) | frappe | noir | G2 |
| cinematic | 15–60 s | musique | noir | G2 · G3 · musique |
| style | 8–60 s | musique ou voix | selon la référence | G3 renforcée |
| explainer | 60–180 s | voix | paper | G2 · pilote · G3 |
| remake | = référence | référence | selon la référence | droits · G3 · compare |

