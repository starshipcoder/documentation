# Choix Techniques EasyWay Flutter

Document de référence pour maintenir la cohérence sur d'autres projets Flutter.

---

## Environnement

- **Flutter**: 3.35+ (stable)
- **Dart**: 3.9+
- **SDK**: `>=3.8.0 <4.0.0`

---

## Architecture Clean Architecture

### Structure des dossiers

Chaque module suit une structure en 3 couches :

```
module_name/
├── data/           # Repositories, sources de données, implémentations
├── domain/         # Entités, interfaces, use cases, logique métier pure
├── presentation/   # Cubits/Blocs, widgets, écrans
└── web_services/   # Clients API externes (si applicable)
```

### Couche `domain/`
- **Entités** : Objets métier purs (pas de dépendances Flutter)
- **Interfaces** : Contrats pour les repositories (abstract class)
- **Use Cases** : Logique métier complexe orchestrant plusieurs repositories

### Couche `data/`
- **Repositories** : Implémentations des interfaces domain
- **Data Sources** : Accès aux APIs, base locale, etc.
- **Mappers** : Conversion DTO <-> Entités

### Couche `presentation/`
- **Cubits** : Logique de présentation, état des écrans
- **Widgets** : Composants UI réutilisables
- **Screens** : Pages complètes

---

## State Management : BLoC / Cubit

```yaml
dependencies:
  bloc: ^9.0.0
  flutter_bloc: ^9.0.0
```

- **Cubit** pour la majorité des cas (logique simple)
- **Bloc** uniquement si besoin d'events complexes avec transformers

```dart
class GetMyLocationCubit extends Cubit<GetMyLocationState> {
  GetMyLocationCubit(this._repository) : super(GetMyLocationInitial());

  final MyLocationRepository _repository;

  Future<void> getLocation() async {
    emit(GetMyLocationLoading());
    try {
      final location = await _repository.getMyLocation();
      emit(GetMyLocationSuccess(location));
    } catch (e) {
      emit(GetMyLocationFailure(e.toString()));
    }
  }
}
```

---

## Injection de Dépendances : Container Pattern

### Principe

Chaque module expose un `Container` qui :
1. Reçoit ses dépendances externes en paramètres du constructeur
2. Instancie ses propres repositories/use cases en `late final`
3. Expose une méthode `createProviders()` retournant les `BlocProvider`

### Container de module

```dart
class ContactbookContainer {
  ContactbookContainer({
    required AppContactbookRepository appContactbookRepository,
    required MyLocationRepository myLocationRepository,
    // ... autres dépendances injectées
  }) : _appContactbookRepository = appContactbookRepository,
       _myLocationRepository = myLocationRepository;

  final AppContactbookRepository _appContactbookRepository;
  final MyLocationRepository _myLocationRepository;

  // Use cases créés en interne
  late final ManageContactDetailsUseCase _manageContactDetailsUseCase =
      ManageContactDetailsUseCase(_appContactbookRepository);

  // Expose le use case si nécessaire
  ManageContactDetailsUseCase get manageContactDetailsUseCase => _manageContactDetailsUseCase;

  /// Crée les BlocProviders du module
  List<BlocProvider> createProviders() {
    return [
      BlocProvider<GetContactsCubit>(
        create: (_) => GetContactsCubit(_appContactbookRepository),
      ),
      // ...
    ];
  }
}
```

### AppContainer (racine)

L'`AppContainer` est le container principal de l'application :

```dart
abstract class AppContainer extends CoreContainer {
  static late AppContainer _instance;
  static AppContainer get instance => _instance;
  static void init(AppContainer appContainer) => _instance = appContainer;

  // Configuration
  AppConfig get config;
  AppFeatures get features;
  AppApiKeys get apiKeys;

  // Repositories partagés
  GeocoderRepository get geocoderRepository;
  ColorRepository get colorRepository;

  // Point d'entrée des providers
  List<BlocProvider> createProviders();
}

class AppContainerImpl extends AppContainer {
  // Containers des modules
  late final LocationContainer _locationContainer = LocationContainer(
    hereApiKey: Env.getHereKey(),
  );

  late final ContactbookContainer _contactbookContainer = ContactbookContainer(
    myLocationRepository: _locationContainer.myLocationRepository,
    // ...
  );

  @override
  List<BlocProvider> createProviders() {
    return [
      ..._locationContainer.createProviders(),
      ..._contactbookContainer.createProviders(),
      // Providers spécifiques à l'app
      BlocProvider<SomeCubit>(create: (_) => SomeCubit(...)),
    ];
  }
}
```

### Initialisation dans main.dart

```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  final container = await AppContainerImpl.create();
  AppContainer.init(container);

  runApp(
    MultiBlocProvider(
      providers: container.createProviders(),
      child: MyApp(),
    ),
  );
}
```

---

## Persistence Locale : Hive CE

```yaml
dependencies:
  hive_ce: ^2.10.1
  hive_ce_flutter: ^2.2.0

dev_dependencies:
  hive_ce_generator: ^1.8.2
  build_runner: ^2.2.1
```

Préféré à SharedPreferences pour le stockage structuré.

---

## Réseau : Dio

```yaml
dependencies:
  dio: ^5.0.0
  json_annotation: ^4.9.0

dev_dependencies:
  json_serializable: ^6.5.3
```

---

## Secrets : Envied

```yaml
dependencies:
  envied: ^1.1.1

dev_dependencies:
  envied_generator: ^1.1.1
```

---

## Géolocalisation & Maps

```yaml
dependencies:
  latlong2: ^0.9.0                    # Modèle LatLng
  geolocator: ^14.0.2                 # Position GPS
  geocoding: ^4.0.0                   # Reverse geocoding
  permission_handler: ^12.0.1         # Permissions système
  flutter_map: ^8.2.2                 # Carte OpenStreetMap
  flutter_map_marker_cluster: ^8.2.2  # Clustering markers
  map_launcher: ^4.4.2                # Ouvrir apps navigation
```

---

## Localisation (i18n)

```yaml
dependencies:
  intl: ^0.20.2

dev_dependencies:
  intl_utils: ^2.4.0
```

Configuration :
```yaml
flutter_intl:
  enabled: true
  arb_dir: lib/l10n
  output_dir: lib/l10n/generated
```

---

## Analytics & Monitoring

```yaml
dependencies:
  firebase_core: ^4.2.1
  firebase_analytics: ^12.0.4
  sentry_flutter: ^9.8.0
```

---

## Tests

```yaml
dev_dependencies:
  flutter_test:
    sdk: flutter
  integration_test:
    sdk: flutter
  test: ^1.17.0
  mocktail: ^1.0.0
```

---

## Conventions

### Imports
- Toujours `package:` imports (jamais de relatifs dans lib/)
- Ordre : dart, flutter, packages externes, packages internes

### Repository Pattern
```dart
// domain/
abstract class MyLocationRepository {
  Future<LatLng?> getMyLocation();
}

// data/
class NativeMyLocationRepository implements MyLocationRepository {
  @override
  Future<LatLng?> getMyLocation() async { /* ... */ }
}
```

---

## Prompt Claude

```
Tu travailles sur un projet Flutter avec ces choix :

ARCHITECTURE:
- Clean Architecture : data/ domain/ presentation/
- State management : BLoC/Cubit (flutter_bloc ^9.0.0)
- DI : Container pattern avec AppContainer racine
- Persistence : Hive CE
- HTTP : Dio

CONTAINERS:
- Chaque module a un Container qui reçoit ses dépendances et expose createProviders()
- AppContainer orchestre tous les containers de modules
- Les repositories sont injectés, les use cases créés en interne

CONVENTIONS:
- Package imports uniquement
- Repository pattern : interface dans domain/, implémentation dans data/
- Cubits pour la logique simple, Blocs si events complexes

SDK: Flutter 3.35+, Dart 3.9+
```
