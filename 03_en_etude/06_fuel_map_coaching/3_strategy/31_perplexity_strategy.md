# FuelMap - Analyse Stratégique

## Pivot : Fuel Finder + Gamification (sans coaching temps réel)

**Raison du pivot** : Le coaching éco-conduite nécessite un suivi GPS en background permanent, ce qui implique :
- Drain batterie significatif
- Permissions iOS/Android complexes (background location)
- UX friction élevée (popups permissions)
- Complexité technique accrue

**Nouveau positionnement** : App simple de comparaison prix carburant avec gamification communautaire.

---

## 1. Verdict

### GO CONDITIONNEL - Confiance : 55%

| Pour | Contre |
|------|--------|
| Marché massif (1.4Md conducteurs monde) | Waze/Google Maps dominent (gratuit, 1B+ users) |
| Monétisation claire (ads + premium) | Crowdsourcing = chicken-and-egg |
| Tech simple sans background GPS | Différenciation faible vs GasBuddy |
| Coûts dev faibles (~50K€) | CAC élevé B2C ($3-8) |

**Condition GO** : Trouver un angle différenciant fort (niche géo, UX premium, ou partenariat pétrolier)

---

## 2. Positionnement

### UVP (Unique Value Proposition)

> "L'app carburant la plus simple : trouve, compare, économise - en 3 taps."

### Pourquoi maintenant ?

- Prix carburant volatils (inflation 2022-2024)
- Waze/Google Maps = features carburant secondaires, pas optimisées
- GasBuddy = US-centric, UX datée
- Opportunité Europe/France : pas de leader clair

### Positioning vs Concurrence

| Dimension | FuelMap (nous) | Waze | GasBuddy | Fuelio |
|-----------|----------------|------|----------|--------|
| **Focus** | Carburant only | Navigation + carburant | Carburant + rewards US | Tracking perso |
| **UX** | Simple, 3 taps | Complexe, multi-features | Datée, cluttered | Geek, manuel |
| **Géo** | France/Europe | Global | USA principalement | Global |
| **Prix** | Freemium €9.99/an | Gratuit (ads) | Freemium $7.99/mo | €9/an |
| **Différenciateur** | Gamification + communauté locale | Network effect | Rewards (Walmart) | Privacy-first |

### Angle d'attaque recommandé

**Option A - Niche France/Europe** : "Le GasBuddy français" - focus qualité data France
**Option B - UX Premium** : "L'app carburant sans friction" - design épuré, pas de bloat
**Option C - Communauté locale** : Gamification forte, leaderboards par ville/région

Recommandation : **Option A + C combinées** = Focus France + gamification locale

---

## 3. Personas & Jobs-to-be-Done

### Persona 1 : Marie, 35 ans - "L'économe quotidienne"

**Profil** :
- Salariée, 2 enfants, banlieue parisienne
- 40km/jour domicile-travail
- Budget carburant : 200-300€/mois
- Smartphone : iPhone, apps basiques

**Pain points** :
1. "Je ne sais jamais où est le moins cher près de chez moi"
2. "J'oublie toujours de regarder les prix avant d'être en réserve"
3. "Les apps existantes sont trop compliquées"

**JTBD** : "Quand je dois faire le plein, je veux trouver la station la moins chère en 10 secondes, pour économiser sans perdre de temps."

**Willingness to pay** : €0-10/an max, sensible au prix

---

### Persona 2 : Thomas, 28 ans - "Le gamer compétitif"

**Profil** :
- Commercial itinérant, 1500km/semaine
- Note de frais entreprise mais bonus si économies
- Smartphone : Android, power user
- Aime les apps gamifiées (Strava, Duolingo)

**Pain points** :
1. "Je fais le plein 3x/semaine, ça représente beaucoup"
2. "J'aimerais tracker mes économies vs mes collègues"
3. "Les apps carburant sont ennuyeuses"

**JTBD** : "Quand je suis sur la route, je veux optimiser chaque plein et voir mes économies cumulées, pour maximiser mon bonus et me sentir malin."

**Willingness to pay** : €10-20/an, prêt à payer pour features avancées

---

### Persona 3 : Jean-Pierre, 55 ans - "Le contributeur local"

**Profil** :
- Retraité actif, petite ville
- Fait le plein 1x/semaine
- Connaît toutes les stations du coin
- Aime aider la communauté

**Pain points** :
1. "Les prix affichés sur les apps sont souvent faux"
2. "Personne ne met à jour les petites stations"
3. "J'aimerais que ma contribution soit reconnue"

**JTBD** : "Quand je passe devant une station, je veux signaler le prix facilement, pour aider les autres et être reconnu comme contributeur fiable."

**Willingness to pay** : €0, mais forte valeur comme data contributor

---

## 4. MVP Features

### Top 8 Must-Have

| # | Feature | Métrique succès | Effort |
|---|---------|-----------------|--------|
| M1 | **Carte stations** avec prix temps réel | 80% users trouvent station <30s | M |
| M2 | **Filtre carburant** (SP95, Diesel, E85...) | 95% users filtrent correctement | S |
| M3 | **Signalement prix** par users (crowdsourcing) | 100+ signalements/jour @ 10K MAU | M |
| M4 | **Itinéraire** vers station (deeplink Maps) | 60% users utilisent navigation | S |
| M5 | **Historique perso** des pleins | 40% users loggent leurs pleins | M |
| M6 | **Économies calculées** vs moyenne | 70% users voient leurs économies | S |
| M7 | **Gamification basique** (badges, streak) | 30% users ont 1+ badge | M |
| M8 | **Notifications prix bas** (zone géo) | 20% users activent notifs | M |

### Risques techniques

| Risque | Impact | Mitigation |
|--------|--------|------------|
| Data prix initiale (cold start) | Bloquant | Scraper data.gouv.fr (prix officiels France) |
| Précision GPS foreground | Moyen | Acceptable sans background tracking |
| Rate limits APIs maps | Moyen | OpenStreetMap gratuit, Mapbox en backup |

### Intégrations/APIs critiques

| API | Usage | Coût |
|-----|-------|------|
| **data.gouv.fr** | Prix officiels France | Gratuit |
| **OpenStreetMap/Mapbox** | Cartographie | Gratuit / $0-500/mo |
| **Apple Maps / Google Maps** | Deeplink navigation | Gratuit |
| **Firebase/Supabase** | Backend + Auth | $0-100/mo |
| **RevenueCat** | Subscriptions | 1% revenue |

---

## 5. Unit Economics

| Métrique | Hypothèse | Rationale |
|----------|-----------|-----------|
| **Pricing** | Gratuit + €9.99/an Premium | Aligné Fuelio, accessible |
| **Premium features** | Sans pub, alertes illimitées, stats avancées | Valeur claire |
| **Conversion free→paid** | 3-5% | Benchmark apps utilitaires |
| **Churn annuel** | 40-50% | Apps commodité = churn élevé |
| **LTV** | €15-20 (sur 2 ans) | €10 × 1.5-2 ans rétention |
| **CAC target** | <€5 | ASO + viral uniquement |
| **LTV/CAC** | 3-4:1 | Viable si organic |
| **Users pour €10K MRR** | ~12K paying users | €10K / €0.83/mo |

### Modèle revenue

| Source | % Revenue Y1 | Notes |
|--------|--------------|-------|
| Ads (AdMob) | 70% | €2-5 CPM, majorité users free |
| Premium subs | 25% | 3-5% conversion |
| Affiliations stations | 5% | Future : partenariats pétroliers |

### Seuil rentabilité

- **Coûts fixes** : ~€500/mo (hosting, APIs, Apple/Google fees)
- **Break-even** : ~50K MAU (ads) ou ~600 paying users (subs)

---

## 6. Plan 0-90 Jours

### Phase 1 (0-30j) : Validation

- [ ] Landing page + waitlist (objectif : 500 emails)
- [ ] 20 interviews users (personas 1, 2, 3)
- [ ] Tester willingness-to-pay (survey pricing)
- [ ] Analyser data.gouv.fr (qualité data, coverage)
- [ ] Benchmark UX : installer Waze, GasBuddy, Fuelio
- [ ] Maquettes Figma (5 écrans clés)

**Critère GO/NO-GO** : 300+ emails waitlist + 70% interviews confirment pain point

### Phase 2 (31-60j) : MVP

- [ ] Setup projet Flutter + Supabase
- [ ] Intégrer data.gouv.fr (scraper + refresh daily)
- [ ] Carte + filtres + détail station
- [ ] Auth simple (email/Google)
- [ ] Signalement prix (crowdsourcing)
- [ ] TestFlight/Internal testing (50 beta users)

**Critère succès** : App fonctionnelle, 50 beta testers actifs

### Phase 3 (61-90j) : Soft Launch

- [ ] Gamification v1 (badges premier plein, contributeur, streak)
- [ ] Notifications prix bas (zone géo)
- [ ] Historique + économies calculées
- [ ] Intégrer AdMob (free users)
- [ ] ASO optimisé (keywords, screenshots)
- [ ] Soft launch France (objectif : 1K downloads)

**Critère succès** : 1K downloads, 200 MAU, 50 signalements prix/jour

---

## 7. Hypothèses Critiques à Valider

| # | Hypothèse | Méthode validation | Deadline |
|---|-----------|-------------------|----------|
| 1 | [?] Users veulent une app dédiée carburant (vs Waze) | Interviews + waitlist conversion | J+30 |
| 2 | [?] Data.gouv.fr suffisante en qualité/fraîcheur | Analyse technique + comparaison terrain | J+15 |
| 3 | [?] Users prêts à signaler les prix (crowdsourcing) | Beta test engagement rate | J+60 |
| 4 | [?] Conversion freemium 3-5% atteignable | A/B test paywall | J+90 |
| 5 | [?] CAC <€5 via ASO seul | Mesure post-launch | J+90 |
| 6 | [?] Gamification augmente rétention +20% | Cohorte avec/sans badges | J+90 |
| 7 | [?] Différenciation suffisante vs Waze gratuit | NPS + churn rate | J+120 |
| 8 | [?] Marché France assez grand (vs expansion EU) | Revenue/MAU France seule | J+180 |

---

## 8. Recommandation Finale

### HOLD - En attente validation hypothèses 1-3

**Risque principal** : Différenciation insuffisante vs Waze (gratuit, déjà installé).

**Pour passer en GO** :
1. Valider que 300+ personnes s'inscrivent sur waitlist "app carburant France"
2. Confirmer que data.gouv.fr est exploitable (fraîcheur <24h)
3. Identifier 1 angle différenciant fort (communauté locale ? UX ? niche E85 ?)

**Alternative si NO-GO** : Pivoter vers niche E85/électrique (moins de concurrence) ou B2B flottes PME.

---

**Dernière mise à jour** : 29 novembre 2025
