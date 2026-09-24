# Registre des patchs Zone A

Un patch = une modification d'un fichier amont. Chaque patch doit pouvoir répondre à la
question : **« comment le supprimer un jour ? »**

Revue trimestrielle obligatoire. Indicateur de santé : le nombre de patchs supprimés par
trimestre doit être ≥ au nombre de patchs ajoutés.

| ID | Motif | Fichiers amont touchés | Remplaçable par un point d'extension ? | Proposable en PR amont ? | Ajouté le |
|----|-------|------------------------|----------------------------------------|--------------------------|-----------|
| P-001 | Déclarer le flavor `gps1fo` qui porte notre identité de paquet. Tout le contenu de marque vit dans `src/gps1fo/`, en fichiers ajoutés. | `android/app/build.gradle.kts` | Non : un product flavor ne se déclare nulle part ailleurs que dans le script Gradle du module. | Non : propre à notre marque. | 2026-09-23 |
| P-002 | Titre affiché de l'application, en dur dans le code Dart. Le contrôle de marque sur l'APK l'a trouvé dans l'instantané Dart, invisible pour `aapt2`. | `lib/main_screen.dart` | Oui, le jour où l'amont lira ce titre depuis `l10n` ou `CFBundleDisplayName` — à proposer. | Oui : « ne pas coder le nom du produit en dur » est recevable en amont. | 2026-09-23 |
| P-003 | Serveur par défaut au premier lancement : `demo.traccar.org` porte la marque et enverrait les positions de nos clients chez un tiers. Remplacé par une valeur injectée au build, vide par défaut. | `lib/preferences.dart` | Oui, si l'amont accepte un `String.fromEnvironment`. | Oui : rendre l'URL par défaut configurable au build est utile à tout le monde. | 2026-09-23 |
| P-004 | Détourner `managed_configurations` vers une copie corrigée : la version publiée ne construit pas (voir `third_party/managed_configurations/CORRECTIF-GPS1FO.md`). | `pubspec.yaml` | Non : `dependency_overrides` n'a pas d'autre emplacement. | Sans objet : le défaut est chez `mwaylabs`, pas chez Traccar — à leur signaler. | 2026-09-23 |
| P-005 | Nom affiché, nom court et schéma d'URL profonde iOS. `gps1fo://` est **ajouté** à côté du schéma amont, que le code Dart route encore. | `ios/Runner/Info.plist` | Non : Xcode lit ces valeurs dans le projet, il n'y a pas de surcharge par variante comme sur Android. | Non : propre à notre marque. | 2026-09-24 |
| P-006 | Identifiant de paquet iOS (irréversible après publication, `docs/07` §2) et bascule vers le jeu d'icônes `AppIconGps1fo`, ajouté à côté de celui de l'amont. | `ios/Runner.xcodeproj/project.pbxproj` | Non : Xcode lit ces valeurs dans le projet, il n'y a pas de surcharge par variante comme sur Android. | Non : propre à notre marque. | 2026-09-24 |
