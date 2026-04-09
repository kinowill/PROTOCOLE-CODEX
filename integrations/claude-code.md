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

## Activer l'auto-monitoring du contexte (`show_context.ps1`)

Le protocole (section 12) prévoit que l'IA s'auto-vérifie sur sa
consommation de tokens avant toute grosse tâche. Claude Code n'a
**aucune introspection native** sur ce point : sans outil externe, il
ne peut pas savoir où il en est dans sa fenêtre de contexte.

L'outil `show_context.ps1` (à la racine de ce dossier) lit les fichiers
`.jsonl` de session de Claude Code et retourne, pour la session en
cours, le total prompt et son pourcentage de la fenêtre.

> **Limite actuelle** : l'outil est en PowerShell, donc **Windows
> uniquement**. Sur macOS / Linux, il faudra le porter (les `.jsonl`
> de Claude Code se trouvent dans `~/.claude/projects/<projet>/`).

### Étape 1 — Repérer le chemin local de ton clone

Note l'emplacement où tu as cloné ce repo, par exemple :
- Windows : `C:\Users\<toi>\dev\PROTOCOLE`
- macOS / Linux : `~/dev/PROTOCOLE` (le script ne marchera pas tel quel,
  voir limite ci-dessus)

### Étape 2 — Coller ce bloc dans `~/.claude/CLAUDE.md`

Ajoute ce bloc à la fin de ton `CLAUDE.md` (global ou projet, selon ta
config). **Remplace `<CHEMIN_VERS_TON_CLONE>`** par ton chemin réel.

```markdown
## Auto-monitoring du contexte

L'IA n'a aucune introspection native sur sa consommation de tokens. Avant toute
grosse tâche (refactor multi-fichiers, audit large, gros docs, batch d'edits) et
périodiquement sur les longues sessions, lancer via Bash :
`powershell.exe -NoProfile -ExecutionPolicy Bypass -File "<CHEMIN_VERS_TON_CLONE>/show_context.ps1"`

Le script affiche le % de la fenêtre 200k consommé. Seuils d'action :
- **< 50 %** feu vert.
- **50–75 %** prévenir, penser à découper.
- **75–90 %** prévenir, **sauvegarder l'état** (commit WIP, note dans journal, maître à jour), découper.
- **> 90 %** stop, tout sauvegarder dans maître/journal, proposer une nouvelle session.

Le chiffre lu = état au **tour précédent** (le tour courant n'est pas encore flushé), prévoir une marge.
Détails complets : section 12 de `PROTOCOLE.md` (repo : github.com/kinowill/PROTOCOLE).
```

### Étape 3 — Vérifier que ton Claude le voit

Dans une nouvelle session Claude Code, demande simplement :
> « Combien de tokens reste-t-il dans ma fenêtre de contexte ? »

Si Claude répond en exécutant la commande `powershell.exe ... show_context.ps1`
et te donne un pourcentage réel, c'est gagné. S'il répond « je ne sais pas »
ou s'il invente, le bloc n'est pas chargé : vérifier le chemin et le fait
que le `CLAUDE.md` est bien lu en début de session.

### Côté utilisateur (toi, pas l'IA)

Pour pouvoir consulter l'état du contexte en deux clics, créer un raccourci
`.bat` sur le bureau qui contient :

```bat
@echo off
chcp 65001 >nul
title Claude Code - Etat des contextes
powershell.exe -NoProfile -ExecutionPolicy Bypass -File "<CHEMIN_VERS_TON_CLONE>\show_context.ps1"
echo.
pause
```
