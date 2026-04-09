# Intégration — Goose

## Principe

Goose utilise des fichiers prompt customisables stockés dans :

```
C:\Users\<toi>\AppData\Roaming\Block\goose\config\prompts\
```

(sous Linux/macOS : `~/.config/goose/prompts/` ou équivalent)

Le fichier qui nous intéresse est **`system.md`** : c'est le prompt
système principal de l'agent. Modifier ce fichier injecte le protocole
dans toutes les sessions Goose.

> ⚠️ Important : ces fichiers utilisent une syntaxe Jinja
> (`{% if %}`, `{% for %}`). Ne jamais casser ces blocs. On ajoute
> en dehors, on ne remplace pas.

## Méthode

1. **Ouvrir** `system.md` dans l'éditeur de prompts de Goose
   (interface "Customize" ou édition manuelle).
2. **Repérer la fin du fichier**, après les sections `# Extensions` et
   `# Response Guidelines`.
3. **Coller le contenu de `PROTOCOLE.md`** (ce dossier) à la fin, sans
   toucher au reste.
4. **Sauvegarder.**
5. **Relancer une session Goose** pour vérifier que le protocole est actif.

## Vérification

- Ouvrir une session sur un projet sans document maître.
- Poser une question.
- Goose doit proposer de créer le maître avant d'agir.

## Restauration

Si tu veux annuler : l'éditeur de prompts de Goose conserve l'original
en interne. Supprimer ta personnalisation rétablit le `system.md` par défaut.

## Ne PAS toucher

Ces autres fichiers ont des rôles spécifiques et y ajouter le protocole
créerait des contradictions :

- `subagent_system.md` (sous-agents efficacité-focus)
- `plan.md` (mode planification)
- `compaction.md` (résumé de conversation)
- `tiny_model_system.md` (petits modèles locaux)
- `recipe.md` / `apps_*.md` / `permission_judge.md` / `session_name.md`

Concentre tout sur `system.md`.
