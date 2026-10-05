# Review : contrôle, critique indépendante, corrections

Rien n'est « fini » avant le contrôle du **vrai fichier rendu** (`out/<slug>.mp4`), pas de l'aperçu. Le constructeur
ne juge pas son propre film : la critique est confiée à des sous-agents neufs, en lecture seule.

Sommaire : 1. L'ordre des contrôles · 2. Ce que `mf qa` vérifie, ce qu'un humain juge · 3. Relecteurs indépendants ·
4. Notes, grille et gravité · 5. Le tour de relecture · 6. Symptôme → correction · 7. Lire une planche contact ·
8. Corriger sans tourner en rond · 9. Quand s'arrêter

## 1. L'ordre des contrôles

On ne montre rien qui n'ait passé la machine, et on ne livre rien qu'un regard neuf n'ait vu.

- **D'abord la machine.** `mf lint` (spec, slots, ancres, durées), puis `mf qa` sur chaque format. Un ✗ se règle
  avant tout le reste. Avant de corriger, regarde comment le contrôle mesure (seuil, fenêtre) : un échec vient
  parfois de l'entrée elle-même (une voix sans respiration rend les SFX inaudibles, quoi qu'on règle), et mieux vaut
  le dire tout de suite.
- **Ensuite un regard neuf.** Un tour de relecteurs indépendants (§ 3) ; tout défaut P0 ou P1 se corrige.
- **Enfin la grille et le téléphone.** La grille du § 4, scène par scène, sur les images de contrôle et le rendu ;
  puis la planche réduite à la largeur d'un téléphone (360–390 px), où chaque ligne doit rester lisible.

## 2. Ce que `mf qa` vérifie, ce qu'un humain juge

| Automatique (`mf qa`, `mf lint`, `mf-manifest.json`) | Jugement (critique ou toi) |
|---|---|
| images noires, segments noirs | l'accroche nomme-t-elle la cible en ≤ 3 s ? |
| pops et flashs d'une image (image n ≠ ses deux voisines) | une seule chose à regarder à la fois ? |
| immobilité (> 1,5 s sans changement visible) | chaque image illustre-t-elle littéralement sa phrase ? |
| sonie −14 LUFS, crête vraie | la métaphore se lit-elle sans le son ? |
| déterminisme (même seconde rendue deux fois = mêmes pixels) | hiérarchie, marges égales, rien de coupé au bord |
| slots inconnus, `max_chars`, durées hors bornes, ancres irrésolues | le mot clé est-il le bon, et un seul ? |
| `warnings[]` du manifeste (coupes, transitions, SFX) | fidélité aux faits, étiquettes « Exemple » présentes |
| — | les SFX tombent-ils sur les gestes, la musique respire-t-elle ? |
| — | goût : est-ce que ça ressemble au style de référence nommé ? |

`mf qa` voit des pixels et des décibels ; il ne voit ni le sens, ni la vérité, ni le goût.

## 3. Relecteurs indépendants

Celui qui a fabriqué les images voit ce qu'il a voulu faire, pas ce qui est à l'écran. La relecture est donc
confiée à des sous-agents qui partent de zéro et ne touchent à rien.

**Qui relit.** Un relecteur par regard, chacun avec sa consigne de sévérité (dans le doute, c'est un défaut) :
le **mouvement** (rythme, continuité, relais, caméra, moments figés), le **design** (composition, typographie,
accent, lisibilité en vertical), le **message** (raconter le film à partir des seules images ; s'il n'y arrive pas,
le film a échoué). Pour un film de plus de 45 s, on ajoute le **son**, à partir du rapport de `mf qa` et de la
liste des SFX du manifeste.

**Comment les lancer.** Outil `Agent`, `subagent_type: "general-purpose"`, `run_in_background: true`, tous dans le
même message pour qu'ils travaillent en parallèle. On ne leur transmet jamais la conversation de fabrication, et un
second tour se fait avec des agents neufs, pas en relançant les mêmes (`SendMessage`).

**Ce qu'ils ont le droit de faire.** Lire et regarder, puis écrire un seul fichier : `video/qa/REVIEW-<regard>.md`.
Ni la spec, ni les blocs, ni les assets, ni aucune commande `mf`.

**Ce qu'on leur envoie** (tel quel, chemins absolus) :

```
Tu relis un film motion-forge sous l'angle <regard>. Tu n'as pas accès à ma conversation : seuls ces fichiers
comptent. Commence par lire <skill>/references/review.md (§ 4 et § 7), puis direction.md.
Fichiers : video.json · facts.json · timing/words.json · build/<slug>/mf-manifest.json · qa/report.md ·
           planches qa/ (contact, téléphone, bandes autour des raccords) · images qa/snap-<fmt>/
Scènes à relire : <s01–s07> (ou le film entier).
Écris qa/REVIEW-<regard>.md : commence par la structure (fichiers lus, sections P0 / P1 / P2 vides), puis ajoute
une ligne par scène relue au fur et à mesure. Pour chaque défaut : scène · instant (s) · ce qu'on voit · ce qu'on
attend · correction mesurable. Note chaque axe sur 10. Au moindre doute, compte-le comme un défaut.
Dernière ligne, exactement : « ## Revue terminée · N/N scènes vues ». Aucun autre fichier.
```

**Savoir qu'ils ont fini.** La notification de l'agent ne suffit pas (elle peut arriver avant l'écriture, ou pour
un fichier vide) : c'est la dernière ligne du fichier qui fait foi, relu sur le disque. Surveille sa taille toutes
les 2 à 3 minutes ; s'il ne grossit plus pendant 10 minutes, arrête l'agent (`TaskStop`) et relance un agent neuf
avec la même consigne, une ligne sur la cause et une charge plus légère (moins d'images, moins de scènes).

**Film long.** Au-delà de 8 scènes, partage la relecture entre 2 ou 3 relecteurs (7 scènes au plus chacun) et
ajoute-en un dernier qui ne juge que l'ensemble : style, caméra, rotation des blocs, rimes.

**Si rien ne revient.** Après trois lancements sans rapport, livre avec la mention « **non revu indépendamment** »
et la cause ; une relecture par soi-même ne se présente jamais comme indépendante.

## 4. Notes, grille et gravité

**Sept notes sur 10**, une par axe : l'accroche (les deux premières secondes), la lecture à 360 px de large, la
qualité du mouvement (ressorts, aucune image morte), le renouvellement (quelque chose de neuf toutes les 2 à 4 s),
la composition, la justesse (marque et données), l'accord du son avec l'image.

**La grille**, oui ou non pour chaque scène :
- le premier mot dit est la première image, pas le logo ; le logo entier n'arrive pas avant 5 s, sauf s'il est le
  sujet ;
- il se passe quelque chose toutes les 0,5 à 1 s ; rien n'est figé plus de 1,5 s ; aucune mise en page ne dure plus
  de 3 s telle quelle ;
- à chaque raccord, un objet ou une direction se prolonge ; rien n'apparaît ni ne disparaît dans les deux images
  qui l'entourent ; rien n'est en double ;
- de 0 à 4 coupes franches avec une voix narrative, 2 fondus au plus ; une coupe tombe sur un premier mot ou un
  silence ;
- un mot mis en avant par phrase, un accent par rôle ; pas de mot géant hors des moments typographiques prévus ;
- un chiffre arrive en roulant ou en fonçant, jamais en fondu, et il a son fait ou l'étiquette « Exemple » ;
- le produit se montre par des gestes (taper, cocher, cliquer), pas par une capture posée ;
- un élément de l'accroche revient avant la fin ; la carte de fin a un seul appel, cliquable, et vit 2 à 3 s ;
- la bande des sous-titres reste libre, les marges latérales sont égales, rien n'est coupé au bord, le film se
  comprend sans le son.

**Trois niveaux de gravité** :
- **P0 (bloquant)** : tout spectateur le remarque et comprend de travers. Faute dans un texte ou un fait, texte
  illisible, son décalé, éléments qui se heurtent, flèche qui montre la mauvaise chose, image noire.
- **P1 (à corriger)** : une règle de la grille est cassée ou la dérive est nette. Plus de 0,3 s entre un mot et son
  image, moment figé, raccord qui saute, bloc hors style, même bloc trois fois de suite, capture posée sans geste,
  scène entière sans son.
- **P2 (finition)** : densité, respiration, détail de style. On le note, on ne bloque pas.

Un tour est réussi quand il ne reste **aucun P0 ni P1** et que chaque note vaut au moins 8. Une scène notée 9 ou
plus ne se retouche pas.

## 5. Le tour de relecture

Une première fois sur les images de contrôle avant le rendu final, une seconde sur le MP4 :

```bash
ffmpeg -i out/16x9.mp4 -vf "fps=2,scale=270:-1,tile=6x5" -frames:v 1 qa/contact.png        # le film entier
ffmpeg -ss <t-0.1> -i out/16x9.mp4 -vf "scale=320:-1,tile=12x1" -frames:v 1 qa/strip-<t>.png # 12 images autour d'un geste rapide ou d'un raccord
ffmpeg -i out/16x9.mp4 -vf "fps=1,scale=360:-1,tile=5x3" -frames:v 1 qa/phone.png          # lecture sur téléphone
```

(Quand `mf qa` a déjà produit ces planches dans `qa/`, prends les siennes.) Note le film, écris **les trois plus
gros problèmes avec leur instant**, corrige, ne re-rends que ce qui a changé, puis note de nouveau. À surveiller :
un texte qui en chevauche un autre pendant un remplacement, un mouvement à vitesse constante, un titre centré sur un
dégradé, un texte agrandi devenu flou, un temps mort, une étiquette ou une bordure parasite dans un coin, une boucle
qui accroche.

## 6. Symptôme → correction (vocabulaire motion-forge)

| Symptôme | Cause → correction |
|---|---|
| « On dirait tous les films IA » | pas de brief, de faits ni de style nommé → `storyboard.md` § 2, `facts.json`, l'idée qui bouge (`direction.md` § 1) |
| Diaporama, tout fond en entrée | blocs choisis par habitude → plan des moments (`storyboard.md` § 3), un état d'arrivée par scène, `transition_in` motivé |
| Immobile plus de 1,5 s | tenue sans couche vivante → raccourcir la scène, ou bloc qui dérive ; jamais combler par une boucle de respiration |
| Bon marché, rebondit | `snap` sur de gros objets → `easeOut` ; snap seulement sur pastilles et lettres |
| Texte flou, logo délavé | copie floue agrandie, raster de logo → SVG, ne flouter qu'un seul geste rapide, jamais un texte à lire |
| Saccade à l'export | animation hors timeline (timer, transition CSS) → règles de `block.js` ; `mf lint` le signale |
| Flash noir à une coupe | scène entrante invisible à sa 1ʳᵉ image → état initial visible ; couture au sommet du flou |
| Deux objets identiques à une couture | le pont est redessiné par N et N+1 → un seul objet, l'un sort quand l'autre entre |
| Mot clé illisible en 9:16 | slot trop long → `max_chars`, couper la scène, `[data-orient="portrait"]` dans le bloc |
| Couleur en trop | accent réutilisé pour un 2ᵉ rôle ou couleur de marque tierce hors tuile → un rôle par couleur |
| Fondus qui grisent | fondu entre deux fonds clairs → `cut` + objet-pont, ou `push` |
| SFX inaudibles | posés sur la voix → déplacer dans les respirations (~0,3 s), `gain_db`, un seul son par instant |
| Début mou | musique de tension trop basse ou intro clairsemée → `music.offset_s` vers une partie pleine, 2–3 dB sous l'élan |
| Drop à côté | drop en secondes devinées → `music.drop_at: "s:N"` sur la phrase de la solution, `mf music` |
| Fonction inventée | pas de captures, de dépôt ni de faits → `mf scan`, `mf capture`, porte de vérité |
| Boucle qui saute | positions raccordées, vitesses non → finir sur l'état 0 avec la même vitesse d'entrée |
| Coût qui explose | effort maximal sur des retouches → retouches simples à effort moyen, rendre seulement le format en cause |

## 7. Lire une planche contact

Une planche se lit comme une bande dessinée : on doit y suivre une histoire, pas feuilleter six affiches.

- **L'histoire** : les vignettes évoluent-elles de l'une à l'autre ? Devine-t-on le film sans les sous-titres ? La
  première vignette montre-t-elle le premier mot dit ?
- **La variété** : une mise en page qui revient, un bloc présent trois fois d'affilée ?
- **Les raccords** : de part et d'autre, même caméra, mêmes objets, même flou ; rien en double, rien qui manque.
- **Le sujet** : assez grand, assez contrasté, pas noyé dans un effet ou une lueur ?
- **Les bords** : texte qui déborde, bande de sous-titres occupée, élément rogné, marges inégales ?
- **L'accent** : un seul, au bon endroit, sans flash de couleur inexpliqué ?
- **Le téléphone** : sur la planche réduite à 360 px, chaque ligne se lit-elle ?

## 8. Corriger sans tourner en rond

- Un retour daté (« à 4 s, le flou passe devant le texte ») se contrôle sur la même image avant la correction, après
  elle, et dans le rendu final ; les trois chemins vont dans le rapport.
- Une correction qui touche un état (relais, remplacement) se contrôle sur toute sa durée : début, milieu, fin et
  raccords.
- Corriger deux fois le même défaut oblige à écrire en une ligne pourquoi la première tentative n'a pas suffi.
- La preuve est une mesure (instant d'apparition, décalage en secondes, pixels), jamais « ça a l'air bon ».
- On change la spec ou le bloc, jamais le verdict. Une leçon générale va dans ces références.

## 9. Quand s'arrêter

- Machine au vert → **un tour** de relecture (relecteurs indépendants pour un film de plus de 45 s ou de 8 scènes et
  plus ; sinon ta propre lecture des planches suffit) → corrections P0 et P1 → livraison avec la liste des P2
  restants.
- Ensuite, propose un tour de plus si l'utilisateur le souhaite, toujours avec des relecteurs neufs, **trois tours
  au plus**. Au-delà, arrête et rends la main avec les défauts restants, l'historique des corrections et la raison de
  leur échec.
- Un film ne s'annonce jamais terminé sans `mf qa` vert sur tous les formats, la durée et les pistes (image et son)
  vérifiées, les planches lues et les chemins des MP4 donnés.
