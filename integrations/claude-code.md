# Intégration — Claude Code

## Principe

Claude Code lit automatiquement les fichiers `CLAUDE.md` qu'il trouve à
deux endroits :

- **Global** : `~/.claude/CLAUDE.md` (ou `C:\Users\<toi>\.claude\CLAUDE.md`
  sous Windows). S'applique à tous les projets.
- **Projet** : `CLAUDE.md` à la racine du projet. S'applique uniquement
  à ce projet.

Le protocole peut vivre aux deux niveaux selon ton besoin.

## Option A — Protocole global (recommandé)

Tu copies le contenu de `PROTOCOLE.md` (ce dossier) dans
`~/.claude/CLAUDE.md`. Toutes tes sessions Claude Code, sur n'importe
quel projet, hériteront du protocole.

Avantages :
- aucun fichier à gérer projet par projet
- mise à jour centralisée

Inconvénients :
- pas d'adaptation par projet (langue, stack, contraintes spécifiques)

## Option B — Protocole par projet

Tu copies `PROTOCOLE.md` dans le `CLAUDE.md` à la racine du projet,
et tu y ajoutes en haut une section spécifique au projet :

```markdown
# CLAUDE.md — [NOM DU PROJET]

## Spécificités projet

- Langue : français
- Stack : (résumé)
- Contraintes particulières : (ex. utilisateur non-développeur, prod sensible, etc.)
- Sources de vérité principales :
  - docs/DOCUMENT_MAITRE.md
  - docs/ROADMAP.md
  - docs/VALIDATION_LOG_*.md

---

(ici tu colles le contenu de PROTOCOLE.md)
```

Avantages :
- adaptation fine par projet
- tout est versionné dans le repo du projet (donc partageable)

## Option C — Hybride (le plus puissant)

- Le protocole générique vit en global dans `~/.claude/CLAUDE.md`
- Chaque projet a un `CLAUDE.md` court qui ne contient **que les
  spécificités projet** (langue, stack, sources de vérité, contraintes)
- Le projet n'a pas besoin de répéter le protocole : il est déjà chargé

C'est la configuration utilisée sur le projet d'origine.

## Vérification

Pour vérifier que le protocole est bien actif :

1. Ouvre une nouvelle session Claude Code dans un projet où il manque
   un `DOCUMENT_MAITRE.md`.
2. Pose une question quelconque sur le projet.
3. Claude doit te proposer de **créer le document maître avant de répondre**.
   Si ce n'est pas le cas, le protocole n'est pas chargé.

## Cas particulier — multi-machines

`~/.claude/CLAUDE.md` n'est pas synchronisé automatiquement entre
machines. Si tu utilises Claude Code sur plusieurs ordinateurs, garde
ce dossier `PROTOCOLE/` dans un endroit synchronisé (Drive, Dropbox,
git privé) et réinjecte manuellement.
