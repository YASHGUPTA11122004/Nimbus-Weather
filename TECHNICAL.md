# TECHNICAL.md — Nimbus Weather: Full Code Map
---

## Project Summary

- **File:** `index.html` (~950 lines, single file, no build step)
- **Live URL:** `https://yashgupta11122004.github.io/Nimbus-Weather/`
- **Repo:** `https://github.com/YASHGUPTA11122004/Nimbus-Weather`
- **Stack:** Vanilla HTML + CSS + JS. Zero npm, zero frameworks, zero API keys.
- **Hosting:** GitHub Pages — replace `index.html` in `main` branch to deploy.

---

## File Structure (inside index.html)

```
index.html
├── <style>         Lines ~9–220    — All CSS
├── <body> HTML     Lines ~221–295  — Static markup only
└── <script>        Lines ~298–949  — All JavaScript
```

---

## CSS Architecture

### Page Layout
The entire app is a **3-row CSS Grid**:
```css
#ui { display: grid; grid-template-rows: auto 1fr auto; }
/* Row 1 (auto): Topbar + chips + alerts                */
/* Row 2 (1fr):  Hero section — fills all remaining space */
/* Row 3 (auto): Bottom forecast strip + footer          */
```

### Hero Section Layout
```css
#hero        { display: flex; align-items: center; padding: 0 28px; gap: 16px; }
.hero-left   { flex: 1; }          /* Left: condition text + temperature    */
.hero-right  { width: 320px;       /* Right: 2×2 grid of float cards        */
               display: grid;
               grid-template-columns: 1fr 1fr; }
/* Card order: Wind | Humidity  (row 1)                  */
/*             UV   | Visibility (row 2)                  */
/*             AQI  (full width) (row 3)                  */
/*             Sunrise/Sunset (full width) (row 4)        */
```

### Key CSS Classes

| Class | Controls |
|-------|----------|
| `#hero` | Main center area flex container |
| `.hero-left` | Left column: date, condition, subtitle, desc, location, temp, feels |
| `.hero-right` | Right column: 2×2 float cards grid |
| `.hero-condition` | Big weather name — Playfair Display, `clamp(32px, 4vw, 66px)` |
| `.hero-temp` | Giant temperature — Playfair Display, `clamp(52px, 6.5vw, 100px)` |
| `.hero-temp sup` | The `°C` / `°F` superscript |
| `.hero-feels` | "Feels like X · Hi X Lo X" |
| `.float-card` | Glassmorphism stat card |
| `.float-card.full-width` | `grid-column: span 2` — used for AQI + Sunrise cards |
| `.fc-label` | Tiny uppercase label inside card |
| `.fc-val` | Large value inside card |
| `.fc-sub` | Small subtitle inside card |
| `#topbar` | Top bar flex row |
| `.search-area` | Search input wrapper (`margin: 0 auto` to center it) |
| `.topbar-right` | Pill buttons + unit toggle on the right |
| `.pill-btn` | Life / Insights / Compare / Radar / 📍 buttons |
| `.chip` | Saved city quick-switch chip |
| `#forecast-strip` | Bottom glass panel containing tabs + views |
| `.stab` | 7-Day / Hourly / Details tab button |
| `#day-strip` | 7-day forecast row (has SVG bezier curve overlay) |
| `.day-col` | Single day column |
| `#hourly-strip` | Horizontal scrollable hourly cards (has visible scrollbar) |
| `.hh` | Single hourly card (58px wide) |
| `.alert-pill` | Animated pulsing alert banner |
| `#overlay` | Full-screen modal backdrop |
| `.overlay-box` | Modal content container |
| `#loader` | Full-screen loading screen (fades out after data loads) |
| `#toast` | Bottom-center notification |

### Background Layer Stack (z-index order)
```
z-index 0:  #bg-canvas    — Canvas animations (rain/snow/sun etc.)
z-index 1:  #scene-grade  — Per-weather color grading overlay
z-index 2:  #vignette     — Radial darkening at screen edges
z-index 3:  #noise        — Film grain texture (opacity: 0.028)
z-index 10: #ui           — All interactive UI
z-index 50: #overlay      — Modal overlays
z-index 999: #loader      — Loading screen
z-index 9999: #toast      — Toast notifications
```

---

## JavaScript Architecture

### Global State
```javascript
let S = {
  unit: 'C',          // 'C' or 'F'
  city: 'New Delhi',  // Current city display name
  lat: 28.6139,       // Current latitude
  lon: 77.2090,       // Current longitude
  data: null,         // Full Open-Meteo weather API response
  aq: null,           // Full Open-Meteo air quality response
  cmp: [],            // Compare cities: [{name, wx, aq}]
  stripTab: 'week'    // Active bottom tab
}

let parts = []        // Canvas particle array (reset each scene change)
let RAF = null        // requestAnimationFrame ID
let lastScene = ''    // Current scene key ('sunny', 'rainy', etc.)
let ctx = null        // Canvas 2D rendering context
```

### API Endpoints
```javascript
const GU = 'https://geocoding-api.open-meteo.com/v1/search'
const WU = 'https://api.open-meteo.com/v1/forecast'
const AU = 'https://air-quality-api.open-meteo.com/v1/air-quality'
// Reverse geocoding: https://nominatim.openstreetmap.org/reverse
// Radar:            https://embed.windy.com/embed2.html (iframe)
```

### WMO Weather Code Map
```javascript
const WMO = {
  key: [emoji, displayName, sceneType, description]
  // sceneType values: 'sunny' | 'cloudy' | 'foggy' | 'drizzle' |
  //                   'rainy' | 'snowy'  | 'stormy'
  // All keys: 0,1,2,3,45,48,51,53,55,61,63,65,71,73,75,77,80,81,82,85,86,95,96,99
}
```

### Utility Functions
```javascript
T(c)         // Celsius → current unit (respects S.unit)
TU()         // Returns '°C' or '°F'
kmh(ms)      // m/s → km/h  ← IMPORTANT: API gives wind in m/s, always convert
wdir(deg)    // Degrees → 'N'/'NE'/'E' etc.
moonP()      // Returns { idx: 0-7, ill: 0-100 }
uvLbl(v)     // Returns [labelStr, colorStr] for UV value
aqLbl(v)     // Returns [labelStr, colorStr] for AQI value
comfOf(dew)  // Returns comfort string from dew point value
```

### Scene Animation System
```javascript
const SCENES = {
  sunny:   { grade: 'radial-gradient(...)', init(c,W,H){}, draw(c,W,H,t){} },
  rainy:   { ... },   // 260 diagonal rain streaks + cloud layer
  stormy:  { ... },   // Heavy rain + randomised lightning bolt flashes
  snowy:   { ... },   // 180 snowflakes with wind sway
  cloudy:  { ... },   // Cloud masses + faint stars
  foggy:   { ... },   // Moving horizontal mist bands
  drizzle: { ... },   // Light rain (separate from heavy rainy scene)
  night:   { ... },   // Moon with craters + full starfield
  haze:    { ... },   // Warm dust particles + haze bands
}

function sceneType(wmo, night)  // WMO code + is_day=0 → scene key string
function startScene(type)       // Cancel old RAF → init particles → start loop
```

Each `draw()` receives `t` (frame counter) for animations like `Math.sin(t * 0.001)`.

---

## Data Flow

### On City Load
```
loadWeather(lat, lon, city)
  ├── fetchWX(lat, lon)    →  S.data
  ├── fetchAQ(lat, lon)    →  S.aq
  ├── addChip()            →  adds to #chips-row
  ├── renderAlerts()       →  writes to #alert-zone
  ├── updateHero()         →  updates #hcond #htemp #hfeels #hloc #hdate + scene
  ├── renderCards()        →  rewrites #hero-right innerHTML (6 float cards)
  └── renderStrip()        →  rewrites #week-view, triggers hourly/details if active
```

### Render Functions
```javascript
updateHero()    // Left hero text: date/time, condition, sub, desc, location, temp, feels
                // Also triggers startScene() if weather type changed

renderCards()   // Builds 6 float cards HTML → #hero-right:
                //   Wind card, Humidity card, UV card, Visibility card,
                //   AQI card (full-width with SVG ring), Sunrise/Sunset card (full-width with SVG arc)

renderStrip()   // 7-day forecast: builds SVG bezier curve + 7 .day-col divs
renderHourly()  // 24 .hh cards in #hourly-strip (called on tab switch or strip render)
renderDetails() // 6 detail boxes: Pressure / UV / Cloud / Precip / Dew / Gust
renderAlerts()  // Storm / wind gust / UV alert pills → #alert-zone

stripTab(name)  // Switches visible view, calls renderHourly/Details if needed
setUnit(u)      // Toggles C/F, calls updateHero + renderCards + renderStrip
```

---

## Overlay System

```javascript
openOverlay(type)         // Builds HTML via buildOverlay(type), shows modal
closeOverlay()            // Hides modal
buildOverlay(type)        // Returns full HTML string for overlay content

// type = 'life':
//   Outfit banner + 8-item outfit grid + pollen bars + 8-activity grid
//   Tabs: 'outfit' | 'pollen' | 'activity'  (controlled by ovTab())

// type = 'insights':
//   Score ring SVG + smart tips list + sci-rows table +
//   weekly temp heatmap + copy weather button

// type = 'compare':
//   Cities table (S.city + S.cmp[]) + inline search input (NO browser prompt)
//   addComp() appends search DOM to overlay, selectComp() fetches and adds city

// type = 'radar':
//   Windy.com iframe centred on S.lat / S.lon

ovTab(id)   // Toggles Life overlay sub-tabs (outfit/pollen/activity)
```

### Compare City Search (important — no `prompt()`)
```javascript
addComp()                    // Creates inline search input inside overlay DOM
selectComp(lat, lon, name)   // Fetches wx+aq → pushes to S.cmp → reopens compare
doAddComp()                  // Reads input value → geocodes → calls selectComp
rmComp(name)                 // Filters S.cmp array
```

---

## Open-Meteo Response Shape

### S.data.current (key fields)
```javascript
{
  temperature_2m,          // °C float — always use T() to display
  apparent_temperature,    // Feels like °C
  relative_humidity_2m,    // % integer
  is_day,                  // 1 or 0 — 0 triggers night scene
  weather_code,            // WMO integer — look up in WMO object
  wind_speed_10m,          // m/s — ALWAYS convert with kmh()
  wind_direction_10m,      // degrees — convert with wdir()
  wind_gusts_10m,          // m/s — ALWAYS convert with kmh()
  uv_index,                // float — ALWAYS use Math.round() for display
  visibility,              // metres — divide by 1000 for km
  cloud_cover,             // %
  pressure_msl,            // hPa
  dew_point_2m,            // °C
  precipitation             // mm
}
```

### S.data.daily (7 entries each)
```javascript
{
  time[],                         // ['2024-03-22', ...]
  temperature_2m_max[],
  temperature_2m_min[],
  weather_code[],
  precipitation_sum[],
  precipitation_probability_max[],
  sunrise[],                      // '2024-03-22T06:22' — split on 'T' for time
  sunset[],
  uv_index_max[],
  shortwave_radiation_sum[]        // kWh/m²
}
```

---

## How to Make Common Changes

### Change what the right-side cards show
Edit `renderCards()` — rewrites `#hero-right` innerHTML completely.

### Add a new bottom strip tab
1. HTML: add `<button class="stab" onclick="stripTab('newtab')">Label</button>`
2. HTML: add `<div id="newtab-view" style="display:none"></div>`
3. In `stripTab()`: add display toggle for `newtab-view`
4. Create `renderNewTab()` and call it in `stripTab()` when active

### Add a new overlay
1. HTML topbar: `<button class="pill-btn" onclick="openOverlay('new')">Label</button>`
2. In `buildOverlay(type)`: add `if(type==='new'){ return \`...\`; }`

### Add a new weather scene
1. Add to `SCENES` object with `init()` and `draw()` methods
2. Add WMO code entries to `WMO` with the new scene type as 3rd array element
3. Optional: add CSS `#bg-canvas` background fallback

### Change the app name / branding
- HTML: `<title>` tag, `.logo` div (`Nim<span>bus</span>`)
- Footer: the "Built by" div below `#forecast-strip`
- Overlay: `copyWT()` function — "via Nimbus Weather" at end of copied text

### Change default city on load
Last line of `<script>`:
```javascript
loadWeather(S.lat, S.lon, S.city);
// Change S.lat, S.lon, S.city at the top of the state object
```

---

## Known Gotchas

| Issue | Detail |
|-------|--------|
| Wind values | API returns m/s. Always use `kmh()` — never display raw value |
| UV index | Returns float (e.g. 7.05). Always `Math.round()` before display |
| Pollen data | **Estimated** — not from a real pollen API. Calculated from temp/humidity/month |
| AQI scale | European AQI (not US AQI). Scale: 0–50 Good, 51–100 Moderate, 101–150 Unhealthy* |
| Sunrise/Sunset | Format from API: `"2024-03-22T06:22"`. Split on `'T'` and slice `[1].slice(0,5)` for time |
| Night scene | Triggered by `is_day === 0` — overrides all other scene types |
| Hourly index | Find current hour with `findIndex()` on `hourly.time` array, then slice 24 forward |

---

## Deployment

**GitHub Pages:**
1. Upload/replace `index.html` in `main` branch
2. Auto-deploys in ~30s
3. No build step, no config needed

**Any static host:**
- Single file upload, no environment variables

---

*Last updated: March 2026 | Built by [Yash Gupta](https://github.com/YASHGUPTA11122004)*
