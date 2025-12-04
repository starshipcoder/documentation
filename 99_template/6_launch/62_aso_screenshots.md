# Guide Screenshots ASO - [NOM APP]

Guide complet pour générer les screenshots App Store et Google Play.

---

## 1. Tailles Requises

### iOS (App Store)

| Device | Taille (px) | Obligatoire |
|--------|-------------|-------------|
| iPhone 6.9" (16 Pro Max) | 1320 x 2868 | ✅ Oui |
| iPad 13" (Pro) | 2064 x 2752 | ⚠️ Si iPad |

### Android (Google Play)

| Device | Taille (px) | Obligatoire |
|--------|-------------|-------------|
| Phone | 1080 x 1920 (min) | ✅ Oui |
| Tablet 7" | 1200 x 1920 | ⚠️ Si tablet |
| Tablet 10" | 1920 x 1200 | ⚠️ Si tablet |

### Feature Graphic (Android)
| Asset | Taille |
|-------|--------|
| Feature Graphic | 1024 x 500 |

---

## 2. Structure des Screenshots

### Recommandations
- **Quantité** : 6-8 screenshots (le 1er est le plus important)
- **Ordre** : Hook → Features → Social proof → CTA
- **Texte** : Max 5-7 mots par titre
- **Police** : Grande, lisible, contrastée

### Template Visuel

```
┌─────────────────────────┐
│                         │
│   ┌─────────────────┐   │
│   │    TITRE HOOK   │   │
│   │   (5-7 mots)    │   │
│   └─────────────────┘   │
│                         │
│   ┌─────────────────┐   │
│   │                 │   │
│   │                 │   │
│   │   SCREENSHOT    │   │
│   │   DE L'APP      │   │
│   │   (mockup)      │   │
│   │                 │   │
│   │                 │   │
│   └─────────────────┘   │
│                         │
│      [Sous-titre]       │
│                         │
└─────────────────────────┘
```

---

## 3. Plan des Screenshots

| # | Écran App | Titre (FR) | Titre (EN) | Wireframe |
|---|-----------|------------|------------|-----------|
| 1 | [Écran principal] | [Hook accrocheur] | [Hook EN] | Voir ci-dessous |
| 2 | [Feature 1] | [Bénéfice 1] | [Benefit 1] | |
| 3 | [Feature 2] | [Bénéfice 2] | [Benefit 2] | |
| 4 | [Feature 3] | [Bénéfice 3] | [Benefit 3] | |
| 5 | [Premium/Stats] | [Value prop] | [Value prop] | |
| 6 | [CTA] | [Call to action] | [CTA EN] | |

---

## 4. Wireframes ASCII

### Screenshot 1 - Hook Principal
```
┌─────────────────────────┐
│                         │
│   ╔═════════════════╗   │
│   ║  [TITRE HOOK]   ║   │
│   ╚═════════════════╝   │
│                         │
│   ┌─────────────────┐   │
│   │ ┌─────────────┐ │   │
│   │ │   HEADER    │ │   │
│   │ ├─────────────┤ │   │
│   │ │             │ │   │
│   │ │   CONTENU   │ │   │
│   │ │  PRINCIPAL  │ │   │
│   │ │             │ │   │
│   │ ├─────────────┤ │   │
│   │ │   FOOTER    │ │   │
│   │ └─────────────┘ │   │
│   └─────────────────┘   │
│                         │
└─────────────────────────┘
```

### Screenshot 2-4 - Features
```
┌─────────────────────────┐
│                         │
│   ╔═════════════════╗   │
│   ║ [BÉNÉFICE #X]   ║   │
│   ╚═════════════════╝   │
│                         │
│   ┌─────────────────┐   │
│   │                 │   │
│   │   [ÉCRAN APP    │   │
│   │    MONTRANT     │   │
│   │   LA FEATURE]   │   │
│   │                 │   │
│   └─────────────────┘   │
│                         │
│   ┌─────────────────┐   │
│   │ Sous-texte      │   │
│   │ explicatif      │   │
│   └─────────────────┘   │
│                         │
└─────────────────────────┘
```

### Screenshot 5 - Social Proof / Stats
```
┌─────────────────────────┐
│                         │
│   ╔═════════════════╗   │
│   ║ "[TÉMOIGNAGE]"  ║   │
│   ╚═════════════════╝   │
│                         │
│   ┌─────────────────┐   │
│   │  ⭐⭐⭐⭐⭐        │   │
│   │  "Super app!"   │   │
│   │  - Utilisateur  │   │
│   └─────────────────┘   │
│                         │
│   ┌───┐ ┌───┐ ┌───┐   │
│   │10K│ │4.8│ │#1 │   │
│   │DL │ │ ★ │ │Cat│   │
│   └───┘ └───┘ └───┘   │
│                         │
└─────────────────────────┘
```

### Screenshot 6 - CTA
```
┌─────────────────────────┐
│                         │
│   ╔═════════════════╗   │
│   ║ [TÉLÉCHARGEZ    ║   │
│   ║  MAINTENANT!]   ║   │
│   ╚═════════════════╝   │
│                         │
│   ┌─────────────────┐   │
│   │                 │   │
│   │   [MONTAGE      │   │
│   │    FEATURES]    │   │
│   │                 │   │
│   └─────────────────┘   │
│                         │
│   ┌─────────────────┐   │
│   │   ✓ Feature 1   │   │
│   │   ✓ Feature 2   │   │
│   │   ✓ Feature 3   │   │
│   └─────────────────┘   │
│                         │
└─────────────────────────┘
```

---

## 5. Prompts Génération IA

### Prompt Midjourney / DALL-E - Style Mockup

```
Professional app store screenshot mockup, iPhone 15 Pro Max,
[DESCRIPTION ÉCRAN], clean minimal UI,
gradient background [COULEUR1] to [COULEUR2],
marketing style, high quality render, 8k
--ar 9:19 --v 6
```

### Prompt pour Background Gradient

```
Abstract gradient background for mobile app marketing,
smooth transition from [COULEUR1] to [COULEUR2],
subtle geometric shapes, modern clean aesthetic,
8k resolution, vertical format
--ar 9:19 --v 6
```

### Prompt Figma/Canva - Texte

```
Créer un screenshot ASO avec :
- Fond : gradient [COULEUR1] → [COULEUR2]
- Titre : "[TEXTE]" en [POLICE] bold, blanc, 80px
- Mockup iPhone centré avec screenshot de l'app
- Sous-titre : "[SOUS-TEXTE]" en 40px, blanc 80%
- Dimensions : 1290x2796px
```

---

## 6. Checklist Production

### Préparation
- [ ] Screenshots bruts de l'app (toutes les pages)
- [ ] Palette couleurs définie
- [ ] Titres/textes validés (FR + EN si besoin)
- [ ] Template Figma/Canva créé

### Production
- [ ] Screenshot 1 - Hook
- [ ] Screenshot 2 - Feature A
- [ ] Screenshot 3 - Feature B
- [ ] Screenshot 4 - Feature C
- [ ] Screenshot 5 - Social proof
- [ ] Screenshot 6 - CTA

### Export
- [ ] Export 1320x2868 (iPhone 6.9")
- [ ] Export 2064x2752 (iPad 13") - si iPad
- [ ] Export 1080x1920 (Android)
- [ ] Feature Graphic 1024x500 (Android)

### Validation
- [ ] Textes lisibles à petite taille
- [ ] Couleurs cohérentes
- [ ] Mockups alignés
- [ ] Pas de texte coupé

---

## 7. Outils Recommandés

| Outil | Usage | Lien |
|-------|-------|------|
| **Figma** | Design screenshots | figma.com |
| **Canva** | Templates rapides | canva.com |
| **Rotato** | Mockups 3D | rotato.app |
| **Previewed** | Mockups templates | previewed.app |
| **Shotsnapp** | Mockups gratuits | shotsnapp.com |
| **MockuPhone** | Mockups devices | mockuphone.com |

---

## 8. Bonnes Pratiques

### DO ✅
- Texte gros et lisible
- Bénéfices utilisateur (pas features)
- Premier screenshot = hook puissant
- Contraste élevé
- Cohérence visuelle

### DON'T ❌
- Trop de texte
- Screenshots bruts sans contexte
- Texte petit illisible
- Mélanger les styles
- Ignorer les guidelines Apple/Google
