# Checklist Développeur - Actions Manuelles

Todo list des actions à faire sur les différentes plateformes, dans l'ordre.

> Utiliser `- [x]` pour cocher les éléments terminés.

---

## Ressources & Credentials

> Centraliser ici tous les liens et identifiants du projet.

### Identifiants App
| Élément | Valeur |
|---------|--------|
| **Nom app** | [NOM] |
| **Bundle ID (iOS)** | `com.company.appname` |
| **Package name (Android)** | `com.company.appname` |

### Pages Légales
| Page | URL |
|------|-----|
| Politique de confidentialité | [À REMPLIR] |
| Conditions d'utilisation | [À REMPLIR] |
| Page Support | [À REMPLIR] |

### Firebase
| Élément | Valeur |
|---------|--------|
| Projet ID | [À REMPLIR] |
| Console | [Lien Firebase Console] |

### RevenueCat
| Élément | Valeur |
|---------|--------|
| Clé API publique | [À REMPLIR] |
| Entitlement ID | [À REMPLIR] |
| Product ID yearly | [À REMPLIR] |
| Product ID monthly | [À REMPLIR] |

### Apple
| Élément | Valeur |
|---------|--------|
| IAP Key ID | [À REMPLIR] |
| Issuer ID | [À REMPLIR] |
| Fichier .p8 | [Emplacement local] |

### Google
| Élément | Valeur |
|---------|--------|
| Service Account JSON | [Emplacement local] |
| Keystore | [Emplacement local] |

---

## Phase 1 : Pages Légales

- [ ] Créer page Notion "Politique de confidentialité"
- [ ] Créer page Notion "Conditions d'utilisation"
- [ ] Créer page Notion "Page Support"
- [ ] Publier les pages en public → récupérer les URLs

---

## Phase 2 : Apple Developer

### 2.1 Certificates & Identifiers
- [ ] Se connecter sur [developer.apple.com](https://developer.apple.com)
- [ ] Créer l'App ID : Identifiers > App IDs > `com.company.appname`
- [ ] Activer capabilities : In-App Purchase, Push Notifications (si besoin)

### 2.2 App Store Connect - Créer l'app
- [ ] Se connecter sur [appstoreconnect.apple.com](https://appstoreconnect.apple.com)
- [ ] Apps > "+" > Nouvelle app
- [ ] Renseigner : nom, bundle ID, SKU, langue

### 2.3 App Store Connect - In-App Purchase Key (pour RevenueCat)
- [ ] Aller sur [App Store Connect > Keys > In-App Purchase](https://appstoreconnect.apple.com/access/integrations/api/subs)
- [ ] Générer une nouvelle clé
- [ ] Télécharger le fichier `.p8`
- [ ] Noter le Key ID et l'Issuer ID
- [ ] ⚠️ Garder ces infos pour RevenueCat

---

## Phase 3 : Google Play Console

### 3.1 Créer l'application
- [ ] Se connecter sur [play.google.com/console](https://play.google.com/console)
- [ ] Créer l'application
- [ ] Définir le package name : `com.company.appname`

### 3.2 Configurer la signature
- [ ] Générer la keystore : `keytool -genkey -v -keystore upload.jks -keyalg RSA -keysize 2048 -validity 10000 -alias upload`
- [ ] Créer `android/key.properties` avec les credentials
- [ ] Activer Play App Signing dans la console

### 3.3 Service Account (pour RevenueCat)
- [ ] Google Cloud Console > IAM > Service Accounts
- [ ] Créer un compte de service
- [ ] Télécharger le fichier JSON
- [ ] Play Console > API Access > Lier le service account
- [ ] ⚠️ Garder le JSON pour RevenueCat

---

## Phase 4 : Firebase Console

- [ ] Se connecter sur [console.firebase.google.com](https://console.firebase.google.com)
- [ ] Créer le projet Firebase
- [ ] Ajouter l'app iOS (avec bundle ID exact)
- [ ] Télécharger `GoogleService-Info.plist`
- [ ] Ajouter l'app Android (avec package name exact)
- [ ] Télécharger `google-services.json`
- [ ] Activer Analytics
- [ ] Activer Crashlytics
- [ ] (Optionnel) Activer Remote Config

### Copier les fichiers dans le projet Flutter
- [ ] `GoogleService-Info.plist` → `ios/Runner/GoogleService-Info.plist`
- [ ] `google-services.json` → `android/app/google-services.json`

---

## Phase 5 : RevenueCat

### 5.1 Créer le projet
- [ ] Se connecter sur [app.revenuecat.com](https://app.revenuecat.com)
- [ ] Créer un nouveau projet
- [ ] Récupérer la clé API publique (pour le code Flutter)

### 5.2 Configurer iOS
- [ ] Apps > Add App > iOS
- [ ] Renseigner le bundle ID
- [ ] Uploader le fichier `.p8` (In-App Purchase Key)
- [ ] Renseigner Key ID et Issuer ID

### 5.3 Configurer Android
- [ ] Apps > Add App > Android
- [ ] Renseigner le package name
- [ ] Uploader le fichier JSON du service account

### 5.4 Créer les produits sur les stores

**App Store Connect :**
- [ ] App > Fonctionnalités > Achats intégrés
- [ ] Créer l'abonnement (ex: `pro_monthly`, `pro_yearly`)
- [ ] Renseigner : prix, durée, description
- [ ] Créer le groupe d'abonnements
- [ ] Soumettre pour review

**Google Play Console :**
- [ ] Monétisation > Produits > Abonnements
- [ ] Créer avec le même Product ID que iOS
- [ ] Renseigner prix et durée

### 5.5 Configurer RevenueCat
- [ ] Products > Ajouter les Product IDs des stores
- [ ] Entitlements > Créer (ex: "premium")
- [ ] Offerings > Créer "default"
- [ ] Packages > Ajouter monthly/yearly dans l'offering

---

## Phase 6 : Projet Flutter

### 6.1 Créer le projet
```bash
flutter create --org com.company appname
cd appname
```

### 6.2 Configurer iOS
- [ ] Ouvrir `ios/Runner.xcworkspace` dans Xcode
- [ ] Signing & Capabilities > Team + Bundle ID
- [ ] Deployment Target > iOS 14.0
- [ ] Vérifier que `GoogleService-Info.plist` est dans le projet Xcode

### 6.3 Configurer Android
- [ ] `android/app/build.gradle` > `applicationId`
- [ ] `android/app/build.gradle` > `minSdkVersion 24`
- [ ] Vérifier `google-services.json` présent
- [ ] Créer `android/key.properties`

### 6.4 Dépendances
```bash
flutter pub add flutter_bloc go_router dio shared_preferences
flutter pub add firebase_core firebase_analytics firebase_crashlytics
flutter pub add purchases_flutter purchases_ui_flutter
flutter pub add package_info_plus url_launcher
```

### 6.5 Initialiser Firebase CLI
```bash
dart pub global activate flutterfire_cli
flutterfire configure
```

---

## Phase 7 : CI/CD (Codemagic)

- [ ] Connecter le repo Git
- [ ] Créer workflow iOS
- [ ] Créer workflow Android
- [ ] Ajouter variables d'environnement (keystore base64, passwords)
- [ ] Configurer déploiement TestFlight / Internal Testing

---

## Phase 8 : ASO & Screenshots

> Générer d'abord le fichier ASO (`61_aso_checklist.md`) avant cette phase.

### App Store
- [ ] Screenshots iPhone 6.7" (1290x2796)
- [ ] Screenshots iPhone 6.5" (1284x2778)
- [ ] Screenshots iPhone 5.5" (1242x2208)
- [ ] (Si iPad) Screenshots iPad Pro 12.9"
- [ ] Icône 1024x1024 (sans transparence)
- [ ] Description (4000 chars max)
- [ ] Keywords (100 chars max)
- [ ] Texte promotionnel (170 chars)
- [ ] Catégorie principale + secondaire
- [ ] URL politique de confidentialité
- [ ] URL support

### Google Play
- [ ] Screenshots phone (min 2, max 8)
- [ ] Feature graphic 1024x500
- [ ] Icône 512x512
- [ ] Description courte (80 chars)
- [ ] Description longue (4000 chars)
- [ ] Catégorie
- [ ] Tags
- [ ] URL politique de confidentialité
- [ ] Email contact

---

## Phase 9 : Soumission

### iOS
- [ ] Archive via Xcode ou Codemagic
- [ ] Uploader sur App Store Connect
- [ ] Remplir les infos de review (compte test si besoin)
- [ ] Soumettre pour review

### Android
- [ ] Build AAB via Codemagic
- [ ] Uploader sur Play Console (Internal → Closed → Open → Production)
- [ ] Remplir le questionnaire contenu
- [ ] Soumettre pour review

---

## Résumé Visuel

```
1. 📄 Notion      → Pages légales (confidentialité, CGU, support)
2. 🍎 Apple      → App ID + App Store Connect + IAP Key
3. 🤖 Google     → App + Keystore + Service Account
4. 🔥 Firebase   → Projet + config files → copier dans Flutter
5. 💰 RevenueCat → Lier stores + créer produits + offerings
6. 📱 Flutter    → Projet + config + dépendances
7. 🔄 Codemagic  → CI/CD
8. 🎨 ASO        → Screenshots + descriptions (après avoir généré 61_aso)
9. 🚀 Submit     → TestFlight / Internal Testing → Production
```
