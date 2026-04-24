# Roadmap - PROTOCOLE CODEX

> Backlog de référence du projet.
> Mis à jour à chaque chantier terminé ou réorienté.

Dernière mise à jour : 2026-04-24

---

## Contexte

Le repo porte la version Codex du protocole, son guide d'intégration et le
template `AGENTS.md`. Le cap actuel est de garder le protocole, l'onboarding
Codex et les rappels outillage (`rtk`, `gh`) alignés et lisibles.

## Hypothèses retenues

- `README.md` sert de document maître opératif du repo.
- `PROTOCOLE.md` reste la source canonique à injecter dans `AGENTS.md`.
- `rtk` et `gh` sont des outils optionnels de workflow, pas des sources
  de vérité du projet.

## État courant

- 2026-04-24 : cadrage de `gh` ajouté dans le protocole, l'intégration et le template.
- 2026-04-18 : adaptation dédiée à Codex publiée avec `AGENTS.md`, sandbox et slash commands.

## Priorités hautes

Format : `[ ]` à faire, `[~]` partiellement fait, `[x]` fait.

### [~] HP1 - Stabiliser l'installation Codex

**Objectif** :
- Garder `PROTOCOLE.md`, `README.md`, `integrations/codex.md` et
  `templates/AGENTS.md` strictement synchronisés.

**Actions** :
- Maintenir les consignes sur les surfaces Codex et l'outillage local.
- Vérifier que la hiérarchie des instructions reste claire pour un non-développeur.

**Livrables** :
- Protocole canonique, guide d'intégration, template `AGENTS.md`, changelog.

**Critère de fin** :
- Un utilisateur peut installer Codex en mode global, projet ou hybride
  sans ambiguïté sur `AGENTS.md`, `rtk`, `gh` et les sources de vérité.

## Priorités moyennes

### [ ] MP1 - Ajouter un exemple de projet sensible

**Objectif** :
- Montrer comment documenter auth, données utilisateurs ou prod sensible
  dans un `AGENTS.md` projet.

**Actions** :
- Rédiger un exemple bref mais réaliste.

**Livrables** :
- Exemple intégré au template ou à la doc d'intégration.

**Critère de fin** :
- Le template montre clairement comment cadrer une zone sensible.

## Priorités basses

### [ ] BP1 - Formaliser un journal de validation type

**Objectif** :
- Montrer comment consigner la validation réelle d'un chantier Codex.

**Actions** :
- Définir un exemple de validation repo / prod / validation.

**Livrables** :
- Exemple documenté ou template complémentaire.

**Critère de fin** :
- Le protocole est plus simple à appliquer après un chantier réel.

## Ordre recommandé d'exécution

1. Stabiliser la doc d'installation et d'outillage.
2. Ajouter un exemple de projet sensible.
3. Ajouter un exemple de validation réelle.

## Definition of done pour le prochain cap

Le projet franchit un cap solide quand :
- l'installation globale, projet et hybride donne les mêmes règles ;
- les outils optionnels (`rtk`, `gh`) sont cadrés sans devenir des dépendances cachées.

## Prochaine action recommandée

Tester l'installation dans un repo vierge avec `~/.codex/AGENTS.md` et un
`AGENTS.md` projet minimal, puis consigner le résultat.
