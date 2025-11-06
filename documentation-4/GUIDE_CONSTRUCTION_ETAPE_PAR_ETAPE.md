# Guide de Construction : App Recettes - Étape par Étape

## Comment utiliser ce guide

1. Copiez le bout de code
2. Collez dans votre fichier
3. Hot reload
4. Vérifiez l'interface
5. Passez au bout suivant

---

## ÉTAPE 0 : Setup Firebase

### main.dart

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

**REMPLACER le Scaffold de l'étape 1 par** :

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

### Bout de code 3 : Ajouter après _AppMainScreenState (en bas du fichier)

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

**DANS _AppMainScreenState, REMPLACER la ligne body par** :

```dart
      body: selectedIndex == 0
          ? const MyAppHomeScreen()
          : Center(child: Text("Page index: $selectedIndex")),
```

**Ce que ça fait** : Affiche MyAppHomeScreen quand onglet Home sélectionné

---

## ÉTAPE 4 : Header avec titre

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

### Bout de code 5 : Méthode headerParts() (ajouter dans _MyAppHomeScreenState)

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

**REMPLACER dans Column children** :

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

**AJOUTER après headerParts()** :

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

### Bout de code 9 : Classe BannerToExplore (ajouter en bas du fichier)

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

**AJOUTER après mySearchBar()** :

```dart
              mySearchBar(),
              SizedBox(height: 20),
              const BannerToExplore(),
```

**Ce que ça fait** : Ajoute banner vert avec chef

---

## ÉTAPE 7 : Titre "Categories"

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

### Bout de code 11 : Ajouter titre

**AJOUTER après BannerToExplore** :

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

**AJOUTER après le titre Categories** :

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

**AJOUTER dans _MyAppHomeScreenState** :

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

**AJOUTER en haut avec les autres imports** :

```dart
import 'view_all_items.dart';
```

### Bout de code 15 : Titre avec bouton

**AJOUTER après StreamBuilder categories** :

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

**AJOUTER après le SizedBox(height: 15)** :

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
ÉTAPE 1 : Structure AppMainScreen
   ↓
ÉTAPE 2 : Bottom Navigation Bar
   ↓
ÉTAPE 3 : MyAppHomeScreen vide
   ↓
ÉTAPE 4 : Header (titre + notification)
   ↓
ÉTAPE 5 : Barre de recherche
   ↓
ÉTAPE 6 : Banner promotionnel
   ↓
ÉTAPE 7 : Titre "Categories"
   ↓
ÉTAPE 8 : StreamBuilder Categories
   ↓
ÉTAPE 9 : Titre "Quick & Easy" + View all
   ↓
ÉTAPE 10 : StreamBuilder Recettes (FINAL)
```

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

## Structure finale du fichier

```
app_main_screen.dart
│
├─ Imports
├─ AppMainScreen (StatefulWidget)
│  └─ _AppMainScreenState
│     ├─ selectedIndex
│     └─ build() avec Scaffold + BottomNavigationBar
│
├─ MyAppHomeScreen (StatefulWidget)
│  └─ _MyAppHomeScreenState
│     ├─ selectedCategory
│     ├─ _firestore
│     ├─ build() avec SafeArea + Column
│     ├─ headerParts()
│     ├─ mySearchBar()
│     └─ categoryButtons()
│
└─ BannerToExplore (StatelessWidget)
```

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

