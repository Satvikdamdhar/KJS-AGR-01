# Kisan Suvidha — UI Reverse-Engineering Blueprint

## 1. Application Overview

Platform: Kisan Suvidha
Type: Government agricultural information and service portal
Reference: Kisan Suvidha homepage screenshot (kisansuvidha.gov.in)

The page groups agriculture-related services into an icon-based grid so users can navigate to schemes, insurance, machinery, irrigation, training, advisory, and other resources from a single dashboard.

---

## 2. Layout Geometry

Four-region structure, left to right / top to bottom:

1. **Top Header** — full-width bar
   - Government of India emblem (far left)
   - "Kisan Suvidha" title + tagline (center)
   - NIC (National Informatics Centre) logo (far right)

2. **Left Utility Rail** — narrow vertical strip, fixed to left edge of content area
   - Home icon
   - Info ("i") icon
   - Support (headset) icon
   - Icons stacked vertically, evenly spaced, no labels

3. **Main Content Panel** — largest region, light-grey background
   - Category tabs (top-left): "Agriculture" (active) / "Animal Husbandry" (inactive)
   - Attribution line (top-right of panel): "An initiative of National Informatics Centre, MeitY"
   - Service grid below: 3 rows × 5 columns = 15 tiles

4. **Right Utility Panel** — narrow column, white background
   - Search bar (top)
   - Language selector below it
   - Kisan Suvidha farmer mascot illustration (curved logo text + character graphic)
   - Facebook / Twitter icons
   - "Visitor Count: 0" text at bottom

---

## 3. Typography Hierarchy

| Level | Element | Style |
|---|---|---|
| 1 | "Kisan Suvidha" main title | Large, bold, dark red/maroon |
| 2 | Service tile labels (e.g. "PM-KISAN") | Bold, small, black, centered under icon |
| 3 | Tagline ("A Smart App for Farmers") | Small, regular weight, centered under title |
| 3 | Attribution line | Small, italic, maroon |
| 3 | "Visitor Count: 0" | Small, regular, grey/black |

Hierarchy prioritizes platform identity (Level 1) and service labels (Level 2) over supporting metadata (Level 3).

---

## 4. Category Tabs

- **Agriculture** (active): filled dark red/maroon pill, white text
- **Animal Husbandry** (inactive): white/outlined pill, dark red border and text
- Positioned top-left of the main panel, side by side

Behavior: selecting a tab is expected to swap the service grid content below it.

---

## 5. Service Grid — Component Inventory

15 tiles, 3 rows of 5, each tile = circular pastel background + icon + bold label underneath.

**Row 1:** PM-KISAN (green), Crop Insurance (pink), Agriculture Marketing and Procurement (purple), KVK (khaki/tan), Organic Farming (green)

**Row 2:** Seeds (purple), Farm Machinery (blue), Horticulture (khaki/tan), Trainings and Extension Services (pink), Government Schemes (pink)

**Row 3:** Directory Services (orange), Advisory Services (pink), DD Kisan (purple), PMKSY-Micro Irrigation (purple), ICAR (green)

---

## 6. Component Behavior

### ServiceTile
- Structure: circular icon container → icon → label
- Click/tap: navigates to the corresponding service or external portal
- Hover: expected visual feedback (not visible in static screenshot — inferred from standard pattern)
- Keyboard: should be focusable for accessibility (inferred, not visible in screenshot)

### SearchBar
- Icon + text input, placeholder "Search"
- Expected to filter/surface matching services

### LanguageSelector
- Globe icon + dropdown, default shows "English"
- Expected to localize visible labels on selection

### Left Rail Icons
- Home: returns to this dashboard view
- Info: opens platform information
- Support: opens help/contact

*(Note: behaviors for Search, Language, and left-rail icons are inferred from standard UI conventions — the screenshot only shows their static state, not their interaction result.)*

---

## 7. Primary Interaction Nodes

- Switch category (Agriculture / Animal Husbandry)
- Open any of the 15 service tiles
- Enter a search query
- Change language
- Open Facebook / Twitter links
- (Left rail) Home / Info / Support

---

## 8. Component Blueprint (tree)

```
App
├── Header
│   ├── GovernmentEmblem
│   ├── AppTitle + Tagline
│   └── NICLogo
├── LeftRail
│   ├── HomeIcon
│   ├── InfoIcon
│   └── SupportIcon
├── MainPanel
│   ├── CategoryTabs (Agriculture | Animal Husbandry)
│   ├── AttributionLabel
│   └── ServiceGrid
│       └── ServiceTile × 15
└── RightPanel
    ├── SearchBar
    ├── LanguageSelector
    ├── FarmerMascotBranding
    ├── SocialLinks (Facebook, Twitter)
    └── VisitorCounter
```
