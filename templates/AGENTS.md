# AGENTS.md - [NOM DU PROJET]

Ce fichier connecte le projet au protocole Codex. Il ne remplace pas
`PROTOCOLE.md` par une version courte.

## Spécificités projet

- **Nom** :
- **But** :
- **Langue de travail** : français sauf indication contraire
- **Stack** :
- **Cible de prod** :
- **Zones sensibles** : auth, données utilisateurs, paiements, migrations,
  sécurité, RGPD, secrets, ou autre zone à préciser

## Sources de vérité projet

À lire en début de session, dans cet ordre :

1. `DOCUMENT_MAITRE.md` ou `docs/DOCUMENT_MAITRE.md`
2. `ROADMAP.md` ou `docs/ROADMAP.md`
3. Dernier `VALIDATION_LOG.md` utile ou journal équivalent
4. Code, migrations, scripts et configuration réellement présents

Si le document maître ou la roadmap manque, Codex doit proposer de les créer
avant d'agir sur le chantier demandé.

## Commandes projet

- Installation :
- Développement local :
- Tests :
- Lint / format :
- Build :
- Déploiement :

## `rtk`

`rtk` peut exister comme wrapper dans certains environnements. Ne pas l'utiliser
systématiquement. Si le projet le mentionne ou si une commande sensible le
justifie, vérifier d'abord qu'il existe (`Get-Command rtk`, `where rtk`,
`command -v rtk`). S'il n'existe pas, utiliser les commandes standard et le dire.

## Protocole canonique

Si le protocole complet est déjà chargé dans `~/.codex/AGENTS.md`, ne pas le
répéter ici : garder ce fichier comme fiche projet.

Si ce projet doit être autonome, coller ci-dessous l'intégralité de :

```text
<chemin-vers-ce-repo>\PROTOCOLE.md
```

Ne pas coller une synthèse.
