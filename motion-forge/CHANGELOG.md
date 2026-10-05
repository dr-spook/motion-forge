# CHANGELOG — motion-forge (skill)

## 0.6.0-alpha — 2026-10-05

Publication open source (MIT). Aucun changement de comportement attendu : les mêmes règles, écrites autrement.

- **Réécriture à neuf** des passages inspirés de video-talkcraft (PolyForm Noncommercial) et de
  video-production-skills (sans licence), pour que le skill ne contienne que du texte original ou adapté de sources
  MIT : `direction.md` § 1–3 (l'idée qui bouge, les gestes du monde, le test du diaporama) et § 6 (courbe
  d'énergie) ; `storyboard.md` § 3–5 (plan des moments, fiches de scène avec un exemple VoxText, choix des blocs) ;
  `review.md` § 1, 3, 4, 5, 7, 8, 9 ; `types.md` (sections opener, style, remake). Noms changés en conséquence
  (« thèse de mouvement » → « l'idée qui bouge », « porte anti-PPT » → « test du diaporama », « shotbook » →
  « fiches de scène », « graphe de beats » → « plan des moments »).
- Le seuil « 80 % des beats » disparaît ; la règle devient « chaque scène finit dans un état différent de son
  début », vérifiable sur `mf board`.
- **Licence MIT** (`LICENSE.txt`) ; `NOTICE.md` reprend les mentions MIT de Colin Blain et de Howseen AI (Raphaël
  Aubry) et décrit ce qui a été réécrit.
- Jeu d'éval et mesure du déclenchement publiés dans `evals/` à la racine du dépôt.

## 0.5.0-alpha — 2026-10-05

IMPROVE (skill-hunter 1.4.0), après une production réelle (VoxText, app Android, utilisateur non technique) : six
allers-retours, jargon (« variante », « fact », « brief »), captures demandées deux fois, outil `mf` absent de
l'environnement. Tier **T3** sur le chemin projet (code de l'utilisateur, entrée non fiable, images avec données
personnelles), T2 ailleurs. Seule la couche skill est modifiée : le toolkit `mf` n'est pas touché.

- **Parcours simple par défaut** (`references/guide-simple.md`, SKILL § 1). Quatre moments : accueil à 3 questions
  avec recommandation et « choisis pour moi », une seule demande de matériel, arrêt 1 (texte recommandé seul), arrêt
  2 (voix + planche). Les portes G1–G3/GV sont regroupées, pas supprimées. Pilote automatique avec résumé des choix.
  Lexique jargon → mots simples. *Pourquoi* : le pipeline était juste mais exposé tel quel à l'utilisateur.
- **Apports** (`references/apports.md`, SKILL § 2). Chemins pour un script fourni (variante `U`, vérifiée, jamais
  réécrite en silence), un README seul ou un dépôt, des captures fournies web ou téléphone, des personnages 2D
  (marionnette avec les primitives existantes du `world`), et l'absence d'outil installé. *Pourquoi* : ces cas
  étaient possibles mais non documentés, ou documentés seulement pour le dépôt de code.
- **Vie privée des images fournies** (principe 8, chemins d'échec). Contrôle image par image, données de test
  redemandées une fois, sinon nettoyage annoncé ; le masquage de `mf capture` ne couvre pas ces images.
- **Contenu inventé sur une vraie capture** étiqueté « Exemple » (principe 5).
- **Droits des personnages** (principe 8) : pas de personnage de franchise, pas de visage réel sans accord.
- **Collision de nom `mf` / Metafont** (§ 0) : on vérifie que `mf --help` parle de motion-forge.
- **Sans motion-forge** (§ 0, `apports.md` § 7) : tout préparer ; rendu de secours seulement à la demande, annoncé.
- **Voix Kokoro française** : une seule voix, débit rapide, mots étrangers à écouter (chemins d'échec).
- **Déclenchement** : `description` réécrite (1010/1024) pour les apports (script, captures de téléphone,
  personnages, README) et le vocabulaire non technique ; SKIP resserré. Jeu d'éval `evals/trigger-eval.json`
  (11 positifs, 9 near-misses).

Non fait, jugé hors couche skill : un bloc `phone-frame` et un bloc `character` (squelette, marche, synchro
labiale) dans `mf`, un champ de locuteur pour les dialogues, une graphie de prononciation pour `mf voice`. Marqués
`⚠️ À VÉRIFIER` ou signalés comme manques là où le skill les rencontre.
