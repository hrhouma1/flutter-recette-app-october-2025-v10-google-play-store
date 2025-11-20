# Guide de Publication sur Google Play Store

## Vue d'ensemble

Ce guide vous accompagne étape par étape pour publier votre application Flutter sur le Google Play Store.

**Durée estimée** : 3-5 heures pour la première publication

**Coût** : 25 USD (frais unique d'inscription développeur)

---

## Table des matières

1. [Prérequis](#1-prérequis)
2. [Créer un compte développeur](#2-créer-un-compte-développeur)
3. [Préparer l'application](#3-préparer-lapplication)
4. [Générer la clé de signature](#4-générer-la-clé-de-signature)
5. [Configurer le build Android](#5-configurer-le-build-android)
6. [Créer le fichier AAB](#6-créer-le-fichier-aab)
7. [Créer la fiche Play Store](#7-créer-la-fiche-play-store)
8. [Télécharger et publier](#8-télécharger-et-publier)
9. [Vérification et validation](#9-vérification-et-validation)

---

## 1. Prérequis

### Avant de commencer

- [ ] Application Flutter fonctionnelle
- [ ] Compte Gmail actif
- [ ] Carte bancaire pour le paiement (25 USD)
- [ ] Icône de l'application (512x512px)
- [ ] Captures d'écran de l'app (minimum 2)
- [ ] Description de l'application préparée
- [ ] Politique de confidentialité (obligatoire)

### Vérifications techniques

```bash
# Vérifier la version de Flutter
flutter --version

# Vérifier que l'app compile
flutter build apk --release

# Tester sur un appareil réel
flutter run --release
```

---

## 2. Créer un compte développeur

### Étape 2.1 : Inscription

1. Aller sur : https://play.google.com/console
2. Se connecter avec votre compte Gmail
3. Accepter les conditions d'utilisation
4. Payer les frais de 25 USD (paiement unique)
5. Remplir les informations du compte développeur

### Informations requises

- Nom du développeur (visible publiquement)
- Adresse email de contact
- Numéro de téléphone
- Adresse physique
- Site web (optionnel mais recommandé)

### Délai d'activation

- Vérification du compte : 24-48 heures
- Vous recevrez un email de confirmation

---

## 3. Préparer l'application

### Étape 3.1 : Mettre à jour pubspec.yaml

```yaml
name: flutter_rec_oct_2025_v3
description: Application de recettes avec favoris
version: 1.0.0+1

# Format : version_majeure.version_mineure.version_patch+build_number
# Exemple : 1.0.0+1 signifie version 1.0.0, build 1
```

**Important** : À chaque mise à jour, incrémentez le numéro de version.

### Étape 3.2 : Configurer android/app/build.gradle.kts

```kotlin
android {
    namespace = "com.votrecompagnie.flutter_rec_oct_2025_v3"
    compileSdk = 34
    
    defaultConfig {
        applicationId = "com.votrecompagnie.flutter_rec_oct_2025_v3"
        minSdk = 21
        targetSdk = 34
        versionCode = 1
        versionName = "1.0.0"
    }
}
```

**À modifier** :
- `namespace` : Identifiant unique de votre app
- `applicationId` : Même valeur que namespace
- `versionCode` : Incrémenter à chaque publication (1, 2, 3...)
- `versionName` : Version visible par les utilisateurs (1.0.0, 1.0.1...)

### Étape 3.3 : Modifier le nom de l'application

**Fichier** : `android/app/src/main/AndroidManifest.xml`

```xml
<application
    android:label="Recipes App"
    android:name="${applicationName}"
    android:icon="@mipmap/ic_launcher">
```

Remplacer `Recipes App` par le nom souhaité.

### Étape 3.4 : Changer l'icône de l'application

**Option 1 : Utiliser flutter_launcher_icons**

1. Ajouter dans `pubspec.yaml` :

```yaml
dev_dependencies:
  flutter_launcher_icons: ^0.13.1

flutter_launcher_icons:
  android: true
  ios: false
  image_path: "assets/icon/app_icon.png"
  adaptive_icon_background: "#ffffff"
  adaptive_icon_foreground: "assets/icon/app_icon.png"
```

2. Placer votre icône (512x512px) dans `assets/icon/app_icon.png`

3. Générer les icônes :

```bash
flutter pub get
flutter pub run flutter_launcher_icons
```

**Option 2 : Manuellement**

Remplacer les fichiers dans `android/app/src/main/res/mipmap-*/ic_launcher.png`

---

## 4. Générer la clé de signature

### Pourquoi une clé de signature ?

La clé de signature garantit que les mises à jour proviennent du même développeur.

**IMPORTANT** : Ne perdez jamais cette clé. Conservez-la en lieu sûr.

### Étape 4.1 : Créer la clé

**Sur Windows** :

```bash
keytool -genkey -v -keystore c:\Users\VOTRE_NOM\upload-keystore.jks -storetype JKS -keyalg RSA -keysize 2048 -validity 10000 -alias upload
```

**Sur Mac/Linux** :

```bash
keytool -genkey -v -keystore ~/upload-keystore.jks -storetype JKS -keyalg RSA -keysize 2048 -validity 10000 -alias upload
```

### Étape 4.2 : Répondre aux questions

```
Entrez le mot de passe du fichier de clés: [Votre mot de passe]
Ressaisissez le nouveau mot de passe: [Même mot de passe]

Quels sont vos nom et prénom ?
  [Votre nom] : John Doe

Quel est le nom de votre unité organisationnelle ?
  [Votre organisation] : MonEntreprise

Quel est le nom de votre organisation ?
  [Nom organisation] : MonEntreprise Inc

Quel est le nom de votre ville de résidence ?
  [Votre ville] : Paris

Quel est le nom de votre état ou province ?
  [Votre région] : Ile-de-France

Quel est le code pays à deux lettres pour cette unité ?
  [Code pays] : FR
```

**Important** : Notez le mot de passe dans un endroit sûr.

### Étape 4.3 : Créer le fichier de configuration

**Fichier** : `android/key.properties` (à créer)

```properties
storePassword=VOTRE_MOT_DE_PASSE
keyPassword=VOTRE_MOT_DE_PASSE
keyAlias=upload
storeFile=C:\\Users\\VOTRE_NOM\\upload-keystore.jks
```

**Sur Mac/Linux** :

```properties
storePassword=VOTRE_MOT_DE_PASSE
keyPassword=VOTRE_MOT_DE_PASSE
keyAlias=upload
storeFile=/Users/VOTRE_NOM/upload-keystore.jks
```

**Sécurité** : Ajoutez `key.properties` dans `.gitignore` :

```
# Android signing
android/key.properties
*.jks
```

---

## 5. Configurer le build Android

### Étape 5.1 : Modifier android/app/build.gradle.kts

**Avant le bloc `android {`**, ajouter :

```kotlin
def keystoreProperties = new Properties()
def keystorePropertiesFile = rootProject.file('key.properties')
if (keystorePropertiesFile.exists()) {
    keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
}

android {
    // ... reste de la configuration
}
```

### Étape 5.2 : Ajouter la configuration de signature

**Dans le bloc `android {}`**, avant `buildTypes` :

```kotlin
signingConfigs {
    create("release") {
        keyAlias = keystoreProperties["keyAlias"] as String
        keyPassword = keystoreProperties["keyPassword"] as String
        storeFile = file(keystoreProperties["storeFile"] as String)
        storePassword = keystoreProperties["storePassword"] as String
    }
}

buildTypes {
    getByName("release") {
        signingConfig = signingConfigs.getByName("release")
    }
}
```

### Configuration complète de build.gradle.kts

```kotlin
def keystoreProperties = new Properties()
def keystorePropertiesFile = rootProject.file('key.properties')
if (keystorePropertiesFile.exists()) {
    keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
}

plugins {
    id("com.android.application")
    id("kotlin-android")
    id("dev.flutter.flutter-gradle-plugin")
}

android {
    namespace = "com.votrecompagnie.flutter_rec_oct_2025_v3"
    compileSdk = 34
    
    defaultConfig {
        applicationId = "com.votrecompagnie.flutter_rec_oct_2025_v3"
        minSdk = 21
        targetSdk = 34
        versionCode = 1
        versionName = "1.0.0"
    }
    
    signingConfigs {
        create("release") {
            keyAlias = keystoreProperties["keyAlias"] as String
            keyPassword = keystoreProperties["keyPassword"] as String
            storeFile = file(keystoreProperties["storeFile"] as String)
            storePassword = keystoreProperties["storePassword"] as String
        }
    }
    
    buildTypes {
        getByName("release") {
            signingConfig = signingConfigs.getByName("release")
            minifyEnabled = true
            shrinkResources = true
        }
    }
}
```

---

## 6. Créer le fichier AAB

### Qu'est-ce qu'un AAB ?

AAB (Android App Bundle) est le format requis par Google Play. Il optimise la taille de l'app pour chaque appareil.

### Étape 6.1 : Nettoyer le projet

```bash
flutter clean
flutter pub get
```

### Étape 6.2 : Générer l'AAB

```bash
flutter build appbundle --release
```

### Étape 6.3 : Localiser le fichier

Le fichier AAB se trouve dans :

```
build/app/outputs/bundle/release/app-release.aab
```

### Vérifications

- Taille du fichier : Typiquement 10-50 MB
- Si l'erreur de signature apparaît, vérifiez `key.properties`
- Testez avant de publier

---

## 7. Créer la fiche Play Store

### Étape 7.1 : Créer une nouvelle application

1. Aller sur : https://play.google.com/console
2. Cliquer sur "Créer une application"
3. Remplir les informations de base

### Informations requises

**Nom de l'application**
- Nom : "Recipes App" (maximum 50 caractères)
- Langue par défaut : Français

**Type d'application**
- Application
- Gratuite ou payante

**Déclarations**
- Conformité aux règles
- Destinée aux enfants : Oui/Non

### Étape 7.2 : Fiche du Store

**Description courte** (80 caractères max)
```
Application de recettes avec favoris et catégories
```

**Description complète** (4000 caractères max)
```
Découvrez des centaines de recettes délicieuses avec notre application intuitive.

FONCTIONNALITÉS :
• Parcourir les recettes par catégorie
• Ajouter des recettes à vos favoris
• Voir les temps de préparation et calories
• Interface moderne et facile à utiliser
• Synchronisation avec Firebase

CATÉGORIES DISPONIBLES :
• Petit-déjeuner
• Déjeuner
• Dîner
• Desserts
• Et plus encore

Parfait pour les cuisiniers débutants et expérimentés !
```

### Étape 7.3 : Ressources graphiques

**Icône de l'application**
- Format : PNG
- Taille : 512x512 pixels
- Pas de transparence

**Capture d'écran du téléphone** (obligatoire)
- Minimum : 2 captures
- Maximum : 8 captures
- Format : PNG ou JPEG
- Dimensions : 16:9 ou 9:16
- Taille min : 320px sur le côté court

**Capture d'écran de la tablette** (optionnel)
- Même format que téléphone
- Recommandé pour meilleure visibilité

**Bannière de l'application** (optionnel)
- Taille : 1024x500 pixels
- Utilisée pour promotions

### Étape 7.4 : Catégorisation

**Catégorie de l'application**
- Alimentation et boissons

**Tags** (5 maximum)
- Recettes
- Cuisine
- Alimentation
- Favoris
- Meal planning

### Étape 7.5 : Coordonnées

**Email de contact**
- Email public visible sur le Play Store

**Politique de confidentialité** (obligatoire)
- URL d'une page web avec votre politique
- Peut être hébergée sur GitHub Pages ou votre site

**Exemple de politique simple** :

```
Politique de Confidentialité

Cette application utilise Firebase pour stocker :
- Les catégories de recettes
- Les détails des recettes
- Les favoris des utilisateurs

Nous ne collectons aucune information personnelle identifiable.
Les données sont stockées de manière anonyme.

Contact : votre-email@example.com
```

---

## 8. Télécharger et publier

### Étape 8.1 : Télécharger l'AAB

1. Dans Play Console, aller dans "Versions" > "Production"
2. Cliquer sur "Créer une version"
3. Télécharger le fichier `app-release.aab`
4. Google analyse automatiquement le fichier (5-10 minutes)

### Étape 8.2 : Compléter les informations de version

**Nom de la version** : Version 1.0.0

**Notes de version** (500 caractères max) :

```
Version initiale :
• Parcourir les recettes par catégorie
• Système de favoris
• Interface moderne
• Synchronisation Firebase
```

### Étape 8.3 : Classification du contenu

**Questionnaire obligatoire** :

1. Violence : Non
2. Contenu sexuel : Non
3. Langage grossier : Non
4. Contenu généré par les utilisateurs : Non (si pas de commentaires)
5. Partage de localisation : Non
6. Achats dans l'app : Non (si gratuit)

### Étape 8.4 : Public cible

**Tranches d'âge**
- Sélectionner : Tout public ou âge spécifique
- Pour une app de recettes : Tout public approprié

### Étape 8.5 : Tarifs et distribution

**Prix**
- Gratuit (ne peut plus être changé en payant)
- Payant : Définir le prix

**Pays de distribution**
- Sélectionner les pays où publier
- Recommandé : Monde entier

### Étape 8.6 : Déclaration de confidentialité des données

**Formulaire obligatoire** :

1. Collectez-vous des données ? Oui/Non
2. Si oui, lesquelles ?
   - Favoris des utilisateurs
3. Comment sont-elles utilisées ?
   - Fonctionnalité de l'app
4. Les données sont-elles partagées ? Non
5. Chiffrement des données ? Oui (Firebase)

---

## 9. Vérification et validation

### Étape 9.1 : Vérification pre-lancement

Google teste automatiquement votre app sur plusieurs appareils :

**Durée** : 1-2 heures

**Tests effectués** :
- Installation
- Ouverture de l'app
- Navigation de base
- Plantages potentiels

**Résultats** :
- Rapport de pré-lancement disponible
- Captures d'écran automatiques
- Logs d'erreurs éventuels

### Étape 9.2 : Révision par Google

**Délai de révision** :
- Version initiale : 3-7 jours
- Mises à jour : 1-3 jours

**Statut possibles** :
1. En cours de révision
2. Approuvé et publié
3. Rejeté (avec raisons)

### Étape 9.3 : Causes de rejet fréquentes

**Problèmes techniques**
- L'app plante au démarrage
- Fonctionnalités cassées
- Problèmes de permissions

**Problèmes de contenu**
- Description trompeuse
- Captures d'écran ne correspondent pas
- Contenu inapproprié

**Problèmes de conformité**
- Politique de confidentialité manquante
- Déclarations inexactes
- Violations de copyright

### Étape 9.4 : Après publication

**Vérifications post-publication** :

1. Rechercher votre app sur Play Store
2. Télécharger et tester
3. Vérifier les statistiques
4. Surveiller les avis utilisateurs
5. Corriger les bugs signalés

---

## Checklist finale

### Avant de soumettre

- [ ] Version et versionCode corrects
- [ ] Clé de signature créée et sauvegardée
- [ ] AAB généré sans erreurs
- [ ] Icône 512x512px prête
- [ ] Minimum 2 captures d'écran
- [ ] Description complète rédigée
- [ ] Politique de confidentialité en ligne
- [ ] Email de contact configuré
- [ ] Catégorie sélectionnée
- [ ] Classification du contenu complétée
- [ ] Public cible défini
- [ ] Pays de distribution sélectionnés
- [ ] Déclaration de données complétée

### Après soumission

- [ ] Révision de pré-lancement passée
- [ ] Pas d'erreurs dans les logs
- [ ] En attente de révision par Google
- [ ] Email de confirmation reçu

### Après publication

- [ ] App visible sur Play Store
- [ ] Installation et test OK
- [ ] Statistiques vérifiées
- [ ] Répondre aux avis utilisateurs
- [ ] Planifier les mises à jour

---

## Commandes utiles

### Générer AAB

```bash
flutter build appbundle --release
```

### Générer APK (pour tests uniquement)

```bash
flutter build apk --release
```

### Analyser la taille de l'app

```bash
flutter build appbundle --analyze-size
```

### Tester en mode release

```bash
flutter run --release
```

### Vérifier la signature

```bash
keytool -list -v -keystore upload-keystore.jks
```

---

## Résolution des problèmes

### Erreur : "Signing key not found"

**Solution** :
1. Vérifier que `key.properties` existe
2. Vérifier le chemin vers le fichier `.jks`
3. Vérifier les mots de passe

### Erreur : "Version code must be greater"

**Solution** :
1. Incrémenter `versionCode` dans `build.gradle.kts`
2. Incrémenter le numéro dans `pubspec.yaml`

### AAB trop volumineux

**Solution** :
1. Activer `shrinkResources` dans `build.gradle.kts`
2. Supprimer les assets inutilisés
3. Compresser les images

### App rejetée pour plantage

**Solution** :
1. Consulter les logs de pré-lancement
2. Tester sur plusieurs appareils
3. Corriger les erreurs null safety
4. Gérer les exceptions

---

## Mises à jour futures

### Pour publier une mise à jour

1. Incrémenter la version dans `pubspec.yaml` :
   ```yaml
   version: 1.0.1+2
   ```

2. Incrémenter dans `build.gradle.kts` :
   ```kotlin
   versionCode = 2
   versionName = "1.0.1"
   ```

3. Générer le nouvel AAB :
   ```bash
   flutter build appbundle --release
   ```

4. Télécharger sur Play Console
5. Ajouter les notes de version
6. Soumettre pour révision

### Versionnement recommandé

- **1.0.0** : Version initiale
- **1.0.1** : Corrections de bugs mineurs
- **1.1.0** : Nouvelles fonctionnalités mineures
- **2.0.0** : Refonte majeure

---

## Ressources utiles

### Documentation officielle

- Flutter : https://docs.flutter.dev/deployment/android
- Play Console : https://support.google.com/googleplay/android-developer
- Android : https://developer.android.com/distribute

### Outils

- App Icon Generator : https://appicon.co
- Screenshot Generator : https://studio.app-mockup.com
- Privacy Policy Generator : https://www.privacypolicygenerator.info

### Support

- Flutter Discord : https://discord.gg/flutter
- Stack Overflow : Tag `flutter` + `google-play`
- Play Console Help Center

---

## Coûts récapitulatifs

| Item | Coût | Fréquence |
|------|------|-----------|
| Compte développeur Google Play | 25 USD | Une fois |
| Hébergement politique de confidentialité | 0-10 USD/mois | Mensuel |
| Certificat SSL (si site perso) | 0-50 USD/an | Annuel |
| Total première publication | ~25-35 USD | - |

**Note** : Après le paiement initial de 25 USD, publier des apps est gratuit.

---

## Temps estimé par étape

| Étape | Durée |
|-------|-------|
| Création compte développeur | 30 min + 24-48h validation |
| Préparation de l'app | 1-2 heures |
| Génération de la clé | 15 minutes |
| Configuration build | 30 minutes |
| Création AAB | 5-10 minutes |
| Création fiche Play Store | 1-2 heures |
| Téléchargement et soumission | 30 minutes |
| Révision par Google | 3-7 jours |
| **Total** | **4-6 heures + attente** |

---

## Conclusion

La publication sur Google Play Store nécessite :
1. Préparation technique de l'app
2. Création des assets graphiques
3. Rédaction du contenu marketing
4. Configuration de la signature
5. Conformité aux règles Google

**Première publication** : Processus long mais nécessaire une seule fois.

**Mises à jour futures** : Beaucoup plus rapides (20-30 minutes).

Suivez ce guide étape par étape et votre application sera publiée avec succès.

