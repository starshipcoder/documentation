# [NOM APP] - Cahier des Charges Fonctionnel

## Informations Générales

| Élément | Valeur |
|---------|--------|
| **Nom de l'app** | [Nom] |
| **Version** | MVP v1.0 |
| **Plateformes** | iOS / Android |
| **Date création** | [JJ/MM/AAAA] |
| **Dernière MAJ** | [JJ/MM/AAAA] |

---

## 1. Vue d'Ensemble

### 1.1 Objectif de l'Application

[Description en 2-3 phrases de ce que fait l'app et pourquoi]

### 1.2 Proposition de Valeur

> "[UVP en 1 phrase]"

### 1.3 Cibles Utilisateurs

| Segment | Description | Priorité |
|---------|-------------|----------|
| Primaire | [Description] | P0 |
| Secondaire | [Description] | P1 |
| Tertiaire | [Description] | P2 |

---

## 2. Personas & Parcours

### 2.1 Persona Principal

**Nom** : [Prénom fictif]
- **Âge** : [X ans]
- **Situation** : [Contexte personnel/pro]
- **Objectif** : [Ce qu'il veut accomplir]
- **Frustrations** : [Pain points actuels]
- **Tech-savviness** : [Faible/Moyen/Élevé]

### 2.2 User Journey Principal

```
[Trigger]          [Découverte]        [Activation]         [Engagement]        [Rétention]
                                                                                 
    |                   |                   |                    |                   |
[Problème]    ->  [App Store]    ->  [Onboarding]    ->  [1ère action]    ->  [Usage régulier]
                                                                                
                                         |                    |                   |
                                   [Création compte]   [Aha moment]       [Conversion]
```

### 2.3 Jobs-to-be-Done

| JTBD | Situation | Motivation | Outcome |
|------|-----------|------------|---------|
| #1 | Quand [situation] | Je veux [action] | Pour [résultat] |
| #2 | Quand [situation] | Je veux [action] | Pour [résultat] |
| #3 | Quand [situation] | Je veux [action] | Pour [résultat] |

---

## 3. Architecture Fonctionnelle

### 3.1 Modules Principaux

```
                      APPLICATION                         
             |             |             |               
   AUTH         CORE        PREMIUM       SETTINGS    
                                                      
 - Login      - [Feature]  - [Feature]  - Profil      
 - Register   - [Feature]  - [Feature]  - Préférences 
 - Forgot PW  - [Feature]  - Paywall    - Compte      
```

### 3.2 Matrice Fonctionnalités

| ID | Fonctionnalité | Priorité | Version | Free | Premium |
|----|----------------|----------|---------|------|---------|
| F01 | [Nom] | P0 (MVP) | 1.0 | ✓ | ✓ |
| F02 | [Nom] | P0 (MVP) | 1.0 | ✓ | ✓ |
| F03 | [Nom] | P0 (MVP) | 1.0 | L | ✓ |
| F04 | [Nom] | P1 | 1.1 | | |
| F05 | [Nom] | P2 | 2.0 | | |

**Légende priorités** :
- P0 : MVP - Indispensable au lancement
- P1 : Quick wins post-launch
- P2 : Différenciation v2

---

## 4. Fonctionnalités Détaillées

### F01 - [Nom de la Fonctionnalité]

**Description** : [Description claire de ce que fait la feature]

**User Stories** :
| ID | En tant que | Je veux | Pour | Critères d'acceptation |
|----|-------------|---------|------|------------------------|
| US01.1 | [Utilisateur] | [Action] | [Bénéfice] | - [Critère 1]<br>- [Critère 2] |
| US01.2 | [Utilisateur] | [Action] | [Bénéfice] | - [Critère 1] |

**Règles métier** :
- RM01.1 : [Règle]
- RM01.2 : [Règle]

**États possibles** :
| État | Description | Action suivante |
|------|-------------|-----------------|
| Initial | [Description] | [Action] |
| En cours | [Description] | [Action] |
| Complété | [Description] | [Action] |
| Erreur | [Description] | [Action] |

**Métriques de succès** :
- [Métrique] : [Objectif]

---

### F02 - [Nom de la Fonctionnalité]

[Répéter le template ci-dessus pour chaque feature]

---

### F03 - Authentification

**Description** : Gestion de l'inscription, connexion et récupération de mot de passe

**User Stories** :
| ID | En tant que | Je veux | Pour | Critères d'acceptation |
|----|-------------|---------|------|------------------------|
| US03.1 | Visiteur | M'inscrire avec email | Créer un compte | - Email valide requis<br>- MDP 8+ caractères<br>- Confirmation email |
| US03.2 | Visiteur | M'inscrire avec Apple/Google | Créer un compte rapidement | - OAuth fonctionnel<br>- Récupération nom/email |
| US03.3 | Utilisateur | Me connecter | Accéder à mes données | - Email + MDP<br>- Session persistante |
| US03.4 | Utilisateur | Réinitialiser mon MDP | Récupérer l'accès | - Email de reset<br>- Lien valide 24h |

**Règles métier** :
- RM03.1 : Email unique par compte
- RM03.2 : MDP minimum 8 caractères, 1 majuscule, 1 chiffre
- RM03.3 : Session expire après 30 jours d'inactivité
- RM03.4 : Maximum 5 tentatives de connexion puis blocage 15 min

---

### F04 - Onboarding

**Description** : Parcours de première utilisation pour collecter les préférences et activer l'utilisateur

**Écrans onboarding** :
| # | Écran | Objectif | Champs/Actions |
|---|-------|----------|----------------|
| 1 | Bienvenue | Accueillir | [Bouton Commencer] |
| 2 | [Question 1] | [Objectif] | [Options] |
| 3 | [Question 2] | [Objectif] | [Options] |
| 4 | Permissions | Demander accès | [Notifications/Localisation/etc.] |
| 5 | Récap | Confirmer choix | [Bouton Terminer] |

**Règles métier** :
- RM04.1 : Onboarding peut être skip après écran 1
- RM04.2 : Données sauvegardées à chaque étape
- RM04.3 : Onboarding affiché une seule fois

---

## 5. Écrans & Navigation

### 5.1 Arborescence

```
App
   Splash Screen
   Auth (non connecté)
      Login
      Register
      Forgot Password
   Onboarding (1ère fois)
      Step 1
      Step 2
      Step N
   Main (connecté)
      Tab 1 - [Nom]
         Liste/Home
         Détail
      Tab 2 - [Nom]
      Tab 3 - [Nom]
      Tab 4 - Profil
          Paramètres
          Abonnement
          Support
   Modals
      Paywall
      Confirmations
   Overlays
       Loading
       Success
       Error
```

### 5.2 Liste des Écrans

| ID | Écran | Accès | Description |
|----|-------|-------|-------------|
| S01 | Splash | Auto | Logo + chargement |
| S02 | Login | Auth | Connexion email/social |
| S03 | Register | Auth | Inscription |
| S04 | Onboarding | Post-register | X étapes |
| S05 | Home | Tab 1 | [Description] |
| S06 | [Écran] | [Accès] | [Description] |
| S07 | Paywall | Modal | Conversion premium |
| S08 | Settings | Tab Profil | Paramètres |

---

## 6. Règles Métier

### 6.1 Règles Générales

| ID | Règle | Impact |
|----|-------|--------|
| RG01 | [Description règle] | [Où elle s'applique] |
| RG02 | [Description règle] | [Où elle s'applique] |

### 6.2 Règles Freemium

| ID | Règle | Free | Premium |
|----|-------|------|---------|
| RF01 | [Limite 1] | [Valeur] | Illimité |
| RF02 | [Limite 2] | [Valeur] | Illimité |
| RF03 | [Feature] | ✗ | ✓ |

### 6.3 Règles de Validation

| Champ | Type | Obligatoire | Validation | Message erreur |
|-------|------|-------------|------------|----------------|
| Email | String | Oui | Format email valide | "Email invalide" |
| Password | String | Oui | Min 8 car, 1 maj, 1 chiffre | "MDP trop faible" |
| [Champ] | [Type] | [O/N] | [Règle] | [Message] |

---

## 7. Notifications

### 7.1 Push Notifications

| ID | Trigger | Titre | Message | Timing |
|----|---------|-------|---------|--------|
| N01 | [Événement] | [Titre] | [Corps] | [Quand] |
| N02 | Inactivité 3j | "Tu nous manques!" | "[Message rétention]" | J+3 |

### 7.2 Emails Transactionnels

| ID | Trigger | Sujet | Template |
|----|---------|-------|----------|
| E01 | Inscription | "Bienvenue sur [App]!" | welcome.html |
| E02 | Reset password | "Réinitialisation MDP" | reset.html |

---

## 8. Monétisation

### 8.1 Modèle Tarifaire

| Plan | Prix/mois | Prix/an | Économie |
|------|-----------|---------|----------|
| Free | 0€ | 0€ | - |
| Premium | X€ | X€ | X% |

### 8.2 Features par Plan

| Feature | Free | Premium |
|---------|------|---------|
| [Feature 1] | ✓ | ✓ |
| [Feature 2] | Limité (X) | Illimité |
| [Feature 3] | ✗ | ✓ |
| Publicités | Oui | Non |

### 8.3 Triggers Paywall

| Moment | Contexte | Message |
|--------|----------|---------|
| [Trigger 1] | [Quand l'utilisateur...] | [Texte paywall] |
| [Trigger 2] | [Quand l'utilisateur...] | [Texte paywall] |

---

## 9. Contraintes & Edge Cases

### 9.1 Contraintes Techniques

| Contrainte | Impact | Solution |
|------------|--------|----------|
| Offline | [Impact] | [Cache local / Message] |
| Connexion lente | [Impact] | [Loading states / Skeleton] |
| Anciens devices | [Impact] | [Version min iOS/Android] |

### 9.2 Edge Cases

| Cas | Comportement attendu |
|-----|---------------------|
| Utilisateur sans internet | [Comportement] |
| Session expirée en cours d'action | [Comportement] |
| Paiement échoué | [Comportement] |
| Double-tap rapide | [Comportement] |

### 9.3 Gestion des Erreurs

| Type erreur | Message utilisateur | Action |
|-------------|---------------------|--------|
| Réseau | "Connexion impossible. Réessayer ?" | Bouton retry |
| Serveur | "Oups, une erreur est survenue" | Bouton retry + support |
| Validation | [Message spécifique au champ] | Highlight champ |

---

## 10. Roadmap Features

### Version 1.0 (MVP)
- [x] F01 - [Feature]
- [x] F02 - [Feature]
- [x] F03 - Auth
- [x] F04 - Onboarding

### Version 1.1
- [ ] F05 - [Feature]
- [ ] F06 - [Feature]

### Version 2.0
- [ ] F07 - [Feature majeure]
- [ ] [Feature]

### Backlog (non priorisé)
- [ ] [Idée 1]
- [ ] [Idée 2]

---

**Document validé le** : [Date]
**Version** : 1.0
