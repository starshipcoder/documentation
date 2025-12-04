# Tronc Commun Flutter - Starship Apps

Base technique réutilisable pour toutes les apps Flutter.

---

## Stack Standard

| Élément | Choix | Package |
|---------|-------|---------|
| State Management | Cubit | `flutter_bloc ^8.x` |
| Architecture | Clean Architecture | - |
| DI | Container Pattern | - |
| HTTP | Dio | `dio ^5.x` |
| Storage | SharedPreferences | `shared_preferences ^2.x` |
| Analytics | Firebase Analytics | `firebase_analytics` |
| Crash | Firebase Crashlytics | `firebase_crashlytics` |
| IAP | RevenueCat | `purchases_flutter ^9.x` |

---

## Structure Projet

```
lib/
├── main.dart
├── app/
│   ├── app.dart              # MaterialApp
│   ├── app_container.dart    # DI racine
│   ├── routes.dart           # GoRouter
│   └── theme.dart
├── core/
│   ├── constants/
│   ├── services/             # Analytics, Logger
│   └── utils/
├── features/
│   └── [feature_name]/
│       ├── data/             # Repository impl, datasources
│       ├── domain/           # Entities, interfaces
│       └── presentation/     # Cubits, pages, widgets
```

---

## Container Pattern

```dart
// app_container.dart
class AppContainer {
  static AppContainer? _instance;
  static AppContainer get instance => _instance!;

  late final SharedPreferences sharedPreferences;
  late final PackageInfo packageInfo;

  static Future<void> init() async {
    _instance = AppContainer._();
    await _instance!._initialize();
  }

  Future<void> _initialize() async {
    sharedPreferences = await SharedPreferences.getInstance();
    packageInfo = await PackageInfo.fromPlatform();
    // ... autres initialisations
  }

  List<BlocProvider> createProviders() {
    return [
      // BlocProvider<MyCubit>(create: (_) => MyCubit(...)),
    ];
  }
}
```

---

## Main.dart Standard

```dart
void main() async {
  await runZonedGuarded(() async {
    WidgetsFlutterBinding.ensureInitialized();

    // Firebase
    await Firebase.initializeApp();
    FlutterError.onError = FirebaseCrashlytics.instance.recordFlutterFatalError;

    // App Container
    await AppContainer.init();

    runApp(const MyApp());
  }, (error, stack) {
    FirebaseCrashlytics.instance.recordError(error, stack, fatal: true);
  });
}
```

---

## Cubit Standard

```dart
// États
abstract class MyState {}
class MyInitial extends MyState {}
class MyLoading extends MyState {}
class MyLoaded extends MyState {
  final Data data;
  MyLoaded(this.data);
}
class MyError extends MyState {
  final String message;
  MyError(this.message);
}

// Cubit
class MyCubit extends Cubit<MyState> {
  MyCubit(this._repository) : super(MyInitial());

  final MyRepository _repository;

  Future<void> load() async {
    emit(MyLoading());
    try {
      final data = await _repository.getData();
      emit(MyLoaded(data));
    } catch (e) {
      emit(MyError(e.toString()));
    }
  }
}
```

---

## Repository Pattern

```dart
// domain/repositories/my_repository.dart
abstract class MyRepository {
  Future<Data> getData();
}

// data/repositories/my_repository_impl.dart
class MyRepositoryImpl implements MyRepository {
  @override
  Future<Data> getData() async {
    // Implementation
  }
}
```

---

## Services Communs

### AnalyticsService
```dart
class AnalyticsService {
  static final _analytics = FirebaseAnalytics.instance;

  static void logEvent(String name, [Map<String, dynamic>? params]) {
    _analytics.logEvent(name: name, parameters: params);
  }

  static void logScreenView(String screenName) {
    _analytics.logScreenView(screenName: screenName);
  }
}
```

### LoggerService
```dart
class Logger {
  static void info(String tag, String message) {
    debugPrint('[$tag] $message');
  }

  static void error(String tag, String message, [Object? error]) {
    debugPrint('[$tag] ERROR: $message ${error ?? ''}');
    FirebaseCrashlytics.instance.log('[$tag] $message');
  }
}
```

---

## Conventions

- **Imports** : Toujours `package:` (jamais relatifs)
- **Nommage fichiers** : `snake_case.dart`
- **Nommage classes** : `PascalCase`
- **Cubits** : Un cubit = une responsabilité
- **Widgets** : Extraire dès que > 50 lignes

---

## Packages Optionnels

| Besoin | Package |
|--------|---------|
| Maps | `flutter_map` + `latlong2` |
| Location | `geolocator` + `permission_handler` |
| Navigation externe | `map_launcher` |
| Remote Config | `firebase_remote_config` |
| Deep links | `go_router` |
