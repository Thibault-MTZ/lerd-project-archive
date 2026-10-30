# LERD Project Archive

**Concept en préparation — aucun moteur d'archivage disponible dans ce dépôt.**

Je manque régulièrement de place sur mes machines de développement. J'utilise déjà
un outil dans mon Homelab pour mettre de côté des projets sur un NAS, puis les
récupérer lorsque j'en ai besoin. Ce dépôt prépare sa transformation en plugin
LERD indépendant de mon infrastructure.

L'idée : une zone Archives pour conserver les projets dont on n'a pas besoin
immédiatement, libérer le disque local et les rapatrier plus tard. Un projet en
stockage froid ne peut pas être lancé directement depuis cette archive.

## Trois usages envisagés

| Action | Projet local | Destination | But |
|---|---|---|---|
| Sauvegarder | Conservé | Copie vérifiée | Disposer d'un point de récupération |
| Archiver | Retiré uniquement après vérification et confirmation | Archive froide | Récupérer de l'espace local |
| Restaurer | Recréé, laissé arrêté | Même instance ou nouvelle instance LERD | Reprendre le travail ou préparer une migration |

Une migration sera une restauration validée sur une autre instance. La source
ne sera jamais supprimée automatiquement à la suite de cette restauration.
L'archive restera conservée après récupération. Une archive unique sur un NAS
n'est pas, à elle seule, une stratégie de sauvegarde indépendante.

## Aujourd'hui et ensuite

Ce premier dépôt contient le concept, le plan, les conventions UX et un manifeste
minimal sans commande, hook, API ou page active. Il ne lit aucun projet, ne modifie
aucune donnée et n'effectue aucun transfert réseau.

Je prévois de pousser le code fonctionnel dans les prochains jours, après avoir
testé et amélioré ce que j'utilise déjà en local. Il faudra ensuite l'adapter aux
interfaces natives de LERD : ce calendrier est une intention, pas une promesse de
version utilisable. Aucune installation ou utilisation en production recommandée.

Le futur export pourra contenir code, fichiers non suivis, médias, historique Git
et bases locales prises en charge. Les fichiers `.env` peuvent contenir des secrets :
leur inclusion devra être expliquée et protégée. Les bases externes à LERD, notamment
de production, seront exclues : aucun export, import ou effacement automatique.
Le transfert vers une destination choisie demandera un accord explicite.

## Documents

- [Feuille de route, schéma et jalons bêta](docs/FEUILLE-DE-ROUTE.md)
- [Plan et critères de validation](docs/PLAN.md)
- [Architecture proposée et points ouverts](docs/ARCHITECTURE.md)
- [Cohérence UX avec Accès et partages](docs/UX.md)
- [Conventions LERD et contribution](docs/CONTRIBUTION-LERD.md)
- [État du module](DOCS.md)

Vos avis sont bienvenus dans les [issues](https://github.com/Thibault-MTZ/lerd-project-archive/issues),
même sans installer quoi que ce soit. Ne publiez pas de données de projet, de
secrets ou de journaux privés. Ce projet est personnel, non officiel, et n'a pas
été soumis au catalogue LERD.

## English overview

Early concept for a LERD plugin: back up projects, move inactive projects to cold
storage, and restore them on the same or another LERD instance. Inspired by a
personal Homelab workflow. This repository currently contains planning documents
and an inert manifest only, not a working archiver. Feedback is welcome. External
production databases are out of scope. No catalog submission has been made.
