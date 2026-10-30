# Contribution LERD : constat et trajectoire

Sources officielles consultées le 30 octobre 2026. Elles peuvent évoluer ; les
recontrôler avant une soumission. Aucun contact, issue ou PR communautaire envoyé.

## Plugin indépendant

Le [guide plugins](https://github.com/lerd-env/lerd/blob/main/docs/features/plugins.md)
décrit le manifeste, le générateur `lerd plugin new`, les surfaces UI/CLI/API et
le dossier `LERD_PLUGIN_DATA`. Les thèmes et variables CSS natifs doivent guider
la présentation. Le manifeste présent est une base documentaire manuelle, sans
exécutable ; ce n'est pas une installation testée issue du générateur.

Les limites d'exécution rendent indispensable une décision d'architecture pour les
transferts longs : API par défaut 30 secondes, maximum 10 minutes ; CLI sans cette
limite automatique. Cela ne constitue pas un ordonnanceur persistant.

## Capacités manquantes

Selon [Étendre le système de plugins](https://github.com/lerd-env/lerd/blob/main/docs/contributing/plugins.md),
une extension ne doit pas modifier la configuration interne ou intervenir directement
dans les conteneurs. Présenter d'abord le besoin dans une issue ; les ajouts au cœur
doivent être génériques, testés et versionnés. Ici, discuter stockage externe autorisé,
jobs durables, arrêt complet et portabilité plutôt que porter les contournements du
prototype. La version minimale sera celle où les contrats nécessaires sont disponibles.

## Catalogue, plus tard

Les [conditions d'approbation](https://github.com/lerd-env/plugins/blob/main/SUBMITTING.md)
imposent notamment code lisible, licence libre, périmètre et transferts expliqués,
absence de privilèges et de code téléchargé puis exécuté. Les assets restent locaux.
Les emplacements d'écriture sont limités : notre destination externe doit être
clarifiée avant de prétendre à la conformité. Aucune collecte ni transfert implicite.

La soumission au [registre](https://github.com/lerd-env/plugins) passe par une PR
sur l'entrée du plugin, pointant un commit précis du dépôt public. Chaque mise à
jour sera revue. Préparer version minimale, plateformes testées, documentation et
captures réelles ; remplir le modèle de soumission. Le présent concept n'est pas prêt.

## Si une contribution au cœur est nécessaire

Appliquer les [règles de PR du cœur](https://github.com/lerd-env/lerd/blob/main/docs/contributing/pull-requests.md) :
format Go, tests du comportement, contrôles de qualité et CI. Pour une évolution
visible, fournir avant/après et thèmes clair/sombre. Ces contrôles du dépôt Go ne
sont pas un prétexte à ajouter une chaîne Go à notre dépôt documentaire.

## Discussion proposée, non envoyée

Une discussion en anglais courte sera utile après une première validation locale.
Demander un avis d'architecture, pas une approbation prématurée ni une annonce de
fonctionnalité déjà disponible. Les commits personnels restent en français.

> I'm preparing a project cold-storage plugin, based on a workflow I already use
> in my Homelab. It would back up inactive projects, optionally free local space
> after verification, and restore them on the same or another LERD instance.
> Before porting it, I'd appreciate guidance on supported external storage
> destinations and durable jobs that can outlive a dashboard request. I want to
> use native contracts rather than edit internal state. External production
> databases would be excluded. This is currently a design proposal, not a release.
