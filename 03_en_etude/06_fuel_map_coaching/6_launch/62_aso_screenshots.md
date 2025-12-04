# Guide Screenshots ASO - Plein Malin

Guide pour générer les screenshots App Store et Google Play.

---

## 1. Tailles Requises

### iOS (App Store)

| Device | Taille (px) | Status |
|--------|-------------|--------|
| iPhone 6.9" (16 Pro Max) | 1320 x 2868 | [ ] |
| iPad 13" (Pro) | 2064 x 2752 | [ ] |

### Android (Google Play)

| Device | Taille (px) | Status |
|--------|-------------|--------|
| Phone | 1080 x 1920 | [ ] |
| Feature Graphic | 1024 x 500 | [ ] |

---

## 2. Palette Couleurs

| Usage | Couleur | Hex |
|-------|---------|-----|
| Primaire (Orange) | 🟠 | `#FF9500` |
| Fond gradient 1 | | `#1A1A2E` |
| Fond gradient 2 | | `#16213E` |
| Texte | Blanc | `#FFFFFF` |
| Accent | Vert (bon prix) | `#34C759` |

---

## 3. Plan des Screenshots

| # | Écran App | Titre FR | Wireframe |
|---|-----------|----------|-----------|
| 1 | Carte avec stations | **Trouvez le carburant le moins cher** | Carte + markers |
| 2 | Détail station | **Comparez les prix en un clic** | Bottom sheet prix |
| 3 | Filtres | **Filtrez par carburant et distance** | Filtres ouverts |
| 4 | Recherche trajet | **Planifiez votre trajet** | Route + stations |
| 5 | Prix plein | **Calculez le prix de votre plein** | Détail avec prix plein |
| 6 | Premium | **Passez à Pro** | Features premium |

---

## 4. Wireframes ASCII

### Screenshot 1 - Carte (Hook)
```
┌─────────────────────────┐
│                         │
│   ╔═════════════════╗   │
│   ║   TROUVEZ LE    ║   │
│   ║   CARBURANT     ║   │
│   ║   MOINS CHER    ║   │
│   ╚═════════════════╝   │
│                         │
│   ┌─────────────────┐   │
│   │ 🔍 Rechercher   │   │
│   ├─────────────────┤   │
│   │                 │   │
│   │    🗺️ CARTE     │   │
│   │                 │   │
│   │  📍1.65€  📍1.72€│   │
│   │      📍1.58€    │   │
│   │  📍1.69€        │   │
│   │                 │   │
│   ├─────────────────┤   │
│   │ SP95 ▼ │ 10km ▼ │   │
│   └─────────────────┘   │
│                         │
│   Économisez à chaque   │
│         plein           │
│                         │
└─────────────────────────┘
```

### Screenshot 2 - Détail Station
```
┌─────────────────────────┐
│                         │
│   ╔═════════════════╗   │
│   ║   COMPAREZ      ║   │
│   ║   LES PRIX      ║   │
│   ║   EN UN CLIC    ║   │
│   ╚═════════════════╝   │
│                         │
│   ┌─────────────────┐   │
│   │    🗺️ CARTE     │   │
│   │   (floue)       │   │
│   └─────────────────┘   │
│   ┌─────────────────┐   │
│   │ TOTAL ACCESS    │   │
│   │ 123 Rue Example │   │
│   │ 📍 2.3 km       │   │
│   ├─────────────────┤   │
│   │ SP95    1.659€  │   │
│   │ SP98    1.789€  │   │
│   │ Diesel  1.549€  │   │
│   ├─────────────────┤   │
│   │ 🚗 Prix plein:  │   │
│   │    82.95€       │   │
│   ├─────────────────┤   │
│   │   [Y ALLER]     │   │
│   └─────────────────┘   │
│                         │
└─────────────────────────┘
```

### Screenshot 3 - Filtres
```
┌─────────────────────────┐
│                         │
│   ╔═════════════════╗   │
│   ║   FILTREZ PAR   ║   │
│   ║   CARBURANT     ║   │
│   ║   ET DISTANCE   ║   │
│   ╚═════════════════╝   │
│                         │
│   ┌─────────────────┐   │
│   │   CARBURANT     │   │
│   │ ┌───┐┌───┐┌───┐ │   │
│   │ │SP95││SP98││E85│ │   │
│   │ └───┘└───┘└───┘ │   │
│   │ ┌────┐┌────┐    │   │
│   │ │Dies││GPL │    │   │
│   │ └────┘└────┘    │   │
│   ├─────────────────┤   │
│   │   DISTANCE      │   │
│   │ ●────────○      │   │
│   │ 5km      50km   │   │
│   ├─────────────────┤   │
│   │   FRAÎCHEUR     │   │
│   │ ○ < 24h         │   │
│   │ ○ < 3 jours     │   │
│   │ ● Tous          │   │
│   └─────────────────┘   │
│                         │
└─────────────────────────┘
```

### Screenshot 4 - Recherche Trajet
```
┌─────────────────────────┐
│                         │
│   ╔═════════════════╗   │
│   ║   PLANIFIEZ     ║   │
│   ║   VOTRE TRAJET  ║   │
│   ╚═════════════════╝   │
│                         │
│   ┌─────────────────┐   │
│   │ 📍 Paris        │   │
│   │ 📍 Lyon         │   │
│   │   [RECHERCHER]  │   │
│   └─────────────────┘   │
│   ┌─────────────────┐   │
│   │                 │   │
│   │  ══════════     │   │
│   │ 📍    📍    📍  │   │
│   │  ════════════   │   │
│   │                 │   │
│   └─────────────────┘   │
│   ┌─────────────────┐   │
│   │ 1. Total  1.58€ │   │
│   │    +2km détour  │   │
│   │ 2. Shell  1.62€ │   │
│   │    sur trajet   │   │
│   └─────────────────┘   │
│                         │
└─────────────────────────┘
```

### Screenshot 5 - Prix du Plein
```
┌─────────────────────────┐
│                         │
│   ╔═════════════════╗   │
│   ║   CALCULEZ      ║   │
│   ║   VOTRE PLEIN   ║   │
│   ╚═════════════════╝   │
│                         │
│   ┌─────────────────┐   │
│   │   VOTRE VÉHICULE│   │
│   │                 │   │
│   │   🚗 Berline    │   │
│   │   ⛽ 50L        │   │
│   │   🛢️ SP95       │   │
│   └─────────────────┘   │
│   ┌─────────────────┐   │
│   │ Station A       │   │
│   │ 1.659€/L        │   │
│   │ ═══════════════ │   │
│   │ PLEIN: 82.95€   │   │
│   ├─────────────────┤   │
│   │ Station B       │   │
│   │ 1.789€/L        │   │
│   │ ═══════════════ │   │
│   │ PLEIN: 89.45€   │   │
│   │                 │   │
│   │ 💰 -6.50€       │   │
│   └─────────────────┘   │
│                         │
└─────────────────────────┘
```

### Screenshot 6 - Premium
```
┌─────────────────────────┐
│                         │
│   ╔═════════════════╗   │
│   ║  PLEIN MALIN    ║   │
│   ║      PRO        ║   │
│   ╚═════════════════╝   │
│                         │
│   ┌─────────────────┐   │
│   │                 │   │
│   │   ✓ Recherche   │   │
│   │     France      │   │
│   │     entière     │   │
│   │                 │   │
│   │   ✓ Filtres     │   │
│   │     avancés     │   │
│   │                 │   │
│   │   ✓ Trajets     │   │
│   │     illimités   │   │
│   │                 │   │
│   │   ✓ Sans pub    │   │
│   │                 │   │
│   └─────────────────┘   │
│                         │
│   ┌─────────────────┐   │
│   │  9.99€ / an     │   │
│   │  [S'ABONNER]    │   │
│   └─────────────────┘   │
│                         │
└─────────────────────────┘
```

---

## 5. Prompts Génération IA

### Prompt Midjourney - Mockup iPhone

```
Professional app store screenshot, iPhone 15 Pro Max mockup,
fuel station map app with orange markers showing gas prices,
dark gradient background #1A1A2E to #16213E,
clean minimal iOS UI, marketing style,
French text "Trouvez le carburant moins cher",
8k quality render
--ar 9:19 --v 6
```

### Prompt Background

```
Abstract gradient background for mobile app marketing,
dark blue to purple gradient, subtle fuel/energy theme,
modern clean aesthetic, smooth transition,
8k resolution, vertical mobile format
--ar 9:19 --v 6
```

---

## 6. Checklist Production

### Préparation
- [ ] Screenshots bruts de l'app capturés
- [ ] Template Figma créé (1290x2796)
- [ ] Textes validés

### Production
- [ ] Screenshot 1 - Carte (Hook)
- [ ] Screenshot 2 - Détail station
- [ ] Screenshot 3 - Filtres
- [ ] Screenshot 4 - Recherche trajet
- [ ] Screenshot 5 - Prix plein
- [ ] Screenshot 6 - Premium

### Export
- [ ] 1320x2868 (iPhone 6.9")
- [ ] 2064x2752 (iPad 13")
- [ ] 1080x1920 (Android)
- [ ] Feature Graphic 1024x500

---

## 7. Textes Screenshots - Variations

### Screenshot 1 - Carte (Hook)
| Option | Titre | Sous-titre |
|--------|-------|------------|
| A | **Trouvez le carburant le moins cher** | Économisez à chaque plein |
| B | **Le plein malin, c'est ici** | Prix en temps réel près de chez vous |
| C | **Fini de payer trop cher** | Comparez les prix autour de vous |
| D | **Économisez jusqu'à 10€ par plein** | 10 000 stations comparées |

### Screenshot 2 - Détail Station
| Option | Titre | Sous-titre |
|--------|-------|------------|
| A | **Comparez les prix en un clic** | Toutes les infos de la station |
| B | **Tous les prix, une station** | Horaires, services, navigation |
| C | **Choisissez en connaissance** | Prix détaillés par carburant |

### Screenshot 3 - Filtres
| Option | Titre | Sous-titre |
|--------|-------|------------|
| A | **Filtrez par carburant et distance** | Trouvez exactement ce qu'il vous faut |
| B | **Votre carburant, votre périmètre** | Filtres intelligents |
| C | **SP95, Diesel, E85...** | Tous les carburants, un seul geste |

### Screenshot 4 - Recherche Trajet
| Option | Titre | Sous-titre |
|--------|-------|------------|
| A | **Planifiez votre trajet** | Stations les moins chères sur votre route |
| B | **Paris → Lyon ? On gère** | Les meilleurs arrêts sur votre route |
| C | **Voyagez malin** | Économisez même sur autoroute |
| D | **Le bon plein au bon moment** | Stations optimales sur votre trajet |

### Screenshot 5 - Prix du Plein
| Option | Titre | Sous-titre |
|--------|-------|------------|
| A | **Calculez le prix de votre plein** | Comparez et économisez |
| B | **82€ ou 89€ ?** | Voyez la différence en euros |
| C | **Votre réservoir, votre budget** | Prix du plein instantané |

### Screenshot 6 - Premium
| Option | Titre | Sous-titre |
|--------|-------|------------|
| A | **Passez à Pro** | Débloquez toutes les fonctionnalités |
| B | **Plein Malin Pro** | France entière, trajets illimités |
| C | **9,99€/an = des dizaines d'€ économisés** | L'investissement le plus rentable |
| D | **Devenez un pro du plein** | Sans limite, sans pub |

---

## 8. Sélection Finale

| # | Écran | Titre choisi | Sous-titre choisi |
|---|-------|--------------|-------------------|
| 1 | Carte | [ ] | [ ] |
| 2 | Détail | [ ] | [ ] |
| 3 | Filtres | [ ] | [ ] |
| 4 | Trajet | [ ] | [ ] |
| 5 | Prix plein | [ ] | [ ] |
| 6 | Premium | [ ] | [ ] |
