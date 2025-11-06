# Exercice Pratique : Développer avec StreamBuilder

## Instructions

Dans cet exercice, vous allez **DÉVELOPPER** (pas seulement analyser) du code avec StreamBuilder.

**Objectif** : Créer 3 applications Flutter fonctionnelles utilisant StreamBuilder.

**Durée estimée** : 90 minutes  
**Notation** : 30 points (10 points par exercice)

**IMPORTANT** : Tapez le code vous-même dans votre éditeur. Ne copiez-collez pas !

---

## PARTIE 1 : StreamBuilder Compteur (10 points)

### Énoncé

Créez une application Flutter avec un **compteur** qui s'incrémente toutes les secondes.

**Spécifications** :

1. Créer un Stream qui émet un nombre entier chaque seconde (0, 1, 2, 3...)
2. Utiliser StreamBuilder pour afficher ce nombre
3. Le compteur doit commencer à 0
4. L'interface doit afficher :
   - Le nombre actuel en grand (taille 48)
   - Un texte "Compteur" au-dessus
   - Un CircularProgressIndicator pendant l'attente de la première valeur

**Contraintes techniques** :
- Le Stream doit être créé dans `initState()` (pas dans build)
- Utiliser `StreamBuilder<int>`
- Gérer l'état `ConnectionState.waiting`
- Utiliser `const` où possible

**Interface attendue** :
```
┌─────────────────────┐
│      Compteur       │
│                     │
│         42          │  ← Taille 48, gras
│                     │
└─────────────────────┘
```

---

### Votre code ici :

```dart
import 'package:flutter/material.dart';

// TODO: Développez votre code ici

class CounterApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CounterScreen(),
    );
  }
}

class CounterScreen extends StatefulWidget {
  @override
  _CounterScreenState createState() => _CounterScreenState();
}

class _CounterScreenState extends State<CounterScreen> {
  // TODO: Déclarez votre Stream ici
  
  
  @override
  void initState() {
    super.initState();
    // TODO: Initialisez votre Stream ici
    
  }
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Compteur StreamBuilder'),
      ),
      body: Center(
        child: // TODO: Créez votre StreamBuilder ici
        
        
        
        
        
        
        
        
        
      ),
    );
  }
}
```

---

### Grille de notation (10 points)

- [ ] Stream créé correctement avec `Stream.periodic` (2 pts)
- [ ] Stream déclaré dans la classe (late final) (1 pt)
- [ ] Stream initialisé dans initState() (1 pt)
- [ ] StreamBuilder avec type `<int>` correct (1 pt)
- [ ] Gestion de ConnectionState.waiting (2 pts)
- [ ] Affichage du nombre avec bonne taille (1 pt)
- [ ] Code compile sans erreur (1 pt)
- [ ] Utilisation appropriée de const (1 pt)

---

---

## PARTIE 2 : StreamBuilder Date et Heure (10 points)

### Énoncé

Créez une **horloge digitale** qui affiche la date et l'heure actuelles, mises à jour chaque seconde.

**Spécifications** :

1. Créer un Stream qui émet `DateTime.now()` chaque seconde
2. Utiliser StreamBuilder pour afficher :
   - L'heure au format : `14:35:27`
   - La date au format : `Mercredi 5 Novembre 2025`
3. L'horloge doit se mettre à jour en temps réel
4. Afficher l'heure immédiatement (utiliser `initialData`)

**Contraintes techniques** :
- Utiliser `StreamBuilder<DateTime>`
- Formater l'heure avec `padLeft(2, '0')` pour avoir 14:05 et pas 14:5
- Gérer tous les états (waiting, error, data)
- L'heure doit être en gros (taille 48)
- La date en plus petit (taille 18)

**Interface attendue** :
```
┌──────────────────────────┐
│                          │
│        14:35:27          │  ← Taille 48, gras
│                          │
│  Mercredi 5 Novembre     │  ← Taille 18
│                          │
└──────────────────────────┘
```

**Aide** : Pour formater la date, vous pouvez utiliser :
```dart
// Jours de la semaine
final days = ['Lundi', 'Mardi', 'Mercredi', 'Jeudi', 'Vendredi', 'Samedi', 'Dimanche'];
final dayName = days[dateTime.weekday - 1];

// Mois
final months = ['Janvier', 'Février', 'Mars', 'Avril', 'Mai', 'Juin', 
                'Juillet', 'Août', 'Septembre', 'Octobre', 'Novembre', 'Décembre'];
final monthName = months[dateTime.month - 1];
```

---

### Votre code ici :

```dart
import 'package:flutter/material.dart';

class ClockApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: ClockScreen(),
    );
  }
}

class ClockScreen extends StatefulWidget {
  @override
  _ClockScreenState createState() => _ClockScreenState();
}

class _ClockScreenState extends State<ClockScreen> {
  // TODO: Déclarez votre Stream de DateTime
  
  
  // TODO: Créez la liste des jours et mois
  
  
  @override
  void initState() {
    super.initState();
    // TODO: Initialisez votre Stream
    
  }
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Horloge Digitale'),
      ),
      body: Center(
        child: // TODO: Créez votre StreamBuilder<DateTime>
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
      ),
    );
  }
}
```

---

### Grille de notation (10 points)

- [ ] Stream DateTime créé avec Stream.periodic (2 pts)
- [ ] Stream initialisé dans initState() (1 pt)
- [ ] StreamBuilder avec type `<DateTime>` (1 pt)
- [ ] initialData utilisé (1 pt)
- [ ] Formatage de l'heure correct (HH:MM:SS) (2 pts)
- [ ] Formatage de la date en français (1 pt)
- [ ] Gestion des états (1 pt)
- [ ] Code compile et fonctionne (1 pt)

---

---

## PARTIE 3 : StreamBuilder avec Firestore (10 points)

### Énoncé

Créez une application qui affiche **en temps réel** une liste de tâches depuis Firestore.

**Spécifications** :

1. Créer une collection Firestore nommée 'tasks'
2. Utiliser StreamBuilder pour écouter cette collection
3. Afficher chaque tâche dans une ListTile
4. Gérer TOUS les états :
   - Chargement : CircularProgressIndicator
   - Erreur : Message d'erreur en rouge
   - Liste vide : "Aucune tâche" avec icône
   - Données : ListView des tâches

5. Ajouter un bouton FloatingActionButton pour ajouter une tâche

**Structure de document Firestore** :
```javascript
{
  "title": "Faire les courses",
  "completed": false,
  "createdAt": Timestamp
}
```

**Interface attendue** :
```
┌──────────────────────────────┐
│  Mes Tâches            [+]   │
├──────────────────────────────┤
│ ☐ Faire les courses          │
│ ☑ Étudier StreamBuilder      │
│ ☐ Créer l'application         │
└──────────────────────────────┘
```

---

### Votre code ici :

```dart
import 'package:flutter/material.dart';
import 'package:cloud_firestore/cloud_firestore.dart';

class TasksApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: TasksScreen(),
    );
  }
}

class TasksScreen extends StatefulWidget {
  @override
  _TasksScreenState createState() => _TasksScreenState();
}

class _TasksScreenState extends State<TasksScreen> {
  // TODO: Déclarez votre instance Firestore
  
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Mes Tâches'),
      ),
      body: // TODO: Créez votre StreamBuilder<QuerySnapshot>
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // TODO: Ajoutez une tâche à Firestore
          
          
          
          
          
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

---

### Grille de notation (10 points)

- [ ] Instance Firestore créée (1 pt)
- [ ] StreamBuilder avec bon type (1 pt)
- [ ] Stream Firestore correct (.snapshots()) (1 pt)
- [ ] Gestion de hasError (1 pt)
- [ ] Gestion de ConnectionState.waiting (1 pt)
- [ ] Gestion de liste vide (1 pt)
- [ ] Affichage des tâches dans ListView (2 pts)
- [ ] Fonction addTask fonctionnelle (1 pt)
- [ ] Code compile sans erreur (1 pt)

---

---

# BONUS : Défis supplémentaires (points bonus)

## Défi 1 : Compteur avec pause (2 points)

Améliorez le compteur (Partie 1) pour ajouter :
- Un bouton "Pause" qui arrête le compteur
- Un bouton "Reprendre" qui le relance
- Un bouton "Reset" qui remet à 0

**Indice** : Utilisez un `StreamController<int>` au lieu de `Stream.periodic`

---

## Défi 2 : Horloge avec fuseaux horaires (2 points)

Améliorez l'horloge (Partie 2) pour afficher :
- L'heure locale
- L'heure UTC
- L'heure à New York (-5h)

---

## Défi 3 : Tâches avec filtres (3 points)

Améliorez la liste de tâches (Partie 3) pour ajouter :
- Filtrer : Toutes / Complétées / À faire
- Marquer une tâche comme complétée en cliquant
- Supprimer une tâche

---

---

# RÉPONSES ET SOLUTIONS

**NE CONSULTEZ PAS AVANT D'AVOIR ESSAYÉ VOUS-MÊME**

<details>
<summary><h2>PARTIE 1 : Solution Compteur - CLIQUEZ ICI</h2></summary>

## Solution complète : Compteur

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(CounterApp());
}

class CounterApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Compteur StreamBuilder',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: CounterScreen(),
    );
  }
}

class CounterScreen extends StatefulWidget {
  @override
  _CounterScreenState createState() => _CounterScreenState();
}

class _CounterScreenState extends State<CounterScreen> {
  // Stream qui émet un entier chaque seconde
  late final Stream<int> _counterStream;
  
  @override
  void initState() {
    super.initState();
    
    // Créer le Stream une seule fois
    _counterStream = Stream.periodic(
      const Duration(seconds: 1),  // Intervalle : 1 seconde
      (count) => count,            // Valeur émise : 0, 1, 2, 3...
    );
  }
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Compteur StreamBuilder'),
        centerTitle: true,
      ),
      body: Center(
        child: StreamBuilder<int>(
          stream: _counterStream,
          initialData: 0,  // Valeur initiale pour éviter null
          builder: (context, snapshot) {
            // Gérer les erreurs (peu probable ici mais bonne pratique)
            if (snapshot.hasError) {
              return Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  const Icon(
                    Icons.error_outline,
                    color: Colors.red,
                    size: 48,
                  ),
                  const SizedBox(height: 16),
                  Text(
                    'Erreur: ${snapshot.error}',
                    style: const TextStyle(color: Colors.red),
                  ),
                ],
              );
            }
            
            // Gérer l'attente (première seconde)
            if (snapshot.connectionState == ConnectionState.waiting) {
              return Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: const [
                  Text(
                    'Compteur',
                    style: TextStyle(
                      fontSize: 24,
                      fontWeight: FontWeight.w300,
                    ),
                  ),
                  SizedBox(height: 16),
                  CircularProgressIndicator(),
                  SizedBox(height: 16),
                  Text('Initialisation...'),
                ],
              );
            }
            
            // Afficher le compteur
            final count = snapshot.data ?? 0;
            
            return Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                const Text(
                  'Compteur',
                  style: TextStyle(
                    fontSize: 24,
                    fontWeight: FontWeight.w300,
                    color: Colors.grey,
                  ),
                ),
                const SizedBox(height: 16),
                Text(
                  '$count',
                  style: const TextStyle(
                    fontSize: 48,
                    fontWeight: FontWeight.bold,
                    color: Colors.blue,
                  ),
                ),
                const SizedBox(height: 8),
                Text(
                  count == 1 ? 'seconde' : 'secondes',
                  style: const TextStyle(
                    fontSize: 16,
                    color: Colors.grey,
                  ),
                ),
              ],
            );
          },
        ),
      ),
    );
  }
}
```

### Points clés de la solution

**1. Déclaration du Stream**
```dart
late final Stream<int> _counterStream;
```
- `late` : Sera initialisé plus tard (dans initState)
- `final` : Ne changera jamais après initialisation
- `Stream<int>` : Type précis

**2. Création du Stream**
```dart
_counterStream = Stream.periodic(
  const Duration(seconds: 1),  // Toutes les secondes
  (count) => count,            // Émet le compteur
);
```

**3. StreamBuilder bien structuré**
```dart
StreamBuilder<int>(
  stream: _counterStream,     // Stream à écouter
  initialData: 0,             // Valeur de départ
  builder: (context, snapshot) {
    // Gestion des états
  },
)
```

**4. Gestion complète des états**
- hasError : Affiche erreur
- waiting : Affiche loading
- data : Affiche le compteur

**5. Bonus : Pluriel géré**
```dart
count == 1 ? 'seconde' : 'secondes'
```

</details>

---

<details>
<summary><h2>PARTIE 2 : Solution Horloge - CLIQUEZ ICI</h2></summary>

## Solution complète : Horloge Digitale

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(ClockApp());
}

class ClockApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Horloge Digitale',
      theme: ThemeData(
        primarySwatch: Colors.indigo,
      ),
      home: ClockScreen(),
    );
  }
}

class ClockScreen extends StatefulWidget {
  @override
  _ClockScreenState createState() => _ClockScreenState();
}

class _ClockScreenState extends State<ClockScreen> {
  // Stream qui émet la date/heure actuelle chaque seconde
  late final Stream<DateTime> _clockStream;
  
  // Listes pour formater en français
  final List<String> _days = [
    'Lundi', 'Mardi', 'Mercredi', 'Jeudi', 
    'Vendredi', 'Samedi', 'Dimanche'
  ];
  
  final List<String> _months = [
    'Janvier', 'Février', 'Mars', 'Avril', 'Mai', 'Juin',
    'Juillet', 'Août', 'Septembre', 'Octobre', 'Novembre', 'Décembre'
  ];
  
  @override
  void initState() {
    super.initState();
    
    // Créer le Stream qui émet DateTime.now() chaque seconde
    _clockStream = Stream.periodic(
      const Duration(seconds: 1),
      (_) => DateTime.now(),  // Émet l'heure actuelle
    );
  }
  
  // Formater l'heure : 14:05:09
  String _formatTime(DateTime dateTime) {
    final hour = dateTime.hour.toString().padLeft(2, '0');
    final minute = dateTime.minute.toString().padLeft(2, '0');
    final second = dateTime.second.toString().padLeft(2, '0');
    
    return '$hour:$minute:$second';
  }
  
  // Formater la date : Mercredi 5 Novembre 2025
  String _formatDate(DateTime dateTime) {
    final dayName = _days[dateTime.weekday - 1];  // weekday : 1-7
    final day = dateTime.day;
    final monthName = _months[dateTime.month - 1];  // month : 1-12
    final year = dateTime.year;
    
    return '$dayName $day $monthName $year';
  }
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Horloge Digitale'),
        centerTitle: true,
      ),
      body: Container(
        decoration: BoxDecoration(
          gradient: LinearGradient(
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
            colors: [
              Colors.indigo[900]!,
              Colors.indigo[600]!,
            ],
          ),
        ),
        child: Center(
          child: StreamBuilder<DateTime>(
            stream: _clockStream,
            initialData: DateTime.now(),  // Afficher immédiatement
            builder: (context, snapshot) {
              // Gérer les erreurs
              if (snapshot.hasError) {
                return Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: [
                    const Icon(
                      Icons.error_outline,
                      color: Colors.red,
                      size: 64,
                    ),
                    const SizedBox(height: 16),
                    Text(
                      'Erreur: ${snapshot.error}',
                      style: const TextStyle(
                        color: Colors.red,
                        fontSize: 18,
                      ),
                    ),
                  ],
                );
              }
              
              // Gérer l'attente (ne devrait pas arriver avec initialData)
              if (!snapshot.hasData) {
                return const CircularProgressIndicator(
                  color: Colors.white,
                );
              }
              
              // Récupérer la date/heure
              final dateTime = snapshot.data!;
              
              return Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  // Heure en grand
                  Text(
                    _formatTime(dateTime),
                    style: const TextStyle(
                      fontSize: 72,
                      fontWeight: FontWeight.bold,
                      color: Colors.white,
                      fontFamily: 'monospace',
                      letterSpacing: 4,
                    ),
                  ),
                  
                  const SizedBox(height: 24),
                  
                  // Date en plus petit
                  Text(
                    _formatDate(dateTime),
                    style: TextStyle(
                      fontSize: 24,
                      fontWeight: FontWeight.w300,
                      color: Colors.white.withOpacity(0.9),
                    ),
                  ),
                  
                  const SizedBox(height: 48),
                  
                  // Indicateur de mise à jour
                  Container(
                    padding: const EdgeInsets.symmetric(
                      horizontal: 12,
                      vertical: 6,
                    ),
                    decoration: BoxDecoration(
                      color: Colors.white.withOpacity(0.2),
                      borderRadius: BorderRadius.circular(20),
                    ),
                    child: Row(
                      mainAxisSize: MainAxisSize.min,
                      children: [
                        Container(
                          width: 8,
                          height: 8,
                          decoration: const BoxDecoration(
                            color: Colors.greenAccent,
                            shape: BoxShape.circle,
                          ),
                        ),
                        const SizedBox(width: 8),
                        const Text(
                          'Mise à jour en temps réel',
                          style: TextStyle(
                            color: Colors.white,
                            fontSize: 12,
                          ),
                        ),
                      ],
                    ),
                  ),
                ],
              );
            },
          ),
        ),
      ),
    );
  }
}
```

### Points clés de la solution

**1. Stream DateTime**
```dart
Stream.periodic(
  const Duration(seconds: 1),
  (_) => DateTime.now(),  // Émet l'heure actuelle à chaque tick
);
```

**2. initialData pour affichage immédiat**
```dart
initialData: DateTime.now(),
```
Sans ça, on attendrait 1 seconde avant le premier affichage.

**3. Formatage avec padLeft**
```dart
dateTime.hour.toString().padLeft(2, '0')
// 5 → "05"
// 14 → "14"
```

**4. Accès aux tableaux**
```dart
_days[dateTime.weekday - 1]
// weekday va de 1 (lundi) à 7 (dimanche)
// Donc -1 pour index tableau (0-6)
```

**5. UI professionnelle**
- Gradient d'arrière-plan
- Espacement soigné
- Police monospace pour l'heure
- Indicateur de mise à jour

</details>

---

<details>
<summary><h2>PARTIE 3 : Solution Tâches Firestore - CLIQUEZ ICI</h2></summary>

## Solution complète : Liste de Tâches

```dart
import 'package:flutter/material.dart';
import 'package:cloud_firestore/cloud_firestore.dart';

void main() {
  runApp(TasksApp());
}

class TasksApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Mes Tâches',
      theme: ThemeData(
        primarySwatch: Colors.teal,
      ),
      home: TasksScreen(),
    );
  }
}

class TasksScreen extends StatefulWidget {
  @override
  _TasksScreenState createState() => _TasksScreenState();
}

class _TasksScreenState extends State<TasksScreen> {
  // Instance Firestore
  final FirebaseFirestore _firestore = FirebaseFirestore.instance;
  
  // Contrôleur pour le TextField
  final TextEditingController _taskController = TextEditingController();
  
  // Ajouter une tâche
  Future<void> _addTask() async {
    final taskTitle = _taskController.text.trim();
    
    // Vérifier que le champ n'est pas vide
    if (taskTitle.isEmpty) {
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(
          content: Text('Veuillez entrer une tâche'),
          backgroundColor: Colors.red,
        ),
      );
      return;
    }
    
    try {
      // Ajouter à Firestore
      await _firestore.collection('tasks').add({
        'title': taskTitle,
        'completed': false,
        'createdAt': FieldValue.serverTimestamp(),
      });
      
      // Effacer le champ
      _taskController.clear();
      
      // Message de succès
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(
          content: Text('Tâche ajoutée !'),
          backgroundColor: Colors.green,
          duration: Duration(seconds: 1),
        ),
      );
    } catch (e) {
      // Gérer les erreurs
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(
          content: Text('Erreur: $e'),
          backgroundColor: Colors.red,
        ),
      );
    }
  }
  
  // Afficher dialogue pour ajouter tâche
  void _showAddTaskDialog() {
    showDialog(
      context: context,
      builder: (context) {
        return AlertDialog(
          title: const Text('Nouvelle tâche'),
          content: TextField(
            controller: _taskController,
            decoration: const InputDecoration(
              hintText: 'Titre de la tâche',
              border: OutlineInputBorder(),
            ),
            autofocus: true,
            onSubmitted: (_) {
              Navigator.pop(context);
              _addTask();
            },
          ),
          actions: [
            TextButton(
              onPressed: () => Navigator.pop(context),
              child: const Text('Annuler'),
            ),
            ElevatedButton(
              onPressed: () {
                Navigator.pop(context);
                _addTask();
              },
              child: const Text('Ajouter'),
            ),
          ],
        );
      },
    );
  }
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Mes Tâches'),
        centerTitle: true,
      ),
      body: StreamBuilder<QuerySnapshot>(
        // Stream qui écoute la collection 'tasks'
        stream: _firestore
          .collection('tasks')
          .orderBy('createdAt', descending: true)
          .snapshots(),
        
        builder: (context, snapshot) {
          // ÉTAT 1 : Gérer les erreurs
          if (snapshot.hasError) {
            return Center(
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  const Icon(
                    Icons.error_outline,
                    color: Colors.red,
                    size: 64,
                  ),
                  const SizedBox(height: 16),
                  const Text(
                    'Erreur de connexion',
                    style: TextStyle(
                      fontSize: 20,
                      fontWeight: FontWeight.bold,
                      color: Colors.red,
                    ),
                  ),
                  const SizedBox(height: 8),
                  Text(
                    '${snapshot.error}',
                    style: const TextStyle(color: Colors.grey),
                    textAlign: TextAlign.center,
                  ),
                  const SizedBox(height: 16),
                  ElevatedButton.icon(
                    onPressed: () {
                      setState(() {});  // Forcer rebuild
                    },
                    icon: const Icon(Icons.refresh),
                    label: const Text('Réessayer'),
                  ),
                ],
              ),
            );
          }
          
          // ÉTAT 2 : Gérer le chargement
          if (snapshot.connectionState == ConnectionState.waiting) {
            return Center(
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: const [
                  CircularProgressIndicator(),
                  SizedBox(height: 16),
                  Text(
                    'Chargement des tâches...',
                    style: TextStyle(fontSize: 16, color: Colors.grey),
                  ),
                ],
              ),
            );
          }
          
          // ÉTAT 3 : Vérifier si des données existent
          if (!snapshot.hasData) {
            return const Center(
              child: Text('Aucune donnée disponible'),
            );
          }
          
          // ÉTAT 4 : Vérifier si la liste est vide
          final tasks = snapshot.data!.docs;
          
          if (tasks.isEmpty) {
            return Center(
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  Icon(
                    Icons.check_circle_outline,
                    size: 80,
                    color: Colors.grey[400],
                  ),
                  const SizedBox(height: 16),
                  const Text(
                    'Aucune tâche',
                    style: TextStyle(
                      fontSize: 24,
                      fontWeight: FontWeight.bold,
                      color: Colors.grey,
                    ),
                  ),
                  const SizedBox(height: 8),
                  const Text(
                    'Appuyez sur + pour ajouter votre première tâche',
                    style: TextStyle(color: Colors.grey),
                  ),
                ],
              ),
            );
          }
          
          // ÉTAT 5 : Afficher les tâches
          return ListView.builder(
            padding: const EdgeInsets.all(16),
            itemCount: tasks.length,
            itemBuilder: (context, index) {
              final taskDoc = tasks[index];
              final taskData = taskDoc.data() as Map<String, dynamic>;
              
              // Extraction sécurisée des données
              final title = taskData['title'] as String? ?? 'Tâche sans titre';
              final completed = taskData['completed'] as bool? ?? false;
              
              return Card(
                margin: const EdgeInsets.only(bottom: 12),
                elevation: 2,
                child: ListTile(
                  leading: Icon(
                    completed 
                      ? Icons.check_box 
                      : Icons.check_box_outline_blank,
                    color: completed ? Colors.green : Colors.grey,
                    size: 28,
                  ),
                  title: Text(
                    title,
                    style: TextStyle(
                      fontSize: 16,
                      decoration: completed 
                        ? TextDecoration.lineThrough 
                        : null,
                      color: completed ? Colors.grey : Colors.black,
                    ),
                  ),
                  trailing: IconButton(
                    icon: const Icon(Icons.delete, color: Colors.red),
                    onPressed: () async {
                      // Supprimer la tâche
                      await taskDoc.reference.delete();
                      
                      ScaffoldMessenger.of(context).showSnackBar(
                        const SnackBar(
                          content: Text('Tâche supprimée'),
                          duration: Duration(seconds: 1),
                        ),
                      );
                    },
                  ),
                  onTap: () async {
                    // Inverser le statut completed
                    await taskDoc.reference.update({
                      'completed': !completed,
                    });
                  },
                );
              },
            ),
          );
        },
      ),
      
      floatingActionButton: FloatingActionButton.extended(
        onPressed: _showAddTaskDialog,
        icon: const Icon(Icons.add),
        label: const Text('Nouvelle tâche'),
      ),
    );
  }
  
  @override
  void dispose() {
    _taskController.dispose();
    super.dispose();
  }
}
```

### Points clés de la solution

**1. Stream Firestore**
```dart
_firestore
  .collection('tasks')
  .orderBy('createdAt', descending: true)  // Plus récentes en premier
  .snapshots()  // Crée le Stream
```

**2. Les 5 états gérés**
1. hasError → Message d'erreur avec bouton retry
2. waiting → CircularProgressIndicator
3. !hasData → Message "pas de données"
4. docs.isEmpty → Message "liste vide" avec icône
5. Données → ListView

**3. Extraction sécurisée**
```dart
final title = taskData['title'] as String? ?? 'Tâche sans titre';
final completed = taskData['completed'] as bool? ?? false;
```
- Pas de `!` dangereux
- Valeurs par défaut appropriées

**4. Interaction avec Firestore**

Ajouter :
```dart
await _firestore.collection('tasks').add({
  'title': taskTitle,
  'completed': false,
  'createdAt': FieldValue.serverTimestamp(),
});
```

Modifier :
```dart
await taskDoc.reference.update({
  'completed': !completed,
});
```

Supprimer :
```dart
await taskDoc.reference.delete();
```

**5. UX améliorée**
- SnackBar pour feedback
- Dialogue pour ajouter tâche
- Icônes visuelles
- Ligne barrée pour tâches complétées
- Bouton supprimer
- Tap pour marquer complet

</details>

---

---

# CRITÈRES D'ÉVALUATION DÉTAILLÉS

## Partie 1 : Compteur (10 points)

### Excellent (9-10 points)
- Stream créé correctement
- initState utilisé
- Tous les états gérés
- Code propre et commenté
- UI soignée

### Bon (7-8 points)
- Stream fonctionne
- États principaux gérés
- Quelques oublis mineurs
- Code compile

### Passable (5-6 points)
- Stream de base fonctionne
- Gestion d'états incomplète
- UI basique
- Code fonctionne mais perfectible

### Insuffisant (0-4 points)
- Stream incorrect
- Pas de gestion d'états
- Ne compile pas
- Erreurs majeures

---

## Partie 2 : Horloge (10 points)

### Excellent (9-10 points)
- Stream DateTime correct
- Formatage parfait (HH:MM:SS)
- Date en français correcte
- initialData utilisé
- UI professionnelle

### Bon (7-8 points)
- Fonctionne correctement
- Formatage bon mais peut-être pas parfait
- Gestion d'états présente
- UI correcte

### Passable (5-6 points)
- Affiche l'heure
- Formatage basique
- Quelques bugs mineurs
- Manque d'états

### Insuffisant (0-4 points)
- Ne fonctionne pas
- Formatage incorrect
- Pas de Stream DateTime
- Erreurs majeures

---

## Partie 3 : Tâches Firestore (10 points)

### Excellent (9-10 points)
- StreamBuilder Firestore parfait
- Tous les 5 états gérés
- Extraction sécurisée (pas de !)
- addTask fonctionne
- UI complète

### Bon (7-8 points)
- StreamBuilder fonctionne
- 3-4 états gérés
- Quelques force unwrap (!)
- addTask basique mais fonctionne
- UI correcte

### Passable (5-6 points)
- StreamBuilder basique
- 1-2 états gérés
- Force unwrap partout
- addTask fonctionne
- UI minimale

### Insuffisant (0-4 points)
- Ne se connecte pas à Firestore
- Pas de gestion d'états
- Ne compile pas
- addTask ne fonctionne pas

---

# CONSEILS POUR RÉUSSIR

## Avant de coder

1. **Lire l'énoncé 2 fois**
2. **Noter les spécifications** sur papier
3. **Dessiner l'interface** voulue
4. **Lister les étapes** de développement

## Pendant le développement

1. **Tester fréquemment** (hot reload)
2. **Gérer les états un par un**
3. **Commenter votre code**
4. **Utiliser des noms de variables clairs**

## Déboggage

Si erreur :
1. **Lire le message d'erreur** complètement
2. **Vérifier les null** (hasData, ?., ??)
3. **Vérifier les types** (Stream<int>, StreamBuilder<int>)
4. **Relire la documentation** si besoin

---

# CHECKLIST AVANT RENDU

Pour chaque exercice, vérifier :

- [ ] Le code compile sans erreur
- [ ] L'application se lance
- [ ] Le Stream fonctionne (valeurs changent)
- [ ] Au moins 2 états gérés (waiting + data minimum)
- [ ] Pas de warning dans la console
- [ ] UI ressemble à ce qui est demandé
- [ ] Code commenté (au moins les parties importantes)
- [ ] Pas de `!` sans vérification hasData avant

---

# RESSOURCES AUTORISÉES

Vous pouvez consulter :
- [02-explication_streambuilder.md](02-explication_streambuilder.md)
- [01-arbre_widgets.md](01-arbre_widgets.md)
- Documentation Flutter officielle
- Vos notes de cours

Vous NE pouvez PAS :
- Copier-coller du code complet
- Demander à ChatGPT/IA de faire l'exercice
- Regarder les solutions avant d'avoir essayé

---

# VARIANTES POUR PROFESSEURS

## Variante A : En classe (guidé)

1. Faire Partie 1 ensemble (30 min)
2. Partie 2 en autonomie (30 min)
3. Partie 3 en binômes (30 min)

## Variante B : Devoir maison

1. Les 3 parties à faire chez soi
2. Rendu dans 1 semaine
3. Présentation du code en classe

## Variante C : Examen pratique

1. Les 3 parties en temps limité
2. 90 minutes chrono
3. Sans documentation
4. Ordinateur avec IDE seulement

---

**Exercice créé pour développer des compétences pratiques avec StreamBuilder**  
*3 exercices progressifs, du compteur simple à Firestore en temps réel*

