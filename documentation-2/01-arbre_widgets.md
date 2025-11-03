# Arbre des Widgets - app_main_screen.dart

## 📚 Table des matières
1. [Vue d'ensemble](#vue-densemble)
2. [Hiérarchie complète des widgets](#hiérarchie-complète-des-widgets)
3. [Détail par composant](#détail-par-composant)
4. [Relations et flux de données](#relations-et-flux-de-données)

---

## Vue d'ensemble

Le fichier `app_main_screen.dart` contient **3 classes principales** de widgets :
1. **AppMainScreen** - Widget racine avec navigation bottom bar
2. **MyAppHomeScreen** - Écran d'accueil avec les recettes
3. **BannerToExplore** - Banner promotionnel

---

## Hiérarchie complète des widgets

### Arbre global

```mermaid
graph TD
    Root[AppMainScreen StatefulWidget] --> Scaffold
    
    Scaffold --> BNB[BottomNavigationBar]
    Scaffold --> Body{body: selectedIndex == 0?}
    
    Body -->|Oui| MHS[MyAppHomeScreen]
    Body -->|Non| Placeholder[Center + Text]
    
    BNB --> BNB1[BottomNavigationBarItem: Home]
    BNB --> BNB2[BottomNavigationBarItem: Favorite]
    BNB --> BNB3[BottomNavigationBarItem: Meal Plan]
    BNB --> BNB4[BottomNavigationBarItem: Setting]
    
    style Root fill:#e1f5ff
    style Scaffold fill:#fff4e1
    style MHS fill:#e1ffe1
    style BNB fill:#ffe1f5
```

---

### Arbre détaillé de MyAppHomeScreen

```mermaid
graph TD
    MHS[MyAppHomeScreen] --> SA[SafeArea]
    SA --> SCS[SingleChildScrollView]
    SCS --> Padding1[Padding h:15]
    Padding1 --> Column
    
    Column --> C1[headerParts]
    Column --> SH1[SizedBox h:20]
    Column --> C2[mySearchBar]
    Column --> SH2[SizedBox h:20]
    Column --> C3[BannerToExplore]
    Column --> C4[Padding + Text 'Categories']
    Column --> C5[StreamBuilder Categories]
    Column --> SH3[SizedBox h:20]
    Column --> C6[Text 'Quick & Easy']
    Column --> SH4[SizedBox h:15]
    Column --> C7[Container h:400]
    
    C7 --> SB2[StreamBuilder Recipes]
    
    style MHS fill:#e1f5ff
    style Column fill:#fff4e1
    style C5 fill:#ffe1e1
    style SB2 fill:#ffe1e1
```

---

## Détail par composant

### 1. AppMainScreen - Structure complète

```mermaid
graph TD
    A[AppMainScreen<br/>StatefulWidget] --> B[_AppMainScreenState]
    
    B --> State1[State: selectedIndex = 0]
    
    B --> Build[build method]
    Build --> Scaffold
    
    Scaffold --> Prop1[backgroundColor: Colors.white]
    Scaffold --> BNB[bottomNavigationBar]
    Scaffold --> Body[body]
    
    BNB --> BNBWidget[BottomNavigationBar]
    BNBWidget --> BNBProp1[currentIndex: selectedIndex]
    BNBWidget --> BNBProp2[selectedItemColor: kprimaryColor]
    BNBWidget --> BNBProp3[type: BottomNavigationBarType.fixed]
    BNBWidget --> BNBProp4[items: List of 4 items]
    BNBWidget --> BNBProp5[onTap: setState selectedIndex]
    
    BNBProp4 --> Item1[Icon: Iconsax.home<br/>Label: 'Home']
    BNBProp4 --> Item2[Icon: Iconsax.heart<br/>Label: 'Favorite']
    BNBProp4 --> Item3[Icon: Iconsax.calendar<br/>Label: 'Meal Plan']
    BNBProp4 --> Item4[Icon: Iconsax.setting<br/>Label: 'Setting']
    
    Body --> Condition{selectedIndex == 0?}
    Condition -->|true| HomeScreen[MyAppHomeScreen]
    Condition -->|false| PlaceholderWidget[Center > Text]
    
    style A fill:#e1f5ff
    style BNBWidget fill:#ffe1f5
    style HomeScreen fill:#e1ffe1
```

---

### 2. MyAppHomeScreen - headerParts()

```mermaid
graph TD
    HP[headerParts Method] --> Padding
    Padding --> PaddingProp[vertical: 20]
    Padding --> Row
    
    Row --> Text1[Text]
    Row --> Spacer
    Row --> IconBtn[IconButton]
    
    Text1 --> TextProp1[text: 'What are you\ncooking today?']
    Text1 --> TextProp2[fontSize: 32]
    Text1 --> TextProp3[fontWeight: bold]
    
    IconBtn --> IconBtnProp1[icon: Iconsax.notification]
    IconBtn --> IconBtnProp2[fixedSize: 55x55]
    IconBtn --> IconBtnProp3[borderRadius: 15]
    
    style HP fill:#e1f5ff
    style Row fill:#fff4e1
```

---

### 3. MyAppHomeScreen - mySearchBar()

```mermaid
graph TD
    MSB[mySearchBar Method] --> Container
    
    Container --> CProp1[width: double.infinity]
    Container --> CProp2[height: 60]
    Container --> CProp3[decoration: BoxDecoration]
    Container --> CProp4[padding: h:20, v:5]
    
    CProp3 --> Deco1[color: Colors.grey 100]
    CProp3 --> Deco2[borderRadius: 30]
    
    Container --> TextField
    
    TextField --> TFProp1[decoration: InputDecoration]
    
    TFProp1 --> Input1[hintText: 'Search any recipes']
    TFProp1 --> Input2[prefixIcon: Iconsax.search_normal]
    TFProp1 --> Input3[border: none]
    
    style MSB fill:#e1f5ff
    style Container fill:#fff4e1
    style TextField fill:#ffe1f5
```

---

### 4. BannerToExplore - Structure complète

```mermaid
graph TD
    BTE[BannerToExplore<br/>StatelessWidget] --> Container
    
    Container --> CProp1[width: double.infinity]
    Container --> CProp2[height: 170]
    Container --> CProp3[decoration]
    Container --> Stack
    
    CProp3 --> Deco1[color: #71B77A]
    CProp3 --> Deco2[borderRadius: 15]
    
    Stack --> Pos1[Positioned<br/>top:32, left:20]
    Stack --> Pos2[Positioned<br/>top:0, bottom:0, right:-20]
    
    Pos1 --> Column1
    Column1 --> Text1[Text: 'Cook the best\nrecipes at home']
    Column1 --> SH1[SizedBox h:10]
    Column1 --> Btn[ElevatedButton: 'Explore']
    
    Text1 --> TextStyle1[fontSize: 22<br/>fontWeight: bold<br/>color: white]
    
    Btn --> BtnStyle[backgroundColor: white<br/>borderRadius: 10]
    
    Pos2 --> Image[Image.asset<br/>'assets/images/chef_PNG190.png'<br/>width: 180]
    
    style BTE fill:#e1f5ff
    style Container fill:#71B77A
    style Stack fill:#fff4e1
```

---

### 5. StreamBuilder Categories - Détail complet

```mermaid
graph TD
    SBC[StreamBuilder Categories<br/>ligne 106-119] --> SBProp1[stream: Firestore categories]
    SBC --> SBProp2[builder function]
    
    SBProp2 --> Condition{snapshot.hasData?}
    
    Condition -->|false| Loading[CircularProgressIndicator]
    Condition -->|true| Process[Traitement des données]
    
    Process --> Loop[Boucle sur docs]
    Loop --> List[List categories = 'All' + docs]
    
    List --> Return[return categoryButtons]
    
    Return --> CB[categoryButtons Method]
    
    CB --> SCSV[SingleChildScrollView<br/>horizontal]
    SCSV --> Row
    
    Row --> Map[categories.map]
    Map --> ForEach[Pour chaque catégorie]
    
    ForEach --> Padding[Padding right:12]
    Padding --> GD[GestureDetector]
    
    GD --> OnTap[onTap: setState<br/>selectedCategory = category]
    GD --> Container2[Container]
    
    Container2 --> ContProp1[padding: h:20, v:12]
    Container2 --> ContProp2[decoration]
    Container2 --> TextWidget[Text: category]
    
    ContProp2 --> Deco1{isSelected?}
    Deco1 -->|true| DecoSelected[color: kprimaryColor<br/>borderRadius: 25]
    Deco1 -->|false| DecoUnselected[color: Colors.grey 200<br/>borderRadius: 25]
    
    TextWidget --> TextStyle{isSelected?}
    TextStyle -->|true| TSSelected[color: white<br/>fontWeight: 600]
    TextStyle -->|false| TSUnselected[color: grey 600<br/>fontWeight: 600]
    
    style SBC fill:#ffe1e1
    style CB fill:#e1ffe1
    style SCSV fill:#fff4e1
```

---

### 6. StreamBuilder Recipes - Détail complet

```mermaid
graph TD
    SBR[StreamBuilder Recipes<br/>ligne 132-278] --> ContainerH[Container height:400]
    
    ContainerH --> SBWidget[StreamBuilder]
    
    SBWidget --> Stream{selectedCategory?}
    Stream -->|'All'| StreamAll[Firestore.collection 'details'<br/>.snapshots]
    Stream -->|Autre| StreamFiltered[Firestore.collection 'details'<br/>.where category<br/>.snapshots]
    
    SBWidget --> Builder[builder function]
    
    Builder --> Cond{snapshot.hasData?}
    Cond -->|false| LoadingCenter[Center<br/>CircularProgressIndicator]
    Cond -->|true| GridView
    
    GridView --> GVProp1[gridDelegate]
    GridView --> GVProp2[itemCount: docs.length]
    GridView --> GVProp3[itemBuilder]
    
    GVProp1 --> Delegate[SliverGridDelegateWithFixedCrossAxisCount<br/>crossAxisCount: 2<br/>crossAxisSpacing: 10<br/>mainAxisSpacing: 10<br/>childAspectRatio: 0.8]
    
    GVProp3 --> ItemBuilder[itemBuilder function]
    ItemBuilder --> RecipeData[Extraction des données:<br/>image, name, time, cal]
    
    RecipeData --> RecipeContainer[Container]
    
    style SBR fill:#ffe1e1
    style GridView fill:#e1ffe1
    style RecipeContainer fill:#fff4e1
```

---

### 7. Item de recette (GridView) - Structure détaillée

```mermaid
graph TD
    Item[Recipe Item Container] --> ContainerProp1[decoration: BoxDecoration]
    Item --> Column
    
    ContainerProp1 --> Deco1[color: white<br/>borderRadius: 15<br/>boxShadow: grey 0.1]
    
    Column --> Expanded
    Column --> PaddingBottom[Padding all:10]
    
    Expanded --> Stack
    
    Stack --> ImgWidget[ClipRRect]
    Stack --> HeartPos[Positioned<br/>top:10, right:10]
    
    ImgWidget --> RoundedTop[borderRadius: top 15]
    ImgWidget --> ImageCond{img.isNotEmpty?}
    
    ImageCond -->|true| ImageNetwork[Image.network<br/>width: infinity<br/>fit: cover]
    ImageCond -->|false| PlaceholderImg[Container grey 200<br/>Icon: restaurant]
    
    HeartPos --> HeartContainer[Container]
    HeartContainer --> HeartProp1[padding: 8<br/>shape: circle<br/>color: white<br/>boxShadow]
    HeartContainer --> HeartIcon[Icon: Iconsax.heart<br/>size: 16]
    
    PaddingBottom --> ColumnBottom[Column]
    
    ColumnBottom --> NameText[Text: name<br/>fontWeight: bold<br/>maxLines: 2]
    ColumnBottom --> SH[SizedBox h:5]
    ColumnBottom --> InfoRow[Row]
    
    InfoRow --> ClockIcon[Icon: Iconsax.clock]
    InfoRow --> TimeText[Text: time Min]
    InfoRow --> SHSmall[SizedBox w:10]
    InfoRow --> FlashIcon[Icon: Iconsax.flash_1]
    InfoRow --> CalText[Text: cal Cal]
    
    style Item fill:#fff4e1
    style Stack fill:#e1f5ff
    style ColumnBottom fill:#ffe1f5
```

---

## Relations et flux de données

### Flux de navigation

```mermaid
graph LR
    User[Utilisateur] -->|Tap Bottom Item| OnTap[onTap callback]
    OnTap -->|setState| SelectedIndex[selectedIndex<br/>State variable]
    SelectedIndex -->|Rebuild| Body{body condition}
    Body -->|index == 0| Home[MyAppHomeScreen]
    Body -->|index != 0| Other[Placeholder]
    
    style User fill:#e1f5ff
    style SelectedIndex fill:#ffe1e1
    style Home fill:#e1ffe1
```

---

### Flux des catégories

```mermaid
graph TB
    SB1[StreamBuilder<br/>Categories] -->|stream| FS1[(Firestore<br/>categories)]
    
    FS1 -->|snapshot| Builder1[builder function]
    
    Builder1 -->|hasData| Process[Traitement:<br/>List categories]
    
    Process --> CB[categoryButtons]
    
    CB --> Buttons[Boutons de catégories]
    
    Buttons -->|User tap| OnTap[onTap callback]
    
    OnTap -->|setState| SelectedCat[selectedCategory<br/>State variable]
    
    SelectedCat -->|Déclenche rebuild| SB2[StreamBuilder<br/>Recipes]
    
    SB2 -->|stream modifié| FS2[(Firestore<br/>details filtered)]
    
    FS2 -->|snapshot| Builder2[builder function]
    
    Builder2 -->|hasData| GridView[GridView<br/>Recipes]
    
    style SB1 fill:#ffe1e1
    style SB2 fill:#ffe1e1
    style SelectedCat fill:#e1ffe1
    style FS1 fill:#fff4e1
    style FS2 fill:#fff4e1
```

---

### Flux complet de l'état

```mermaid
stateDiagram-v2
    [*] --> AppMainScreen
    
    AppMainScreen --> NavigationState: selectedIndex = 0
    
    NavigationState --> MyAppHomeScreen: Affichage
    
    MyAppHomeScreen --> CategoryState: selectedCategory = 'All'
    
    CategoryState --> StreamCategories: Écoute Firestore
    CategoryState --> StreamRecipes: Écoute Firestore
    
    StreamCategories --> DisplayCategories: Affiche boutons
    StreamRecipes --> DisplayRecipes: Affiche GridView
    
    DisplayCategories --> UserTapCategory: Utilisateur tap
    UserTapCategory --> CategoryState: setState selectedCategory
    
    CategoryState --> StreamRecipes: Stream mis à jour
    
    note right of CategoryState
        Variable d'état qui contrôle
        le filtre des recettes
    end note
    
    note right of StreamRecipes
        Stream dynamique basé sur
        selectedCategory
    end note
```

---

### Relations de dépendance entre widgets

```mermaid
graph TD
    MS[main.dart<br/>MyApp] --> AMS[AppMainScreen]
    
    AMS --> |Dépend de| State1[State: selectedIndex]
    AMS --> |Contient| BNB[BottomNavigationBar]
    AMS --> |Contient conditionnellement| MHS[MyAppHomeScreen]
    
    MHS --> |Dépend de| State2[State: selectedCategory]
    MHS --> |Dépend de| FS[FirebaseFirestore instance]
    MHS --> |Utilise| HP[headerParts]
    MHS --> |Utilise| MSB[mySearchBar]
    MHS --> |Contient| BTE[BannerToExplore]
    MHS --> |Utilise| CB[categoryButtons]
    MHS --> |Contient| SBC[StreamBuilder Categories]
    MHS --> |Contient| SBR[StreamBuilder Recipes]
    
    SBC --> |Lit| FSCat[(Firestore categories)]
    SBC --> |Appelle| CB
    
    CB --> |Modifie| State2
    
    State2 --> |Contrôle| SBR
    
    SBR --> |Lit| FSDetails[(Firestore details)]
    
    AMS --> |Utilise| Const[constants.dart<br/>kprimaryColor]
    MHS --> |Utilise| Const
    
    AMS --> |Utilise| Icons[Iconsax package]
    MHS --> |Utilise| Icons
    BTE --> |Utilise| Icons
    
    style AMS fill:#e1f5ff
    style MHS fill:#e1ffe1
    style State1 fill:#ffe1e1
    style State2 fill:#ffe1e1
    style FSCat fill:#fff4e1
    style FSDetails fill:#fff4e1
```

---

### Hiérarchie des StatefulWidgets et leur State

```mermaid
classDiagram
    class AppMainScreen {
        +StatefulWidget
        +Key? key
        +createState() State
    }
    
    class _AppMainScreenState {
        +State~AppMainScreen~
        -int selectedIndex = 0
        +build(BuildContext) Widget
    }
    
    class MyAppHomeScreen {
        +StatefulWidget
        +Key? key
        +createState() State
    }
    
    class _MyAppHomeScreenState {
        +State~MyAppHomeScreen~
        -String selectedCategory = "All"
        -FirebaseFirestore _firestore
        +build(BuildContext) Widget
        +headerParts() Padding
        +mySearchBar() Container
        +categoryButtons(List~String~) Widget
    }
    
    class BannerToExplore {
        +StatelessWidget
        +Key? key
        +build(BuildContext) Widget
    }
    
    AppMainScreen --> _AppMainScreenState : creates
    MyAppHomeScreen --> _MyAppHomeScreenState : creates
    AppMainScreen ..> MyAppHomeScreen : contains
    _MyAppHomeScreenState ..> BannerToExplore : uses
```

---

## Récapitulatif visuel

### Carte mentale de la structure

```mermaid
mindmap
  root((app_main_screen.dart))
    AppMainScreen
      Scaffold
      BottomNavigationBar
        4 items navigation
        État: selectedIndex
      Body conditionnel
        MyAppHomeScreen si index=0
        Placeholder sinon
    MyAppHomeScreen
      SafeArea
      SingleChildScrollView
      Column principale
        headerParts
          Titre + Notification
        mySearchBar
          TextField recherche
        BannerToExplore
          Promo banner
        StreamBuilder Categories
          Boutons catégories
          État: selectedCategory
        StreamBuilder Recipes
          GridView recettes
          Filtrage dynamique
    BannerToExplore
      Container décoré
      Stack layout
        Texte + Bouton
        Image chef
    État global
      selectedIndex
        Contrôle navigation
      selectedCategory
        Filtre recettes
    Firebase
      Collection categories
        Lit catégories
      Collection details
        Lit recettes
        Filtre par catégorie
```

---

## Points clés à retenir

### Structure hiérarchique
1. **AppMainScreen** = Widget racine avec navigation
   - État : `selectedIndex` (int)
   - Rôle : Gérer la navigation entre pages

2. **MyAppHomeScreen** = Page d'accueil
   - État : `selectedCategory` (String)
   - Rôle : Afficher et filtrer les recettes

3. **BannerToExplore** = Widget sans état
   - Rôle : Affichage statique promotionnel

### Relations importantes
- **selectedIndex** (dans AppMainScreen) → Contrôle quelle page afficher
- **selectedCategory** (dans MyAppHomeScreen) → Contrôle quel Stream Firestore utiliser
- **StreamBuilder Categories** → Modifie selectedCategory via callbacks
- **selectedCategory** → Déclenche rebuild du StreamBuilder Recipes

### Flux de données
```
Firestore → StreamBuilder → UI → User interaction → setState → Rebuild → Firestore
```

---

**Document créé pour visualiser l'arbre des widgets de app_main_screen.dart**
*Tous les widgets et leurs relations sont documentés avec des diagrammes Mermaid*

