# Intégration — Codex

## Principe

Codex lit des instructions persistantes via `AGENTS.md`. C'est la surface
naturelle pour appliquer ce protocole.

Le protocole ne doit pas être injecté sous forme courte. `PROTOCOLE.md` est le
texte canonique complet. Les instructions ci-dessous servent uniquement à le
charger correctement dans Codex.

## Surfaces Codex concernées

| Surface | Rôle dans le protocole |
|---|---|
| `~/.codex/AGENTS.md` | Instructions globales chargées dans tous les projets. |
| `~/.codex/AGENTS.override.md` | Override global temporaire. À utiliser avec prudence. |
| `AGENTS.md` projet | Instructions versionnées avec un repo précis. |
| `AGENTS.override.md` projet | Override local ou spécialisé dans un sous-dossier. |
| Skills | Workflows réutilisables, utiles mais non garantis à chaque session. |
| Rules | Autorisations de commandes hors sandbox. Pas des consignes de projet. |
| Memories | Aides de reprise. Pas des sources de vérité. |
| Slash commands | Contrôle de session : `/status`, `/diff`, `/review`, `/compact`, `/init`, etc. |

## Option A — Protocole global Codex

À utiliser si tu veux que toutes tes sessions Codex héritent du protocole.

1. Ouvrir ou créer :

```text
C:\Users\<toi>\.codex\AGENTS.md
```

Sous macOS / Linux :

```text
~/.codex/AGENTS.md
```

2. Coller **l'intégralité** de `PROTOCOLE.md` dans ce fichier.

3. Ne pas coller une synthèse. Si la taille devient un jour un problème,
   augmenter la limite de documentation projet côté config Codex ou déplacer
   les compléments dans des `AGENTS.md` plus proches des sous-dossiers, mais
   ne pas réduire le protocole sans arbitrage explicite.

4. Relancer Codex.

5. Vérifier que le protocole est actif en demandant à Codex, dans un projet
   sans document maître, de commencer une session. Il doit identifier l'absence
   de maître et proposer de le créer avant d'agir sur le chantier demandé.

## Option B — Protocole par projet

À utiliser si tu veux versionner le protocole avec un repo précis.

1. Copier `templates/AGENTS.md` à la racine du projet :

```text
<projet>\AGENTS.md
```

2. Remplir les spécificités projet : stack, commandes, sources de vérité,
   zones sensibles, contraintes de prod.

3. Coller ensuite **l'intégralité** de `PROTOCOLE.md` dans la section prévue.

4. Committer `AGENTS.md` avec le projet si le protocole doit suivre le repo.

## Option C — Hybride recommandé

Pour un usage quotidien, le plus robuste est :

- `~/.codex/AGENTS.md` contient l'intégralité du protocole ;
- chaque projet contient un `AGENTS.md` court qui ne répète pas le protocole,
  mais ajoute les spécificités du projet ;
- si un projet nécessite une règle contradictoire, l'utilisateur arbitre et la
  contradiction est documentée dans le `AGENTS.md` projet.

Dans cette option, le `AGENTS.md` projet n'est pas une synthèse du protocole.
C'est une fiche projet complémentaire.

## Skills Codex

Une skill peut compléter le protocole, mais ne doit pas être son seul support.
Codex charge les skills par invocation explicite ou par correspondance avec leur
description. Le protocole, lui, doit être actif avant de décider quelles skills
sont utiles.

Utilisation correcte :
- créer une skill pour un workflow spécialisé ;
- annoncer quand elle est utilisée ;
- garder `AGENTS.md` comme support principal du protocole ;
- ne pas remplacer la lecture des sources de vérité par une skill.

## Rules Codex

Ne pas mettre le protocole dans `~/.codex/rules/default.rules`.

Les rules servent à autoriser, demander confirmation ou interdire des commandes
hors sandbox. Exemple de rôle acceptable : autoriser une commande récurrente ou
faire demander confirmation pour une commande sensible.

Si tu veux autoriser des wrappers projet comme `rtk`, ajoute une rule seulement
après avoir vérifié que la commande existe et qu'elle est réellement utilisée
dans tes projets. Ne pas créer de rule large qui permettrait n'importe quoi.

## Sandbox et dossiers hors workspace

Codex travaille avec des frontières d'accès. Quand un dossier est hors writable
roots, l'agent doit demander l'autorisation avant d'écrire. C'est normal.

Le protocole demande à Codex de ne pas contourner ces limites : il doit expliquer
l'accès nécessaire, demander l'autorisation, puis continuer seulement si elle est
accordée.

## `rtk`

`rtk` peut exister dans certains environnements comme wrapper autour de commandes
projet, par exemple `rtk npm ...` ou `rtk git ...`. Ce protocole demande
simplement à Codex de savoir que cette option peut exister.

Règles :
- ne pas utiliser `rtk` systématiquement ;
- vérifier si le projet le mentionne (`AGENTS.md`, README, scripts, permissions) ;
- vérifier s'il est disponible (`Get-Command rtk`, `where rtk`, `command -v rtk`)
  quand la question se pose ;
- si `rtk` n'est pas disponible, utiliser les commandes standard et le signaler ;
- ne jamais inventer une sous-commande `rtk`.

## Contexte Codex

Codex expose des commandes utiles selon la surface :

- `/status` pour voir la configuration de session et l'usage du contexte ;
- `/compact` pour compacter la conversation ;
- `/diff` pour revoir les modifications ;
- `/review` pour demander une revue du working tree ;
- `/init` pour générer un `AGENTS.md` initial ;
- `/mention` ou `@chemin` pour attacher des fichiers ;
- `/mcp`, `/apps`, `/plugins` pour voir les outils externes disponibles.

Avant `/compact`, reprise, fork ou changement d'agent, l'état réel doit être
écrit dans le document maître, la roadmap ou le journal de validation si la
vérité du projet a changé.

## Test minimal

Dans un projet sans document maître :

1. Lancer une nouvelle session Codex.
2. Poser une demande simple sur le projet.
3. Codex doit constater l'absence du maître et proposer de le créer avant de
   modifier ou analyser profondément le projet.

Si Codex répond directement à la demande sans mentionner les sources de vérité,
le protocole n'est pas chargé ou il est trop faible dans la hiérarchie des
instructions. Vérifier `AGENTS.md`, `AGENTS.override.md`, le dossier de lancement
et les instructions projet.
