# Prompt de Création d'App Flutter

Copier ce prompt pour démarrer un nouveau projet avec Claude.

---

## Prompt à utiliser

```
Tu vas m'aider à créer une app Flutter.

## Documents de référence
- Cahier des charges : [coller le contenu ou le chemin]
- Tronc commun technique : 50_flutter_base.md

## Stack technique
- Flutter + Dart
- State management : flutter_bloc (Cubit)
- Architecture : Clean Architecture (data/domain/presentation)
- DI : Container Pattern (AppContainer)
- HTTP : Dio
- Storage : SharedPreferences
- Analytics : Firebase Analytics + Crashlytics
- IAP : RevenueCat (si applicable)

## Structure attendue
```
lib/
├── main.dart
├── app/
│   ├── app.dart
│   ├── app_container.dart
│   ├── routes.dart
│   └── theme.dart
├── core/
│   ├── constants/
│   ├── services/
│   └── utils/
├── features/
│   └── [feature]/
│       ├── data/
│       ├── domain/
│       └── presentation/
```

## Conventions
- Imports : toujours `package:` (pas de relatifs)
- Un cubit = une responsabilité
- Repository pattern : interface dans domain/, impl dans data/
- Extraire les widgets > 50 lignes

## Ce que j'attends
1. Commence par créer la structure de base (app_container, main.dart, routes)
2. Implémente feature par feature selon le backlog
3. Garde le code simple, pas d'over-engineering
4. Utilise les patterns du tronc commun

## Informations projet
- Nom app : [NOM]
- Bundle ID : com.company.[nom]
- Features principales : [LISTE]

Commence par me proposer la structure du projet et le app_container.dart.
```

---

## Variante courte

```
Crée une app Flutter "[NOM]" avec :
- Clean Architecture + Cubit
- Container Pattern pour la DI
- Firebase (Analytics + Crashlytics)
- RevenueCat si IAP

Features : [LISTE DES FEATURES]

Réfère-toi au cahier des charges : [LIEN/CONTENU]

Commence par app_container.dart et main.dart.
```

---

## Tips d'utilisation

1. **Toujours fournir le cahier des charges** - Claude a besoin du contexte métier

2. **Itérer feature par feature** - Ne pas demander toute l'app d'un coup

3. **Valider la structure avant le code** - Demander d'abord le plan

4. **Fournir des exemples de code existant** - Si tu as du code similaire, montre-le

5. **Préciser les contraintes** - API externe ? Offline ? Multi-langue ?
