# [NOM APP] - Liste des Features

## Vue d'ensemble

| Total Features | Must Have | Should Have | Could Have | Won't Have |
|----------------|-----------|-------------|------------|------------|
| X | X | X | X | X |

---

## Features par Priorité (MoSCoW)

### Must Have (MVP)

| # | Feature | Description | Effort | Dépendances | Métrique succès |
|---|---------|-------------|--------|-------------|-----------------|
| M1 | [Nom] | [Description courte] | S/M/L/XL | - | [KPI] |
| M2 | | | | | |
| M3 | | | | | |
| M4 | | | | | |
| M5 | | | | | |
| M6 | | | | | |
| M7 | | | | | |
| M8 | | | | | |

### Should Have (V1.1)

| # | Feature | Description | Effort | Dépendances | Métrique succès |
|---|---------|-------------|--------|-------------|-----------------|
| S1 | [Nom] | [Description courte] | S/M/L/XL | M1 | [KPI] |
| S2 | | | | | |
| S3 | | | | | |
| S4 | | | | | |

### Could Have (V2+)

| # | Feature | Description | Effort | Dépendances | Métrique succès |
|---|---------|-------------|--------|-------------|-----------------|
| C1 | [Nom] | [Description courte] | S/M/L/XL | S1 | [KPI] |
| C2 | | | | | |
| C3 | | | | | |

### Won't Have (Out of Scope)

| # | Feature | Raison exclusion |
|---|---------|------------------|
| W1 | [Nom] | [Pourquoi pas maintenant] |
| W2 | | |

---

## Matrice Effort / Impact

```
Impact élevé
    ^
    |   [C1]     [M1] [M2]
    |            [M3] [M4]
    |   [S2]     [S1]
    |
    +-------------------------> Effort élevé
    |   [M5]     [S3]
    |   [M6]     [C2]
    |
Impact faible
```

---

## Dépendances entre Features

```
M1 (Auth)
  └── M2 (Profil)
       └── S1 (Settings avancés)
            └── C1 (Export données)

M3 (Core feature 1)
  └── M4 (Core feature 2)
       └── S2 (Enhancement)
```

---

## Estimation Effort (T-shirt sizing)

| Taille | Définition | Jours dev estimés |
|--------|------------|-------------------|
| **S** | Simple, peu de code, pas d'intégration | 1-2 jours |
| **M** | Modéré, quelques écrans/composants | 3-5 jours |
| **L** | Complexe, intégrations tierces | 1-2 semaines |
| **XL** | Très complexe, R&D nécessaire | 2-4 semaines |

---

## Features par Module/Écran

### Module : Onboarding
- [ ] M1 - [Feature]
- [ ] M2 - [Feature]

### Module : Core
- [ ] M3 - [Feature]
- [ ] M4 - [Feature]
- [ ] M5 - [Feature]

### Module : Profil/Settings
- [ ] M6 - [Feature]
- [ ] S1 - [Feature]

### Module : Monétisation
- [ ] M7 - [Feature]
- [ ] M8 - [Feature]

---

## Notes & Décisions

| Date | Décision | Contexte |
|------|----------|----------|
| [Date] | [Décision prise] | [Pourquoi] |

---

**Dernière mise à jour** : [Date]
**Auteur** : [Nom]
