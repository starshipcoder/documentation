# FuelMap - Cahier des Charges Fonctionnel (MVP)

## Informations Générales

| Élément | Valeur |
|---------|--------|
| **Nom de l'app** | FuelMap |
| **Version** | MVP v1.0 |
| **Plateformes** | iOS / Android (React Native) |
| **Date création** | 29/11/2025 |
| **Scope** | Must Have uniquement (M1-M8) |

---

## 1. Vue d'Ensemble

### 1.1 Objectif de l'Application

FuelMap permet aux automobilistes français de trouver les stations-service les moins chères autour d'eux, de suivre leurs dépenses carburant et de voir les économies réalisées. L'app s'appuie sur les données ouvertes data.gouv.fr enrichies par la communauté.

### 1.2 Proposition de Valeur

> "Trouve le carburant le moins cher près de toi et vois combien tu économises."

### 1.3 Cibles Utilisateurs

| Segment | Description | Priorité |
|---------|-------------|----------|
| Primaire | Conducteurs réguliers (trajets domicile-travail) | P0 |
| Secondaire | Gros rouleurs (commerciaux, VRP) | P1 |
| Tertiaire | Familles multi-véhicules | P2 |

---

## 2. Personas & Parcours

### 2.1 Persona Principal

**Nom** : Thomas
- **Âge** : 35 ans
- **Situation** : Cadre, 50km de trajet quotidien, Peugeot 308 diesel
- **Objectif** : Réduire sa facture carburant (~200€/mois)
- **Frustrations** : Ne sait jamais où sont les stations les moins chères, pas de visibilité sur ses dépenses
- **Tech-savviness** : Moyen (utilise Waze, apps bancaires)

### 2.2 User Journey Principal

```
[Besoin de faire le plein]  ->  [Ouvre FuelMap]  ->  [Voit carte + prix]  ->  [Choisit station]  ->  [Navigue]  ->  [Fait le plein]  ->  [Logge son plein]  ->  [Voit économies]
```

### 2.3 Jobs-to-be-Done

| JTBD | Situation | Motivation | Outcome |
|------|-----------|------------|---------|
| #1 | Quand je dois faire le plein | Je veux trouver la station la moins chère | Pour économiser de l'argent |
| #2 | Quand je fais le plein | Je veux logger mes dépenses | Pour suivre mon budget carburant |
| #3 | Quand je consulte l'app | Je veux voir mes économies | Pour me sentir malin et motivé |

---

## 3. Architecture Fonctionnelle

### 3.1 Modules MVP

```
                    FUELMAP MVP
                         |
                      CARTE

              - Carte stations
              - Filtres carburant
              - Détail station
              - Navigation externe
```

### 3.2 Matrice Fonctionnalités MVP

| ID | Fonctionnalité | Description | Effort | Free | Premium |
|----|----------------|-------------|--------|------|---------|
| M1 | Carte stations | Carte + prix + estimation plein + code couleur | M | ✓ | ✓ |
| M2 | Filtres | Carburant, distance, prix max, fraîcheur | S | ✓ | ✓ |
| M3 | Détail station | Prix, adresse, horaires, services, fraîcheur | S | ✓ | ✓ |
| M4 | Navigation externe | Deeplink Apple/Google Maps | S | ✓ | ✓ |
| M5 | Recherche trajet | Stations sur une route avec détour estimé | M | ✓ | ✓ |

---

## 4. Fonctionnalités Détaillées

### M1 - Carte Stations

**Description** : Affichage d'une carte interactive avec les stations-service et leurs prix, incluant une estimation du prix du plein personnalisée.

**User Stories** :

| ID | En tant que | Je veux | Pour | Critères d'acceptation |
|----|-------------|---------|------|------------------------|
| US1.1 | Utilisateur | Voir les stations autour de moi sur une carte | Trouver où faire le plein | - Carte centrée sur ma position GPS<br>- Stations visibles dans rayon 10km<br>- Chargement < 2s |
| US1.2 | Utilisateur | Voir le prix du carburant sur chaque station | Comparer rapidement | - Prix affiché sur marker<br>- Couleur selon prix (vert/orange/rouge) |
| US1.3 | Utilisateur | Voir le prix estimé de mon plein | Savoir combien je vais payer | - Calcul : prix/L × volume réservoir<br>- Affichage "1.65€/L (~58€)" |
| US1.4 | Utilisateur | Voir si le prix est récent | Éviter les prix obsolètes | - Badge fraîcheur (vert <24h, orange 1-3j, gris >3j)<br>- Texte "il y a 2h" |
| US1.5 | Utilisateur | Me recentrer sur ma position | Retrouver les stations proches | - Bouton "recentrer" visible |

**Règles métier** :
- RM1.1 : Rayon par défaut 10km, extensible à 25km
- RM1.2 : Clustering des markers si zoom out (>50 stations visibles)
- RM1.3 : Volume réservoir basé sur type véhicule (citadine 40L, berline 50L, SUV 60L, utilitaire 70L)
- RM1.4 : Si pas de type véhicule renseigné, afficher uniquement prix/L
- RM1.5 : Code couleur prix : vert = 20% moins cher que moyenne zone, rouge = 20% plus cher

**États possibles** :

| État | Description | Action |
|------|-------------|--------|
| Chargement | Récupération position + stations | Afficher skeleton map |
| Affiché | Carte avec stations | Interaction possible |
| Erreur GPS | Position indisponible | Message + bouton réessayer |
| Aucune station | Pas de station dans le rayon | Message + suggestion étendre rayon |

**Métriques de succès** :
- 80% des utilisateurs trouvent une station en < 30s
- Temps de chargement carte < 2s

---

### M2 - Filtres Carburant

**Description** : Filtrage des stations par type de carburant et fraîcheur des prix.

**User Stories** :

| ID | En tant que | Je veux | Pour | Critères d'acceptation |
|----|-------------|---------|------|------------------------|
| US2.1 | Utilisateur | Filtrer par type de carburant | Voir uniquement ce qui m'intéresse | - Options : SP95, SP95-E10, SP98, Diesel, E85, GPL<br>- Sélection persistante |
| US2.2 | Utilisateur | Filtrer par distance | Ajuster le rayon de recherche | - Slider 5km à 50km<br>- Par défaut : 10km |
| US2.3 | Utilisateur | Filtrer par prix max | Ne voir que les stations abordables | - Slider 1.00€ à 2.50€/L<br>- Par défaut : pas de limite |
| US2.4 | Utilisateur | Filtrer par fraîcheur des prix | Voir uniquement les prix fiables | - Options : < 24h, < 3 jours, Tous<br>- Par défaut : Tous |

**Règles métier** :
- RM2.1 : Le filtre carburant est sauvegardé en préférence utilisateur
- RM2.2 : Le filtre distance est sauvegardé
- RM2.3 : Le filtre prix max n'est pas sauvegardé (reset à chaque session)
- RM2.4 : Le filtre fraîcheur n'est pas sauvegardé (reset à chaque session)
- RM2.5 : Les stations sans prix pour le carburant sélectionné sont masquées

**Métriques de succès** :
- 95% des utilisateurs filtrent correctement

---

### M3 - Détail Station

**Description** : Écran détaillé d'une station avec toutes ses informations.

**User Stories** :

| ID | En tant que | Je veux | Pour | Critères d'acceptation |
|----|-------------|---------|------|------------------------|
| US3.1 | Utilisateur | Voir tous les prix de la station | Comparer les carburants | - Liste tous carburants disponibles<br>- Prix + date MAJ pour chacun |
| US3.2 | Utilisateur | Voir l'adresse complète | Savoir où aller | - Adresse formatée<br>- Distance depuis ma position |
| US3.3 | Utilisateur | Voir les horaires | Savoir si c'est ouvert | - Horaires par jour<br>- Indicateur "Ouvert/Fermé" |
| US3.4 | Utilisateur | Voir les services | Savoir ce qui est disponible | - Liste : lavage, boutique, gonflage, DAB, etc. |
| US3.5 | Utilisateur | Voir la fraîcheur du prix | Évaluer la fiabilité | - "Mis à jour il y a 2h"<br>- Source (data.gouv / communauté) |

**Règles métier** :
- RM3.1 : Afficher estimation prix du plein pour chaque carburant
- RM3.2 : Indiquer clairement si ouvert 24h/24

**Métriques de succès** :
- 70% des utilisateurs consultent le détail après tap sur marker

---

### M4 - Navigation Externe

**Description** : Lancer la navigation vers une station dans Apple Maps ou Google Maps.

**User Stories** :

| ID | En tant que | Je veux | Pour | Critères d'acceptation |
|----|-------------|---------|------|------------------------|
| US5.1 | Utilisateur | Naviguer vers la station | Y aller facilement | - Bouton "Y aller" visible<br>- Ouvre app de navigation par défaut |
| US5.2 | Utilisateur | Choisir mon app de navigation | Utiliser celle que je préfère | - Si plusieurs apps dispo : choix Apple/Google Maps<br>- Mémoriser préférence |

**Règles métier** :
- RM4.1 : Deeplink avec coordonnées GPS de la station
- RM4.2 : Si une seule app de navigation disponible, l'ouvrir directement
- RM4.3 : Préférence navigation sauvegardée en local

**Métriques de succès** :
- 60% des utilisateurs utilisent la navigation

---

### M5 - Recherche Trajet

**Description** : Permettre aux utilisateurs de rechercher un trajet et voir toutes les stations le long de la route, avec estimation du détour.

**User Stories** :

| ID | En tant que | Je veux | Pour | Critères d'acceptation |
|----|-------------|---------|------|------------------------|
| US5.1 | Utilisateur | Rechercher un trajet (départ → arrivée) | Planifier mes arrêts carburant | - Champ départ (position par défaut)<br>- Champ arrivée (autocomplete)<br>- Historique des recherches |
| US5.2 | Utilisateur | Voir les stations sur ma route | Choisir où m'arrêter | - Tracé de la route sur la carte<br>- Markers stations le long du trajet<br>- Filtrage par distance à la route |
| US5.3 | Utilisateur | Voir le détour pour chaque station | Évaluer si ça vaut le coup | - Distance du détour (km)<br>- Temps estimé du détour (min)<br>- Distance depuis le départ |
| US5.4 | Utilisateur | Trier les stations du trajet | Trouver la meilleure option | - Tri par prix<br>- Tri par distance depuis départ<br>- Tri par détour minimum |

**Règles métier** :
- RM5.1 : Stations affichées si à moins de 5km de la route
- RM5.2 : Calcul du détour = distance aller-retour depuis la route
- RM5.3 : Temps détour estimé à 50km/h en moyenne (sortie autoroute)
- RM5.4 : Historique des 5 dernières recherches sauvegardé en local
- RM5.5 : Route calculée via API de routing (OSRM ou similaire)

**Composants** :
- Barre de recherche trajet (bottom sheet)
- Polyline route sur la carte
- Header sticky avec infos trajet
- Station bottom sheet enrichi (infos détour)

**Métriques de succès** :
- 30% des utilisateurs utilisent la recherche trajet
- 50% des recherches aboutissent à un clic sur station

---

## 5. Onboarding

### 5.1 Parcours Onboarding

| # | Écran | Objectif | Contenu |
|---|-------|----------|---------|
| 1 | Bienvenue | Accueillir | Logo + "Trouve le carburant le moins cher" + [Commencer] |
| 2 | Type de véhicule | Personnaliser estimation plein | Choix : Citadine / Berline / SUV / Utilitaire |
| 3 | Carburant | Définir préférence | Choix : SP95 / SP95-E10 / SP98 / Diesel / E85 / GPL |
| 4 | Localisation | Demander permission GPS | Explication bénéfice + demande permission |

**Règles métier** :
- RM-OB1 : Écrans 2-3 peuvent être skip (valeurs par défaut : Berline + Diesel)
- RM-OB2 : Données sauvegardées en local à chaque étape
- RM-OB3 : Onboarding affiché une seule fois par device

---

## 6. Écrans & Navigation

### 6.1 Arborescence

```
App
├── Splash Screen
├── Onboarding (1ère fois)
│   ├── Bienvenue
│   ├── Type véhicule
│   ├── Carburant
│   └── Permission GPS
└── Main (écran unique)
    ├── Carte (Home)
    ├── Filtres (bottom sheet)
    ├── Détail station (bottom sheet)
    │   └── Navigation externe
    └── Paramètres (bottom sheet)
        └── Préférences (véhicule, carburant)
```

### 6.2 Liste des Écrans MVP

| ID | Écran | Accès | Description |
|----|-------|-------|-------------|
| S01 | Splash | Auto | Logo + chargement |
| S02 | Onboarding | 1ère fois | 4 étapes |
| S03 | Carte | Home | Carte stations + markers |
| S04 | Filtres | Bottom sheet depuis carte | Sélection carburant + fraîcheur |
| S05 | Détail station | Tap marker | Infos complètes station |
| S06 | Paramètres | Bottom sheet | Préférences véhicule/carburant |

---

## 7. Règles Métier Générales

### 7.1 Règles Générales

| ID | Règle | Impact |
|----|-------|--------|
| RG01 | App utilisable sans compte | Toutes les fonctionnalités MVP |
| RG02 | Données stockées en local | Préférences véhicule/carburant |
| RG03 | GPS requis pour afficher carte | Demandé à l'onboarding |
| RG04 | Données stations : data.gouv.fr | Refresh quotidien automatique |

### 7.2 Règles de Validation

Pas de validation utilisateur requise pour le MVP (pas de saisie manuelle).

---

## 8. Contraintes & Edge Cases

### 8.1 Contraintes Techniques

| Contrainte | Impact | Solution |
|------------|--------|----------|
| Offline | Carte inutilisable | Message "Connexion requise" |
| GPS refusé | Carte non centrée | Recherche manuelle par ville |
| Connexion lente | Chargement long | Skeleton + cache local |

### 8.2 Edge Cases

| Cas | Comportement attendu |
|-----|---------------------|
| Utilisateur sans internet | Message erreur + retry |
| GPS imprécis | Rayon élargi automatiquement |
| Aucune station dans rayon | Message + bouton "Étendre à 25km" |
| Prix très ancien (>7j) | Badge gris + mention "prix ancien" |

### 8.3 Gestion des Erreurs

| Type erreur | Message utilisateur | Action |
|-------------|---------------------|--------|
| Réseau | "Connexion impossible" | Bouton retry |
| GPS | "Position indisponible" | Recherche manuelle |
| Serveur | "Une erreur est survenue" | Retry + support |
| Validation | Message spécifique | Highlight champ |

---

## 9. Data Model

### 9.1 Données locales (AsyncStorage)

```
preferences
├── type_vehicule (enum: citadine/berline/suv/utilitaire)
├── volume_reservoir (int: 40/50/60/70)
├── carburant_defaut (enum: sp95/sp95e10/sp98/diesel/e85/gpl)
├── app_navigation (enum: apple_maps/google_maps)
└── onboarding_completed (bool)
```

### 9.2 Données API (data.gouv.fr)

```
stations
├── id (string, ID data.gouv)
├── nom (string)
├── adresse (string)
├── ville (string)
├── code_postal (string)
├── lat (decimal)
├── lng (decimal)
├── horaires (json)
├── services (json array)
└── prix[] (liste des prix par carburant)
    ├── carburant (enum)
    ├── prix (decimal)
    └── maj (timestamp)
```

---

## 10. Métriques de Succès MVP

| Métrique | Objectif | Mesure |
|----------|----------|--------|
| Temps trouver station | < 30s | 80% users |
| Utilisation navigation | 60% | Des sessions |
| Rétention J7 | 30% | Standard apps utils |
| Note App Store | 4.0+ | Moyenne avis |

---

## 11. Hors Scope MVP

Les fonctionnalités suivantes sont explicitement exclues du MVP :

- Authentification / création de compte
- Signalement prix par les utilisateurs
- Historique des pleins
- Calcul des économies
- Notifications prix bas
- Gamification (badges, leaderboard)
- Favoris stations
- Mode liste
- Premium/abonnement
- Stats avancées
- Widget
- Apple Watch / CarPlay
- Multi-véhicules
- Export données
- Coaching éco-conduite

---

**Document validé le** : 29/11/2025
**Version** : 1.0 MVP
**Estimation effort** : ~10 jours de développement
