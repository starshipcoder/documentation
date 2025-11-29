# Playbook : Création d'une App Mobile

## Vue d'ensemble

```
1_IDEATION --> 2_RESEARCH --> 3_STRATEGY --> 4_DESIGN --> 5_DEVELOPMENT
  Doc 11        Doc 21        Doc 31-33      Doc 41-42      Doc 51-52
                                 |                              |
                                 v                              v
                         (specs avant design)            6_LAUNCH  <--  7_OPERATIONS
                                                         Doc 61-62      Doc 71-72
```

---

## Structure du Projet

```
nom_projet/
|-- 1_ideation/
|   +-- 11_brief.md
|-- 2_research/
|   +-- 21_perplexity_research.md
|-- 3_strategy/
|   |-- 31_perplexity_strategy.md
|   |-- 32_features_list.md
|   +-- 33_cahier_des_charges.md
|-- 4_design/
|   |-- 41_user_research.md
|   |-- 42_wireframes.md
|   |-- wireframes/
|   +-- prototype/
|-- 5_development/
|   |-- 51_tech_spec.md
|   +-- 52_backlog.md
|-- 6_launch/
|   |-- 61_aso_checklist.md
|   |-- 62_marketing_plan.md
|   |-- aso_assets/
|   +-- press_kit/
+-- 7_operations/
    |-- 71_kpi_dashboard.md
    |-- 72_user_feedback.md
    +-- 73_roadmap.md
```

---

## Index des Documents

| # | Document | Dossier | Objectif | Outil |
|---|----------|---------|----------|-------|
| **11** | `11_brief.md` | 1_ideation | Synthèse idée 1 page | - |
| **21** | `21_perplexity_research.md` | 2_research | Données marché factuelles | Perplexity |
| **31** | `31_perplexity_strategy.md` | 3_strategy | Analyse + recommandations | GPT/Claude |
| **32** | `32_features_list.md` | 3_strategy | Liste features priorisées | - |
| **33** | `33_cahier_des_charges.md` | 3_strategy | Spec fonctionnelle exhaustive | - |
| **41** | `41_user_research.md` | 4_design | Interviews utilisateurs | - |
| **42** | `42_wireframes.md` | 4_design | Description des maquettes | Figma |
| **51** | `51_tech_spec.md` | 5_development | Architecture technique | - |
| **52** | `52_backlog.md` | 5_development | User stories priorisées | - |
| **61** | `61_aso_checklist.md` | 6_launch | Assets App Store | - |
| **62** | `62_marketing_plan.md` | 6_launch | Plan GTM | - |
| **71** | `71_kpi_dashboard.md` | 7_operations | Suivi métriques | - |
| **72** | `72_user_feedback.md` | 7_operations | Retours utilisateurs | - |
| **73** | `73_roadmap.md` | 7_operations | Features à venir | - |

---

## Phase 1 : Idéation

### Document : `1_ideation/11_brief.md`

**Objectif** : Décider rapidement GO/NO-GO sur l'idée

**Contenu** :
- L'idée en 3 lignes
- Problème résolu
- Cible principale
- Value Proposition (1 phrase)
- Modèle économique (hypothèse)
- "Pourquoi maintenant ?"
- Difficulté technique (1-10)
- Stack envisagée
- Coûts mensuels estimés

**Critère de sortie** : Brief complété -> passer en recherche

---

## Phase 2 : Recherche Marché

### Document : `2_research/21_perplexity_research.md`

**Objectif** : Données factuelles sur le marché et la concurrence

**Contenu** :
1. Marché & demande (TAM/SAM/SOM, CAGR, tendances)
2. Analyse concurrentielle (tableau 10-12 acteurs)
3. Pricing & monétisation (benchmark)
4. Distribution & acquisition (canaux, CAC)
5. Contexte réglementaire & technique
6. Top 7 insights actionnables

**Critère de sortie** : Red flags identifiés ou opportunité confirmée

---

## Phase 3 : Analyse Stratégique & Spécifications

### Documents : `3_strategy/31_perplexity_strategy.md` + `32_features_list.md` + `33_cahier_des_charges.md`

**Objectif** : Recommandations, features et specs fonctionnelles AVANT le design

**Contenu doc 31** (Analyse stratégique) :
1. Verdict GO/HOLD/NO-GO + niveau confiance
2. Positionnement différenciant (UVP)
3. Personas & Jobs-to-be-Done (3 profils)
4. MVP Features (Top 8 Must-Have)
5. Unit Economics (pricing, LTV/CAC)
6. Plan 0-90 jours
7. 8 hypothèses critiques à valider

**Contenu doc 32** (Features List) :
- Liste exhaustive des features avec priorité (Must/Should/Could/Won't)
- Dépendances entre features
- Estimation effort (T-shirt sizing)
- Métriques de succès par feature

**Contenu doc 33** (Cahier des charges) :
- Spec fonctionnelle exhaustive
- User stories détaillées par feature
- Parcours utilisateur (user flows)
- Règles métier
- États et edge cases
- Critères d'acceptation

**Critère de sortie** : Specs validées -> passer en design

---

## Phase 4 : Design & Validation

### Documents : `4_design/41_user_research.md` + `42_wireframes.md`

**Objectif** : Valider avec de vrais utilisateurs et créer les maquettes basées sur les specs

**Actions** :
- [ ] 15-20 interviews utilisateurs cibles
- [ ] Landing page + waitlist (objectif : 100+ emails)
- [ ] Tests de messaging/pricing
- [ ] Wireframes basés sur le cahier des charges (33)
- [ ] Tests utilisateurs sur prototype

**Critère de sortie** : Validation qualitative + quantitative (emails) + wireframes validés

---

## Phase 5 : Développement

### Documents : `5_development/51_tech_spec.md` + `52_backlog.md`

**Objectif doc 51** (Tech Spec) : Architecture technique
- Stack technique
- Architecture système
- Schéma base de données
- APIs et intégrations
- CI/CD

**Objectif doc 52** (Backlog) : User stories priorisées pour le dev
- Sprint planning
- Stories découpées depuis le cahier des charges (33)
- Critères d'acceptation techniques

**Critère de sortie** : Tech spec validée -> démarrer dev

---

## Phase 6 : Lancement

### Documents : `6_launch/61_aso_checklist.md` + `62_marketing_plan.md`

**Objectif doc 61** : Préparer tous les assets pour App Store / Play Store
- Nom app + sous-titre
- Description courte/longue
- Mots-clés ASO
- Screenshots (6-10)
- Vidéo preview
- Icône app

**Actions** :
- [ ] Soumission App Store + Play Store
- [ ] Activation canaux acquisition
- [ ] Monitoring reviews

---

## Phase 7 : Post-Launch & Itération

### Documents : `7_operations/71_kpi_dashboard.md` + `72_user_feedback.md` + `73_roadmap.md`

**Objectif** : Suivre les métriques et itérer

**KPIs clés** :
| Métrique | J+7 | J+30 | J+90 |
|----------|-----|------|------|
| Downloads | | | |
| DAU/MAU | | | |
| Conversion free->paid | | | |
| Churn mensuel | | | |
| Rating App Store | | | |

---

## Checklist Globale

### 1_ideation
- [ ] Brief complété (11)
- [ ] GO/NO-GO initial

### 2_research
- [ ] Recherche marché (21)

### 3_strategy
- [ ] Analyse stratégique (31)
- [ ] Features list priorisée (32)
- [ ] Cahier des charges complet (33)
- [ ] Décision GO définitive

### 4_design
- [ ] Interviews utilisateurs (41)
- [ ] Wireframes (42)
- [ ] Landing page live
- [ ] 100+ emails waitlist

### 5_development
- [ ] Tech spec validée (51)
- [ ] Backlog priorisé (52)
- [ ] MVP features complètes
- [ ] Bêta testée

### 6_launch
- [ ] Assets ASO prêts (61)
- [ ] Marketing plan (62)
- [ ] App soumise iOS + Android
- [ ] App publiée

### 7_operations
- [ ] Dashboard KPIs actif (71)
- [ ] Process feedback en place (72)
- [ ] Roadmap V2 définie (73)

---

## Usage Rapide

Pour référencer un document :
> "Regarde le doc 51" -> `5_development/51_cahier_des_charges.md`
> "Mets à jour le 71" -> `7_operations/71_kpi_dashboard.md`

Pour créer un nouveau projet :
```bash
cp -r 99_template/ 03_en_etude/[nom_projet]/
```
