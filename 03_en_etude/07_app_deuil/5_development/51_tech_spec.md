# [NOM APP] - Spécifications Techniques

## Informations Générales

| Élément | Valeur |
|---------|--------|
| **Nom de l'app** | [Nom] |
| **Version** | 1.0.0 |
| **Date création** | [JJ/MM/AAAA] |
| **Dernière MAJ** | [JJ/MM/AAAA] |

---

## 1. Stack Technique

### 1.1 Vue d'ensemble

```
                      FRONTEND                            
                    [Flutter/RN]                          
                        |                                
                     REST/GraphQL
                        v
                      BACKEND                             
                    [Supabase/Firebase]                   
             |             |             |               
    Auth        Database     Storage      Functions   
                         
                        v
                   SERVICES TIERS                         
   [RevenueCat] [Analytics] [Push] [APIs externes]       
```

### 1.2 Choix Technologiques

| Couche | Technologie | Justification |
|--------|-------------|---------------|
| **Frontend** | Flutter 3.x | Cross-platform, performance native |
| **Backend** | Supabase | BaaS complet, PostgreSQL, temps réel |
| **Auth** | Supabase Auth | Email, OAuth (Apple, Google) |
| **Database** | PostgreSQL (Supabase) | Relationnel, RLS |
| **Storage** | Supabase Storage | Fichiers, images |
| **Paiements** | RevenueCat | IAP iOS/Android simplifié |
| **Analytics** | Mixpanel / PostHog | Events tracking, funnels |
| **Push** | Firebase Cloud Messaging | iOS + Android |
| **Crash reporting** | Sentry | Monitoring erreurs |

### 1.3 Versions Minimales

| Plateforme | Version min | Raison |
|------------|-------------|--------|
| iOS | 14.0 | SwiftUI, App Clips support |
| Android | API 24 (7.0) | 95%+ market coverage |
| Flutter | 3.16+ | Dernières features stables |

---

## 2. Architecture Application

### 2.1 Structure Projet (Flutter)

```
lib/
   main.dart
   app/
      app.dart
      routes.dart
      theme.dart
   core/
      constants/
      errors/
      network/
      utils/
   data/
      datasources/
      models/
      repositories/
   domain/
      entities/
      repositories/
      usecases/
   presentation/
      blocs/ (ou providers/)
      pages/
      widgets/
   services/
       analytics_service.dart
       auth_service.dart
       push_service.dart
       revenue_service.dart
```

### 2.2 State Management

**Solution choisie** : [Riverpod / Bloc / Provider]

**Justification** : [Raison du choix]

### 2.3 Navigation

**Solution** : [GoRouter / Auto Route / Navigator 2.0]

```dart
// Routes principales
/                     -> Splash
/auth                 -> Auth flow
/auth/login           -> Login
/auth/register        -> Register
/onboarding           -> Onboarding
/home                 -> Home (Tab 1)
/settings             -> Settings
/paywall              -> Paywall modal
```

---

## 3. Base de Données

### 3.1 Schéma Entités

```
   users              [entity1]           [entity2]  
                                                    
 id (PK)            id (PK)             id (PK)     
 email              user_id(FK)         entity1_id  
 name             -> [field]             [field]     
 avatar_url          created_at          created_at  
 is_premium                                          
 created_at  
```

### 3.2 Tables Détaillées

#### Table `users`
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  email VARCHAR(255) UNIQUE NOT NULL,
  name VARCHAR(100),
  avatar_url TEXT,
  is_premium BOOLEAN DEFAULT FALSE,
  premium_expires_at TIMESTAMP,
  onboarding_completed BOOLEAN DEFAULT FALSE,
  settings JSONB DEFAULT '{}',
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- RLS
ALTER TABLE users ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Users can view own data" ON users
  FOR SELECT USING (auth.uid() = id);
CREATE POLICY "Users can update own data" ON users
  FOR UPDATE USING (auth.uid() = id);
```

---

## 4. APIs & Intégrations

### 4.1 API Backend (Supabase)

**Base URL** : `https://[project].supabase.co`

| Endpoint | Méthode | Description | Auth |
|----------|---------|-------------|------|
| `/auth/v1/signup` | POST | Inscription | - |
| `/auth/v1/token` | POST | Login | - |
| `/rest/v1/users` | GET/PATCH | Profil user | Bearer |
| `/rest/v1/[entity]` | CRUD | [Description] | Bearer |

### 4.2 Services Tiers

#### RevenueCat
- **Usage** : Gestion IAP, abonnements
- **SDK** : `purchases_flutter`
- **Entitlements** : `premium`

#### Analytics (Mixpanel/PostHog)
- **Events clés** :
  | Event | Properties | Trigger |
  |-------|------------|---------|
  | `app_opened` | `source` | App launch |
  | `signup_completed` | `method` | Post signup |
  | `paywall_viewed` | `trigger` | Paywall affiché |
  | `purchase_completed` | `product_id`, `price` | Achat réussi |

---

## 5. Sécurité

### 5.1 Authentification

- **Méthode** : JWT via Supabase Auth
- **Refresh token** : Rotation automatique
- **Session** : 7 jours, refresh 30 jours
- **Stockage token** : FlutterSecureStorage

### 5.2 Autorisation (RLS)

Toutes les tables ont Row Level Security activé :
- Users ne voient que leurs propres données
- Premium features vérifiées côté serveur

### 5.3 Conformité

- [ ] RGPD : Suppression compte, export données
- [ ] COPPA : [Si applicable - vérification âge]
- [ ] App Tracking Transparency (iOS)

---

## 6. Performance

### 6.1 Objectifs

| Métrique | Objectif |
|----------|----------|
| Cold start | < 2s |
| Hot start | < 500ms |
| Time to Interactive | < 3s |
| API response | < 200ms (p95) |
| App size | < 50MB |

### 6.2 Optimisations

- [ ] Lazy loading des images
- [ ] Pagination des listes
- [ ] Cache HTTP
- [ ] Compression assets (WebP, Lottie)

---

## 7. CI/CD

### 7.1 Environnements

| Env | Usage | Backend | Build |
|-----|-------|---------|-------|
| `dev` | Développement | Supabase dev | Debug |
| `staging` | Tests QA | Supabase staging | Release |
| `prod` | Production | Supabase prod | Release |

### 7.2 Pipeline

```yaml
# .github/workflows/ci.yml
name: CI/CD

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: subosito/flutter-action@v2
      - run: flutter pub get
      - run: flutter analyze
      - run: flutter test
```

---

## 8. Coûts Infrastructure

### 8.1 Estimation Mensuelle

| Service | Plan | Coût/mois | Limite |
|---------|------|-----------|--------|
| Supabase | Free/Pro | $0-25 | 500MB DB, 1GB storage |
| RevenueCat | Free | $0 | <$2.5K MTR |
| Firebase (FCM) | Free | $0 | Illimité push |
| Sentry | Free | $0 | 5K events/mois |
| Apple Developer | - | $8 | $99/an |
| Google Play | - | $2 | $25 one-time |
| **Total** | | **~$10-35/mois** | |

---

## 9. Checklist Technique

### Pré-développement
- [ ] Repo Git créé
- [ ] Projet Flutter initialisé
- [ ] Supabase project créé (dev)
- [ ] RevenueCat configuré
- [ ] Firebase project créé
- [ ] Sentry project créé

### Développement
- [ ] Architecture mise en place
- [ ] Auth flow fonctionnel
- [ ] Database schema déployé
- [ ] RLS configuré
- [ ] Analytics intégrées
- [ ] IAP testés (sandbox)

### Pré-lancement
- [ ] Env prod configuré
- [ ] Secrets sécurisés (pas en dur)
- [ ] Tests passants
- [ ] Crash reporting actif
- [ ] Privacy policy URL

---

**Document validé le** : [Date]
**Version** : 1.0
