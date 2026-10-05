# motion-forge

**Un réalisateur de motion design pour Claude Code.** Tu lui donnes une idée, ton texte, ton projet, des captures
d'écran ou tes personnages ; il te pose trois questions simples et fabrique une vidéo de lancement prête à publier
sur TikTok, Instagram, LinkedIn, YouTube ou GitHub.

![version](https://img.shields.io/badge/version-0.6.0--alpha-7C3AED)
![licence](https://img.shields.io/badge/licence-MIT-2EA44F)
![Claude Code](https://img.shields.io/badge/Claude%20Code-skill-D97757)
![déclenchement](https://img.shields.io/badge/d%C3%A9clenchement-20%2F20-2EA44F)

<p align="center">
  <img src="docs/voxtext-demo.gif" alt="Extrait du film de lancement de VoxText" width="560">
  <br>
  <sub>Film de lancement de <a href="https://github.com/dr-spook/voxtext">VoxText</a>, dirigé par ce skill
  (rendu de secours hors <code>mf</code>, voix de synthèse Kokoro, captures nettoyées, contenus d'exemple étiquetés).</sub>
</p>

## Ce que ça fait

- **Part de ce que tu as** : une simple idée, un script déjà écrit, un README ou un dépôt de code, des captures de
  site ou de téléphone, des personnages 2D (SVG ou PNG).
- **Te parle simplement** : trois questions avec une option recommandée, une seule liste de fichiers à envoyer, puis
  deux validations (le texte, puis la voix et le plan du film). Ou bien « fais tout » et tu regardes à la fin.
- **Livre tous les formats d'un coup** : vertical (TikTok, Reels, Shorts), 4:5 (fil Instagram), carré (LinkedIn,
  X), 16:9 (YouTube, site), plus un GIF pour ton README.
- **Écrit la voix off et les sous-titres mot à mot**, avec ta voix ou une voix de synthèse gratuite.
- **Ne raconte pas n'importe quoi** : chaque affirmation du film doit pouvoir se prouver (code, capture, ta
  parole). Un chiffre d'exemple s'affiche « Exemple ». « 100 % privé » ne passe pas si l'audio part sur un serveur.
- **Protège ta vie privée** : chaque capture est vérifiée avant usage (contacts, messages, clés, notifications) et
  nettoyée ou redemandée.

## Ce qu'il te faut

Ce dépôt contient **le skill** (le savoir-faire du réalisateur). La fabrication des vidéos passe par l'outil local
**motion-forge** (`mf` : HyperFrames, GSAP, ffmpeg, Node 22+, Python 3.10+), qui n'est pas inclus ici.

- **Avec l'outil installé** : Claude écrit, fabrique, mixe le son et vérifie chaque image.
- **Sans l'outil** : Claude prépare tout (texte, captures nettoyées, plan, fichier du film `video.json`) et te dit
  où se fera la fabrication.

## Installation

Copie le dossier `motion-forge/` dans le dossier des skills de Claude Code.

**Windows (invite de commandes)**

```
git clone https://github.com/dr-spook/motion-forge.git
xcopy /E /I /Y motion-forge\motion-forge "%USERPROFILE%\.claude\skills\motion-forge"
```

**macOS / Linux**

```bash
git clone https://github.com/dr-spook/motion-forge.git
mkdir -p ~/.claude/skills && cp -r motion-forge/motion-forge ~/.claude/skills/
```

Ouvre ensuite une **nouvelle** session Claude Code.

## Utilisation

Écris simplement ce que tu veux, par exemple :

- « Fais-moi une vidéo pour présenter mon appli, je n'y connais rien en montage. »
- « J'ai écrit mon script, fais-en une vidéo de 30 secondes pour TikTok. »
- « Voici le README de mon SaaS et 4 captures d'écran : vidéo de lancement. »
- « Anime ma mascotte (SVG) qui explique comment marche mon produit. »
- « Une intro de 6 secondes avec le nom de ma chaîne tapé à la machine. »

Le skill se déclenche aussi avec `/motion-forge` ou `mf`.

## Comment se passe une vidéo

1. **Accueil** : à quoi sert la vidéo, où elle sera publiée, quelle voix. Chaque question a une option recommandée.
2. **Matériel** : une seule liste de ce qu'il faut envoyer, avec les consignes (données de test, clé masquée).
3. **Le texte** : la version recommandée, en entier, avec sa durée. Tu changes ce que tu veux.
4. **La voix et le plan** : tu écoutes, tu regardes le film en images, tu dis « vas-y ».
5. **Livraison** : les fichiers classés par usage (« pour TikTok », « pour Instagram »), avec ce qui a été modifié
   dans tes images.

## Ce qu'il sait faire, et ce qu'il ne fait pas

| Oui | Pas encore / jamais |
|---|---|
| Films de lancement, démos, intros tapées à la machine, films calés sur la musique, explications en voix off, remakes du style d'une vidéo (avec tes droits) | Montage de vidéos filmées |
| Personnages 2D en marionnette : poses, expressions, bouche qui bat sur les répliques, bras découpés | Squelette articulé, marche, synchronisation labiale fine, import Lottie |
| Ta voix, ou une voix de synthèse locale gratuite | Dialogues à plusieurs voix sans enregistrements ou service payant (une seule voix française en local) |
| Tes propres personnages ou ceux que tu as le droit d'utiliser | Personnages de franchises connues, visages réels sans accord |
| | Vidéo générée par IA à partir d'un prompt |

## Qualité du déclenchement

Mesuré avec le mode MEASURE de skill-hunter : sur 20 requêtes répétées 3 fois, le skill se déclenche pour les 11
demandes de vidéo et pour aucun des 9 pièges (montage, logo, PowerPoint…). Détails et commande :
[`evals/RESULTS.md`](evals/RESULTS.md).

## Contenu du dépôt

```
motion-forge/            le skill (à copier dans ~/.claude/skills/)
  SKILL.md               noyau : parcours simple, apports, principes, pipeline, chemins d'échec
  references/            savoir-faire chargé à la demande (parcours, apports, script, mise en scène…)
  CHANGELOG.md           historique des versions
  LICENSE.txt, NOTICE.md licence MIT et provenance (voyagent avec le skill)
evals/                   jeu de test du déclenchement et résultats
docs/                    démo
```

## Crédits

Des éléments de méthode sont adaptés des projets MIT de **Colin Blain** et de **Raphaël Aubry** (Howseen AI). Les
travaux de **Vincent Wei** et de **Pluviobyte** ont été étudiés, sans reprise de texte. Le détail est dans
[`NOTICE.md`](NOTICE.md). Conçu, durci et mesuré avec **skill-hunter**.

## Licence

[MIT](LICENSE) : libre d'utiliser, de modifier et de partager ce skill, y compris pour un usage commercial, en
gardant la mention de copyright. Les vidéos que tu fabriques t'appartiennent. Provenance et mentions des sources :
[`NOTICE.md`](NOTICE.md).

## Contribuer

Les retours sont bienvenus : ouvre une issue avec la conversation qui a coincé (demande, ce que le skill a fait, ce
que tu attendais). C'est ce qui sert à chaque amélioration du skill.

## Auteur

**Boubacar Sidiki ZANGO** · [@dr-spook](https://github.com/dr-spook)
