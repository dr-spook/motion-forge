# NOTICE — provenance et mentions

motion-forge (ce skill) est écrit par **Boubacar Sidiki ZANGO** ([@dr-spook](https://github.com/dr-spook)) avec
Claude, et distribué sous licence **MIT** (`LICENSE`). Ce document n'est pas un avis juridique.

## Sources dont des passages ont été adaptés (licence MIT)

Des éléments de méthode de ces deux projets ont été adaptés en français dans ce skill. Leur licence MIT l'autorise
à condition de conserver leurs mentions, reproduites ci-dessous.

| Projet | Ce qui en vient |
|---|---|
| [motion-design-claude-code](https://github.com/cblain100-prog/motion-design-claude-code) | méthode de production à validations humaines, continuité entre scènes (objets qui passent de l'une à l'autre) |
| [claude-motion-design](https://github.com/howseen-ai/claude-motion-design) | image comme fonction du temps (`seek(t)`), faits sourcés, son calé sur les gestes, démarche de remake |

> Copyright (c) 2026 Colin Blain — MIT License
>
> Copyright (c) 2026 Howseen AI (Raphaël Aubry) — MIT License

Texte de la licence MIT applicable à ces deux mentions :

> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated
> documentation files (the "Software"), to deal in the Software without restriction, including without limitation
> the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and
> to permit persons to whom the Software is furnished to do so, subject to the following conditions: The above
> copyright notice and this permission notice shall be included in all copies or substantial portions of the
> Software. THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT
> LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT
> SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
> OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
> DEALINGS IN THE SOFTWARE.

## Sources étudiées, sans reprise de texte

| Projet | Licence | Statut dans ce dépôt |
|---|---|---|
| [video-talkcraft](https://github.com/Vincentwei1021/video-talkcraft) (Vincent Wei) | PolyForm Noncommercial 1.0.0 | étudié ; aucun texte ni code repris |
| [video-production-skills](https://github.com/Pluviobyte/video-production-skills) (Pluviobyte) | aucune licence publiée | étudié ; aucun texte ni code repris |

Les passages de la version privée qui s'en inspiraient ont été **réécrits à neuf** le 2026-10-05, avec une autre
structure, d'autres exemples et des règles tirées des outils de motion-forge et de productions réelles :
`references/direction.md` § 1–3 et § 6, `references/storyboard.md` § 3–5 (et le vocabulaire du brief et de
l'exemple), `references/review.md` § 1, 3–5 et 7–9, et les sections `opener`, `style` et `remake` de `references/types.md`. Ne
restent que des idées générales du motion design (montrer une transformation plutôt qu'une suite d'écrans, relire
avec un regard neuf), qui n'appartiennent à personne. Merci à leurs auteurs pour ce travail.

## L'outil `mf` (hors de ce dépôt)

Ce dépôt ne contient que le skill. L'outil local motion-forge (`mf`) n'est pas couvert par ce dépôt ni par sa
licence ; il a ses propres dépendances : HyperFrames (Apache-2.0), GSAP (licence « Standard no-charge » de
GreenSock), Playwright (Apache-2.0), faster-whisper (MIT), Kokoro (Apache-2.0), ffmpeg (LGPL/GPL selon la
compilation).

## Outils

Conçu, durci et mesuré avec **skill-hunter** (modes CREATE, IMPROVE, MEASURE).
