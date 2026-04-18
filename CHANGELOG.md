# Changelog

## v1.2 - 2026-04-18

Adaptation dédiée à Codex.

### Ajouts
- `integrations/codex.md` : guide d'injection du protocole dans Codex via
  `AGENTS.md`, `AGENTS.override.md`, skills, rules, sandbox, slash commands et
  rappel `rtk`.
- `templates/AGENTS.md` : squelette projet pour connecter un repo à Codex sans
  résumer le protocole.
- `PROTOCOLE.md` : nouvelle section **13 - Spécificités Codex** couvrant
  `AGENTS.md`, skills, rules, sandbox, agents parallèles et `rtk`.

### Changements
- `PROTOCOLE.md` : adaptation de la section de début de session pour inclure
  les instructions Codex actives avant l'analyse projet.
- `PROTOCOLE.md` : section contexte réécrite pour Codex avec `/status`,
  `/compact`, `/diff`, `/review`, `/mention`, `/mcp`, `/apps`, `/plugins`,
  `/permissions` et `/sandbox-add-read-dir`.
- `README.md` : repositionnement du dossier comme protocole Codex, avec règle
  explicite de non-substitution par une version courte.

### Retraits
- Suppression des intégrations Claude Code, Goose et générique dans cette copie
  Codex. Elles restent dans `PROTOCOLE CLAUDE` ou dans les versions dédiées aux
  autres agents.
- Suppression de `show_context.ps1`, spécifique à Claude Code. Pour Codex,
  utiliser les surfaces natives comme `/status` et écrire l'état durable dans
  les sources de vérité du projet avant compaction ou reprise.

## v1.1 - 2026-04-09

Ajout de l'auto-monitoring du contexte de l'IA dans la version Claude.

### Ajouts
- `PROTOCOLE.md` : nouvelle **section 12 - Auto-monitoring du contexte**.
  L'IA doit s'auto-vérifier sur sa consommation de tokens avant toute
  grosse tâche, avec des seuils d'action explicites (50 / 75 / 90 %).
  L'ancienne section 12 « Pourquoi ce protocole tient » est renumérotée 13.
- `show_context.ps1` à la racine : outil PowerShell qui lit les `.jsonl`
  de session de Claude Code et retourne, pour la session en cours, le
  total prompt et son pourcentage de la fenêtre de contexte.
- `integrations/claude-code.md` : nouvelle section « Activer l'auto-monitoring
  du contexte » avec un bloc prêt à coller dans `~/.claude/CLAUDE.md`,
  et un raccourci `.bat` à créer pour l'utilisateur.
- `README.md` : `show_context.ps1` listé dans le tableau des fichiers.

### Limites connues
- L'outil est en PowerShell, donc **Windows uniquement** pour l'instant.
  Portage macOS / Linux à faire.
- Le chiffre lu correspond à l'état au tour précédent de la session
  (le tour courant n'est pas encore flushé dans le `.jsonl`).

## v1.0 - 2026-04-07

Première version stable du protocole, extraite et généralisée à partir
du protocole opérationnel utilisé sur le projet Lucide.

### Contenu initial
- `PROTOCOLE.md` - protocole canonique en 12 sections
- `templates/` - squelettes de document maître, roadmap, journal de validation
- `integrations/` - instructions d'intégration pour Claude Code, Goose et agents génériques
- `README.md` - guide d'usage du dossier

### Principes consolidés
- Création obligatoire du document maître si absent en début de session
- Distinction stricte repo / prod / validation comme contrat de fin de tâche
- Mise à jour du maître dans la même session que toute modification de vérité
- Profondeur de lecture dictée par le périmètre, jamais estimée
- Posture critique face aux recommandations externes
