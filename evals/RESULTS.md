# Mesure du déclenchement

| Date | Version | Environnement | Jeu | Répétitions | Résultat |
|---|---|---|---|---|---|
| 2026-10-05 | 0.5.0-alpha | Claude Code, Windows 11, backend `claude` | `trigger-eval.json` (11 doivent déclencher, 9 pièges) | 3 | accuracy 100 % · TPR 100 % · FPR 0 % (tp 11, fp 0, fn 0, tn 9) |

La `description` n'a pas changé depuis (0.6.0-alpha) : la mesure reste valable.

Limites : 20 requêtes seulement, et le juge voit ce skill seul, sans la concurrence des autres skills installés.

Relancer (depuis un dossier qui contient `skill-hunter/` et ce dépôt) :

```
python skill-hunter/scripts/measure.py --skill motion-forge --eval-set evals/trigger-eval.json --backend claude
```
