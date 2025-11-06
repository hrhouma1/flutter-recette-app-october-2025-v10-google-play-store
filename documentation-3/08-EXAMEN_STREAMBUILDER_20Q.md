# Examen StreamBuilder - 20 Questions

## Informations

**Durée** : 45 minutes  
**Total** : 20 points (1 point par question)  
**Seuil de réussite** : 12/20 (60%)  
**Type** : QCM - Une seule bonne réponse par question  

**Instructions** :
- Lisez attentivement chaque question
- Choisissez la meilleure réponse parmi les choix proposés
- Les réponses se trouvent à la fin du document
- Pas de calculatrice nécessaire
- Pas de matériel autorisé (examen fermé)

---

## PARTIE 1 : CONCEPTS DE BASE (Questions 1-7)

### Question 1
Qu'est-ce qu'un Stream en Flutter ?

A) Une variable qui contient une seule valeur  
B) Un flux de données qui peut émettre plusieurs valeurs au fil du temps  
C) Une méthode pour télécharger des images  
D) Un type de widget pour afficher des listes  

---

### Question 2
Quelle est la différence principale entre un Stream et un Future ?

A) Future est plus rapide que Stream  
B) Stream émet une seule valeur, Future émet plusieurs valeurs  
C) Future émet une seule valeur, Stream peut émettre plusieurs valeurs  
D) Il n'y a pas de différence  

---

### Question 3
Quel est le rôle principal de StreamBuilder ?

A) Créer des animations Flutter  
B) Écouter un Stream et reconstruire automatiquement l'UI  
C) Télécharger des fichiers depuis Internet  
D) Gérer la navigation entre les pages  

---

### Question 4
Dans `StreamBuilder<QuerySnapshot>`, que représente `QuerySnapshot` ?

A) Une photo de l'écran  
B) Le type de données attendues du Stream  
C) Le nom du Stream  
D) Une méthode de Firestore  

---

### Question 5
Quelle méthode Firestore crée un Stream qui écoute les changements en temps réel ?

A) `.get()`  
B) `.fetch()`  
C) `.snapshots()`  
D) `.listen()`  

---

### Question 6
Que contient l'objet `snapshot` dans la fonction builder de StreamBuilder ?

A) Seulement les données  
B) L'état de la connexion et les données  
C) Seulement les erreurs  
D) Rien, il est toujours vide  

---

### Question 7
Quelle propriété permet de vérifier si le Stream a des données disponibles ?

A) `snapshot.isReady`  
B) `snapshot.hasData`  
C) `snapshot.dataAvailable`  
D) `snapshot.exists`  

---

## PARTIE 2 : GESTION DES ÉTATS (Questions 8-12)

### Question 8
Dans quel ordre devez-vous vérifier les états du snapshot ?

A) hasData → hasError → connectionState  
B) connectionState → hasData → hasError  
C) hasError → connectionState → hasData  
D) L'ordre n'a pas d'importance  

---

### Question 9
Que devez-vous afficher quand `snapshot.connectionState == ConnectionState.waiting` ?

A) Un message d'erreur  
B) Les données  
C) Un indicateur de chargement (ex: CircularProgressIndicator)  
D) Rien  

---

### Question 10
Comment gérer le cas où `snapshot.hasError` est true ?

A) Ignorer l'erreur  
B) Afficher un message d'erreur à l'utilisateur  
C) Fermer l'application  
D) Retourner un Container vide  

---

### Question 11
Que signifie `snapshot.data!` avec le point d'exclamation `!` ?

A) C'est une erreur de syntaxe  
B) Cela signifie que la donnée n'est jamais null à ce point  
C) Cela crée une alerte  
D) Cela supprime la donnée  

---

### Question 12
Si `snapshot.hasData` est false, que contient `snapshot.data` ?

A) Une liste vide  
B) Un objet vide  
C) null  
D) La dernière valeur reçue  

---

## PARTIE 3 : CODE PRATIQUE (Questions 13-17)

### Question 13
Dans ce code, quelle est l'erreur ?

```dart
StreamBuilder<int>(
  stream: myStream,
  builder: (context, snapshot) {
    return Text('Valeur: ${snapshot.data}');
  },
)
```

A) Il n'y a pas d'erreur  
B) On n'a pas vérifié si snapshot.hasData avant d'accéder à data  
C) Le type <int> est incorrect  
D) Le stream n'est pas défini  

---

### Question 14
Quelle est la bonne façon de limiter le nombre de documents Firestore récupérés ?

A) `.limit(20)` avant `.snapshots()`  
B) `.limit(20)` après `.snapshots()`  
C) `.max(20)` avant `.snapshots()`  
D) On ne peut pas limiter  

---

### Question 15
Que fait l'opérateur `??` dans ce code ?
```dart
final name = recipe['name'] ?? 'Sans nom';
```

A) Division  
B) Fournit une valeur par défaut si recipe['name'] est null  
C) Multiplie les valeurs  
D) Compare deux valeurs  

---

### Question 16
Pourquoi utiliser `const` devant les widgets dans StreamBuilder ?

A) C'est obligatoire  
B) Pour améliorer les performances  
C) Pour éviter les erreurs  
D) Cela n'a aucun effet  

---

### Question 17
Dans quel widget devez-vous créer votre Stream pour de meilleures performances ?

A) Dans build() d'un StatelessWidget  
B) Dans initState() d'un StatefulWidget  
C) Dans un constructeur  
D) Directement dans StreamBuilder  

---

## PARTIE 4 : FIRESTORE ET STREAMBUILDER (Questions 18-20)

### Question 18
Comment filtrer les données Firestore dans un Stream ?

A) Utiliser `.filter()` avant `.snapshots()`  
B) Utiliser `.where()` avant `.snapshots()`  
C) Filtrer dans le builder après avoir reçu les données  
D) On ne peut pas filtrer avec StreamBuilder  

---

### Question 19
Combien de fois le builder de StreamBuilder est-il appelé ?

A) Une seule fois au démarrage  
B) À chaque fois que le Stream émet une nouvelle valeur  
C) Seulement quand l'utilisateur scroll  
D) Jamais, il est statique  

---

### Question 20
Quelle est la bonne pratique pour afficher une liste vide dans Firestore ?

A) Ne rien afficher  
B) Afficher un CircularProgressIndicator  
C) Afficher un message informatif (ex: "Aucune recette disponible")  
D) Afficher une erreur  

---

---

# FEUILLE DE RÉPONSES

Inscrivez vos réponses ci-dessous avant de consulter les corrections.

| Question | Votre réponse | Points |
|----------|---------------|--------|
| 1 | _____ | /1 |
| 2 | _____ | /1 |
| 3 | _____ | /1 |
| 4 | _____ | /1 |
| 5 | _____ | /1 |
| 6 | _____ | /1 |
| 7 | _____ | /1 |
| 8 | _____ | /1 |
| 9 | _____ | /1 |
| 10 | _____ | /1 |
| 11 | _____ | /1 |
| 12 | _____ | /1 |
| 13 | _____ | /1 |
| 14 | _____ | /1 |
| 15 | _____ | /1 |
| 16 | _____ | /1 |
| 17 | _____ | /1 |
| 18 | _____ | /1 |
| 19 | _____ | /1 |
| 20 | _____ | /1 |
| **TOTAL** | | **/20** |

---

---

# CORRECTIONS DÉTAILLÉES

<details>
<summary><h2>Cliquez ici pour voir les réponses</h2></summary>

## PARTIE 1 : CONCEPTS DE BASE

### Question 1 : B
**Un Stream est un flux de données qui peut émettre plusieurs valeurs au fil du temps**

Explication : Contrairement à une variable normale qui contient une seule valeur, un Stream est comme un tuyau qui transporte des données. Il peut envoyer plusieurs valeurs successivement (comme une chaîne YouTube qui publie plusieurs vidéos).

Exemple :
```dart
Stream<int> counter = Stream.periodic(Duration(seconds: 1), (i) => i);
// Émet : 0, 1, 2, 3, 4, 5...
```

---

### Question 2 : C
**Future émet une seule valeur, Stream peut émettre plusieurs valeurs**

Explication :
- **Future** = Commander un plat au restaurant (une seule fois)
- **Stream** = Abonnement Netflix (contenu continu)

```dart
// Future : UNE seule réponse
Future<String> getNom() async {
  return "Pierre";  // Retourne une fois
}

// Stream : PLUSIEURS valeurs
Stream<int> compteur() {
  return Stream.periodic(Duration(seconds: 1), (i) => i);
  // Émet : 0, 1, 2, 3...
}
```

---

### Question 3 : B
**Écouter un Stream et reconstruire automatiquement l'UI**

Explication : StreamBuilder fait deux choses essentielles :
1. Écoute un Stream (s'abonne automatiquement)
2. Reconstruit le widget à chaque nouvelle donnée

Sans StreamBuilder, vous devriez :
- Écouter manuellement avec `.listen()`
- Appeler `setState()` à chaque fois
- Gérer le `dispose()` pour annuler l'écoute

Avec StreamBuilder : tout est automatique !

---

### Question 4 : B
**Le type de données attendues du Stream**

Explication : `QuerySnapshot` indique que le Stream va émettre des snapshots (photos) de la base de données Firestore.

```dart
StreamBuilder<QuerySnapshot>  // Attend des données Firestore
StreamBuilder<int>            // Attend des entiers
StreamBuilder<String>         // Attend des chaînes de caractères
StreamBuilder<List<Recipe>>   // Attend des listes de recettes
```

---

### Question 5 : C
**`.snapshots()`**

Explication : La méthode `.snapshots()` crée un Stream qui écoute les changements en temps réel dans Firestore.

```dart
// .get() : UNE SEULE lecture
FirebaseFirestore.instance.collection('recipes').get()

// .snapshots() : ÉCOUTE CONTINUE
FirebaseFirestore.instance.collection('recipes').snapshots()
```

Avec `.snapshots()`, si quelqu'un ajoute une recette, vous la recevez automatiquement !

---

### Question 6 : B
**L'état de la connexion et les données**

Explication : Le snapshot contient TOUT ce dont vous avez besoin :

```dart
snapshot.connectionState  // État (waiting, active, done)
snapshot.data            // Les données reçues
snapshot.error           // L'erreur si problème
snapshot.hasData         // bool : y a-t-il des données ?
snapshot.hasError        // bool : y a-t-il une erreur ?
```

---

### Question 7 : B
**`snapshot.hasData`**

Explication : Cette propriété retourne `true` si le Stream a émis des données.

```dart
if (snapshot.hasData) {
  // Sûr d'accéder à snapshot.data maintenant
  final data = snapshot.data!;
}
```

---

## PARTIE 2 : GESTION DES ÉTATS

### Question 8 : C
**hasError → connectionState → hasData**

Explication : L'ordre recommandé pour vérifier les états :

```dart
builder: (context, snapshot) {
  // 1. D'abord vérifier les ERREURS
  if (snapshot.hasError) {
    return Text('Erreur: ${snapshot.error}');
  }
  
  // 2. Ensuite vérifier l'état de CONNEXION
  if (snapshot.connectionState == ConnectionState.waiting) {
    return CircularProgressIndicator();
  }
  
  // 3. Enfin vérifier les DONNÉES
  if (!snapshot.hasData) {
    return Text('Pas de données');
  }
  
  // 4. Afficher les données
  return Text('${snapshot.data}');
}
```

Pourquoi cet ordre ? Les erreurs sont prioritaires, puis le chargement, puis les données.

---

### Question 9 : C
**Un indicateur de chargement (ex: CircularProgressIndicator)**

Explication : `ConnectionState.waiting` signifie "en attente de données". L'utilisateur doit voir que l'app charge.

```dart
if (snapshot.connectionState == ConnectionState.waiting) {
  return Center(
    child: CircularProgressIndicator(),
  );
}
```

Alternatives visuelles :
- CircularProgressIndicator
- LinearProgressIndicator
- Shimmer effect (skeleton loading)
- Texte "Chargement..."

---

### Question 10 : B
**Afficher un message d'erreur à l'utilisateur**

Explication : Si une erreur survient (perte de connexion, erreur Firestore, etc.), l'utilisateur doit être informé.

```dart
if (snapshot.hasError) {
  return Center(
    child: Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Icon(Icons.error_outline, size: 60, color: Colors.red),
        SizedBox(height: 16),
        Text('Une erreur est survenue'),
        Text('${snapshot.error}'),
        ElevatedButton(
          onPressed: () {
            // Permettre de réessayer
          },
          child: Text('Réessayer'),
        ),
      ],
    ),
  );
}
```

---

### Question 11 : B
**Cela signifie que la donnée n'est jamais null à ce point**

Explication : Le `!` est le "null assertion operator". Il dit au compilateur Dart : "Je garantis que cette valeur n'est pas null ici".

```dart
if (snapshot.hasData) {
  // Ici, on a vérifié que data existe
  final data = snapshot.data!;  // Sûr d'utiliser !
}
```

ATTENTION : N'utilisez `!` que si vous êtes certain que la valeur n'est pas null (après hasData).

---

### Question 12 : C
**null**

Explication : Si `hasData` est false, cela signifie que le Stream n'a pas encore émis de données, donc `snapshot.data` vaut null.

```dart
if (!snapshot.hasData) {
  // snapshot.data == null ici
  print(snapshot.data);  // Affiche: null
}
```

C'est pourquoi il faut TOUJOURS vérifier `hasData` avant d'accéder à `data`.

---

## PARTIE 3 : CODE PRATIQUE

### Question 13 : B
**On n'a pas vérifié si snapshot.hasData avant d'accéder à data**

Explication : Ce code va crasher ou afficher "Valeur: null" au démarrage.

Code INCORRECT :
```dart
StreamBuilder<int>(
  stream: myStream,
  builder: (context, snapshot) {
    return Text('Valeur: ${snapshot.data}');  // Peut être null !
  },
)
```

Code CORRECT :
```dart
StreamBuilder<int>(
  stream: myStream,
  builder: (context, snapshot) {
    if (!snapshot.hasData) {
      return CircularProgressIndicator();
    }
    return Text('Valeur: ${snapshot.data}');  // Sûr maintenant
  },
)
```

Ou avec valeur par défaut :
```dart
StreamBuilder<int>(
  stream: myStream,
  initialData: 0,  // Valeur par défaut
  builder: (context, snapshot) {
    return Text('Valeur: ${snapshot.data}');  // Jamais null
  },
)
```

---

### Question 14 : A
**`.limit(20)` avant `.snapshots()`**

Explication : Pour limiter le nombre de documents récupérés de Firestore :

```dart
// CORRECT
FirebaseFirestore.instance
  .collection('recipes')
  .limit(20)        // Limiter à 20 documents
  .snapshots()      // Créer le Stream

// INCORRECT
FirebaseFirestore.instance
  .collection('recipes')
  .snapshots()
  .limit(20)        // Erreur : .limit() n'existe pas sur Stream
```

Avantages de `.limit()` :
- Performance : Moins de données chargées
- Coût : Moins de lectures Firestore facturées
- Mémoire : Application plus légère

---

### Question 15 : B
**Fournit une valeur par défaut si recipe['name'] est null**

Explication : L'opérateur `??` (null-coalescing operator) dit : "Si la valeur à gauche est null, utilise la valeur à droite".

```dart
final name = recipe['name'] ?? 'Sans nom';

// Si recipe['name'] = "Pizza" → name = "Pizza"
// Si recipe['name'] = null    → name = "Sans nom"
```

Autres exemples :
```dart
final img = recipe['image'] ?? '';
final time = recipe['time'] ?? '0';
final cal = recipe['cal'] ?? 0;
```

---

### Question 16 : B
**Pour améliorer les performances**

Explication : `const` indique que le widget ne change jamais. Flutter peut le réutiliser au lieu de le recréer.

```dart
// Sans const : widget recréé à chaque rebuild
return CircularProgressIndicator();

// Avec const : widget réutilisé
return const CircularProgressIndicator();
```

Impact :
- Moins de garbage collection
- Moins de CPU utilisé
- UI plus fluide

---

### Question 17 : B
**Dans initState() d'un StatefulWidget**

Explication : Créer le Stream une seule fois évite de créer plusieurs connexions.

MAUVAIS (nouveau Stream à chaque rebuild) :
```dart
class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return StreamBuilder(
      stream: FirebaseFirestore.instance.collection('data').snapshots(),
      // Nouveau Stream à chaque build !
    );
  }
}
```

BON (Stream créé une fois) :
```dart
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  late final Stream<QuerySnapshot> _stream;
  
  @override
  void initState() {
    super.initState();
    _stream = FirebaseFirestore.instance.collection('data').snapshots();
  }
  
  @override
  Widget build(BuildContext context) {
    return StreamBuilder(
      stream: _stream,  // Même Stream réutilisé
    );
  }
}
```

---

## PARTIE 4 : FIRESTORE ET STREAMBUILDER

### Question 18 : B
**Utiliser `.where()` avant `.snapshots()`**

Explication : Pour filtrer les données Firestore :

```dart
// Filtrer par catégorie
FirebaseFirestore.instance
  .collection('recipes')
  .where('category', isEqualTo: 'Dessert')  // Filtre
  .snapshots()

// Filtrer par plusieurs critères
FirebaseFirestore.instance
  .collection('recipes')
  .where('category', isEqualTo: 'Dessert')
  .where('calories', lessThan: 500)
  .snapshots()
```

Opérateurs disponibles :
- `isEqualTo` : égal à
- `isLessThan` : inférieur à
- `isGreaterThan` : supérieur à
- `arrayContains` : contient dans un tableau

---

### Question 19 : B
**À chaque fois que le Stream émet une nouvelle valeur**

Explication : C'est la magie de StreamBuilder ! Le builder est appelé automatiquement :
- Au démarrage (ConnectionState.waiting)
- Quand la première donnée arrive
- À CHAQUE changement dans Firestore
- En cas d'erreur

Exemple :
```
13:00:00 → builder appelé (waiting)
13:00:01 → builder appelé (données initiales)
13:05:30 → builder appelé (nouvelle recette ajoutée)
13:10:15 → builder appelé (recette modifiée)
13:15:45 → builder appelé (recette supprimée)
```

---

### Question 20 : C
**Afficher un message informatif (ex: "Aucune recette disponible")**

Explication : Si la collection est vide, guidez l'utilisateur.

```dart
if (!snapshot.hasData || snapshot.data!.docs.isEmpty) {
  return Center(
    child: Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Icon(Icons.restaurant, size: 64, color: Colors.grey),
        SizedBox(height: 16),
        Text(
          'Aucune recette disponible',
          style: TextStyle(fontSize: 18, color: Colors.grey),
        ),
        SizedBox(height: 8),
        Text('Ajoutez votre première recette !'),
      ],
    ),
  );
}
```

Un bon message vide :
- Explique pourquoi c'est vide
- Suggère une action
- Est visuellement clair (icône + texte)

---

</details>

---

## BARÈME DE NOTATION

### Score et appréciation

| Score | Appréciation | Niveau |
|-------|--------------|--------|
| 18-20 | Excellent | Expert StreamBuilder |
| 15-17 | Très bien | Maîtrise avancée |
| 12-14 | Bien | Compétence solide |
| 10-11 | Passable | Bases acquises |
| 0-9 | Insuffisant | Révision nécessaire |

---

### Analyse par partie

**Partie 1 : Concepts (7 points)**
- 6-7 : Excellente compréhension théorique
- 4-5 : Bonne compréhension
- 2-3 : Lacunes théoriques
- 0-1 : Revoir les concepts de base

**Partie 2 : États (5 points)**
- 5 : Maîtrise complète de la gestion d'états
- 3-4 : Bonne gestion
- 1-2 : Compréhension partielle
- 0 : Revoir la gestion d'états

**Partie 3 : Code (5 points)**
- 5 : Capable de lire et déboguer du code
- 3-4 : Bonne lecture de code
- 1-2 : Difficultés avec le code
- 0 : Revoir la syntaxe

**Partie 4 : Firestore (3 points)**
- 3 : Maîtrise Firestore + StreamBuilder
- 2 : Bonne compréhension
- 1 : Bases acquises
- 0 : Revoir Firestore

---

## RECOMMANDATIONS SELON VOTRE SCORE

### Si vous avez moins de 12/20
**Révision nécessaire**

Documents à relire :
1. [02-explication_streambuilder.md](02-explication_streambuilder.md) - Concepts de base
2. [01-arbre_widgets.md](01-arbre_widgets.md) - Structure de l'application

Exercices :
- Refaire le quiz jusqu'à obtenir 15/20
- Pratiquer avec de petits exemples
- Coder un StreamBuilder simple vous-même

---

### Si vous avez entre 12-17/20
**Bon niveau, continuez à pratiquer**

Pour progresser :
1. Relire les questions ratées avec attention
2. Lire [04-navigation_view_all.md](04-navigation_view_all.md) - Cas pratique
3. Faire le [Quiz avancé (30 questions)](03-quiz_streambuilder.md)

Exercices :
- Implémenter une fonctionnalité avec StreamBuilder
- Déboguer du code avec des erreurs

---

### Si vous avez 18-20/20
**Excellent ! Niveau avancé**

Pour aller plus loin :
1. [05-approche_critique_firebase_functions.md](05-approche_critique_firebase_functions.md) - Architecture
2. [06-etudes_de_cas_pratiques.md](06-etudes_de_cas_pratiques.md) - 15 études de cas réelles

Challenges :
- Implémenter une architecture avec Repository Pattern
- Comparer StreamBuilder vs Firebase Functions
- Mentorat d'autres étudiants

---

## CONSEILS POUR LA RÉVISION

### Concepts clés à maîtriser absolument

1. **Stream vs Future**
   - Future = 1 valeur
   - Stream = plusieurs valeurs

2. **Les 3 états à gérer**
   - Erreur (`hasError`)
   - Chargement (`connectionState.waiting`)
   - Données (`hasData`)

3. **Firestore + StreamBuilder**
   - `.snapshots()` crée un Stream
   - `.where()` pour filtrer
   - `.limit()` pour limiter

4. **Bonnes pratiques**
   - Toujours vérifier `hasData` avant `data!`
   - Utiliser `??` pour valeurs par défaut
   - Créer Stream dans `initState()`
   - Utiliser `const` pour performance

---

## QUESTIONS FRÉQUENTES

### Q : Puis-je utiliser mes notes pendant l'examen ?
**R :** Non, c'est un examen fermé. Mais vous pouvez consulter la documentation pour réviser avant.

### Q : Combien de temps par question ?
**R :** 45 minutes / 20 questions = ~2 minutes par question. Certaines sont plus rapides, d'autres nécessitent réflexion.

### Q : Que faire si j'hésite entre deux réponses ?
**R :** Utilisez l'élimination : éliminez les réponses évidemment fausses, puis choisissez la meilleure parmi celles restantes.

### Q : Les questions piège existent ?
**R :** Non. Les questions sont directes. Si vous avez compris les concepts, les réponses sont claires.

### Q : Puis-je retourner en arrière pour changer mes réponses ?
**R :** Oui, tant que le temps n'est pas écoulé.

---

## RESSOURCES DE RÉVISION

### Documents à lire AVANT l'examen

**Priorité 1 (Obligatoire)** :
- [02-explication_streambuilder.md](02-explication_streambuilder.md) - 15 minutes

**Priorité 2 (Recommandé)** :
- [01-arbre_widgets.md](01-arbre_widgets.md) - Section StreamBuilder - 10 minutes

**Priorité 3 (Bonus)** :
- [04-navigation_view_all.md](04-navigation_view_all.md) - Exemple pratique - 10 minutes

### Exercices de préparation

1. **Écrire un StreamBuilder basique**
   ```dart
   // Sans regarder la documentation, écrivez un StreamBuilder
   // qui affiche une liste de textes depuis Firestore
   ```

2. **Déboguer ce code**
   ```dart
   StreamBuilder<QuerySnapshot>(
     stream: _firestore.collection('data').snapshots(),
     builder: (context, snapshot) {
       final docs = snapshot.data!.docs;
       return ListView.builder(
         itemCount: docs.length,
         itemBuilder: (context, index) => Text(docs[index]['name']),
       );
     },
   )
   // Trouvez 3 problèmes
   ```

3. **Compléter ce code**
   ```dart
   StreamBuilder<QuerySnapshot>(
     stream: _firestore.collection('recipes').______(),  // À compléter
     builder: (context, snapshot) {
       if (snapshot.______) {  // À compléter
         return CircularProgressIndicator();
       }
       
       if (!snapshot.______) {  // À compléter
         return Text('Pas de données');
       }
       
       return ListView(...);
     },
   )
   ```

---

## CHECKLIST DE PRÉPARATION

Avant l'examen, assurez-vous de savoir :

**Concepts** :
- [ ] Définir ce qu'est un Stream
- [ ] Expliquer la différence Stream vs Future
- [ ] Expliquer le rôle de StreamBuilder

**États** :
- [ ] Lister les 3 états principaux à gérer
- [ ] Savoir quoi afficher dans chaque état
- [ ] Connaître l'ordre de vérification

**Code** :
- [ ] Écrire un StreamBuilder basique de mémoire
- [ ] Utiliser `.snapshots()` correctement
- [ ] Utiliser `.where()` pour filtrer
- [ ] Utiliser `.limit()` pour limiter

**Firestore** :
- [ ] Créer un Stream Firestore
- [ ] Filtrer des documents
- [ ] Accéder aux données d'un document

**Bonnes pratiques** :
- [ ] Vérifier hasData avant d'accéder à data
- [ ] Utiliser ?? pour valeurs par défaut
- [ ] Gérer les erreurs
- [ ] Utiliser const pour performance

---

## SIMULATION D'EXAMEN

### Testez-vous AVANT l'examen réel

1. Imprimez ce document (ou utilisez un chronomètre)
2. Réglez 45 minutes
3. Répondez aux 20 questions SANS regarder la correction
4. À la fin, vérifiez vos réponses
5. Notez votre score
6. Identifiez vos points faibles
7. Révisez ces parties spécifiquement

**Objectif** : Obtenir au moins 15/20 en simulation avant l'examen réel.

---

**Examen créé pour évaluer les connaissances fondamentales de StreamBuilder**  
*20 questions, niveau débutant à intermédiaire, 45 minutes*

