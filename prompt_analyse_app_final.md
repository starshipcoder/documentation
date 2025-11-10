# Prompt d'analyse d'idée d'application mobile

## 🎯 Guide d'utilisation

Ce document contient 3 versions de prompts pour analyser le potentiel d'une idée d'application mobile :
- **Version 1** : Recherche marché (Perplexity recommandé)
- **Version 2** : Analyse stratégique (après recherche)
- **Version 3** : Prompt tout-en-un (GPT-4 ou Claude avec web search)

---

## 📋 Version 1 : Recherche initiale marché
**Recommandé pour : Perplexity, ChatGPT avec web browsing**

```
**Contexte**
Je souhaite évaluer l'opportunité de lancer une application mobile : [DÉCRIRE TON IDÉE EN 2-3 PHRASES PRÉCISES]

**Ta mission**
Tu es un market researcher senior. Conduis une recherche web approfondie (données des 12-18 derniers mois) sur :

### 1. Marché & demande
- Taille du marché global et adressable (TAM/SAM avec méthodologie de calcul)
- Taux de croissance annuel (CAGR si disponible)
- Tendances clés : évolutions technologiques, changements comportementaux, nouveaux besoins
- Segmentation : géographies principales, types d'utilisateurs, use cases dominants
- Barrières à l'entrée et facteurs de succès observés

### 2. Analyse concurrentielle détaillée
Créer un tableau avec au minimum 10-12 acteurs incluant :

| Nom | Pays | Cible | Modèle prix | Downloads/MAU estimés | Dernière levée/Revenus | Points forts | Points faibles |
|-----|------|-------|-------------|----------------------|------------------------|--------------|----------------|

Inclure dans l'analyse :
- Applications natives (iOS/Android)
- Solutions web/SaaS alternatives
- Solutions "good enough" (Excel, outils généralistes)
- Nouveaux entrants (< 2 ans)

Pour chaque concurrent majeur (top 5), détailler :
- Proposition de valeur principale
- Fonctionnalités clés
- Stratégie de différenciation observée
- Avis utilisateurs (synthèse des reviews App Store/Play Store)

### 3. Pricing & monétisation
- Benchmark des modèles : freemium, abonnement (mensuel/annuel), one-time purchase, in-app purchases
- Fourchettes de prix observées par segment
- Stratégies d'acquisition : durée des trials, offres promotionnelles
- Part de la publicité dans le modèle (si applicable)
- Add-ons et upsells courants

### 4. Distribution & acquisition utilisateurs
- Canaux d'acquisition utilisés par les leaders (ASO, SEA, content marketing, partnerships, sales direct)
- Coûts d'acquisition estimés (CPI/CAC si données disponibles)
- Stratégies de croissance observées (viral, PLG, sales-led)
- Partenariats et intégrations stratégiques récurrents

### 5. Contexte réglementaire & technique
- Contraintes légales (RGPD, protection des données, licences sectorielles)
- Dépendances techniques critiques (APIs tierces, SDKs, plateformes)
- Risques identifiés (changements de politique plateforme, coûts APIs)

**Format de sortie attendu**
- Sections clairement structurées avec titres
- Tableaux comparatifs (markdown ou texte structuré)
- **Citations obligatoires** : Pour chaque fait/chiffre clé, indiquer :
  - [Titre source](URL) - Date publication - Date d'accès
  - Minimum 12-20 sources variées
- Distinguer clairement :
  - ✅ Faits sourcés
  - 📊 Estimations (indiquer méthodologie)
  - 💭 Inférences (marquer explicitement)

**Terminer par : "Top 7 insights actionnables"**
Liste numérotée des découvertes les plus importantes pour la décision GO/NO-GO.

**Contraintes de qualité**
- Privilégier les sources primaires : App Store, Play Store, sites officiels des concurrents, rapports publics (Sensor Tower, data.ai, Statista), articles spécialisés
- Éviter : articles génériques marketing, données > 18 mois, sources non vérifiables
- Si une donnée n'est pas disponible publiquement : l'indiquer explicitement plutôt que d'inventer
```

---

## 🧠 Version 2 : Analyse stratégique et recommandations
**À utiliser après avoir obtenu les résultats de la Version 1**

```
**Contexte**
[COLLER ICI LES RÉSULTATS COMPLETS DE LA RECHERCHE VERSION 1]

**Ta mission**
Sur la base de cette recherche, produis une analyse stratégique critique et des recommandations actionnables.

### 1. Résumé exécutif et verdict
- **Décision recommandée** : GO / HOLD / NO-GO
- **Niveau de confiance** : X% (justifier pourquoi)
- **3 arguments majeurs POUR** (avec poids relatif)
- **3 arguments majeurs CONTRE** (avec poids relatif)
- **Proposition de valeur unique** (1 phrase percutante)

### 2. Positionnement et différenciation
- **UVP (Unique Value Proposition)** : Formuler en une phrase la promesse unique
- **"Pourquoi maintenant ?"** : Identifier les triggers marché/technologiques qui créent l'opportunité
- **Tableau de positionnement** :

| Dimension | Notre approche | Concurrent principal 1 | Concurrent principal 2 |
|-----------|----------------|------------------------|------------------------|
| Cible prioritaire | | | |
| Différenciateur clé | | | |
| Modèle économique | | | |
| Avantage défendable | | | |

### 3. Personas et Jobs-to-be-Done
Définir **3 personas prioritaires** avec pour chacun :
- **Profil** : Rôle, âge, contexte d'usage, niveau tech
- **Objectifs mesurables** : Que veulent-ils accomplir ?
- **Pain points actuels** : Frustrations avec solutions existantes (citer des verbatims si disponibles)
- **Jobs-to-be-Done** : Format "Quand [situation], je veux [action], pour [résultat désiré]"
- **Critères de décision** : Qu'est-ce qui les fera payer ?
- **Canaux d'accès** : Où les trouver ?

### 4. MVP et roadmap fonctionnelle
**Matrice de priorisation des fonctionnalités** (méthode MoSCoW) :

**Must-Have (MVP Phase 1 - 0-3 mois)** :
1. [Fonctionnalité] - Métrique de succès : [ex: taux d'activation > 40%]
2. [Fonctionnalité] - Métrique de succès : [...]
3-8. [...]

**Should-Have (Phase 2 - 4-6 mois)** :
[Lister avec justification et dépendances]

**Could-Have (Phase 3 - 6-12 mois)** :
[Fonctionnalités différenciatrices avancées]

**Won't-Have (hors scope initial)** :
[Fonctionnalités tentantes mais non prioritaires]

**Risques techniques identifiés** :
- [Risque 1] - Criticité : Haute/Moyenne/Faible - Plan de mitigation
- [Risque 2] - ...

**Intégrations/APIs critiques** :
- [API/Service] - Usage prévu - Coût estimé - Alternative si indisponible

### 5. Stratégie de pricing et unit economics
**Pricing recommandé** :
- Modèle : [Freemium / Abonnement / Hybride / ...]
- Prix : [Détailler les tiers]
- Justification : [Basée sur benchmarks + positionnement valeur]

**Hypothèses d'unit economics** (à valider) :

| Métrique | Cas pessimiste | Cas de base | Cas optimiste | Source/Rationale |
|----------|----------------|-------------|---------------|------------------|
| Conversion free→paid | % | % | % | |
| ARPU mensuel | € | € | € | |
| Churn mensuel | % | % | % | |
| LTV (12 mois) | € | € | € | Calculé |
| CAC target | € | € | € | |
| Ratio LTV/CAC | | | | > 3 souhaitable |

**Seuil de rentabilité estimé** :
- MRR cible : X €/mois
- Nombre d'utilisateurs payants : X
- Délai estimé : X mois post-lancement

### 6. Go-To-Market (GTM)
**Matrice de priorisation des canaux** :

| Canal | Effort (1-5) | Impact potentiel (1-5) | Coût | Délai résultats | Priorité |
|-------|--------------|------------------------|------|-----------------|----------|
| ASO (App Store Optimization) | | | | | |
| SEA (Apple Search Ads, Google) | | | | | |
| Content marketing / SEO | | | | | |
| Partnerships stratégiques | | | | | |
| Sales outbound (si B2B) | | | | | |
| Réseaux sociaux (préciser) | | | | | |
| Viral / Referral | | | | | |

**Top 3 canaux recommandés pour démarrage** :
1. [Canal] - Tactique : [...] - Budget initial : [...] - KPI : [...]
2. [Canal] - ...
3. [Canal] - ...

**Mots-clés prioritaires** (si ASO/SEA) :
- Primaires (3-5) : [...]
- Secondaires (5-10) : [...]
- Volume de recherche estimé et CPC si disponible

**Partenariats "must-have"** :
- [Partenaire/Intégration] - Rationale - Approche suggérée

### 7. Durabilité et avantages compétitifs
**Sources d'avantage cumulatif (moat)** :
- Effets de réseau : [Oui/Non - Expliquer]
- Données propriétaires : [Quel type ? Comment valoriser ?]
- Coûts de changement (switching costs) : [Élevés/Moyens/Faibles]
- Écosystème / intégrations : [Stratégie de lock-in]
- Brand / communauté : [Potentiel]

**Menaces à long terme** :
- Commoditisation : [Risque ? Défense ?]
- Plateformes (Apple/Google) : [Pourraient-elles intégrer cette fonction ?]
- Grands éditeurs (Microsoft, Google, etc.) : [Risque d'entrée ?]
- IA générative : [Impact potentiel sur le besoin ?]

### 8. Plan d'action 0-90 jours
**Phase 1 : Validation (Jours 0-30)**
- [ ] Interviews qualitatifs : 15-20 utilisateurs cibles
- [ ] Landing page + waitlist (objectif : X inscriptions)
- [ ] Tests de pricing (A/B testing sur messaging)
- [ ] Prototypes basse-fidélité + tests utilisateurs
- [ ] Validation technique (faisabilité APIs, performances)

**Phase 2 : MVP (Jours 31-60)**
- [ ] Développement fonctionnalités Must-Have (liste)
- [ ] Bêta fermée : 30-50 utilisateurs
- [ ] Implémentation analytics (events tracking)
- [ ] Intégrations critiques : [Top 3]
- [ ] Setup payment provider
- [ ] Contenu marketing initial (site, app store)

**Phase 3 : Premiers payants (Jours 61-90)**
- [ ] Lancement App Store + Play Store
- [ ] Activation canaux d'acquisition prioritaires
- [ ] Objectif : 20-50 utilisateurs payants
- [ ] Setup dashboard KPIs temps réel
- [ ] Premières itérations produit (feedback beta)
- [ ] Documentation support / FAQ

**KPIs de suivi par phase** :
[Définir 3-5 métriques critiques par phase]

### 9. Checklist des hypothèses critiques à valider
Liste des **8 hypothèses les plus risquées** qui peuvent faire échouer le projet :

1. ✅ / ⚠️ [Hypothèse] - Méthode de validation : [...] - Deadline : [...]
2. ✅ / ⚠️ [Hypothèse] - ...
[...]

**Format de sortie**
- Sections numérotées et titres clairs
- Tableaux en markdown
- ✅ pour conclusions solides / ⚠️ pour hypothèses non validées
- 🚨 pour risques critiques
- Synthèse finale : "Prochaines 3 actions immédiates"
```

---

## ⚡ Version 3 : Prompt tout-en-un (compact)
**Pour GPT-4 avec web browsing activé ou Claude avec capacités web**

```
**Rôle** : Senior Product Analyst + Market Researcher

**Mission** : Évaluer de façon critique et sourcée l'opportunité de lancer cette application mobile :
[DÉCRIRE TON IDÉE EN 2-4 PHRASES]

**Livrables attendus** :

**1. Résumé exécutif** (max 12 lignes)
- Verdict : GO / HOLD / NO-GO + confiance (X%)
- 3 raisons POUR + 3 CONTRE (hiérarchisées)
- UVP en une phrase

**2. Marché**
- TAM/SAM/SOM (méthode + sources)
- Croissance, tendances clés (12 mois)
- Segmentation principale

**3. Concurrence** (tableau)
Minimum 10 acteurs : Nom | Pays | Prix | Traction estimée | Forces | Faiblesses | Notre angle d'attaque

**4. Personas & JTBD**
3 profils détaillés (démographie, pain points, jobs-to-be-done format "Quand..., je veux..., pour...")

**5. MVP**
- Top 8 fonctionnalités Must-Have
- Métrique de succès pour chacune
- Risques techniques + dépendances APIs

**6. Pricing & Unit economics**
- Benchmark détaillé
- Recommandation pricing justifiée
- Hypothèses : Conversion, ARPU, Churn, LTV, CAC, seuil rentabilité

**7. Go-To-Market**
- 5 canaux priorisés (matrice effort/impact/coût/délai)
- Tactiques concrètes pour top 3
- Mots-clés ASO/SEA si pertinent

**8. Moat & durabilité**
- Sources d'avantage défendable
- Menaces long terme (plateformes, commoditisation, grands acteurs)

**9. Plan 0-90 jours**
- 3 phases avec jalons mesurables
- KPIs de suivi par phase

**10. Checklist validation**
8 hypothèses critiques à tester en priorité

**Contraintes qualité** :
- Recherche web approfondie (données < 18 mois)
- **12-20 sources citées** : [Titre](URL) - Date
- Distinguer faits ✅ vs estimations 📊 vs inférences 💭
- Tableaux, bullets, chiffres précis
- Objectivité : pas de langue de bois marketing
- Si donnée indisponible : le dire clairement (ne pas inventer)

**Format** : Markdown structuré, sections numérotées, visuellement scannable
```

---

## 🎯 Guide d'utilisation par outil

### Pour Perplexity (recommandé pour recherche factuelle)
1. Copier **Version 1** en remplaçant [DÉCRIRE TON IDÉE]
2. Lancer la recherche (Perplexity Pro conseillé pour sources illimitées)
3. Analyser les résultats et sources fournies
4. Copier **Version 2** avec les résultats de V1 en contexte
5. Obtenir l'analyse stratégique

**Avantages** : Excellentes citations, recherche approfondie, vérifiable

### Pour ChatGPT Plus (GPT-4 avec web browsing)
1. Activer "Browse with Bing" dans les paramètres
2. Copier **Version 3 (tout-en-un)**
3. Si réponse incomplète : "Continue en détaillant [section X]"
4. Demander précisions : "Approfondir la partie concurrence avec 5 acteurs de plus"

**Avantages** : Analyse synthétique, bon équilibre recherche/analyse

### Pour Claude (sans web, analyse pure)
1. Faire d'abord la recherche sur Perplexity (**Version 1**)
2. Copier les résultats complets dans Claude
3. Demander : "Analyse ces données avec la méthodologie de la Version 2"

**Avantages** : Analyse stratégique fine, esprit critique, structuration

---

## 📝 Checklist avant de lancer la recherche

- [ ] J'ai décrit mon idée en 2-4 phrases claires et précises
- [ ] J'ai précisé la cible principale (B2C grand public / B2B / niche spécifique)
- [ ] J'ai indiqué la géographie prioritaire (France / Europe / US / Global)
- [ ] J'ai une hypothèse de modèle économique (freemium / abonnement / one-time)
- [ ] Je sais ce que je veux valider en priorité (marché / concurrence / faisabilité technique)

---

## 🚀 Exemple d'utilisation complète

**Idée à analyser** :
"Application mobile pour les parents qui transforme les corvées ménagères des enfants en jeux avec système de récompenses, challenges famille et suivi éducatif de la responsabilisation (cible : 6-12 ans, freemium, France puis Europe)."

**Processus** :
1. Lancer Version 1 sur Perplexity → Obtenir recherche marché + concurrence
2. Lancer Version 2 sur ChatGPT avec résultats V1 → Obtenir analyse stratégique
3. Décision GO/NO-GO basée sur faits + recommandations actionnables
4. Si GO → Utiliser le plan 0-90j comme roadmap

---

## ⚠️ Limites et mise en garde

**Ce que ces prompts NE PEUVENT PAS faire** :
- Accéder à des données propriétaires (métriques internes des concurrents)
- Prédire le succès avec certitude (trop de variables externes)
- Remplacer des interviews utilisateurs réels
- Valider la faisabilité technique précise (besoin d'un audit tech dédié)

**Ce qu'ils PEUVENT faire** :
- Donner une vision factuelle du marché et de la concurrence
- Identifier les red flags évidents
- Structurer la réflexion stratégique
- Fournir une base solide pour décider GO/NO-GO
- Créer un plan d'action initial

**Recommandation finale** : Utiliser ces analyses comme **point de départ**, pas comme vérité absolue. Toujours valider les hypothèses critiques avec de vrais utilisateurs avant d'investir massivement.
