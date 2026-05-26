# 🦖 Deep Time Explorer - Struttura Completa con Routing

## 📌 Overview Progetto

**Deep Time Explorer** è un sito web multi-pagina che esplora la storia della Terra e della vita:

1. **Home Page** → Presentazione + CTA
2. **Slider Page** → Carousel per sfogliare 5 ere
3. **Era Pages** (5 pagine) → Una per ogni era geologicach bar (ce
4. **Species Pages** (25 pagine) → 5 specie per era + dettagli

**Total pagine**: 1 (home) + 1 (slider) + 5 (ere) + 25 (specie) = **32 pagine generate dinamicamente**

---

## 🗺️ ROUTING MAP

```
/                          → Home page
/explorer                  → Slider page (5 ere)
/era/:eraId                → Pagina singola era
  ├── /era/archean         → Archean Eon
  ├── /era/proterozoic     → Proterozoic Eon
  ├── /era/paleozoic       → Paleozoic Era
  ├── /era/mesozoic        → Mesozoic Era
  └── /era/cenozoic        → Cenozoic Era
/era/:eraId/species/:speciesId → Pagina singola specie
  ├── /era/mesozoic/species/t-rex
  ├── /era/mesozoic/species/triceratops
  └── ... (5 per era)
```

---

## 🏗️ ARCHITETTURA COMPLETA

### **Struttura Cartelle**

```
deep-time-explorer/
├── src/
│   ├── components/
│   │   ├── Header.jsx                ← Logo + Navigation
│   │   ├── Footer.jsx                ← Link footer
│   │   ├── Navigation.jsx            ← Nav breadcrumb
│   │   ├── EraCard.jsx               ← Singola era card
│   │   ├── SpeciesCard.jsx           ← Singola specie card
│   │   ├── ThemeToggle.jsx           ← Dark/Light mode
│   │   └── NotFound.jsx              ← 404 page
│   │
│   ├── pages/
│   │   ├── Home.jsx                  ← Home page
│   │   ├── ExplorerSlider.jsx        ← Slider page
│   │   ├── EraDetail.jsx             ← Template per era
│   │   ├── SpeciesDetail.jsx         ← Template per specie
│   │   └── NotFound.jsx              ← 404
│   │
│   ├── data/
│   │   ├── eras.json                 ← 5 ere + meta
│   │   └── species.json              ← 25 specie (5 per era)
│   │
│   ├── hooks/
│   │   ├── useTheme.js               ← Dark/Light mode
│   │   ├── useEra.js                 ← Fetch era by ID
│   │   └── useSpecies.js             ← Fetch specie by ID
│   │
│   ├── utils/
│   │   ├── formatters.js             ← Format Mya, dates
│   │   └── colors.js                 ← Color mapping eras
│   │
│   ├── styles/
│   │   ├── globals.css               ← Reset + variables
│   │   └── animations.css            ← CSS animations
│   │
│   ├── App.jsx                       ← Router setup
│   └── main.jsx                      ← Entry point
│
├── public/
│   ├── images/
│   │   ├── fossils/
│   │   │   ├── archean.svg
│   │   │   ├── proterozoic.svg
│   │   │   └── ... (5 total)
│   │   └── species/
│   │       ├── t-rex.svg
│   │       ├── triceratops.svg
│   │       └── ... (25 total)
│   └── index.html
│
├── package.json
├── vite.config.js
├── tailwind.config.js
└── README.md
```

---

## 📄 DATA STRUCTURE

### **eras.json** (5 ere)

```json
[
  {
    "id": "archean",
    "name": "Archean Eon",
    "startMya": 4600,
    "endMya": 2500,
    "color": "#1a1a2e",
    "bgGradient": "from-slate-900 to-slate-800",
    "emoji": "🌋",
    "description": "L'eon più antico della storia terrestre...",
    "climate": "Estremamente caldo, no ossigeno atmosferico",
    "atmosphere": "Metano, CO2, azoto",
    "geography": "Continenti primitivi, oceani globali",
    "dominantLife": "Batteri e archaea (unicellulari)",
    "majorEvents": [
      "Formazione della Terra",
      "Bombardamento pesante tardivo",
      "Prime forme di vita (~3.8 Mya)"
    ],
    "extinction": "N/A",
    "image": "/images/fossils/archean.svg",
    "species": ["stromatolites", "cyanobacteria", "archaea", "thermophiles", "methanogens"]
  },
  {
    "id": "proterozoic",
    "name": "Proterozoic Eon",
    "startMya": 2500,
    "endMya": 541,
    "color": "#2d3561",
    "bgGradient": "from-blue-900 to-blue-800",
    "emoji": "🌊",
    "description": "Eon della Grande Ossigenazione...",
    "climate": "Snowball Earth, glaciazioni periodiche",
    "atmosphere": "Graduale aumento ossigeno",
    "geography": "Supercontinenti (Rodinia, Pangea I)",
    "dominantLife": "Alghe, primi animali morbidi",
    "majorEvents": [
      "Great Oxidation Event (2.4 Mya)",
      "Neoproterozoic glaciations",
      "Ediacara fauna (~600 Mya)"
    ],
    "extinction": "Neoproterozoic glaciation",
    "image": "/images/fossils/proterozoic.svg",
    "species": ["spirulina", "red-algae", "ediacara", "dickinsonia", "spriggina"]
  },
  // ... (paleozoic, mesozoic, cenozoic)
]
```

### **species.json** (25 specie, 5 per era)

```json
[
  {
    "id": "t-rex",
    "name": "Tyrannosaurus rex",
    "scientificName": "T. rex",
    "eraId": "mesozoic",
    "period": "Late Cretaceous",
    "timeMya": 68,
    "era": "Mesozoic",
    "emoji": "🦖",
    "length": "12 m",
    "weight": "9000 kg",
    "diet": "Carnivore",
    "description": "Il re dei dinosauri...",
    "characteristics": [
      "Mascelle potentissime (bite force 12,800 N)",
      "Arti posteriori muscolosi",
      "Arti anteriori piccoli",
      "Visione binoculare",
      "Velocità massima: 40 km/h"
    ],
    "extinction": "K-Pg extinction event (66 Mya)",
    "image": "/images/species/t-rex.svg",
    "funFact": "Viveva più vicino alla nostra epoca che a quella di Stegosaurus (100 Mya di differenza!)"
  },
  {
    "id": "triceratops",
    "name": "Triceratops",
    "scientificName": "T. horridus",
    "eraId": "mesozoic",
    "period": "Late Cretaceous",
    "timeMya": 68,
    "era": "Mesozoic",
    "emoji": "🦕",
    "length": "9 m",
    "weight": "6000 kg",
    "diet": "Herbivore",
    "description": "Ceratopsido a tre corna...",
    "characteristics": [
      "Tre corna (2 sopra gli occhi, 1 sul naso)",
      "Scudo osseo (frill)",
      "Mascelle a forma di becco",
      "Potenziale herbivore gregario",
      "Potenziale combattente"
    ],
    "extinction": "K-Pg extinction event (66 Mya)",
    "image": "/images/species/triceratops.svg",
    "funFact": "La coda era corta e non aveva funzione difensiva come una frusta"
  },
  // ... (23 altre specie)
]
```

---

## 🎨 PAGE LAYOUTS

### **1️⃣ HOME PAGE** (`/`)

```
┌─────────────────────────────────┐
│  Header (Logo + Nav)            │
├─────────────────────────────────┤
│  Hero Section                   │
│  "Explore Deep Time"            │
│  🦖 Subtitle + CTA              │
├─────────────────────────────────┤
│  Quick Stats                    │
│  ┌─────────┐ ┌─────────┐       │
│  │4.6 Bya  │ │ 5 Eras  │       │
│  │ Archean │ │TimeSpan │       │
│  └─────────┘ └─────────┘       │
│  ┌─────────┐ ┌─────────┐       │
│  │25 Species│ │5M years │       │
│  │Cataloged │ │Duration │       │
│  └─────────┘ └─────────┘       │
├─────────────────────────────────┤
│  5 Era Cards (Preview)          │
│  ┌──────┐ ┌──────┐ ┌──────┐    │
│  │🌋    │ │🌊    │ │🌿    │    │
│  │Arch- │ │Proto-│ │Paleo-│    │
│  │ean   │ │zoic  │ │zoic  │    │
│  └──────┘ └──────┘ └──────┘    │
│  ┌──────┐ ┌──────┐              │
│  │🦖    │ │🦁    │              │
│  │Meso- │ │Ceno- │              │
│  │zoic  │ │zoic  │              │
│  └──────┘ └──────┘              │
├─────────────────────────────────┤
│  CTA Buttons                    │
│  [Explore with Slider] [Learn]  │
├─────────────────────────────────┤
│  Footer                         │
└─────────────────────────────────┘
```

### **2️⃣ SLIDER PAGE** (`/explorer`)

```
┌─────────────────────────────────┐
│  Header (Logo + Nav)            │
├─────────────────────────────────┤
│                                 │
│  ◄ [Mesozoic] 252-66 Mya ►      │
│                                 │
│  ╔═════════════════════════╗    │
│  ║  🦖 MESOZOIC ERA        ║    │
│  ║  252 - 66 Million Years ║    │
│  ║                         ║    │
│  ║  [Large fossil image]   ║    │
│  ║                         ║    │
│  ║  Dominati da dinosauri. ║    │
│  ║  Era di transizione.    ║    │
│  ║                         ║    │
│  ║  [Learn More ↗]         ║    │
│  ╚═════════════════════════╝    │
│                                 │
│  Indicatore Progression         │
│  ●●●●○                          │
│  4 / 5 (Mesozoic)               │
│                                 │
├─────────────────────────────────┤
│  Footer                         │
└─────────────────────────────────┘
```

### **3️⃣ ERA DETAIL PAGE** (`/era/:eraId`)

```
┌─────────────────────────────────┐
│  Header (Logo + Nav)            │
│  Breadcrumb: Home > Slider > Mesozoic
├─────────────────────────────────┤
│  Hero Section                   │
│  🦖 Mesozoic Era               │
│  252 - 66 Million Years Ago     │
├─────────────────────────────────┤
│  Main Info Grid (2 col)         │
│  ┌──────────────┬──────────────┐│
│  │Climate       │Atmosphere    ││
│  │Caldo, umido  │CO2 alto      ││
│  ├──────────────┼──────────────┤│
│  │Geography     │Dominant Life ││
│  │Pangea split  │Dinosauri     ││
│  └──────────────┴──────────────┘│
├─────────────────────────────────┤
│  Featured Image (fossil)        │
│  [Large SVG illustration]       │
├─────────────────────────────────┤
│  Major Events Timeline          │
│  • 252 Mya: Triassic begins     │
│  • 201 Mya: Jurassic begins     │
│  • 145 Mya: Cretaceous begins   │
│  • 66 Mya: K-Pg extinction      │
├─────────────────────────────────┤
│  5 Species in this Era          │
│  ┌────────┐ ┌────────┐          │
│  │ T-Rex  │ │Trice-  │          │
│  │🦖     │ │ratops  │          │
│  │[Link] │ │🦕[Link]│          │
│  └────────┘ └────────┘          │
│  ┌────────┐ ┌────────┐          │
│  │Stego-  │ │Brachio-│          │
│  │saurus  │ │saurus  │          │
│  │🦕[Link]│ │🦕[Link]│          │
│  └────────┘ └────────┘          │
│  ┌────────┐                     │
│  │Veloci- │                     │
│  │raptor  │                     │
│  │🦖[Link]│                     │
│  └────────┘                     │
├─────────────────────────────────┤
│  Navigation Buttons             │
│  [← Paleozoic] [Cenozoic →]     │
├─────────────────────────────────┤
│  Footer                         │
└─────────────────────────────────┘
```

### **4️⃣ SPECIES DETAIL PAGE** (`/era/:eraId/species/:speciesId`)

```
┌─────────────────────────────────┐
│  Header (Logo + Nav)            │
│  Breadcrumb: Home > Mesozoic > T-Rex
├─────────────────────────────────┤
│  Hero + Stats Row (4 col)       │
│  ┌────┬────┬────┬────┐         │
│  │🦖  │Len │Wei │Diet│         │
│  │T-R │12m │9tn │Meat│         │
│  └────┴────┴────┴────┘         │
├─────────────────────────────────┤
│  Large Fossil Image             │
│  [SVG centered]                 │
├─────────────────────────────────┤
│  Description                    │
│  "Tyrannosaurus rex was the..."  │
├─────────────────────────────────┤
│  Key Characteristics (5 bullets) │
│  • Mascelle potentissime         │
│  • Arti posteriori muscolosi     │
│  • Visione binoculare           │
│  • Velocità 40 km/h             │
│  • Lunghe artigli posteriori     │
├─────────────────────────────────┤
│  Fun Fact!                      │
│  "Viveva più vicino a noi che.."│
├─────────────────────────────────┤
│  Related Species (same era)     │
│  ┌────────┐ ┌────────┐          │
│  │Trice-  │ │Stego-  │          │
│  │ratops  │ │saurus  │          │
│  │🦕[Link]│ │🦕[Link]│          │
│  └────────┘ └────────┘          │
├─────────────────────────────────┤
│  Navigation                     │
│  [← Back to Era] [← Prev Species]
│  [Next Species →] [Other Eras →]
├─────────────────────────────────┤
│  Footer                         │
└─────────────────────────────────┘
```

---

## 🛠️ TECH STACK

```
Core
├── React 18 + Vite
├── React Router v6 (per routing)
├── Tailwind CSS
└── Zustand (state: theme)

Animations (optional)
├── Framer Motion (page transitions)
└── CSS transitions (slide effects)

No Database
├── JSON statico (eras.json, species.json)
└── LocalStorage (theme preference)
```

### **Dipendenze**

```json
{
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.17.0",
    "zustand": "^4.4.0",
    "tailwindcss": "^3.3.0",
    "framer-motion": "^10.16.0"
  },
  "devDependencies": {
    "@vitejs/plugin-react": "^4.1.0",
    "vite": "^5.0.0"
  }
}
```

---

## 📱 RESPONSIVE DESIGN

### **Desktop (>1024px)**
- Header fixed a top
- 2-column layouts dove possibile
- Hero sections full-width
- Slider fullscreen

### **Tablet (768px-1024px)**
- Header sticky
- Stacked layouts (1 col)
- Slider con padding laterale
- Cards responsive grid

### **Mobile (<768px)**
- Header sticky con menu hamburger
- Single column tutto
- Slider full-width con swipe gestures
- Touch-optimized buttons (>48px)
- Compact spacing

---

## 🗂️ COMPONENT REUSABILITY

```jsx
// Componenti riutilizzabili
<Header />                  // Su tutte le pagine
<Navigation breadcrumbs />  // Su tutte le pagine sub
<EraCard />                 // Home + Slider + Era detail
<SpeciesCard />             // Era detail + Species nav
<ThemeToggle />             // Header
<Footer />                  // Tutte pagine

// Componenti page-specific
<HeroSection />             // Home + Era detail
<StatsGrid />               // Home
<SliderContainer />         // Explorer page
<SpeciesGrid />             // Era detail
```

---

## 🔧 HOOKS CUSTOM

```javascript
// useTheme.js
const { isDark, toggleTheme } = useTheme();

// useEra.js
const era = useEra(eraId); // Fetch da eras.json

// useSpecies.js
const species = useSpecies(speciesId); // Fetch da species.json

// useRelatedSpecies.js
const relatedSpecies = useRelatedSpecies(eraId); // 5 specie di un'era
```

---

## 🚀 ROUTING CON REACT ROUTER

```jsx
// App.jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Home from './pages/Home';
import ExplorerSlider from './pages/ExplorerSlider';
import EraDetail from './pages/EraDetail';
import SpeciesDetail from './pages/SpeciesDetail';
import NotFound from './pages/NotFound';

export default function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/explorer" element={<ExplorerSlider />} />
        <Route path="/era/:eraId" element={<EraDetail />} />
        <Route path="/era/:eraId/species/:speciesId" element={<SpeciesDetail />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

## 📅 TIMELINE DI SVILUPPO

### **Week 1: Setup + Routing + Home**
- [ ] Setup Vite + React Router
- [ ] Crea struttura cartelle
- [ ] Home page + Header/Footer
- [ ] Data JSON setup
- [ ] Dark/Light mode

### **Week 2: Slider + Era Pages**
- [ ] Slider/Carousel component
- [ ] Era detail pages template
- [ ] Fetch dati dinamici
- [ ] Styling + responsivo
- [ ] Animazioni transizioni

### **Week 3: Species Pages + Polish**
- [ ] Species detail pages
- [ ] Related species navigation
- [ ] Mobile optimization
- [ ] Testing
- [ ] Deploy su Vercel

---

## 🎨 DESIGN TOKENS

```css
:root {
  /* Colors - Era mapping */
  --color-archean: #1a1a2e;
  --color-proterozoic: #2d3561;
  --color-paleozoic: #4a90e2;
  --color-mesozoic: #e24a4a;
  --color-cenozoic: #2ecc71;

  /* Typography */
  --font-display: 'Outfit', sans-serif;
  --font-body: 'Inter', sans-serif;

  /* Spacing */
  --spacing-xs: 0.5rem;
  --spacing-sm: 1rem;
  --spacing-md: 1.5rem;
  --spacing-lg: 2rem;
  --spacing-xl: 3rem;
}
```

---

## 🚀 SETUP INITIAL

```bash
# Create project
npm create vite@latest deep-time-explorer -- --template react
cd deep-time-explorer

# Install dependencies
npm install react-router-dom zustand framer-motion
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p

# Create structure
mkdir -p src/{components,pages,data,hooks,utils,styles}
mkdir -p public/{images/fossils,images/species}

# Start dev
npm run dev
```

---

## ✨ BONUS FEATURES (Dopo MVP)

- [ ] Search bar (cerca specie/ere)
- [ ] Favorites (salva specie preferite)
- [ ] Quiz paleontologia
- [ ] Timeline comparativa (eras side-by-side)
- [ ] 3D fossil viewer
- [ ] Share buttons (social)
- [ ] Print pages as PDF

---

