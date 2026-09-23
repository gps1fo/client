# Correctif GPS 1fo sur `managed_configurations` 1.2.0

Copie de `managed_configurations` 1.2.0 (MIT, M-Way Solutions GmbH), embarquée parce que la
version publiée **ne construit pas** : `android/build.gradle` appelle `kotlinOptions` alors
qu'il n'applique jamais le greffon Kotlin — seul `com.android.library` l'est. La méthode
n'existe donc sur aucune version de Kotlin, et tout build Android du client échoue, y compris
en amont.

Mesuré le 23/09/2026 :

```
A problem occurred evaluating project ':managed_configurations'.
> Could not find method kotlinOptions() for arguments [...] on extension 'android'
  of type com.android.build.gradle.LibraryExtension.
```

## Ce qui est modifié

`android/build.gradle`, et rien d'autre :

1. `apply plugin: 'org.jetbrains.kotlin.android'` ajouté — il manquait, alors que le greffon
   livre des sources Kotlin (`src/main/kotlin/`) ;
2. le bloc `kotlinOptions { jvmTarget = ... }` remplacé par `kotlin { compilerOptions { ... } }`,
   sa forme actuelle.

## Comment le supprimer un jour

Dès qu'une version publiée construit : retirer `third_party/managed_configurations/`, retirer
l'entrée `dependency_overrides` de `pubspec.yaml`, relever la contrainte de version. Le défaut
est à signaler à https://github.com/mwaylabs/flutter-managed-configuration.
