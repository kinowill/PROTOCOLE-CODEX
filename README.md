# Protocole de travail IA - Codex

## Pourquoi ce protocole existe

Ce dossier contient un protocole de travail pour Codex appliqué à des projets
maîtrisés par un utilisateur qui ne code pas forcément lui-même.

L'enjeu n'est pas la productivité brute. L'enjeu est que **l'utilisateur reste
maître d'un projet qu'il ne code pas lui-même**. Sans cadre, un agent IA :

- avance sans laisser de trace lisible ;
- introduit des erreurs qui ne se voient que des semaines plus tard ;
- présente comme "fini" du code qui n'a jamais touché la prod ;
- repart à chaque session d'une interprétation différente du projet ;
- transforme progressivement le repo en boîte noire.

Le protocole transforme ce risque en processus contrôlable.

## Règle de lecture

`PROTOCOLE.md` est la source canonique. Il ne doit pas être remplacé par une
version courte, une checklist ou une synthèse. Les fichiers d'intégration
expliquent comment l'injecter dans Codex, mais ils ne remplacent pas sa lecture
complète.

## Démarrage rapide

### Installation globale recommandée

À utiliser si tu veux que Codex applique le protocole dans tous tes projets.

1. Ouvre ou crée le fichier global Codex :

```text
Windows : C:\Users\<toi>\.codex\AGENTS.md
macOS / Linux : ~/.codex/AGENTS.md
```

2. Colle dedans **l'intégralité** de `PROTOCOLE.md`.

3. Relance Codex.

4. Teste dans un projet sans document maître : Codex doit proposer de créer le
   maître avant d'agir sur le chantier demandé.

### Installation par projet

À utiliser si le protocole doit vivre dans un repo précis.

1. Copie `templates/AGENTS.md` à la racine du projet.
2. Remplis les spécificités projet : stack, commandes, sources de vérité,
   zones sensibles, contraintes de prod.
3. Colle ensuite l'intégralité de `PROTOCOLE.md` dans la section prévue si le
   projet doit être autonome.

### Hybride recommandé

Le mode le plus pratique au quotidien :

- `~/.codex/AGENTS.md` contient le protocole complet ;
- chaque projet contient un `AGENTS.md` court avec seulement ses spécificités ;
- le `AGENTS.md` projet ne résume pas le protocole, il le complète.

## Ce que contient ce dossier

| Fichier | Rôle |
|---|---|
| `PROTOCOLE.md` | Le protocole canonique complet. C'est le cœur du dossier. |
| `ROADMAP.md` | Backlog opératif du repo protocole lui-même. |
| `CHANGELOG.md` | Historique des versions du protocole Codex. |
| `templates/DOCUMENT_MAITRE.md` | Squelette de document maître à copier dans un nouveau projet. |
| `templates/ROADMAP.md` | Squelette de roadmap minimale. |
| `templates/VALIDATION_LOG.md` | Squelette de journal de validation. |
| `templates/AGENTS.md` | Squelette `AGENTS.md` pour connecter un projet à Codex sans résumer le protocole. |
| `integrations/codex.md` | Méthode d'intégration Codex : global, projet, skills, rules, contexte, `rtk`, `gh`. |

## Comment utiliser ce dossier avec Codex

1. Lire `PROTOCOLE.md` en entier au moins une fois.
2. Suivre `integrations/codex.md` pour choisir l'intégration : globale,
   projet, ou hybride.
3. Sur chaque projet, copier les fichiers de `templates/` utiles à la racine
   ou dans `docs/`, puis les remplir.
4. Si le projet n'a pas encore de document maître ou de roadmap, Codex doit
   les créer en début de session avant d'agir sur le chantier demandé.
5. Faire évoluer ce dossier, pas des copies divergentes. Quand une règle
   change, la modifier ici, puis réinjecter le protocole dans Codex.

## Test minimal

Dans un projet sans document maître :

1. Lance une nouvelle session Codex.
2. Pose une demande simple sur le projet.
3. Codex doit constater l'absence du maître et proposer de le créer avant de
   modifier ou analyser profondément le projet.

Si Codex répond directement à la demande sans mentionner les sources de vérité,
le protocole n'est pas chargé ou il est trop faible dans la hiérarchie des
instructions. Vérifie `AGENTS.md`, `AGENTS.override.md`, le dossier de lancement
et les instructions projet.

## Positionnement Codex

Codex dispose de mécanismes propres : `AGENTS.md`, `AGENTS.override.md`,
skills, rules, sandbox, permissions, slash commands, agents parallèles,
connecteurs et mémoires. Le protocole Codex les utilise comme surfaces
d'intégration, mais ne délègue jamais la vérité du projet à ces mécanismes.

La vérité durable reste : document maître, roadmap, journal de validation,
code réellement présent, migrations et prod réellement alignée.

## Licence

Usage libre, personnel ou commercial. Pas de garantie. Améliorer et redistribuer
encouragé.
