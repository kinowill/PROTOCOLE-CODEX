# Protocole de travail IA — sur projet maîtrisé par un non-développeur

## Pourquoi ce protocole existe

Ce dossier contient un protocole de travail pour assistants IA (Claude Code,
Goose, Cursor, ou tout autre agent) appliqué à des projets dont **l'utilisateur
n'est pas développeur**.

L'enjeu n'est pas la productivité brute. L'enjeu est que **l'utilisateur reste
maître d'un projet qu'il ne code pas lui-même**. Sans cadre, une IA :

- avance sans laisser de trace lisible
- introduit des erreurs idiotes qui ne se voient que des semaines plus tard
- présente comme "fini" du code qui n'a jamais touché la prod
- repart à chaque session d'une interprétation un peu différente du projet
- finit par transformer le repo en boîte noire

Le protocole transforme cette roulette russe en processus.

## Ce que contient ce dossier

| Fichier | Rôle |
|---|---|
| `PROTOCOLE.md` | Le protocole canonique. C'est le cœur du produit. |
| `CHANGELOG.md` | Historique des versions du protocole. |
| `show_context.ps1` | Outil d'auto-monitoring du contexte (sections 12 du protocole). Lit les `.jsonl` de session de Claude Code et affiche la consommation de tokens en cours. **Windows / PowerShell uniquement** pour l'instant. |
| `templates/DOCUMENT_MAITRE.md` | Squelette de document maître à copier dans un nouveau projet. |
| `templates/ROADMAP.md` | Squelette de roadmap minimale. |
| `templates/VALIDATION_LOG.md` | Squelette de journal de validation. |
| `integrations/claude-code.md` | Comment injecter le protocole dans Claude Code (et activer `show_context.ps1`). |
| `integrations/goose.md` | Comment injecter le protocole dans Goose. |
| `integrations/generic.md` | Comment l'adapter à n'importe quel agent IA. |

## Comment utiliser ce dossier

1. **Lire `PROTOCOLE.md` en entier au moins une fois.** C'est court. Tout part de là.
2. **Choisir un agent** (Claude Code, Goose, etc.) et suivre l'instruction
   d'intégration correspondante dans `integrations/`.
3. **Sur chaque nouveau projet** : copier les fichiers de `templates/`
   à la racine du projet et les remplir. Si un projet existe déjà sans ces
   fichiers, le protocole impose à l'IA de les créer en début de session.
4. **Faire évoluer ce dossier**, pas chaque copie. Quand tu améliores une
   règle, tu l'améliores ici, puis tu réinjectes dans tes outils.

## Principes fondamentaux (résumé)

1. **Sources de vérité avant tout.** Aucune action sans avoir lu la vérité actuelle du projet.
2. **Document maître obligatoire.** S'il n'existe pas, le créer est la première action.
3. **Profondeur dictée par le périmètre, pas estimée.** Aucune étape n'est sautée pour gagner du temps.
4. **Distinction stricte repo / prod / validation.** Rien n'est "fini" tant que ces trois états ne sont pas explicites.
5. **Mise à jour du maître dans la même session.** Sans ça, la prochaine session travaillera sur une carte périmée.
6. **Décisions lourdes : jamais seul.** L'IA propose, l'utilisateur arbitre.

## Licence

Usage libre, personnel ou commercial. Pas de garantie. Améliorer et redistribuer
encouragé.
