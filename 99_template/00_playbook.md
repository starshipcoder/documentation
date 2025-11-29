# Playbook : Création d'une App Mobile

## Vue d'ensemble

```
1_IDEATION --> 2_RESEARCH --> 3_STRATEGY --> 4_DESIGN --> 5_DEVELOPMENT
  Doc 11        Doc 21        Doc 31       Doc 41-42      Doc 51-52
                                                              |
                                                              v
                              6_LAUNCH  <--  7_OPERATIONS  <--+
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
|   +-- 32_competitive_analysis.md
|-- 4_design/
|   |-- 41_user_research.md
|   |-- 42_wireframes.md
|   |-- wireframes/
|   +-- prototype/
|-- 5_development/
|   |-- 51_cahier_des_charges.md
|   |-- 52_tech_spec.md
|   +-- 53_backlog.md
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
| **32** | `32_competitive_analysis.md` | 3_strategy | Analyse concurrence détaillée | - |
| **41** | `41_user_research.md` | 4_design | Interviews utilisateurs | - |
| **42** | `42_wireframes.md` | 4_design | Description des maquettes | Figma |
| **51** | `51_cahier_des_charges.md` | 5_development | Spec fonctionnelle exhaustive | - |
| **52** | `52_tech_spec.md` | 5_development | Architecture technique | - |
| **53** | `53_backlog.md` | 5_development | User stories priorisées | - |
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

## Phase 3 : Analyse Stratégique

### Documents : `3_strategy/31_perplexity_strategy.md` + `32_competitive_analysis.md`

**Objectif** : Recommandations et plan d'action

**Contenu doc 31** :
1. Verdict GO/HOLD/NO-GO + niveau confiance
2. Positionnement différenciant (UVP)
3. Personas & Jobs-to-be-Done (3 profils)
4. MVP Features (Top 8 Must-Have)
5. Unit Economics (pricing, LTV/CAC)
6. Plan 0-90 jours
7. 8 hypothèses critiques à valider

**Critère de sortie** : Décision GO -> passer en validation

---

## Phase 4 : Design & Validation

### Documents : `4_design/41_user_research.md` + `42_wireframes.md`

**Objectif** : Valider le problème et la solution avec de vrais utilisateurs

**Actions** :
- [ ] 15-20 interviews utilisateurs cibles
- [ ] Landing page + waitlist (objectif : 100+ emails)
- [ ] Tests de messaging/pricing
- [ ] Wireframes basse fidélité
- [ ] Tests utilisateurs sur prototype

**Critère de sortie** : Validation qualitative + quantitative (emails)

---

## Phase 5 : Spécification & Développement

### Documents : `5_development/51_cahier_des_charges.md` + `52_tech_spec.md` + `53_backlog.md`

**Objectif doc 51** : Spec fonctionnelle exhaustive
- User stories détaillées par feature
- Parcours utilisateur (user flows)
- Règles métier
- Écrans et composants
- États et edge cases
- Critères d'acceptation

**Objectif doc 52** : Architecture technique
- Stack technique
- Architecture système
- Schéma base de données
- APIs et intégrations
- CI/CD

**Critère de sortie** : Specs validées -> démarrer dev

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
- [ ] Décision GO définitive

### 4_design
- [ ] Interviews utilisateurs (41)
- [ ] Wireframes (42)
- [ ] Landing page live
- [ ] 100+ emails waitlist

### 5_development
- [ ] Cahier des charges complet (51)
- [ ] Tech spec validée (52)
- [ ] Backlog priorisé (53)
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
