# Parcours simple : faire un film avec quelqu'un qui n'est pas technique

Le pipeline de `SKILL.md` § 5 reste la mécanique. Ce fichier règle **la conversation** : ce qu'on demande, quand, avec
quels mots. Il est le mode par défaut, sauf si l'utilisateur parle lui-même de `mf`, de spec ou de `video.json`.

Sommaire : 1. Pourquoi · 2. Les quatre moments · 3. L'accueil · 4. La demande de matériel · 5. Arrêt 1, le texte ·
6. Arrêt 2, la voix et le plan · 7. La livraison · 8. Pilote automatique · 9. Lexique · 10. Exemple rejoué

## 1. Pourquoi

Session réelle (VoxText, app Android, 2026-10) : six allers-retours, des mots inconnus (« variante », « fact »,
« brief », « G2 »), des captures demandées deux fois, une note de script en tableau. Le film final était bon ; le
chemin, lui, aurait perdu quelqu'un qui n'est pas développeur. Chaque question coûte un aller-retour et un peu de
confiance : on en pose moins, on les pose mieux, et chacune arrive avec une recommandation.

## 2. Les quatre moments (et rien d'autre)

| Moment | Ce que voit l'utilisateur | Remplace |
|---|---|---|
| **Accueil** | 3 questions à options, une option « recommandé » et « choisis pour moi » | le brief à valider, le choix du type, du profil, des formats |
| **Matériel** | une seule liste de ce qu'il faut envoyer, avec consignes de vie privée | les demandes de fichiers au fil de l'eau, G1 |
| **Arrêt 1 : le texte** | le texte recommandé en entier, sa durée, une ligne de pourquoi | les variantes A/B/C et leur tableau de notes (G2) |
| **Arrêt 2 : la voix et le plan** | le fichier audio + la planche du film en images, « je lance ? » | GV et G3 séparés, la musique à part |

Les portes techniques existent toujours : elles sont **regroupées**, pas supprimées. G1 se fait seul (tri des
captures, nettoyage) et n'interrompt que s'il y a un problème ; G2 = arrêt 1 ; GV + G3 + musique = arrêt 2.

## 3. L'accueil

Un seul message. Si un outil de questions à boutons existe (ex. `ask_user_input`), utilise-le ; sinon des options
numérotées. Ne pose pas une question dont la réponse est déjà dans la demande ou les fichiers reçus.

1. **Qu'est-ce que la vidéo doit faire ?** Présenter mon produit (recommandé si on t'envoie un projet) · Montrer une
   fonctionnalité · Raconter une histoire avec des personnages · Une intro courte (moins de 10 s)
2. **Où sera-t-elle publiée ?** TikTok / Reels / Shorts · Instagram ou Facebook (fil) · LinkedIn ou X · Mon site,
   YouTube ou GitHub · Partout (recommandé si on hésite)
3. **Quelle voix ?** Voix de synthèse gratuite (recommandé pour aller vite) · Ma propre voix (je t'envoie un
   enregistrement) · Pas de voix, juste de la musique et du texte

Ajoute toujours la sortie : « Je n'y connais rien, fais au mieux » → pilote automatique (§ 8).

Ce que les réponses décident, sans le dire en jargon :

| Canal | Formats | Durée conseillée |
|---|---|---|
| TikTok / Reels / Shorts | 9:16 | 20–35 s |
| Instagram / Facebook (fil) | 4:5 (+ 9:16 pour les stories) | 20–35 s |
| LinkedIn / X | 1:1 + 16:9 | 30–45 s |
| Site, YouTube, GitHub | 16:9 + GIF de README | 30–60 s |
| Partout | 9:16, 4:5, 1:1, 16:9 + GIF | 30 s |

Réponse 1 → type (`project` si un projet est fourni, `launch` sinon, `opener` pour une intro, personnages →
`launch` avec le patron de `apports.md` § 5). Le profil et la structure se choisissent seuls (`SKILL.md` § 4) et ne
sont jamais demandés.

## 4. La demande de matériel (une seule fois)

Juste après l'accueil, **une** liste, construite à partir de ce que l'utilisateur a déjà envoyé et de ce que le type
demande (`apports.md`). Pour chaque élément : quoi, pourquoi en quelques mots, et ce qu'on fait s'il ne l'a pas.

Modèle :

> Pour faire ta vidéo, envoie-moi :
> 1. **4 ou 5 captures de ton app** : l'accueil, l'écran principal, le résultat. Prends-les avec un compte ou une
>    conversation de test : tout ce qui est à l'écran apparaîtra dans la vidéo (noms, messages, photos, clés).
> 2. **Ton logo** si tu en as un (sinon je reprends l'icône de l'app).
> 3. *(facultatif)* une musique que tu as le droit d'utiliser. Sans musique, j'en génère une discrète.
>
> Si tu n'as pas tout, envoie ce que tu as : je fais sans et je te dis ce qui manque.

Puis vérifie ce qui arrive (`apports.md` § 4 : vie privée, nom du produit, cohérence) et ne redemande que ce qui est
inutilisable, en disant pourquoi en une phrase.

## 5. Arrêt 1 : le texte

Écris toujours 2 ou 3 variantes et note-les (`script.md`), mais **montre la recommandée**, pas le tableau :

> Voici le texte que je te propose (environ 30 secondes) :
> « … le texte entier, une phrase par ligne … »
> Pourquoi celui-là : il commence par une situation que tout le monde connaît.
> Tu peux changer n'importe quel mot. J'ai aussi deux autres façons de le raconter, si tu veux les voir.

Interdits à cet arrêt : les rôles (`hook`, `cta`), les notes chiffrées, les identifiants de faits, les noms de
structures. Si une phrase affirme quelque chose qu'on ne peut pas prouver, dis-le simplement : « Je n'ai pas mis
"100 % privé" : l'audio passe par un serveur, ce serait faux. »

## 6. Arrêt 2 : la voix et le plan

Après `mf voice` et `mf board` : envoie l'audio et **une** image de planche (le format principal), avec une phrase par
moment clé du film. Une seule question : « Ça te va ? Je lance la fabrication (environ N minutes). » Les remarques
reçues se traduisent en corrections de spec ; on ne redemande pas une validation pour chaque correction mineure.

## 7. La livraison

- Les fichiers par **usage**, pas par nom technique : « Pour TikTok et les statuts : … · Pour Instagram : … ».
- Ce qui a été modifié dans ses images (floutage, texte d'exemple, nom corrigé), en une ligne chacun.
- Les réserves en mots simples, trois au plus (« la voix de synthèse est correcte mais moins chaleureuse qu'une vraie
  voix »).
- **Une** suggestion de suite, pas un menu.
- Le rapport technique (`qa/report.md`) est joint pour qui le veut ; on ne le recopie pas dans le message.

## 8. Pilote automatique

Déclencheurs : « fais tout », « je n'y connais rien », « fais au mieux », ou pas de réponse en session non surveillée.
Prends l'option recommandée à chaque question, écris chaque choix dans `video/qa/decisions.json`, et livre avec
un paragraphe « Ce que j'ai choisi pour toi » (canal, durée, voix, texte) et comment le changer en une phrase. Le
consentement reste obligatoire pour ce qui ne se rattrape pas : lancer le code de l'utilisateur, une voix payante,
un remake (principe 8).

## 9. Lexique (ce qu'on dit à la place)

| Jargon | Dire |
|---|---|
| variante A/B/C | « trois façons de raconter » (montrer la recommandée) |
| facts.json, fait sourcé | « ce que je peux prouver » / « d'où je le tiens » |
| brief | « le plan du film » (une image, pas un tableau) |
| spec, video.json | « le fichier du film » (seulement si on en parle) |
| G1, G2, GV, G3 | ne jamais nommer les portes |
| 9:16, 16:9, 4:5, 1:1 | « format TikTok », « format YouTube », « format Instagram », « format carré » |
| LUFS, QA, framemd5 | « le son est au bon niveau », « j'ai vérifié chaque image » |
| capture | « capture d'écran » |
| slot, bloc, profil | ne pas nommer |

## 10. Exemple rejoué (VoxText : quatre échanges au lieu de six)

1. Utilisateur : zip du projet. → Claude lit le projet, trouve l'app Android, pose l'accueil (3 questions) et, dans le
   même message, la liste de matériel (5 captures précises, conversation de test, sans la clé visible), plus ce qu'il
   a repéré (nom mal orthographié dans l'app, phrase « 100 % privé » fausse).
2. Utilisateur : réponses + captures. → Claude nettoie les captures, écrit le texte, montre le recommandé (arrêt 1).
3. Utilisateur : « ok ». → voix + planche du film (arrêt 2).
4. Utilisateur : « vas-y ». → fabrication, livraison par usage.

En pilote automatique, les échanges 3 et 4 disparaissent : le film arrive avec « Ce que j'ai choisi pour toi ».
