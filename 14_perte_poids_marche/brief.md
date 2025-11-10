# 🚶 App Perte de Poids par la Marche

## 💡 L'Idée en 3 Lignes

Application mobile **"walk-specific weight loss"** combinant step counter (Apple Health/Google Fit sync), weight tracking + progress charts, gamification daily challenges (10K steps, streaks), community leaderboards (friends/family teams), approche "douce" vs apps fitness agressives.

**Problème résolu** : Strava (135M users) = running-centric. Noom ($1B+ ARR) = cher ($17-70/mo) + not gamified walking. MyFitnessPal = nutrition-centric, weak walk features. Pacer = pure walk tracker MAIS no perte de poids angle, weak monetization. Gap = walk + weight loss + gamification + affordable.

**Cible** : Beginners sedentary→active 25-55 ans, people post-injury (low-impact), elderly health-conscious, budget-conscious (<$10/mo).

---

## 🎯 Value Proposition

"**Lose weight by walking, made simple**. Track steps, set daily challenges, compete with friends. Gamification addictive. $6.99/mois (vs Noom $17-70). Accessible à tous, no gym needed."

---

## 💰 Modèle Économique

**Freemium gamifié** :
- Free : Step counter basique, 7-day history
- Premium $6.99/mois : Unlimited history, weight tracking, advanced analytics, community challenges, ad-free
- Annual $59.99/an : -15% discount

---

## 🚀 Pourquoi Maintenant ?

- ✅ Market size : $6.27B TAM (2024), CAGR 14-17%
- ✅ Gap "walk-specific weight loss" underserved (Strava running, Noom expensive, Pacer weak)
- ✅ Sweatcoin proof : 190M users, +19.5% steps impact = gamification works
- ✅ Wearable ecosystem : 64% US users trackers = table-stakes integration feasible

---

## ⚠️ ALERTE CRITIQUE - Retention

**Brutal retention crisis fitness apps** :
- 77% churn dans 3 jours
- Need gamification excellence (not just step counter)
- Competition intense : Strava 135M, MyFitnessPal 220M, Noom $1B+ ARR

---

## ⚡ Difficulté Technique

**4/10** - Simple techniquement (step counter + charts + gamification)

---

## 🎨 Stack Technique Recommandée

- **Frontend** : Flutter
- **Backend** : Supabase
- **Pedometer** : pedometer package
- **Health data** : health package (HealthKit + Google Fit)
- **Gamification** : Challenges, streaks, badges locaux
- **Social** : Classements, partage (share_plus)
- **Charts** : fl_chart
- **Push** : firebase_messaging (rappels quotidiens)

---

**Coûts mensuels estimés** : $50-150/mois
