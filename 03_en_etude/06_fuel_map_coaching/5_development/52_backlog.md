# FuelMap - Backlog

## Sprint Overview

| Sprint | Objectif | Durée | Status |
|--------|----------|-------|--------|
| Sprint 0 | Setup projet | 2 jours | [ ] |
| Sprint 1 | Core (Carte + Stations) | 4 jours | [ ] |
| Sprint 2 | Onboarding + Filtres + Recherche Trajet | 3 jours | [ ] |
| Sprint 3 | Polish + Release | 2 jours | [ ] |

**Total estimé** : 11 jours

---

## Sprint 0 : Setup (2 jours)

### Objectif
Mettre en place l'infrastructure technique et l'architecture du projet.

### Stories

| ID | Story | Points | Status |
|----|-------|--------|--------|
| S0-1 | Créer le repo Git + structure projet Flutter | 1 | [ ] |
| S0-2 | Setup architecture Clean + Container pattern | 2 | [ ] |
| S0-3 | Configurer Codemagic (CI/CD) | 2 | [ ] |
| S0-4 | Setup Sentry (error tracking) | 1 | [ ] |
| S0-5 | Setup Mixpanel (analytics) | 1 | [ ] |
| S0-6 | Configurer environments (dev/prod) avec Envied | 1 | [ ] |

**Total** : 8 points

### Tâches détaillées

#### S0-1 : Créer le repo Git + structure projet Flutter
```
- [ ] flutter create fuelmap
- [ ] Initialiser Git + .gitignore
- [ ] Créer structure dossiers (features/, core/, services/, app/)
- [ ] Ajouter pubspec.yaml avec toutes les dépendances
- [ ] Configurer analysis_options.yaml
```

#### S0-2 : Setup architecture Clean + Container pattern
```
- [ ] Créer AppContainer avec init()
- [ ] Créer DioClient dans core/network/
- [ ] Créer classes de base (Failure, etc.)
- [ ] Setup GoRouter avec routes de base
- [ ] Setup MultiBlocProvider dans main.dart
```

#### S0-3 : Configurer Codemagic
```
- [ ] Créer codemagic.yaml
- [ ] Configurer workflow iOS (signing, build, TestFlight)
- [ ] Configurer workflow Android (keystore, build, Play Store)
- [ ] Ajouter secrets (SENTRY_DSN, MIXPANEL_TOKEN, etc.)
- [ ] Tester build dev
```

#### S0-4 : Setup Sentry
```
- [ ] Créer projet Sentry
- [ ] Ajouter sentry_flutter au projet
- [ ] Configurer dans main.dart avec DSN
- [ ] Tester capture d'erreur
```

#### S0-5 : Setup Mixpanel
```
- [ ] Créer projet Mixpanel
- [ ] Ajouter mixpanel_flutter
- [ ] Créer AnalyticsService
- [ ] Implémenter trackEvent() et setUserProperties()
- [ ] Tester event app_opened
```

#### S0-6 : Configurer environments
```
- [ ] Créer .env.dev et .env.prod
- [ ] Setup Envied avec env.dart
- [ ] Créer main_dev.dart et main_prod.dart
- [ ] Configurer AppConfig.fromEnv()
```

---

## Sprint 1 : Core - Carte + Stations (4 jours)

### Objectif
Afficher la carte avec les stations et leurs prix depuis data.gouv.fr.

### Stories

| ID | Story | Feature | Points | Status |
|----|-------|---------|--------|--------|
| S1-1 | Intégrer API data.gouv.fr | M1 | 3 | [ ] |
| S1-2 | Implémenter cache Drift (SQLite) | M1 | 3 | [ ] |
| S1-3 | Afficher la carte avec flutter_map | M1 | 2 | [ ] |
| S1-4 | Créer les markers stations avec prix | M1 | 3 | [ ] |
| S1-5 | Gérer la localisation utilisateur | M1 | 2 | [ ] |
| S1-6 | Créer Station Bottom Sheet | M3 | 3 | [ ] |
| S1-7 | Implémenter navigation externe | M4 | 2 | [ ] |

**Total** : 18 points

### Tâches détaillées

#### S1-1 : Intégrer API data.gouv.fr
```
Feature: stations
Fichiers:
- [ ] features/stations/data/datasources/stations_remote_datasource.dart
- [ ] features/stations/data/models/station_model.dart
- [ ] features/stations/data/models/fuel_price_model.dart

Critères d'acceptation:
- [ ] Appel GET /records avec filtre géographique within_distance()
- [ ] Parsing JSON → StationModel
- [ ] Mapping carburants (Gazole→diesel, SP95→sp95, etc.)
- [ ] Gestion erreurs réseau (timeout, 404, 500)
- [ ] Tests unitaires datasource
```

#### S1-2 : Implémenter cache Drift (SQLite)
```
Feature: stations
Fichiers:
- [ ] core/database/app_database.dart
- [ ] core/database/tables/stations_table.dart
- [ ] core/database/tables/prices_table.dart
- [ ] features/stations/data/datasources/stations_local_datasource.dart

Critères d'acceptation:
- [ ] Tables Stations et Prices créées
- [ ] Insert/Update stations en batch
- [ ] Query stations par rayon (lat/lng + distance)
- [ ] Gestion cachedAt pour invalidation (1h)
- [ ] Tests unitaires local datasource
```

#### S1-3 : Afficher la carte avec flutter_map
```
Feature: stations
Fichiers:
- [ ] features/stations/presentation/pages/map_page.dart
- [ ] features/stations/presentation/widgets/fuel_map.dart

Critères d'acceptation:
- [ ] FlutterMap avec TileLayer OpenStreetMap
- [ ] Zoom initial adapté (rayon 10km visible)
- [ ] Gestes: pan, pinch zoom
- [ ] FAB recentrer sur position user
- [ ] Loading state avec skeleton
```

#### S1-4 : Créer les markers stations avec prix
```
Feature: stations
Fichiers:
- [ ] features/stations/presentation/widgets/station_marker.dart
- [ ] features/stations/presentation/cubits/stations_cubit.dart
- [ ] features/stations/presentation/cubits/stations_state.dart

Critères d'acceptation:
- [ ] Marker affiche prix/L + estimation plein
- [ ] Couleur prix (vert/orange/rouge vs moyenne)
- [ ] Badge fraîcheur (vert <24h, orange 1-3j, gris >3j)
- [ ] Clustering si trop de markers (flutter_map_marker_cluster)
- [ ] Tap marker → ouvre bottom sheet
- [ ] StationsCubit: loadStations(), états Loading/Loaded/Error
```

#### S1-5 : Gérer la localisation utilisateur
```
Feature: location
Fichiers:
- [ ] features/location/data/location_repository_impl.dart
- [ ] features/location/domain/repositories/location_repository.dart
- [ ] features/location/presentation/cubits/location_cubit.dart
- [ ] features/location/location_container.dart

Critères d'acceptation:
- [ ] Demande permission GPS (permission_handler)
- [ ] Récupère position actuelle (geolocator)
- [ ] Marker position user sur carte
- [ ] Gestion refus permission (message + bouton settings)
- [ ] LocationCubit: getLocation(), états
```

#### S1-6 : Créer Station Bottom Sheet
```
Feature: stations
Fichiers:
- [ ] features/stations/presentation/widgets/station_bottom_sheet.dart
- [ ] features/stations/presentation/widgets/price_row.dart
- [ ] features/stations/presentation/widgets/services_list.dart

Critères d'acceptation:
- [ ] Header: nom, adresse, distance
- [ ] Liste prix: tous carburants, prix/L, estimation plein, fraîcheur
- [ ] Horaires: statut ouvert/fermé, détails
- [ ] Services: icons (lavage, boutique, DAB, etc.)
- [ ] Bouton "Y aller" en bas
- [ ] Swipe down pour fermer
- [ ] Analytics: station_viewed
```

#### S1-7 : Implémenter navigation externe
```
Feature: stations
Fichiers:
- [ ] features/stations/presentation/widgets/navigation_picker.dart
- [ ] features/preferences/data/preferences_repository_impl.dart

Critères d'acceptation:
- [ ] Utilise map_launcher pour ouvrir Apple Maps / Google Maps
- [ ] Si plusieurs apps: dialog de choix
- [ ] Option "Se souvenir de mon choix"
- [ ] Sauvegarde préférence dans SharedPreferences
- [ ] Analytics: navigation_launched
```

---

## Sprint 2 : Onboarding + Filtres + Recherche Trajet (3 jours)

### Objectif
Implémenter l'onboarding, les filtres avancés et la recherche de trajet.

### Stories

| ID | Story | Feature | Points | Status |
|----|-------|---------|--------|--------|
| S2-1 | Créer Splash Screen avec redirection | Onboarding | 1 | [ ] |
| S2-2 | Implémenter Onboarding (4 étapes) | Onboarding | 3 | [ ] |
| S2-3 | Créer Filters Bottom Sheet (carburant + distance + prix + fraîcheur) | M2 | 3 | [ ] |
| S2-4 | Créer Settings Bottom Sheet | Settings | 2 | [ ] |
| S2-5 | Connecter filtres à la carte | M2 | 2 | [ ] |
| S2-6 | Implémenter Route Search Bottom Sheet | M5 | 3 | [ ] |
| S2-7 | Afficher route + stations sur trajet | M5 | 5 | [ ] |
| S2-8 | Ajouter infos détour dans Station Bottom Sheet | M5 | 2 | [ ] |

**Total** : 21 points

### Tâches détaillées

#### S2-1 : Créer Splash Screen avec redirection
```
Feature: onboarding
Fichiers:
- [ ] features/onboarding/presentation/pages/splash_page.dart

Critères d'acceptation:
- [ ] Logo centré + loader
- [ ] Initialise AppContainer
- [ ] Vérifie onboardingCompleted dans SharedPreferences
- [ ] Redirige vers /onboarding ou /map
- [ ] Durée max 2s
```

#### S2-2 : Implémenter Onboarding (4 étapes)
```
Feature: onboarding
Fichiers:
- [ ] features/onboarding/presentation/pages/onboarding_page.dart
- [ ] features/onboarding/presentation/widgets/welcome_step.dart
- [ ] features/onboarding/presentation/widgets/vehicle_type_step.dart
- [ ] features/onboarding/presentation/widgets/fuel_type_step.dart
- [ ] features/onboarding/presentation/widgets/location_permission_step.dart
- [ ] features/onboarding/presentation/cubits/onboarding_cubit.dart

Critères d'acceptation:
- [ ] PageView avec 4 étapes
- [ ] Indicateur de progression (dots)
- [ ] Step 1: Bienvenue + bouton Commencer
- [ ] Step 2: Sélection type véhicule (citadine/berline/SUV/utilitaire)
- [ ] Step 3: Sélection carburant (6 types)
- [ ] Step 4: Permission GPS
- [ ] Bouton "Passer" pour skip
- [ ] Sauvegarde dans SharedPreferences à chaque étape
- [ ] Analytics: onboarding_started, onboarding_completed, onboarding_skipped
```

#### S2-3 : Créer Filters Bottom Sheet
```
Feature: stations
Fichiers:
- [ ] features/stations/presentation/widgets/filters_bottom_sheet.dart
- [ ] features/stations/presentation/cubits/filters_cubit.dart
- [ ] features/stations/presentation/cubits/filters_state.dart

Critères d'acceptation:
- [ ] Section carburant: 6 chips (single select)
- [ ] Section fraîcheur: 3 chips (<24h, <3j, Tous)
- [ ] Compteur stations filtré en temps réel
- [ ] Bouton "Appliquer"
- [ ] Filtre carburant sauvegardé en préférence
- [ ] Filtre fraîcheur non sauvegardé
- [ ] Analytics: filter_changed
```

#### S2-4 : Créer Settings Bottom Sheet
```
Feature: preferences
Fichiers:
- [ ] features/preferences/presentation/widgets/settings_bottom_sheet.dart
- [ ] features/preferences/presentation/cubits/preferences_cubit.dart
- [ ] features/preferences/domain/entities/user_preferences.dart

Critères d'acceptation:
- [ ] Dropdown type véhicule
- [ ] Dropdown carburant par défaut
- [ ] Dropdown app navigation
- [ ] Liens: À propos, Politique confidentialité
- [ ] Version app en bas
- [ ] Sauvegarde immédiate au changement
- [ ] Analytics: preferences_updated
```

#### S2-5 : Connecter filtres à la carte
```
Feature: stations
Fichiers:
- [ ] Modifier stations_cubit.dart
- [ ] Modifier map_page.dart

Critères d'acceptation:
- [ ] FiltersCubit écoute changements
- [ ] StationsCubit filtre la liste selon FiltersCubit
- [ ] Markers mis à jour en temps réel
- [ ] Footer affiche filtre actuel + compteur
- [ ] Tap footer → ouvre Filters Bottom Sheet
```

#### S2-6 : Implémenter Route Search Bottom Sheet
```
Feature: route
Fichiers:
- [ ] features/route/presentation/widgets/route_search_bottom_sheet.dart
- [ ] features/route/presentation/cubits/route_cubit.dart
- [ ] features/route/data/datasources/geocoding_datasource.dart

Critères d'acceptation:
- [ ] Champ départ (position actuelle par défaut)
- [ ] Champ arrivée avec autocomplete (Nominatim OSM)
- [ ] Liste des 5 dernières recherches
- [ ] Bouton "Rechercher stations"
- [ ] Analytics: route_search_started, route_search_completed
```

#### S2-7 : Afficher route + stations sur trajet
```
Feature: route
Fichiers:
- [ ] features/route/data/datasources/routing_datasource.dart (OSRM)
- [ ] features/route/presentation/widgets/route_overlay.dart
- [ ] features/route/domain/usecases/get_stations_along_route.dart

Critères d'acceptation:
- [ ] Appel API OSRM pour obtenir la route
- [ ] Polyline bleue sur la carte
- [ ] Header sticky "Paris → Lyon · 465km · 12 stations"
- [ ] Bouton fermer pour quitter le mode trajet
- [ ] Filtrer stations à moins de 5km de la route
- [ ] Zoom auto pour voir tout le trajet
- [ ] Tri: par prix, par distance, par détour
```

#### S2-8 : Ajouter infos détour dans Station Bottom Sheet
```
Feature: route
Fichiers:
- [ ] Modifier station_bottom_sheet.dart

Critères d'acceptation:
- [ ] Section "Sur votre trajet" si mode route actif
- [ ] Afficher distance au trajet ("Sur le trajet" ou "À 500m")
- [ ] Afficher détour en km ("+2 km")
- [ ] Afficher temps détour ("+3 min")
- [ ] Afficher position sur trajet ("À 120 km du départ")
- [ ] Analytics: route_station_viewed
```

---

## Sprint 3 : Polish + Release (2 jours)

### Objectif
Finaliser l'app, corriger les bugs et préparer la release.

### Stories

| ID | Story | Type | Points | Status |
|----|-------|------|--------|--------|
| S3-1 | Ajouter gestion erreurs UI | UX | 2 | [ ] |
| S3-2 | Implémenter mode offline | Tech | 2 | [ ] |
| S3-3 | Ajouter Dark Mode | UX | 1 | [ ] |
| S3-4 | Tests unitaires et widget | Test | 3 | [ ] |
| S3-5 | Optimisation performance | Tech | 1 | [ ] |
| S3-6 | Préparer assets stores | Release | 2 | [ ] |
| S3-7 | Soumettre aux stores | Release | 1 | [ ] |

**Total** : 12 points

### Tâches détaillées

#### S3-1 : Ajouter gestion erreurs UI
```
Fichiers:
- [ ] core/widgets/error_view.dart
- [ ] core/widgets/empty_view.dart

Critères d'acceptation:
- [ ] Écran erreur GPS avec bouton "Paramètres"
- [ ] Écran erreur réseau avec bouton "Réessayer"
- [ ] Écran vide "Aucune station trouvée"
- [ ] Snackbar pour erreurs mineures
```

#### S3-2 : Implémenter mode offline
```
Critères d'acceptation:
- [ ] Cache Drift utilisé si pas de réseau
- [ ] Indicateur "Données en cache" si offline
- [ ] Badge "Dernière MAJ: il y a Xh" si cache expiré
- [ ] Retry automatique quand réseau revient
```

#### S3-3 : Ajouter Dark Mode
```
Fichiers:
- [ ] app/theme.dart (light + dark)

Critères d'acceptation:
- [ ] ThemeData.light() et ThemeData.dark()
- [ ] Suit le mode système
- [ ] Bottom sheets adaptés
- [ ] Markers lisibles en dark
```

#### S3-4 : Tests unitaires et widget
```
Fichiers:
- [ ] test/unit/domain/usecases/get_nearby_stations_test.dart
- [ ] test/unit/data/repositories/stations_repository_test.dart
- [ ] test/widget/station_marker_test.dart
- [ ] test/widget/filters_bottom_sheet_test.dart

Critères d'acceptation:
- [ ] Coverage use cases > 80%
- [ ] Coverage repositories > 80%
- [ ] Widget tests composants critiques
- [ ] CI passe tous les tests
```

#### S3-5 : Optimisation performance
```
Critères d'acceptation:
- [ ] Cold start < 2s
- [ ] Chargement carte < 2s
- [ ] Pas de jank au scroll/zoom
- [ ] Taille APK < 30MB
```

#### S3-6 : Préparer assets stores
```
Fichiers:
- [ ] assets/screenshots/
- [ ] assets/icon/

Critères d'acceptation:
- [ ] App icon (1024x1024)
- [ ] Screenshots iPhone 6.5" (3 min)
- [ ] Screenshots iPhone 5.5" (3 min)
- [ ] Screenshots Android (3 min)
- [ ] Feature graphic Android (1024x500)
- [ ] Description courte (80 chars)
- [ ] Description longue (4000 chars)
- [ ] Keywords ASO
- [ ] Privacy policy URL
```

#### S3-7 : Soumettre aux stores
```
Critères d'acceptation:
- [ ] Build prod signé iOS
- [ ] Build prod signé Android
- [ ] Upload TestFlight
- [ ] Upload Google Play (internal)
- [ ] Remplir fiches stores
- [ ] Soumettre pour review
```

---

## Icebox (Post-MVP)

| ID | Story | Feature | Priorité | Notes |
|----|-------|---------|----------|-------|
| ICE-1 | Signalement prix par utilisateurs | M4 (ancien) | High | Nécessite auth |
| ICE-2 | Historique des pleins | M7 (ancien) | High | Nécessite auth + backend |
| ICE-3 | Calcul économies | M8 (ancien) | High | Dépend de ICE-2 |
| ICE-4 | Authentification (email + social) | Auth | High | Prérequis ICE-1,2,3 |
| ICE-5 | Notifications prix bas | S1 | Medium | Nécessite backend |
| ICE-6 | Badges gamification | S2 | Medium | |
| ICE-7 | Favoris stations | S4 | Medium | |
| ICE-8 | Mode liste | S5 | Low | Alternative à la carte |
| ICE-9 | Premium sans pub | S6 | Low | Pas de pub dans MVP |
| ICE-10 | Widget iOS/Android | C2 | Low | |
| ICE-11 | Apple Watch | C3 | Low | |
| ICE-12 | CarPlay/Android Auto | C4 | Low | |

---

## Definition of Done

### Story
- [ ] Code implémenté et fonctionnel
- [ ] Code reviewé (si équipe)
- [ ] Tests unitaires passent
- [ ] Pas de régression
- [ ] Testé sur iOS (simulateur + device si possible)
- [ ] Testé sur Android (émulateur + device si possible)
- [ ] Analytics events implémentés
- [ ] Pas d'erreurs Sentry

### Sprint
- [ ] Toutes les stories "Done"
- [ ] Build CI passe
- [ ] Demo fonctionnelle
- [ ] Backlog mis à jour

---

## Points de Complexité

| Points | Signification | Exemple |
|--------|---------------|---------|
| 1 | Trivial, < 2h | Config, copier/coller |
| 2 | Simple, 2-4h | Widget simple, CRUD basique |
| 3 | Moyen, 4-8h | Feature complète, intégration API |
| 5 | Complexe, 1-2j | Feature majeure, logique complexe |
| 8 | Très complexe, 2-3j | Architecture, refacto majeur |

---

## Vélocité

| Sprint | Points planifiés | Points réalisés | Notes |
|--------|------------------|-----------------|-------|
| Sprint 0 | 8 | - | |
| Sprint 1 | 18 | - | |
| Sprint 2 | 21 | - | |
| Sprint 3 | 12 | - | |
| **Total** | **59** | - | |

---

## Risques Identifiés

| Risque | Impact | Probabilité | Mitigation |
|--------|--------|-------------|------------|
| API data.gouv.fr indisponible | High | Low | Cache local, retry |
| Format API change | Medium | Low | Versioning, tests |
| Performance carte (trop de markers) | Medium | Medium | Clustering, pagination |
| Rejet App Store (permissions) | Medium | Low | Justification claire GPS |
| Rejet Play Store | Low | Low | Conformité policies |

---

**Dernière mise à jour** : 29/11/2025
**Version** : 1.0
