# FuelMap - Liste des Features

## Vue d'ensemble

| Total Features | Must Have | Should Have | Could Have | Won't Have |
|----------------|-----------|-------------|------------|------------|
| 24 | 8 | 6 | 6 | 4 |

---

## Features par Priorité (MoSCoW)

### Must Have (MVP)

| # | Feature | Description | Effort | Dépendances | Métrique succès |
|---|---------|-------------|--------|-------------|-----------------|
| M1 | Carte stations | Affichage carte avec stations et prix + estimation prix du plein basé sur moyenne litres user | M | - | 80% users trouvent station <30s |
| M2 | Filtres carburant | SP95, SP98, Diesel, E85, E10, GPL + filtre fraîcheur prix | S | M1 | 95% filtrent correctement |
| M3 | Détail station | Prix, adresse, horaires, services | S | M1 | 70% consultent détail |
| M4 | Signalement prix | User peut signaler/corriger un prix | M | M1, Auth | 100+ signalements/jour @ 10K MAU |
| M5 | Navigation externe | Deeplink vers Apple/Google Maps | S | M3 | 60% utilisent navigation |
| M6 | Auth basique | Email + Google/Apple Sign-In | M | - | 50% users créent compte |
| M7 | Historique pleins | Logger ses pleins (prix, litres, km) | M | Auth | 40% loggent leurs pleins |
| M8 | Calcul économies | Afficher économies vs prix moyen zone | S | M7 | 70% voient leurs économies |

### Should Have (V1.1)

| # | Feature | Description | Effort | Dépendances | Métrique succès |
|---|---------|-------------|--------|-------------|-----------------|
| S1 | Notifications prix | Alerte quand prix bas dans zone | M | Auth, M1 | 20% activent notifs |
| S2 | Badges gamification | Premier plein, contributeur, streak 7j | M | Auth, M4, M7 | 30% ont 1+ badge |
| S3 | Leaderboard local | Classement contributeurs par ville | M | S2 | 10% consultent leaderboard |
| S4 | Favoris stations | Sauvegarder stations préférées | S | Auth, M3 | 25% ont 1+ favori |
| S5 | Mode liste | Vue liste alternative à la carte | S | M1 | 15% utilisent vue liste |
| S6 | Premium sans pub | Abonnement €9.99/an ad-free | M | Auth | 3-5% conversion |

### Could Have (V2+)

| # | Feature | Description | Effort | Dépendances | Métrique succès |
|---|---------|-------------|--------|-------------|-----------------|
| C1 | Stats avancées | Conso moyenne, coût/km, graphiques | L | M7, S6 | 50% premium utilisent |
| C2 | Widget iOS/Android | Prix station favorite sur home screen | M | S4 | 10% installent widget |
| C3 | Apple Watch | Prix rapide au poignet | L | M1 | 5% utilisent Watch |
| C4 | CarPlay/Android Auto | Interface voiture simplifiée | L | M1, M5 | 8% utilisent en voiture |
| C5 | Multi-véhicules | Gérer plusieurs voitures | M | M7 | 15% ont 2+ véhicules |
| C6 | Export données | CSV/PDF pour notes de frais | S | M7, S6 | 20% premium exportent |

### Won't Have (Out of Scope MVP)

| # | Feature | Raison exclusion |
|---|---------|------------------|
| W1 | Coaching éco-conduite | Trop complexe (background GPS), retiré du scope |
| W2 | Paiement in-app station | Intégrations pétroliers complexes, pas prioritaire |
| W3 | Comparateur assurances | Hors scope, autre business |
| W4 | Covoiturage | Hors scope, autre marché |

---

## Matrice Effort / Impact

```
Impact élevé
    ^
    |   [S1]       [M1] [M4]
    |   [S2]       [M7] [M8]
    |              [M2] [M3]
    |   [C1]       [S6]
    +-------------------------> Effort élevé
    |   [M5][M6]   [S3] [C2]
    |   [S4][S5]   [C4] [C3]
    |              [C5] [C6]
Impact faible
```

**Priorité dev** : Quadrant haut-gauche d'abord (M1-M8), puis S1-S6

---

## Dépendances entre Features

```
M1 (Carte stations)
 ├── M2 (Filtres)
 ├── M3 (Détail station)
 │    └── M5 (Navigation)
 │    └── S4 (Favoris)
 │         └── C2 (Widget)
 └── M4 (Signalement prix)
      └── S2 (Badges)
           └── S3 (Leaderboard)

M6 (Auth)
 ├── M4 (Signalement)
 ├── M7 (Historique pleins)
 │    └── M8 (Économies)
 │    └── C1 (Stats avancées)
 │    └── C5 (Multi-véhicules)
 │    └── C6 (Export)
 ├── S1 (Notifications)
 └── S6 (Premium)
```

---

## Estimation Effort (T-shirt sizing)

| Taille | Définition | Jours dev estimés |
|--------|------------|-------------------|
| **S** | Simple, 1-2 écrans, pas d'API externe | 1-2 jours |
| **M** | Modéré, 3-5 écrans, 1 intégration | 3-5 jours |
| **L** | Complexe, logique métier, multi-intégrations | 1-2 semaines |
| **XL** | Très complexe, R&D nécessaire | 2-4 semaines |

### Estimation totale MVP (M1-M8)

| Feature | Effort | Jours |
|---------|--------|-------|
| M1 Carte | M | 5 |
| M2 Filtres | S | 1 |
| M3 Détail | S | 2 |
| M4 Signalement | M | 4 |
| M5 Navigation | S | 1 |
| M6 Auth | M | 3 |
| M7 Historique | M | 4 |
| M8 Économies | S | 2 |
| **Total MVP** | | **~22 jours** (~1 mois) |

### Estimation V1.1 (S1-S6)

| Feature | Effort | Jours |
|---------|--------|-------|
| S1 Notifications | M | 4 |
| S2 Badges | M | 3 |
| S3 Leaderboard | M | 3 |
| S4 Favoris | S | 1 |
| S5 Mode liste | S | 1 |
| S6 Premium | M | 3 |
| **Total V1.1** | | **~15 jours** (~3 semaines) |

---

## Features par Module/Écran

### Module : Onboarding
- [ ] M6 - Auth (email + social)
- [ ] Écran permissions (localisation)
- [ ] Sélection carburant par défaut
- [ ] Sélection type de véhicule (citadine/berline/SUV/utilitaire) → volume réservoir par défaut

### Module : Carte (Home)
- [ ] M1 - Carte stations
- [ ] M2 - Filtres carburant
- [ ] M2 - Filtre fraîcheur prix (< 24h, < 3 jours, tous)
- [ ] S5 - Toggle vue liste
- [ ] Barre recherche ville/adresse

### Module : Station
- [ ] M3 - Détail station
- [ ] M4 - Signalement prix
- [ ] M5 - Navigation externe
- [ ] S4 - Ajouter aux favoris

### Module : Profil/Historique
- [ ] M7 - Historique pleins
- [ ] M8 - Économies calculées
- [ ] S2 - Badges obtenus
- [ ] C1 - Stats avancées (premium)
- [ ] C5 - Multi-véhicules
- [ ] C6 - Export données

### Module : Communauté
- [ ] S3 - Leaderboard local
- [ ] Liste mes contributions

### Module : Settings
- [ ] S1 - Config notifications
- [ ] S6 - Gestion abonnement premium
- [ ] Préférences carburant
- [ ] Unités (€/L, km/miles)

### Module : Monétisation
- [ ] Bannière pub (free users)
- [ ] S6 - Paywall premium
- [ ] Interstitiel pub (optionnel, après X actions)

---

## Spécifications Clés par Feature

### M1 - Carte stations

**User Story** : En tant qu'utilisateur, je veux voir les stations autour de moi sur une carte pour trouver où faire le plein.

**Specs** :
- Afficher carte centrée sur position GPS user
- Markers stations avec prix du carburant sélectionné
- **Afficher le prix estimé du plein** (prix/L × volume réservoir)
  - Volume basé sur type de véhicule (demandé à l'onboarding)
  - Affichage : "1.65€/L (~58€ le plein)"
- **Afficher la date de dernière mise à jour du prix** (ex: "il y a 2h", "hier", "il y a 3 jours")
- Couleur marker selon prix (vert=pas cher, rouge=cher)
- Indicateur visuel fraîcheur (ex: badge vert <24h, orange 1-3j, gris >3j)
- Cluster markers si zoom out
- Bouton "recentrer sur moi"
- Rayon par défaut : 10km

**Critères d'acceptation** :
- [ ] Carte charge en <2s
- [ ] Stations visibles dans rayon 10km
- [ ] Prix affichés sur markers
- [ ] Prix du plein estimé affiché si historique disponible
- [ ] Tap marker ouvre détail (M3)

---

### M4 - Signalement prix

**User Story** : En tant qu'utilisateur, je veux signaler un prix que j'ai vu pour aider la communauté.

**Specs** :
- Depuis écran détail station
- Champ prix (clavier numérique)
- Sélection carburant
- Photo optionnelle (preuve)
- Timestamp automatique
- Validation : prix dans fourchette réaliste (0.50€ - 3.00€/L)

**Anti-abuse** :
- 1 signalement/station/user/jour max
- Compte vérifié requis (email confirmé)
- Score confiance user (basé historique)

**Critères d'acceptation** :
- [ ] Signalement en <30s
- [ ] Validation prix (fourchette)
- [ ] Confirmation visuelle
- [ ] Prix mis à jour dans app

---

### M7 - Historique pleins

**User Story** : En tant qu'utilisateur, je veux logger mes pleins pour suivre mes dépenses carburant.

**Specs** :
- Formulaire : date, station, carburant, litres, prix total, km compteur (optionnel)
- Calcul automatique prix/litre
- Liste chronologique des pleins
- Suppression/édition possible

**Critères d'acceptation** :
- [ ] Ajout plein en <1min
- [ ] Historique affiché chronologiquement
- [ ] Prix/litre calculé automatiquement
- [ ] Sync cloud (pas perdu si change téléphone)

---

### S2 - Badges gamification

**Badges MVP** :

| Badge | Condition | Icône |
|-------|-----------|-------|
| Premier Plein | Logger 1er plein | |
| Contributeur | 1er signalement prix | |
| Fidèle | 5 pleins loggés | |
| Streak 7j | Ouvrir app 7 jours consécutifs | |
| Expert Local | 10 signalements même ville | |
| Économe | 50€ économisés cumulés | |

**Specs** :
- Notification in-app quand badge débloqué
- Section badges dans profil
- Badges grisés si non obtenus (teasing)

---

## Data Model (simplifié)

### Tables principales

```
users
- id (uuid)
- email
- created_at
- carburant_defaut (enum)
- type_vehicule (enum: citadine/berline/suv/utilitaire)
- volume_reservoir (int, en litres, déduit du type)
- is_premium (bool)
- trust_score (int)

stations
- id (uuid)
- nom
- adresse
- lat, lng
- horaires (json)
- services (json)
- source (data.gouv / crowdsourced)

prix
- id (uuid)
- station_id (fk)
- carburant (enum)
- prix (decimal)
- reported_by (fk user, nullable si data.gouv)
- reported_at (timestamp)
- photo_url (nullable)

pleins
- id (uuid)
- user_id (fk)
- station_id (fk)
- carburant (enum)
- litres (decimal)
- prix_total (decimal)
- km_compteur (int, nullable)
- date (timestamp)

badges
- id (uuid)
- user_id (fk)
- badge_type (enum)
- unlocked_at (timestamp)
```

---

## Notes & Décisions

| Date | Décision | Contexte |
|------|----------|----------|
| 29/11/2025 | Retrait coaching éco-conduite | Complexité background GPS trop élevée |
| 29/11/2025 | Focus France uniquement pour MVP | Data.gouv.fr disponible, marché connu |
| 29/11/2025 | Freemium €9.99/an | Aligné sur Fuelio, prix accessible |
| 29/11/2025 | Pas de paiement in-app station | Hors scope, intégrations trop lourdes |

---

**Dernière mise à jour** : 29 novembre 2025
**Auteur** : Claude
