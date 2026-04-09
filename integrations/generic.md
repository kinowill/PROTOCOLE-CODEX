# Intégration — Agent générique

Ce guide s'applique à n'importe quel assistant IA qui accepte un
**prompt système** ou un **fichier d'instructions persistant** :
Cursor, Cline, Continue, Aider, ChatGPT custom GPTs, agents maison
basés sur l'API Claude / OpenAI / Gemini, etc.

## Principe général

Tous ces outils ont, sous une forme ou une autre, un endroit pour mettre
des instructions qui s'appliquent à chaque session. C'est là qu'on
injecte le protocole.

| Outil | Endroit où injecter |
|---|---|
| Cursor | `.cursorrules` à la racine du projet, ou Settings → Rules |
| Cline | Custom Instructions dans les settings |
| Continue | `~/.continue/config.json` → `systemMessage` |
| Aider | `--read CONVENTIONS.md` ou `.aider.conf.yml` |
| ChatGPT custom GPT | Champ "Instructions" du GPT |
| API directe | Paramètre `system` de l'appel |

## Méthode universelle

1. Copier le contenu de `PROTOCOLE.md`.
2. Le coller dans le champ "instructions système" de l'outil choisi.
3. Si l'outil supporte un fichier projet en plus du système global,
   y ajouter une courte fiche projet (langue, stack, sources de vérité)
   pour éviter de réécrire le protocole à chaque projet.

## Adaptations possibles

Selon l'outil, tu peux :

- **Raccourcir** le protocole si la fenêtre de prompt est limitée
  (mais ne jamais retirer les sections 3, 5, 6 — protocole de début,
  distinction repo/prod/validation, mise à jour du maître).
- **Traduire** le protocole dans une autre langue si l'utilisateur
  ne travaille pas en français.
- **Ajouter** des sections projet-spécifiques (conventions de code,
  outils de test, contraintes de déploiement).

## Test minimal

Quel que soit l'outil, le test pour vérifier que le protocole est actif
est toujours le même :

> Ouvrir une session sur un projet sans document maître.
> Poser une question.
> L'agent doit proposer de créer le maître avant de répondre.

Si l'agent répond directement à la question sans mentionner le maître,
le protocole n'est pas chargé ou est ignoré. Vérifier la configuration.

## Limites connues

- **Petits modèles locaux** (7B et moins) ont du mal à tenir le protocole
  sur la durée. Ils oublient une étape sur deux. Utiliser de préférence
  un modèle de classe Sonnet / GPT-4o / Gemini Pro ou équivalent.
- **Agents en mode "tool calling agressif"** peuvent vouloir exécuter
  avant de lire. Bien vérifier que l'instruction "lire avant d'agir"
  est tenue dans tes premiers tests.
- **Fenêtres de contexte courtes** : si l'agent oublie le protocole
  après quelques tours, c'est que sa fenêtre est saturée. Réduire
  la longueur des réponses ou changer d'outil.
