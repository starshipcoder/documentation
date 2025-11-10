# ❤️ Heart Rate Monitor - Zone 2 Training

## 💡 L'Idée en 3 Lignes

Application mobile de **coaching Zone 2 running avec alertes audio temps réel** qui guide les débutants à rester dans leur zone aérobie optimale (fréquence cardiaque cible) via feedback vocal ("Zone 2, ralentis", "Parfait, reste là"), intégration Apple Health/Garmin/Polar.

**Problème résolu** : Les runners veulent faire du Zone 2 training (+850% search growth 3 ans, Huberman/Kipchoge trend) mais Strava = confusing beginners, Garmin = steep learning curve, WHOOP = trop cher ($25-30/mo).

**Cible** : New runners 18-35 ans, débutants structured training, owns smartwatch, willing pay $5-10/mo guidance.

---

## 🎯 Value Proposition

"**Zone 2 training made simple for beginners**. Real-time audio coaching pendant ta course : on te dit quand ralentir, quand accélérer. $7.99/mois, pas $30 comme WHOOP."

---

## 💰 Modèle Économique

**Freemium tiered** :
- Free : Basic zone tracking (1-week history), manual input
- Premium $7.99/mois : Wearable sync (Apple/Garmin/Polar), **real-time audio alerts**, AI weekly insights, unlimited history
- Premium Annual $59.99/an : -25% discount

---

## 🚀 Pourquoi Maintenant ?

- ✅ Zone 2 trend explosif : +850% search growth 2021-2024 (10K monthly searches US)
- ✅ Validation scientifique (Kipchoge, Huberman) = sustained demand, not fad
- ✅ Gap "beginners + affordable" : Strava confusing, Garmin complex, WHOOP expensive
- ✅ 71% users willing pay premium fitness apps

---

## ⚠️ ALERTE CRITIQUE - Retention

**Brutal retention crisis fitness apps** :
- 77% churn dans 3 jours
- 92% @ 30 jours
- Industry avg 8-12% Day-30 retention
- **Target minimum : >20% @ 30 jours**

Need audio coaching + gamification + first-week engagement hooks

---

## ⚡ Difficulté Technique

**5/10** - Wearable APIs integration + audio TTS real-time + algoritmes heart rate zones

---

## 🎨 Stack Technique Recommandée

- **Frontend** : Flutter
- **Camera** : camera package (PPG heart rate detection alternative)
- **Algo** : Algorithme PPG (Photoplethysmography) ou heart_bpm package
- **Audio** : audioplayers (pour alertes vocales temps réel)
- **Health** : health package (iOS HealthKit + Android Google Fit)
- **Wearable APIs** : Garmin Connect API, Polar Accesslink API
- **Storage** : shared_preferences

---

**Coûts mensuels estimés** : $20-50/mois
