# Guide de Construction : App Recettes - Étape par Étape

## Comment utiliser ce guide

1. Lisez "OÙ AJOUTER" pour savoir où coller le code
2. Copiez le bout de code
3. Collez exactement à l'endroit indiqué
4. Hot reload
5. Vérifiez l'interface
6. Passez au bout suivant

---

## Arborescence des fichiers du projet

```
flutter_rec_oct_2025_v3/
├── lib/
│   ├── main.dart                    ← ÉTAPE 0
│   ├── constants.dart               (déjà existant)
│   ├── firebase_options.dart        (déjà existant)
│   └── Views/
│       ├── app_main_screen.dart     ← ÉTAPES 1-10 (fichier principal)
│       └── view_all_items.dart      (déjà créé)
├── assets/
│   └── images/
│       └── chef_PNG190.png          (déjà existant)
└── pubspec.yaml                     (déjà configuré)
```

**Fichiers à créer/modifier** :
- ÉTAPE 0 : Modifier `lib/main.dart`
- ÉTAPES 1-10 : Créer/Modifier `lib/Views/app_main_screen.dart`

---

## Plan de construction visuel

```
ÉTAPE 0: main.dart
    ↓
ÉTAPE 1: app_main_screen.dart (structure vide)
    ↓
ÉTAPE 2: + BottomNavigationBar
    ↓
ÉTAPE 3: + MyAppHomeScreen (classe)
ÉTAPE 4: + Lier MyAppHomeScreen au body
    ↓
ÉTAPE 5: + headerParts() méthode
ÉTAPE 6: + headerParts() dans Column
    ↓
ÉTAPE 7: + mySearchBar() méthode
ÉTAPE 8: + mySearchBar() dans Column
    ↓
ÉTAPE 9: + BannerToExplore classe
ÉTAPE 10: + Banner dans Column
    ↓
ÉTAPE 11: + Titre "Categories" dans Column
    ↓
ÉTAPE 12: + StreamBuilder categories dans Column
ÉTAPE 13: + categoryButtons() méthode
    ↓
ÉTAPE 14: + import view_all_items
ÉTAPE 15: + Row "Quick & Easy" dans Column
    ↓
ÉTAPE 16: + StreamBuilder recettes dans Column
    ↓
    ✅ APP COMPLÈTE
```

---

## ÉTAPE 0 : Setup Firebase

### OÙ : Fichier `lib/main.dart`

**ACTION** : Remplacer tout le contenu du fichier par ce code

```dart
import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';
import 'package:flutter_rec_oct_2025_v3/firebase_options.dart';
import 'Views/app_main_screen.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(
    options: DefaultFirebaseOptions.currentPlatform,
  );
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const AppMainScreen(),
    );
  }
}
```

**Ce que ça fait** : Initialise Firebase et lance l'app

---

## ÉTAPE 1 : Structure de base

### OÙ : Créer fichier `lib/Views/app_main_screen.dart`

**ACTION** : Créer un nouveau fichier vide et coller ce code

### Interface actuelle
```
┌────────────────────┐
│                    │
│   Page vide        │
│                    │
│                    │
│                    │
│                    │
└────────────────────┘
```

### Bout de code 1 : Imports + Widget racine

```dart
import 'package:flutter/material.dart';
import 'package:iconsax/iconsax.dart';
import 'package:cloud_firestore/cloud_firestore.dart';
import '../constants.dart';

class AppMainScreen extends StatefulWidget {
  const AppMainScreen({Key? key}) : super(key: key);

  @override
  State<AppMainScreen> createState() => _AppMainScreenState();
}

class _AppMainScreenState extends State<AppMainScreen> {
  int selectedIndex = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      body: Center(child: Text("Page index: $selectedIndex")),
    );
  }
}
```

**Ce que ça fait** : Crée la structure de base avec Scaffold

---

## ÉTAPE 2 : Bottom Navigation Bar

### OÙ : Fichier `lib/Views/app_main_screen.dart`

**ACTION** : Dans la classe `_AppMainScreenState`, REMPLACER la méthode `build()` complète

### Interface actuelle
```
┌────────────────────┐
│                    │
│   Page index: 0    │
│                    │
│                    │
├────────────────────┤
│[🏠][♥][📅][⚙️]    │ ← Navigation bar
└────────────────────┘
```

### Bout de code 2 : Ajouter bottomNavigationBar

**REMPLACER** toute la méthode `build()` (lignes 17-23 environ) par :

```dart
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      bottomNavigationBar: BottomNavigationBar(
        backgroundColor: Colors.white,
        elevation: 0,
        iconSize: 28,
        currentIndex: selectedIndex,
        selectedItemColor: kprimaryColor,
        unselectedItemColor: Colors.grey,
        type: BottomNavigationBarType.fixed,
        items: [
          BottomNavigationBarItem(
            icon: Icon(Iconsax.home),
            label: "Home",
          ),
          BottomNavigationBarItem(
            icon: Icon(Iconsax.heart),
            label: "Favorite",
          ),
          BottomNavigationBarItem(
            icon: Icon(Iconsax.calendar),
            label: "Meal Plan",
          ),
          BottomNavigationBarItem(
            icon: Icon(Iconsax.setting),
            label: "Setting",
          ),
        ],
        onTap: (index) {
          setState(() {
            selectedIndex = index;
          });
        },
      ),
      body: Center(child: Text("Page index: $selectedIndex")),
    );
  }
```

**Ce que ça fait** : Ajoute barre de navigation avec 4 onglets

---

## ÉTAPE 3 : Créer MyAppHomeScreen

### OÙ : Fichier `lib/Views/app_main_screen.dart`

**ACTION** : Aller TOUT EN BAS du fichier (après le `}` de `_AppMainScreenState`)

### Interface actuelle
```
┌────────────────────┐
│                    │
│  MyAppHomeScreen   │
│    (vide)          │
│                    │
├────────────────────┤
│[🏠][♥][📅][⚙️]    │
└────────────────────┘
```

### Bout de code 3 : AJOUTER en bas du fichier (après la classe _AppMainScreenState)

```dart
class MyAppHomeScreen extends StatefulWidget {
  const MyAppHomeScreen({Key? key}) : super(key: key);

  @override
  State<MyAppHomeScreen> createState() => _MyAppHomeScreenState();
}

class _MyAppHomeScreenState extends State<MyAppHomeScreen> {
  String selectedCategory = "All";
  final FirebaseFirestore _firestore = FirebaseFirestore.instance;

  @override
  Widget build(BuildContext context) {
    return SafeArea(
      child: SingleChildScrollView(
        child: Padding(
          padding: const EdgeInsets.symmetric(horizontal: 15),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Text("Hello from HomeScreen"),
            ],
          ),
        ),
      ),
    );
  }
}
```

**Ce que ça fait** : Crée page d'accueil vide

### Bout de code 4 : Utiliser MyAppHomeScreen

### OÙ : Dans la classe `_AppMainScreenState`, méthode `build()`

**ACTION** : Chercher la ligne `body: Center(child: Text("Page index: $selectedIndex")),` et REMPLACER par :

```dart
      body: selectedIndex == 0
          ? const MyAppHomeScreen()
          : Center(child: Text("Page index: $selectedIndex")),
```

**Ce que ça fait** : Affiche MyAppHomeScreen quand onglet Home sélectionné

---

## ÉTAPE 4 : Header avec titre

### OÙ : Classe `_MyAppHomeScreenState`

**ACTION** : AJOUTER cette méthode APRÈS la méthode `build()`, juste avant le `}` final de la classe

### Interface actuelle
```
┌────────────────────┐
│ What are you       │
│ cooking today? 🔔  │
│                    │
│                    │
├────────────────────┤
│[🏠][♥][📅][⚙️]    │
└────────────────────┘
```

### Bout de code 5 : Méthode headerParts()

```dart
  Padding headerParts() {
    return Padding(
      padding: const EdgeInsets.symmetric(vertical: 20),
      child: Row(
        children: [
          Text(
            "What are you\ncooking today?",
            style: TextStyle(
              fontSize: 32,
              fontWeight: FontWeight.bold,
              height: 1,
            ),
          ),
          Spacer(),
          IconButton(
            onPressed: () {},
            style: IconButton.styleFrom(
              fixedSize: Size(55, 55),
              shape: RoundedRectangleBorder(
                borderRadius: BorderRadius.circular(15),
              ),
            ),
            icon: Icon(Iconsax.notification),
          ),
        ],
      ),
    );
  }
```

### Bout de code 6 : Utiliser headerParts dans build

### OÙ : Dans la méthode `build()` de `_MyAppHomeScreenState`

**ACTION** : Chercher la ligne `Text("Hello from HomeScreen"),` dans le Column et REMPLACER par :

```dart
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              headerParts(),
            ],
          ),
```

**Ce que ça fait** : Affiche titre + bouton notification

---

## ÉTAPE 5 : Barre de recherche

### OÙ : Classe `_MyAppHomeScreenState`

**ACTION** : AJOUTER cette méthode APRÈS `headerParts()`, avant le `}` final de la classe

### Interface actuelle
```
┌────────────────────┐
│ What are you       │
│ cooking today? 🔔  │
│                    │
│ 🔍 Search recipes  │ ← Barre recherche
│                    │
├────────────────────┤
│[🏠][♥][📅][⚙️]    │
└────────────────────┘
```

### Bout de code 7 : Méthode mySearchBar()

```dart
  Container mySearchBar() {
    return Container(
      width: double.infinity,
      height: 60,
      decoration: BoxDecoration(
        color: Colors.grey[100],
        borderRadius: BorderRadius.circular(30),
      ),
      padding: EdgeInsets.symmetric(horizontal: 20, vertical: 5),
      child: TextField(
        decoration: InputDecoration(
          hintText: "Search any recipes",
          hintStyle: TextStyle(color: Colors.grey, fontSize: 16),
          prefixIcon: Icon(Iconsax.search_normal, color: Colors.grey),
          border: InputBorder.none,
          contentPadding: EdgeInsets.symmetric(vertical: 15),
        ),
      ),
    );
  }
```

### Bout de code 8 : Ajouter dans Column

### OÙ : Dans `build()` de `_MyAppHomeScreenState`, dans le `Column`

**ACTION** : MODIFIER le `children:` du Column pour ajouter SizedBox et mySearchBar()

```dart
            children: [
              headerParts(),
              SizedBox(height: 20),
              mySearchBar(),
            ],
```

**Ce que ça fait** : Ajoute barre de recherche

---

## ÉTAPE 6 : Banner promotionnel

### OÙ : Fichier `lib/Views/app_main_screen.dart`

**ACTION** : AJOUTER cette classe TOUT EN BAS du fichier (après MyAppHomeScreen)

### Interface actuelle
```
┌────────────────────────┐
│ What are you cooking? │
│ 🔍 Search recipes      │
│                        │
│ ╔══════════════════╗   │
│ ║ Cook the best    ║   │ ← Banner vert
│ ║ recipes at home  ║   │
│ ║ [Explore] 👨‍🍳    ║   │
│ ╚══════════════════╝   │
└────────────────────────┘
```

### Bout de code 9 : Classe BannerToExplore

```dart
class BannerToExplore extends StatelessWidget {
  const BannerToExplore({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Container(
      width: double.infinity,
      height: 170,
      decoration: BoxDecoration(
        color: Color(0xFF71B77A),
        borderRadius: BorderRadius.circular(15),
      ),
      child: Stack(
        children: [
          Positioned(
            top: 32,
            left: 20,
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Text(
                  "Cook the best\nrecipes at home",
                  style: TextStyle(
                    height: 1.1,
                    fontSize: 22,
                    fontWeight: FontWeight.bold,
                    color: Colors.white,
                  ),
                ),
                SizedBox(height: 10),
                ElevatedButton(
                  onPressed: () {},
                  child: Text(
                    "Explore",
                    style: TextStyle(
                      fontSize: 15,
                      fontWeight: FontWeight.w600,
                      color: Color(0xFF71B77A),
                    ),
                  ),
                  style: ElevatedButton.styleFrom(
                    backgroundColor: Colors.white,
                    shape: RoundedRectangleBorder(
                      borderRadius: BorderRadius.circular(10),
                    ),
                  ),
                ),
              ],
            ),
          ),
          Positioned(
            top: 0,
            bottom: 0,
            right: -20,
            child: Image.asset(
              "assets/images/chef_PNG190.png",
              width: 180,
            ),
          ),
        ],
      ),
    );
  }
}
```

### Bout de code 10 : Ajouter banner dans Column

### OÙ : Dans `build()` de `_MyAppHomeScreenState`, dans le `Column`

**ACTION** : AJOUTER après la ligne `mySearchBar(),` dans le children du Column

```dart
              mySearchBar(),
              SizedBox(height: 20),
              const BannerToExplore(),
```

**Ce que ça fait** : Ajoute banner vert avec chef

---

## ÉTAPE 7 : Titre "Categories"

### OÙ : Dans `build()` de `_MyAppHomeScreenState`, dans le `Column`

**ACTION** : AJOUTER après la ligne `const BannerToExplore(),`

### Interface actuelle
```
┌────────────────────────┐
│ What are you cooking?  │
│ 🔍 Search              │
│ [Banner vert]          │
│                        │
│ Categories             │ ← Titre
│                        │
└────────────────────────┘
```

### Bout de code 11 : Ajouter titre Categories

```dart
              const BannerToExplore(),
              const Padding(
                padding: EdgeInsets.symmetric(vertical: 20),
                child: Text(
                  "Categories",
                  style: TextStyle(
                    fontSize: 20,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
```

**Ce que ça fait** : Ajoute titre "Categories"

---

## ÉTAPE 8 : StreamBuilder Categories

### OÙ : Dans `build()` de `_MyAppHomeScreenState`, dans le `Column`

**ACTION** : AJOUTER après le Padding du titre "Categories"

### Interface actuelle
```
┌────────────────────────┐
│ Categories             │
│                        │
│ [All][Breakfast][...]  │ ← Boutons de Firestore
│                        │
└────────────────────────┘
```

### Bout de code 12 : StreamBuilder pour categories

```dart
              StreamBuilder<QuerySnapshot>(
                stream: _firestore.collection('categories').snapshots(),
                builder: (context, snapshot) {
                  if (snapshot.hasData) {
                    List<String> categories = ["All"];
                    for (var doc in snapshot.data!.docs) {
                      categories.add(doc['name']);
                    }
                    return categoryButtons(categories);
                  } else {
                    return CircularProgressIndicator();
                  }
                },
              ),
```

**Ce que ça fait** : Lit categories depuis Firestore

### Bout de code 13 : Méthode categoryButtons()

### OÙ : Classe `_MyAppHomeScreenState`

**ACTION** : AJOUTER cette méthode APRÈS `mySearchBar()`, avant le `}` final de la classe

```dart
  Widget categoryButtons(List<String> categories) {
    return SingleChildScrollView(
      scrollDirection: Axis.horizontal,
      child: Row(
        children: categories.map((category) {
          bool isSelected = selectedCategory == category;
          return Padding(
            padding: const EdgeInsets.only(right: 12),
            child: GestureDetector(
              onTap: () {
                setState(() {
                  selectedCategory = category;
                });
              },
              child: Container(
                padding: EdgeInsets.symmetric(horizontal: 20, vertical: 12),
                decoration: BoxDecoration(
                  color: isSelected ? kprimaryColor : Colors.grey[200],
                  borderRadius: BorderRadius.circular(25),
                ),
                child: Text(
                  category,
                  style: TextStyle(
                    color: isSelected ? Colors.white : Colors.grey[600],
                    fontWeight: FontWeight.w600,
                    fontSize: 14,
                  ),
                ),
              ),
            ),
          );
        }).toList(),
      ),
    );
  }
```

**Ce que ça fait** : Crée boutons de catégories cliquables

---

## ÉTAPE 9 : Titre "Quick & Easy" + View all

### Interface actuelle
```
┌────────────────────────┐
│ [All][Breakfast][...]  │
│                        │
│ Quick & Easy  View all │ ← Nouveau titre
│                        │
└────────────────────────┘
```

### Bout de code 14 : Import view_all_items

### OÙ : TOUT EN HAUT du fichier `app_main_screen.dart`

**ACTION** : AJOUTER cette ligne après `import '../constants.dart';`

```dart
import 'view_all_items.dart';
```

### Bout de code 15 : Titre avec bouton

### OÙ : Dans `build()` de `_MyAppHomeScreenState`, dans le `Column`

**ACTION** : AJOUTER après le StreamBuilder des categories (après la ligne avec `),` qui ferme le StreamBuilder)

```dart
              const SizedBox(height: 20),
              Row(
                mainAxisAlignment: MainAxisAlignment.spaceBetween,
                children: [
                  const Text(
                    "Quick & Easy",
                    style: TextStyle(
                      fontSize: 20,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  TextButton(
                    onPressed: () {
                      Navigator.push(
                        context,
                        MaterialPageRoute(
                          builder: (context) => const ViewAllItems(
                            categoryTitle: "Quick & Easy",
                            categoryName: null,
                          ),
                        ),
                      );
                    },
                    child: const Text(
                      "View all",
                      style: TextStyle(
                        color: kprimaryColor,
                        fontSize: 14,
                        fontWeight: FontWeight.w600,
                      ),
                    ),
                  ),
                ],
              ),
              const SizedBox(height: 15),
```

**Ce que ça fait** : Ajoute titre + bouton View all

---

## ÉTAPE 10 : StreamBuilder Recettes (FINAL)

### OÙ : Dans `build()` de `_MyAppHomeScreenState`, dans le `Column`

**ACTION** : AJOUTER après la ligne `const SizedBox(height: 15),` (juste après le Row du titre "Quick & Easy")

### Interface finale
```
┌────────────────────────────────┐
│ What are you cooking today? 🔔 │
│ 🔍 Search any recipes          │
│ ╔════════════════════════════╗ │
│ ║ Cook the best recipes      ║ │
│ ╚════════════════════════════╝ │
│                                │
│ Categories                     │
│ [All] [Breakfast] [Lunch]      │
│                                │
│ Quick & Easy         View all  │
│ ┌──────────┐  ┌──────────┐    │
│ │  🍕      │  │  🍔      │    │
│ │  Pizza   │  │  Burger  │    │
│ │ ⏱ 30 Min│  │ ⏱ 20 Min│    │
│ │ ⚡450 Cal│  │ ⚡380 Cal│    │
│ └──────────┘  └──────────┘    │
│ ┌──────────┐  ┌──────────┐    │
│ │  🍝      │  │  🥗      │    │
│ │  Pasta   │  │  Salad   │    │
│ └──────────┘  └──────────┘    │
├────────────────────────────────┤
│ [🏠] [♥] [📅] [⚙️]             │
└────────────────────────────────┘
```

### Bout de code 16 : StreamBuilder recettes (LE PLUS IMPORTANT)

```dart
              Container(
                height: 400,
                child: StreamBuilder<QuerySnapshot>(
                  stream: selectedCategory == "All" 
                      ? _firestore.collection('details').limit(4).snapshots()
                      : _firestore.collection('details')
                          .where('category', isEqualTo: selectedCategory)
                          .limit(4)
                          .snapshots(),
                  builder: (context, snapshot) {
                    if (snapshot.hasData) {
                      return GridView.builder(
                        gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
                          crossAxisCount: 2,
                          crossAxisSpacing: 10,
                          mainAxisSpacing: 10,
                          childAspectRatio: 0.8,
                        ),
                        itemCount: snapshot.data!.docs.length,
                        itemBuilder: (context, index) {
                          final recipe = snapshot.data!.docs[index];
                          final img = (recipe['image'] ?? '').toString();
                          final name = (recipe['name'] ?? 'Sans nom').toString();
                          final time = (recipe['time'] ?? '').toString();
                          final cal = (recipe['cal'] ?? '0').toString();

                          return Container(
                            decoration: BoxDecoration(
                              color: Colors.white,
                              borderRadius: BorderRadius.circular(15),
                              boxShadow: [
                                BoxShadow(
                                  color: Colors.grey.withOpacity(0.1),
                                  spreadRadius: 1,
                                  blurRadius: 5,
                                ),
                              ],
                            ),
                            child: Column(
                              crossAxisAlignment: CrossAxisAlignment.start,
                              children: [
                                Expanded(
                                  child: Stack(
                                    children: [
                                      ClipRRect(
                                        borderRadius: const BorderRadius.vertical(
                                          top: Radius.circular(15),
                                        ),
                                        child: img.isNotEmpty
                                            ? Image.network(
                                                img,
                                                width: double.infinity,
                                                fit: BoxFit.cover,
                                              )
                                            : Container(
                                                color: Colors.grey[200],
                                                child: Center(
                                                  child: Icon(
                                                    Icons.restaurant,
                                                    size: 50,
                                                    color: Colors.grey[400],
                                                  ),
                                                ),
                                              ),
                                      ),
                                      Positioned(
                                        top: 10,
                                        right: 10,
                                        child: Container(
                                          padding: const EdgeInsets.all(8),
                                          decoration: BoxDecoration(
                                            color: Colors.white,
                                            shape: BoxShape.circle,
                                            boxShadow: [
                                              BoxShadow(
                                                color: Colors.grey.withOpacity(0.3),
                                                spreadRadius: 1,
                                                blurRadius: 3,
                                              ),
                                            ],
                                          ),
                                          child: Icon(
                                            Iconsax.heart,
                                            size: 16,
                                            color: Colors.grey[600],
                                          ),
                                        ),
                                      ),
                                    ],
                                  ),
                                ),
                                Padding(
                                  padding: const EdgeInsets.all(10),
                                  child: Column(
                                    crossAxisAlignment: CrossAxisAlignment.start,
                                    children: [
                                      Text(
                                        name,
                                        style: const TextStyle(
                                          fontWeight: FontWeight.bold,
                                          fontSize: 16,
                                        ),
                                        maxLines: 2,
                                        overflow: TextOverflow.ellipsis,
                                      ),
                                      const SizedBox(height: 5),
                                      Row(
                                        children: [
                                          Icon(
                                            Iconsax.clock,
                                            size: 14,
                                            color: Colors.grey[600],
                                          ),
                                          const SizedBox(width: 4),
                                          Text(
                                            time.isNotEmpty ? "$time Min" : "- Min",
                                            style: TextStyle(
                                              color: Colors.grey[600],
                                              fontSize: 12,
                                            ),
                                          ),
                                          const SizedBox(width: 10),
                                          Icon(
                                            Iconsax.flash_1,
                                            size: 14,
                                            color: Colors.grey[600],
                                          ),
                                          const SizedBox(width: 4),
                                          Text(
                                            "$cal Cal",
                                            style: TextStyle(
                                              color: Colors.grey[600],
                                              fontSize: 12,
                                            ),
                                          ),
                                        ],
                                      ),
                                    ],
                                  ),
                                ),
                              ],
                            ),
                          );
                        },
                      );
                    } else {
                      return Center(child: CircularProgressIndicator());
                    }
                  },
                ),
              ),
```

**Ce que ça fait** : Affiche 4 recettes en grille depuis Firestore

---

## RÉSUMÉ : Ordre de construction

```
ÉTAPE 0 : main.dart (Firebase)
   ↓
ÉTAPE 1-2 : Structure + Navigation
   ┌──────────┐
   │  Page 0  │
   │          │
   ├──────────┤
   │[🏠][♥]..│
   └──────────┘
   ↓
ÉTAPES 3-4 : Page d'accueil
   ┌──────────┐
   │HomeScreen│
   ├──────────┤
   │[🏠][♥]..│
   └──────────┘
   ↓
ÉTAPES 5-6 : Header + Recherche
   ┌──────────┐
   │ What...🔔│
   │🔍 Search │
   ├──────────┤
   │[🏠][♥]..│
   └──────────┘
   ↓
ÉTAPES 7-8 : Banner
   ┌──────────┐
   │🔍 Search │
   │[Banner]  │
   ├──────────┤
   │[🏠][♥]..│
   └──────────┘
   ↓
ÉTAPES 9-11 : Categories
   ┌──────────┐
   │[Banner]  │
   │Categories│
   │[All][...]│
   ├──────────┤
   │[🏠][♥]..│
   └──────────┘
   ↓
ÉTAPES 12-14 : Recettes
   ┌──────────┐
   │[All][...]│
   │Quick&Easy│
   │┌──┐ ┌──┐│
   ││🍕│ │🍔││
   │└──┘ └──┘│
   ├──────────┤
   │[🏠][♥]..│
   └──────────┘
   ↓
   ✅ TERMINÉ
```

---

## AIDE-MÉMOIRE : Où ajouter quoi ?

| Étape | Fichier | Où exactement | Action |
|-------|---------|---------------|--------|
| 0 | main.dart | Tout le fichier | REMPLACER tout |
| 1 | app_main_screen.dart | Nouveau fichier | CRÉER + coller |
| 2 | app_main_screen.dart | Méthode build() | REMPLACER build() |
| 3 | app_main_screen.dart | Fin de fichier | AJOUTER classe |
| 4 | app_main_screen.dart | Ligne body | REMPLACER body |
| 5 | app_main_screen.dart | Après build() | AJOUTER méthode |
| 6 | app_main_screen.dart | Dans Column | MODIFIER children |
| 7 | app_main_screen.dart | Après headerParts() | AJOUTER méthode |
| 8 | app_main_screen.dart | Dans Column | AJOUTER dans children |
| 9 | app_main_screen.dart | Fin de fichier | AJOUTER classe |
| 10 | app_main_screen.dart | Dans Column | AJOUTER dans children |
| 11 | app_main_screen.dart | Dans Column | AJOUTER dans children |
| 12 | app_main_screen.dart | Dans Column | AJOUTER StreamBuilder |
| 13 | app_main_screen.dart | Après mySearchBar() | AJOUTER méthode |
| 14 | app_main_screen.dart | Ligne 5 (imports) | AJOUTER import |
| 15 | app_main_screen.dart | Dans Column | AJOUTER Row |
| 16 | app_main_screen.dart | Dans Column | AJOUTER Container |

---

## Checklist finale

Votre app doit avoir :
- [ ] main.dart avec Firebase
- [ ] AppMainScreen avec BottomNavigationBar
- [ ] MyAppHomeScreen
- [ ] headerParts()
- [ ] mySearchBar()
- [ ] BannerToExplore
- [ ] categoryButtons()
- [ ] 2 StreamBuilder (categories + recettes)
- [ ] Navigation vers ViewAllItems
- [ ] Aucune erreur de compilation

---

## Structure finale du fichier app_main_screen.dart

```
app_main_screen.dart (475 lignes environ)
│
├─ IMPORTS (lignes 1-5)                        ← Bout 1, 14
│  ├─ package:flutter/material.dart
│  ├─ package:iconsax/iconsax.dart
│  ├─ package:cloud_firestore/cloud_firestore.dart
│  ├─ ../constants.dart
│  └─ view_all_items.dart
│
├─ AppMainScreen (lignes 6-67)                 ← Bouts 1, 2
│  └─ _AppMainScreenState
│     ├─ selectedIndex = 0
│     └─ build()
│        └─ Scaffold
│           ├─ backgroundColor: white
│           ├─ bottomNavigationBar (4 items)
│           └─ body (conditionnel)
│
├─ MyAppHomeScreen (lignes 69-379)             ← Bouts 3-16
│  └─ _MyAppHomeScreenState
│     ├─ selectedCategory = "All"
│     ├─ _firestore
│     ├─ build()                               ← Bout 3, 6, 8, 10, 11, 12, 15, 16
│     │  └─ SafeArea
│     │     └─ SingleChildScrollView
│     │        └─ Padding
│     │           └─ Column
│     │              ├─ headerParts()
│     │              ├─ SizedBox
│     │              ├─ mySearchBar()
│     │              ├─ SizedBox
│     │              ├─ BannerToExplore
│     │              ├─ Padding ("Categories")
│     │              ├─ StreamBuilder (categories)
│     │              ├─ SizedBox
│     │              ├─ Row ("Quick & Easy" + "View all")
│     │              ├─ SizedBox
│     │              └─ Container (StreamBuilder recettes)
│     ├─ headerParts()                         ← Bout 5
│     ├─ mySearchBar()                         ← Bout 7
│     └─ categoryButtons()                     ← Bout 13
│
└─ BannerToExplore (lignes 381-443)            ← Bout 9
   └─ build()
      └─ Container (vert)
         └─ Stack
            ├─ Positioned (texte + bouton)
            └─ Positioned (image chef)
```

### Correspondance Bouts → Lignes

| Bout | Quoi | Où dans le fichier |
|------|------|-------------------|
| 1 | Imports + AppMainScreen | Lignes 1-23 |
| 2 | BottomNavigationBar | Lignes 17-61 (méthode build) |
| 3 | MyAppHomeScreen vide | Lignes 69-98 |
| 4 | Lier MyAppHomeScreen | Ligne 62-64 (body) |
| 5 | headerParts() | Lignes ~287-314 |
| 6 | Utiliser headerParts | Ligne ~89 (dans Column) |
| 7 | mySearchBar() | Lignes ~317-342 |
| 8 | Utiliser mySearchBar | Lignes ~90-92 (dans Column) |
| 9 | BannerToExplore | Lignes ~381-443 (classe séparée) |
| 10 | Utiliser Banner | Ligne ~94 (dans Column) |
| 11 | Titre "Categories" | Lignes ~95-103 (dans Column) |
| 12 | StreamBuilder categories | Lignes ~106-119 (dans Column) |
| 13 | categoryButtons() | Lignes ~344-378 |
| 14 | Import view_all_items | Ligne 5 |
| 15 | Titre "Quick & Easy" | Lignes ~122-157 (dans Column) |
| 16 | StreamBuilder recettes | Lignes ~159-278 (dans Column) |

---

## Points clés à retenir

**StreamBuilder 1** (categories) :
```dart
stream: _firestore.collection('categories').snapshots()
```
→ Lit toutes les catégories

**StreamBuilder 2** (recettes) :
```dart
stream: selectedCategory == "All" 
    ? _firestore.collection('details').limit(4).snapshots()
    : _firestore.collection('details')
        .where('category', isEqualTo: selectedCategory)
        .limit(4).snapshots()
```
→ Lit 4 recettes (toutes ou filtrées)

**Opérateurs null-safety utilisés** :
- `recipe['image'] ?? ''` → Valeur par défaut si null
- `snapshot.data!.docs` → Force non-null (après hasData)

---

**Guide de construction étape par étape de l'application de recettes**  
*Copier-coller chaque bout dans l'ordre*

