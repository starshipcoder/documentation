# FuelMap - Spécifications Techniques

## Informations Générales

| Élément | Valeur |
|---------|--------|
| **Nom de l'app** | Plein Malin (FuelMap) |
| **Version** | 0.0.4 (MVP) |
| **Date création** | 29/11/2025 |
| **Dernière mise à jour** | 01/12/2025 |

---

## 1. Stack Technique

### 1.1 Vue d'ensemble

```
                      FRONTEND
                     [Flutter]
                         |
      +--------+---------+---------+---------+
      |        |         |         |         |
data.gouv.fr Firebase  Firebase  RevenueCat OSRM
 (Stations) Analytics Crashlytics (IAP)   (Routes)
      |
  [Cache Local]
  (SharedPrefs)
```

**Architecture sans serveur** : L'app appelle directement l'API data.gouv.fr et cache les données localement.

### 1.2 Choix Technologiques

| Couche | Technologie | Justification |
|--------|-------------|---------------|
| **Frontend** | Flutter 3.x | Cross-platform, cohérence avec autres apps |
| **State Management** | flutter_bloc 8.x (Cubit) | Cohérence EasyWay, séparation logique/UI |
| **Maps** | flutter_map 7.x | OpenStreetMap, gratuit, pas de clé API |
| **Architecture** | Clean Architecture | Maintenabilité, testabilité |
| **DI** | Container Pattern | Cohérence EasyWay |
| **HTTP** | Dio | Interceptors, cache, retry |
| **Cache stations** | SharedPreferences + JSON | Simple, suffisant pour MVP |
| **Préférences** | SharedPreferences | Simple pour settings user |
| **Analytics** | Firebase Analytics | Gratuit, intégré Firebase |
| **Crash reporting** | Firebase Crashlytics | Gratuit, intégré Firebase |
| **In-App Purchase** | RevenueCat | Paywalls, gestion abonnements |
| **Routing** | OSRM | Open source, calcul itinéraires |

### 1.3 Versions Minimales

| Plateforme | Version min | Raison |
|------------|-------------|--------|
| iOS | 14.0 | 95%+ market coverage |
| Android | API 24 (7.0) | 95%+ market coverage |
| Flutter | 3.x | Stable |
| Dart | 3.9+ | Records, patterns |

---

## 2. Architecture Application

### 2.1 Structure Projet

```
lib/
├── main.dart
├── main_dev.dart
├── main_prod.dart
├── app/
│   ├── app.dart
│   ├── app_container.dart
│   ├── routes.dart
│   └── theme.dart
├── core/
│   ├── config/
│   │   ├── app_config.dart
│   │   └── env.dart
│   ├── constants/
│   │   └── fuel_types.dart
│   ├── errors/
│   │   └── failures.dart
│   ├── network/
│   │   └── dio_client.dart
│   └── utils/
│       ├── distance_utils.dart
│       └── price_utils.dart
├── features/
│   ├── stations/
│   │   ├── data/
│   │   │   ├── datasources/
│   │   │   │   ├── stations_remote_datasource.dart
│   │   │   │   └── stations_local_datasource.dart
│   │   │   ├── models/
│   │   │   │   └── station_model.dart
│   │   │   └── repositories/
│   │   │       └── stations_repository_impl.dart
│   │   ├── domain/
│   │   │   ├── entities/
│   │   │   │   ├── station.dart
│   │   │   │   └── fuel_price.dart
│   │   │   ├── repositories/
│   │   │   │   └── stations_repository.dart
│   │   │   └── usecases/
│   │   │       ├── get_nearby_stations.dart
│   │   │       └── get_station_details.dart
│   │   ├── presentation/
│   │   │   ├── cubits/
│   │   │   │   ├── stations_cubit.dart
│   │   │   │   └── filters_cubit.dart
│   │   │   ├── pages/
│   │   │   │   └── map_page.dart
│   │   │   └── widgets/
│   │   │       ├── station_marker.dart
│   │   │       ├── station_bottom_sheet.dart
│   │   │       └── filters_bottom_sheet.dart
│   │   └── stations_container.dart
│   ├── preferences/
│   │   ├── data/
│   │   │   └── preferences_repository_impl.dart
│   │   ├── domain/
│   │   │   ├── entities/
│   │   │   │   └── user_preferences.dart
│   │   │   └── repositories/
│   │   │       └── preferences_repository.dart
│   │   ├── presentation/
│   │   │   ├── cubits/
│   │   │   │   └── preferences_cubit.dart
│   │   │   └── widgets/
│   │   │       └── preferences_bottom_sheet.dart
│   │   └── preferences_container.dart
│   ├── onboarding/
│   │   └── presentation/
│   │       ├── pages/
│   │       │   └── onboarding_page.dart
│   │       └── widgets/
│   │           ├── vehicle_type_step.dart
│   │           ├── fuel_type_step.dart
│   │           └── location_permission_step.dart
│   └── location/
│       ├── data/
│       │   └── location_repository_impl.dart
│       ├── domain/
│       │   └── repositories/
│       │       └── location_repository.dart
│       ├── presentation/
│       │   └── cubits/
│       │       └── location_cubit.dart
│       └── location_container.dart
├── services/
│   ├── analytics_service.dart
│   └── error_service.dart
└── l10n/
    ├── app_fr.arb
    └── app_en.arb
```

### 2.2 Clean Architecture - Couches

```
┌─────────────────────────────────────────────────────────┐
│                    PRESENTATION                         │
│  Cubits, Pages, Widgets                                 │
│  (flutter_bloc, flutter_map)                            │
├─────────────────────────────────────────────────────────┤
│                      DOMAIN                             │
│  Entities, Repository Interfaces, Use Cases             │
│  (Dart pur, aucune dépendance Flutter)                  │
├─────────────────────────────────────────────────────────┤
│                       DATA                              │
│  Repository Impl, DataSources, Models                   │
│  (Dio, Drift, SharedPreferences)                        │
└─────────────────────────────────────────────────────────┘
```

### 2.3 Container Pattern (DI)

```dart
// stations_container.dart
class StationsContainer {
  StationsContainer({
    required LocationRepository locationRepository,
    required DioClient dioClient,
    required AppDatabase database,
  }) : _locationRepository = locationRepository,
       _dioClient = dioClient,
       _database = database;

  final LocationRepository _locationRepository;
  final DioClient _dioClient;
  final AppDatabase _database;

  late final StationsRemoteDataSource _remoteDataSource =
      StationsRemoteDataSource(_dioClient);

  late final StationsLocalDataSource _localDataSource =
      StationsLocalDataSource(_database);

  late final StationsRepository _stationsRepository =
      StationsRepositoryImpl(
        remoteDataSource: _remoteDataSource,
        localDataSource: _localDataSource,
      );

  late final GetNearbyStations _getNearbyStations =
      GetNearbyStations(_stationsRepository);

  List<BlocProvider> createProviders() {
    return [
      BlocProvider<StationsCubit>(
        create: (_) => StationsCubit(
          getNearbyStations: _getNearbyStations,
          locationRepository: _locationRepository,
        ),
      ),
      BlocProvider<FiltersCubit>(
        create: (_) => FiltersCubit(),
      ),
    ];
  }
}
```

```dart
// app_container.dart
class AppContainer {
  static late AppContainer _instance;
  static AppContainer get instance => _instance;

  static Future<void> init() async {
    _instance = AppContainer._();
    await _instance._initialize();
  }

  AppContainer._();

  late final AppConfig config;
  late final DioClient dioClient;
  late final AppDatabase database;

  late final LocationContainer _locationContainer;
  late final StationsContainer _stationsContainer;
  late final PreferencesContainer _preferencesContainer;

  Future<void> _initialize() async {
    config = AppConfig.fromEnv();
    dioClient = DioClient(config: config);
    database = AppDatabase();

    _locationContainer = LocationContainer();

    _stationsContainer = StationsContainer(
      locationRepository: _locationContainer.locationRepository,
      dioClient: dioClient,
      database: database,
    );

    _preferencesContainer = PreferencesContainer();
  }

  List<BlocProvider> createProviders() {
    return [
      ..._locationContainer.createProviders(),
      ..._stationsContainer.createProviders(),
      ..._preferencesContainer.createProviders(),
    ];
  }
}
```

### 2.4 Navigation

**Solution** : GoRouter

```dart
// routes.dart
final router = GoRouter(
  initialLocation: '/',
  routes: [
    GoRoute(
      path: '/',
      builder: (_, __) => const SplashPage(),
    ),
    GoRoute(
      path: '/onboarding',
      builder: (_, __) => const OnboardingPage(),
    ),
    GoRoute(
      path: '/map',
      builder: (_, __) => const MapPage(),
    ),
  ],
  redirect: (context, state) {
    final prefs = context.read<PreferencesCubit>().state;
    if (!prefs.onboardingCompleted && state.matchedLocation != '/onboarding') {
      return '/onboarding';
    }
    return null;
  },
);
```

---

## 3. API data.gouv.fr

### 3.1 Source de Données

**URL** : `https://data.economie.gouv.fr/api/explore/v2.1/catalog/datasets/prix-des-carburants-en-france-flux-instantane-v2/records`

**Format** : JSON (API REST)

**Mise à jour** : Toutes les 10 minutes par les stations (obligation légale)

### 3.2 Endpoints Utilisés

| Endpoint | Méthode | Description | Params |
|----------|---------|-------------|--------|
| `/records` | GET | Liste des stations | `where`, `limit`, `offset`, `select` |

### 3.3 Requête Type

```
GET /records?
  select=id,adresse,ville,cp,latitude,longitude,horaires,services_service,prix
  &where=within_distance(geom, geom'POINT(2.3522 48.8566)', 10km)
  &limit=100
```

### 3.4 Modèle de Données API

```json
{
  "id": "75116001",
  "adresse": "123 Avenue des Champs-Élysées",
  "ville": "Paris",
  "cp": "75008",
  "latitude": 48.8698,
  "longitude": 2.3075,
  "horaires": "24/24",
  "services_service": ["Lavage auto", "Boutique", "DAB"],
  "prix": [
    {
      "nom": "Gazole",
      "valeur": 1.659,
      "maj": "2025-11-29T10:30:00"
    },
    {
      "nom": "SP95",
      "valeur": 1.789,
      "maj": "2025-11-29T10:30:00"
    }
  ]
}
```

### 3.5 Mapping Carburants

| API data.gouv | App enum | Display |
|---------------|----------|---------|
| `Gazole` | `diesel` | Diesel |
| `SP95` | `sp95` | SP95 |
| `SP98` | `sp98` | SP98 |
| `E10` | `sp95e10` | SP95-E10 |
| `E85` | `e85` | E85 |
| `GPLc` | `gpl` | GPL |

---

## 4. Stockage Local

### 4.1 SharedPreferences (Préférences)

```dart
// Clés
const String kVehicleType = 'vehicle_type';       // citadine|berline|suv|utilitaire
const String kTankVolume = 'tank_volume';         // 40|50|60|70
const String kDefaultFuel = 'default_fuel';       // diesel|sp95|sp98|sp95e10|e85|gpl
const String kNavigationApp = 'navigation_app';   // apple_maps|google_maps
const String kOnboardingDone = 'onboarding_done'; // bool
```

### 4.2 Drift (Cache Stations)

```dart
// database.dart
@DriftDatabase(tables: [Stations, Prices])
class AppDatabase extends _$AppDatabase {
  AppDatabase() : super(_openConnection());

  @override
  int get schemaVersion => 1;
}

// stations_table.dart
class Stations extends Table {
  TextColumn get id => text()();
  TextColumn get name => text().nullable()();
  TextColumn get address => text()();
  TextColumn get city => text()();
  TextColumn get postalCode => text()();
  RealColumn get latitude => real()();
  RealColumn get longitude => real()();
  TextColumn get hours => text().nullable()();        // JSON string
  TextColumn get services => text().nullable()();     // JSON array string
  DateTimeColumn get cachedAt => dateTime()();

  @override
  Set<Column> get primaryKey => {id};
}

// prices_table.dart
class Prices extends Table {
  IntColumn get id => integer().autoIncrement()();
  TextColumn get stationId => text().references(Stations, #id)();
  TextColumn get fuelType => text()();               // enum string
  RealColumn get price => real()();
  DateTimeColumn get updatedAt => dateTime()();
}
```

### 4.3 Stratégie de Cache

```dart
class StationsRepositoryImpl implements StationsRepository {
  static const _cacheValidityDuration = Duration(hours: 1);

  @override
  Future<List<Station>> getNearbyStations(LatLng center, double radiusKm) async {
    // 1. Vérifier le cache
    final cachedStations = await _localDataSource.getStationsInRadius(
      center, radiusKm,
    );

    final cacheIsValid = cachedStations.isNotEmpty &&
        cachedStations.first.cachedAt.isAfter(
          DateTime.now().subtract(_cacheValidityDuration),
        );

    if (cacheIsValid) {
      return cachedStations;
    }

    // 2. Fetch depuis API
    try {
      final remoteStations = await _remoteDataSource.fetchStations(
        center, radiusKm,
      );

      // 3. Sauvegarder en cache
      await _localDataSource.cacheStations(remoteStations);

      return remoteStations;
    } catch (e) {
      // 4. Fallback sur cache expiré si offline
      if (cachedStations.isNotEmpty) {
        return cachedStations;
      }
      rethrow;
    }
  }
}
```

---

## 5. Entités Domain

### 5.1 Station

```dart
class Station {
  final String id;
  final String address;
  final String city;
  final String postalCode;
  final LatLng location;
  final String? hours;
  final List<String> services;
  final List<FuelPrice> prices;

  const Station({
    required this.id,
    required this.address,
    required this.city,
    required this.postalCode,
    required this.location,
    this.hours,
    this.services = const [],
    this.prices = const [],
  });

  String get fullAddress => '$address, $postalCode $city';

  bool get isOpen24h => hours?.contains('24') ?? false;

  FuelPrice? getPriceForFuel(FuelType type) {
    return prices.firstWhereOrNull((p) => p.type == type);
  }
}
```

### 5.2 FuelPrice

```dart
class FuelPrice {
  final FuelType type;
  final double pricePerLiter;
  final DateTime updatedAt;

  const FuelPrice({
    required this.type,
    required this.pricePerLiter,
    required this.updatedAt,
  });

  /// Fraîcheur du prix
  PriceFreshness get freshness {
    final age = DateTime.now().difference(updatedAt);
    if (age.inHours < 24) return PriceFreshness.fresh;
    if (age.inDays < 3) return PriceFreshness.recent;
    return PriceFreshness.old;
  }

  /// Prix du plein estimé
  double estimatedFullTank(int tankVolume) => pricePerLiter * tankVolume;
}

enum PriceFreshness { fresh, recent, old }

enum FuelType { diesel, sp95, sp98, sp95e10, e85, gpl }
```

### 5.3 UserPreferences

```dart
class UserPreferences {
  final VehicleType vehicleType;
  final int tankVolume;
  final FuelType defaultFuel;
  final NavigationApp? preferredNavApp;
  final bool onboardingCompleted;

  const UserPreferences({
    this.vehicleType = VehicleType.berline,
    this.tankVolume = 50,
    this.defaultFuel = FuelType.diesel,
    this.preferredNavApp,
    this.onboardingCompleted = false,
  });
}

enum VehicleType {
  citadine(40),
  berline(50),
  suv(60),
  utilitaire(70);

  final int defaultTankVolume;
  const VehicleType(this.defaultTankVolume);
}

enum NavigationApp { appleMaps, googleMaps }
```

---

## 6. Dépendances

### 6.1 pubspec.yaml (Actuel)

```yaml
name: fuelmap
description: Trouve le carburant le moins cher près de toi
version: 0.0.4+004

environment:
  sdk: ^3.9.2

dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter

  cupertino_icons: ^1.0.8

  # State Management
  bloc: ^8.1.4
  flutter_bloc: ^8.1.6

  # Navigation
  go_router: ^14.6.2

  # Network
  dio: ^5.7.0
  http: ^1.2.2

  # Maps & Location
  flutter_map: ^7.0.2
  flutter_map_marker_cluster: ^1.4.0
  latlong2: ^0.9.1
  geolocator: ^13.0.2
  permission_handler: ^11.3.1
  map_launcher: ^3.5.0

  # Storage
  shared_preferences: ^2.3.3

  # Firebase
  firebase_core: ^3.8.1
  firebase_analytics: ^11.4.1
  firebase_crashlytics: ^4.2.1
  firebase_remote_config: ^5.2.1

  # In-App Purchases (RevenueCat)
  purchases_flutter: ^9.9.9
  purchases_ui_flutter: ^9.9.9

  # Utils
  package_info_plus: ^8.3.0
  url_launcher: ^6.3.1
  intl: ^0.20.2
  equatable: ^2.0.5
  collection: ^1.18.0

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^5.0.0
  mocktail: ^1.0.4
  bloc_test: ^9.1.7
  flutter_launcher_icons: ^0.14.3
  flutter_native_splash: ^2.4.4

flutter:
  uses-material-design: true

  assets:
    - assets/images/
    - assets/data/
```

---

## 7. Analytics (Mixpanel)

### 7.1 Events

| Event | Properties | Trigger |
|-------|------------|---------|
| `app_opened` | `first_open`, `version` | App launch |
| `onboarding_started` | - | Début onboarding |
| `onboarding_completed` | `vehicle_type`, `fuel_type` | Fin onboarding |
| `onboarding_skipped` | `step` | Skip onboarding |
| `map_loaded` | `stations_count`, `load_time_ms` | Carte affichée |
| `station_viewed` | `station_id`, `fuel_type`, `price` | Tap marker |
| `navigation_launched` | `station_id`, `app` | Bouton "Y aller" |
| `filter_changed` | `fuel_type`, `freshness` | Changement filtre |
| `preferences_updated` | `field`, `value` | Modif préférences |
| `error_occurred` | `type`, `message` | Erreur app |

### 7.2 User Properties

| Property | Type | Description |
|----------|------|-------------|
| `vehicle_type` | string | citadine/berline/suv/utilitaire |
| `default_fuel` | string | Type carburant préféré |
| `tank_volume` | int | Volume réservoir |
| `app_version` | string | Version app |
| `os` | string | iOS/Android |

---

## 8. Error Handling (Sentry)

### 8.1 Configuration

```dart
Future<void> main() async {
  await SentryFlutter.init(
    (options) {
      options.dsn = Env.sentryDsn;
      options.environment = Env.environment; // dev/prod
      options.tracesSampleRate = 0.2;
      options.enableAutoSessionTracking = true;
    },
    appRunner: () async {
      await AppContainer.init();
      runApp(const FuelMapApp());
    },
  );
}
```

### 8.2 Breadcrumbs

```dart
Sentry.addBreadcrumb(Breadcrumb(
  category: 'navigation',
  message: 'Opened station detail',
  data: {'station_id': station.id},
));
```

---

## 9. CI/CD (Codemagic)

### 9.1 Environnements

| Env | Usage | API | Build |
|-----|-------|-----|-------|
| `dev` | Développement local | data.gouv.fr | Debug |
| `prod` | Production | data.gouv.fr | Release |

### 9.2 Configuration codemagic.yaml

```yaml
workflows:
  ios-release:
    name: iOS Release
    max_build_duration: 60
    instance_type: mac_mini_m2
    environment:
      flutter: stable
      xcode: latest
      groups:
        - app_credentials
      vars:
        BUNDLE_ID: com.yourcompany.fuelmap
    triggering:
      events:
        - tag
      tag_patterns:
        - pattern: 'v*'
    scripts:
      - name: Set up code signing
        script: |
          keychain initialize
          app-store-connect fetch-signing-files $BUNDLE_ID --type IOS_APP_STORE
          keychain add-certificates
          xcode-project use-profiles
      - name: Get packages
        script: flutter pub get
      - name: Build
        script: |
          flutter build ipa --release \
            --dart-define=ENV=prod \
            --export-options-plist=/Users/builder/export_options.plist
    artifacts:
      - build/ios/ipa/*.ipa
    publishing:
      app_store_connect:
        auth: integration
        submit_to_testflight: true

  android-release:
    name: Android Release
    max_build_duration: 60
    instance_type: linux_x2
    environment:
      flutter: stable
      java: 17
      groups:
        - app_credentials
    triggering:
      events:
        - tag
      tag_patterns:
        - pattern: 'v*'
    scripts:
      - name: Set up signing
        script: |
          echo $KEYSTORE | base64 --decode > keystore.jks
      - name: Get packages
        script: flutter pub get
      - name: Build
        script: |
          flutter build appbundle --release \
            --dart-define=ENV=prod
    artifacts:
      - build/app/outputs/bundle/release/*.aab
    publishing:
      google_play:
        credentials: $GCLOUD_SERVICE_ACCOUNT_CREDENTIALS
        track: internal
```

### 9.3 Secrets (Codemagic Groups)

| Variable | Description |
|----------|-------------|
| `SENTRY_DSN` | DSN Sentry |
| `MIXPANEL_TOKEN` | Token Mixpanel |
| `KEYSTORE` | Android keystore (base64) |
| `KEYSTORE_PASSWORD` | Password keystore |
| `KEY_ALIAS` | Alias de la clé |
| `KEY_PASSWORD` | Password clé |

---

## 10. Tests

### 10.1 Structure

```
test/
├── unit/
│   ├── domain/
│   │   └── usecases/
│   │       └── get_nearby_stations_test.dart
│   └── data/
│       └── repositories/
│           └── stations_repository_test.dart
├── widget/
│   ├── station_marker_test.dart
│   └── filters_bottom_sheet_test.dart
└── integration/
    └── map_flow_test.dart
```

### 10.2 Exemple Test Cubit

```dart
void main() {
  group('StationsCubit', () {
    late StationsCubit cubit;
    late MockGetNearbyStations mockGetNearbyStations;
    late MockLocationRepository mockLocationRepository;

    setUp(() {
      mockGetNearbyStations = MockGetNearbyStations();
      mockLocationRepository = MockLocationRepository();
      cubit = StationsCubit(
        getNearbyStations: mockGetNearbyStations,
        locationRepository: mockLocationRepository,
      );
    });

    blocTest<StationsCubit, StationsState>(
      'emits [loading, loaded] when loadStations succeeds',
      build: () {
        when(() => mockLocationRepository.getCurrentLocation())
            .thenAnswer((_) async => const LatLng(48.8566, 2.3522));
        when(() => mockGetNearbyStations(any(), any()))
            .thenAnswer((_) async => [mockStation]);
        return cubit;
      },
      act: (cubit) => cubit.loadStations(),
      expect: () => [
        const StationsLoading(),
        isA<StationsLoaded>(),
      ],
    );
  });
}
```

---

## 11. Performance

### 11.1 Objectifs

| Métrique | Objectif |
|----------|----------|
| Cold start | < 2s |
| Chargement carte | < 2s |
| Taille app | < 30MB |
| Cache refresh | < 3s |

### 11.2 Optimisations

- [x] Clustering markers (flutter_map_marker_cluster)
- [x] Cache SQLite pour offline
- [x] Lazy loading stations par zone visible
- [x] Compression JSON response (gzip)

---

## 12. Checklist Technique

### Pré-développement
- [ ] Repo Git créé
- [ ] Projet Flutter initialisé
- [ ] Mixpanel project créé
- [ ] Sentry project créé
- [ ] Codemagic configuré

### Développement
- [ ] Architecture Clean mise en place
- [ ] Container pattern implémenté
- [ ] API data.gouv.fr intégrée
- [ ] Cache Drift fonctionnel
- [ ] flutter_map avec markers
- [ ] Onboarding 4 étapes
- [ ] Filtres carburant + fraîcheur
- [ ] Navigation externe (map_launcher)
- [ ] Analytics intégrées
- [ ] Error handling Sentry

### Tests
- [ ] Unit tests use cases
- [ ] Unit tests repositories
- [ ] Widget tests composants clés
- [ ] Integration test flow principal

### Pré-lancement
- [ ] Env prod configuré
- [ ] Secrets dans Codemagic
- [ ] Privacy policy URL
- [ ] App Store screenshots
- [ ] Play Store listing

---

**Document validé le** : 29/11/2025
**Version** : 1.0
