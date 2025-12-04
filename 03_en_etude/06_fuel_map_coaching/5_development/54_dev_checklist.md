# Checklist Développeur - Plein Malin (FuelMap)

Todo list des actions manuelles pour le lancement.

> Cocher avec `- [x]` les éléments terminés.

---

## Phase 1 : Pages Légales (Notion)

- [ ] Créer page Notion "Politique de confidentialité"
- [ ] Créer page Notion "Conditions d'utilisation"
- [ ] Créer page Notion "Page Support"
- [ ] Publier les pages en public → récupérer les URLs

---

## Phase 2 : Apple Developer

### 2.1 Certificates & Identifiers
- [x] Se connecter sur [developer.apple.com](https://developer.apple.com)
- [x] Créer l'App ID : `com.music.fuelmap`
- [x] Activer capability In-App Purchase

### 2.2 App Store Connect - Créer l'app
- [x] Se connecter sur [appstoreconnect.apple.com](https://appstoreconnect.apple.com)
- [x] Créer l'app "Plein Malin"
- [x] Bundle ID : `com.music.fuelmap`

### 2.3 App Store Connect - In-App Purchase Key (pour RevenueCat)
- [x] Aller sur [App Store Connect > Keys > In-App Purchase](https://appstoreconnect.apple.com/access/integrations/api/subs)
- [x] Générer une nouvelle clé
- [x] Télécharger le fichier `.p8`
- [x] Noter le Key ID et l'Issuer ID

---

## Phase 3 : Google Play Console

### 3.1 Créer l'application
- [ ] Se connecter sur [play.google.com/console](https://play.google.com/console)
- [ ] Créer l'application "Plein Malin"
- [ ] Package name : `com.music.fuelmap`

### 3.2 Configurer la signature
- [ ] Générer la keystore
- [ ] Créer `android/key.properties`
- [ ] Activer Play App Signing

### 3.3 Service Account (pour RevenueCat)
- [ ] Google Cloud Console > Service Accounts
- [ ] Créer compte de service
- [ ] Télécharger fichier JSON
- [ ] Play Console > API Access > Lier

---

## Phase 4 : Firebase Console

- [x] Créer le projet Firebase "plein-malin"
- [x] Ajouter l'app iOS
- [x] Télécharger `GoogleService-Info.plist`
- [ ] Ajouter l'app Android
- [ ] Télécharger `google-services.json`
- [x] Activer Analytics
- [x] Activer Crashlytics
- [x] Activer Remote Config

### Copier les fichiers
- [x] `GoogleService-Info.plist` → `ios/Runner/`
- [ ] `google-services.json` → `android/app/`

---

## Phase 5 : RevenueCat

### 5.1 Projet
- [x] Créer projet sur [app.revenuecat.com](https://app.revenuecat.com)
- [x] Récupérer clé API : `appl_NIDqiyhmAAOtxsXpHLmnRtIlbWO`

### 5.2 Configurer iOS
- [x] Ajouter app iOS avec bundle ID
- [x] Uploader fichier `.p8`
- [x] Renseigner Key ID et Issuer ID

### 5.3 Configurer Android
- [ ] Ajouter app Android
- [ ] Uploader fichier JSON service account

### 5.4 Créer les produits

**App Store Connect :**
- [x] Créer abonnement `pleinmalin_pro_yearly` (9.99€/an)
- [ ] Créer abonnement `pleinmalin_pro_monthly` (1.99€/mois) - optionnel
- [x] Créer groupe d'abonnements "Plein Malin Pro"

**Google Play Console :**
- [ ] Créer `pleinmalin_pro_yearly`
- [ ] Créer `pleinmalin_pro_monthly` - optionnel

### 5.5 Configurer RevenueCat
- [x] Products > Ajouter les Product IDs
- [x] Entitlements > Créer "Plein Malin Pro"
- [x] Offerings > Créer "default"
- [x] Packages > Ajouter yearly (+ monthly)

---

## Phase 6 : Projet Flutter

- [x] Projet créé
- [x] iOS configuré (bundle ID, signing)
- [ ] Android configuré (applicationId, keystore)
- [x] Dépendances installées
- [x] Firebase configuré

---

## Phase 7 : CI/CD (Codemagic)

- [ ] Connecter repo Git
- [ ] Workflow iOS
- [ ] Workflow Android
- [ ] Variables d'environnement
- [ ] Déploiement TestFlight

---

## Phase 8 : ASO & Screenshots

> Générer d'abord `61_aso_checklist.md`

### App Store
- [ ] Screenshots iPhone 6.7"
- [ ] Screenshots iPhone 6.5"
- [ ] Screenshots iPhone 5.5"
- [ ] Icône 1024x1024
- [ ] Description
- [ ] Keywords
- [ ] Texte promotionnel
- [ ] Catégorie : Navigation ou Utilitaires
- [ ] URL politique de confidentialité
- [ ] URL support

### Google Play
- [ ] Screenshots phone
- [ ] Feature graphic 1024x500
- [ ] Icône 512x512
- [ ] Description courte/longue
- [ ] URL politique de confidentialité

---

## Phase 9 : Soumission

### iOS
- [ ] Archive
- [ ] Upload App Store Connect
- [ ] Infos review
- [ ] Soumettre

### Android
- [ ] Build AAB
- [ ] Upload Play Console
- [ ] Questionnaire contenu
- [ ] Soumettre

---

## Résumé

```
1. 📄 Notion      → Pages légales         [ ]
2. 🍎 Apple      → ✅ App + IAP Key       [x]
3. 🤖 Google     → App + Service Account  [ ]
4. 🔥 Firebase   → iOS ✅ / Android [ ]
5. 💰 RevenueCat → iOS ✅ / Android [ ]
6. 📱 Flutter    → iOS ✅ / Android [ ]
7. 🔄 Codemagic  → CI/CD                  [ ]
8. 🎨 ASO        → Screenshots            [ ]
9. 🚀 Submit     → Stores                 [ ]
```
