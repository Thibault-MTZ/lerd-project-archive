# Plan de développement

Suivi des cases à cocher et versions proposées : [feuille de route](FEUILLE-DE-ROUTE.md).
Le présent document détaille les étapes techniques ; la feuille de route suit leur validation.

État au 30 octobre 2026 : conception uniquement. Chaque étape fonctionnelle
demande une validation avant de passer à des données réelles.

## 0 — Fondation, maintenant

README français, résumé anglais, manifeste inerte, plan, analyse des conventions
LERD et contrat UX commun. Aucun service, montage, export ou changement du cœur.

## 1 — Audit du prototype local et des capacités natives

Inventorier sans les publier les dépendances du prototype Homelab. Distinguer
fichiers de projet, bases locales gérées par LERD, bases externes et liens Git.
Vérifier sur une version identifiée les API/commandes d'inventaire, arrêt,
export/import, enregistrement et retrait. Documenter chaque contrat et son test.
Ouvrir ensuite une discussion ciblée sur les capacités manquantes ; aucun
contournement des fichiers internes ou accès direct aux conteneurs.

**Sortie :** matrice des capacités vérifiées, dépendances et blocages documentés.

## 2 — Prévisualisation sans écriture

Inventaire natif, sélection, poids et espace potentiellement libérable, groupe de
worktrees complet, destination choisie et exclusions visibles. Estimations séparées
des mesures ; une base inconnue bloque au lieu d'être traitée comme vide.

**Sortie :** plan d'opération lisible, empreinte du périmètre et conflits détectés.

## 3 — Sauvegarde et restauration sur jeux jetables

Créer un format versionné et vérifiable. Tester export puis restauration dans un
autre dossier sans suppression de source, avec SQLite et bases locales supportées.
Préserver dépôt Git commun, branches, fichiers non suivis et métadonnées requises.
Contrôler les chemins, permissions et liens à l'extraction. Ne pas exécuter de
scripts de l'archive ni appliquer des migrations automatiquement.

**Sortie :** aller-retour contrôlé, corruption et archive incomplète refusées.

## 4 — File durable et interface

Une tâche active au départ ; plusieurs ajouts possibles. Journal expurgé, étapes,
temps écoulé, activité récente et reprise contrôlée après interruption. La fermeture
du navigateur ne doit pas perdre les tâches. Annulation seulement aux points sûrs.
L'architecture du worker doit d'abord respecter les surfaces autorisées par LERD.

**Sortie :** panne réseau, manque d'espace, double clic, redémarrage et concurrence
couverts ; aucun succès affiché avant la vérification complète.

## 5 — Archivage froid sur la même instance

Arrêter les composants propres au projet via les interfaces supportées ; ne pas
arrêter les services partagés. Revalider le plan, vérifier l'archive et sa durabilité,
puis demander la libération locale. Ne jamais supprimer une base externe. Le retrait
du catalogue LERD et les dossiers surveillés doivent être traités sans réapparition
automatique du projet. Un worktree ne se sépare pas de son dépôt commun par accident.

**Sortie :** espace réellement récupéré mesuré, restauration complète démontrée,
pas de destruction de l'unique copie en cas d'échec.

## 6 — Nouvelle instance et bêta indépendante

Importer le catalogue depuis les manifestes, sans dépendre de l'ancienne machine.
Prévisualiser chemins, noms, domaines, versions et conflits ; aucun écrasement.
Vérifier les bases locales, dépendances externes et besoins de secrets. Restaurer
arrêté, sans workers de production ni partage public réactivés automatiquement.

**Sortie :** essai sur une instance propre, documentation FR/EN, captures clair/sombre,
compatibilité annoncée et retour arrière. La soumission communautaire vient ensuite.

## Plus tard

Préférences d'affichage partagées dans leur logique avec Accès et partages ; chiffrement
portable et gestion des clés à arrêter avant toute archive sensible distante ;
destinations supplémentaires, rétention et réplication indépendantes. Pas de purge
automatique ni de transfert cloud implicite dans la première version.
