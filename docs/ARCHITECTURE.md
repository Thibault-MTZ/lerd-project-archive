# Architecture proposée — non implémentée

## Frontières

- LERD reste responsable du cycle de vie, de son registre et de ses bases gérées.
- Le plugin organise plans, manifestes, file, vérifications et présentation.
- Le stockage est choisi par l'utilisateur ; le plugin ne monte pas un NAS,
  ne demande pas de privilèges et ne modifie pas les services système.
- Les bases externes sont des dépendances référencées sans identifiants, jamais
  des ressources à exporter, importer ou supprimer. Détection incertaine : blocage.

## Deux décisions bloquantes avant le moteur

**Stockage externe.** Les règles du catalogue limitent les emplacements d'écriture.
Il faut faire confirmer le contrat d'une destination externe explicitement choisie
(NAS ou répertoire déjà monté), ou proposer une capacité native. Un choix dans une
boîte de dialogue ne prouve pas à lui seul la conformité au catalogue. Pas de lien
symbolique utilisé pour contourner cette restriction.

**Tâches longues.** Les surfaces plugin ont des délais maximum ; une archive peut
les dépasser. Ne pas détacher un processus clandestinement depuis une requête API.
Étudier une orchestration native, un job pris en charge ou une commande CLI explicite.
Le worker persistant de l'outil Homelab n'est pas transférable tel quel dans un plugin
communautaire. La fermeture du navigateur et les redémarrages doivent être couverts.

## Format envisagé

Une archive indépendante de l'instance : identifiant stable, version de format,
date UTC, origine non sensible, liste de projets/worktrees, chemins relatifs,
tailles, sommes de contrôle, versions requises, bases locales incluses et exclusions.
Le catalogue doit pouvoir être reconstruit depuis les manifestes. Les informations
de récupération ne dépendent pas uniquement d'un registre sur la machine source.

Le format exact (conteneur, compression, chiffrement) reste à sélectionner après
essais. Une somme SHA256 vérifie l'intégrité, pas la confidentialité ni l'authenticité.
Les clés de chiffrement ne seront ni commitées ni stockées avec l'archive comme seul
moyen de protection ; prévoir aussi leur récupération sur une nouvelle machine.

## Transaction proposée

Préparer → revalider → arrêter les composants concernés → exporter → transférer
en zone temporaire → vérifier → publier l'archive complète → proposer libération.
Une sauvegarde s'arrête avant libération. La restauration utilise une zone temporaire,
vérifie le résultat puis enregistre le projet via LERD ; l'archive est conservée.

Verrouiller par groupe Git et base locale partagée ; éviter doubles tâches et opérations
sur une source modifiée depuis la confirmation. Conserver un journal transactionnel
durable. Après interruption, réévaluer les deux côtés avant toute reprise destructive.
Ne jamais assimiler destination démontée et dossier local vide ; vérifier identité,
accessibilité et espace disponible du stockage avant chaque tâche.

Pas d'écrasement de destination non vide, de traversée `../`, de suivi aveugle des
liens sortants ni d'extraction exécutant du code. Une base locale partagée est une
ressource de groupe : pas de double import ni d'effacement au nom d'un seul projet.
La restauration sur une nouvelle machine impose un mappage explicite des chemins
Git et un contrôle des références, sans réutiliser aveuglément les chemins absolus.

## Contrats à vérifier

Le prototype emploie notamment `lerd db:export`/`db:import`. Leur présence ne prouve
pas que tous les moteurs, bases externes, worktrees et échecs sont couverts. Les
routes d'archivage ne sont pas inventées ici. La matrice des capacités devra citer
version, commande/API, entrées, sorties, effets et test de chaque opération.

La file, le catalogue local et les préférences techniques utiliseront le répertoire
de données du plugin. Le jeton LERD restera local et absent des journaux/archives.
Les journaux utilisateur seront des événements structurés expurgés, pas une sortie
shell brute pouvant révéler des secrets.
