# 🌤️ Nimbus — Weather Intelligence

> *Nimbus* — Latin for the dark rain-bearing cloud, and the luminous halo surrounding divine figures. A name that holds both storm and light. That's exactly what this app does — it shows you the sky in all its moods, beautifully.

[![Live Demo](https://img.shields.io/badge/Live%20Demo-yashgupta11122004.github.io%2FNimbus--Weather-blue?style=flat-square)](https://yashgupta11122004.github.io/Nimbus-Weather/)
[![GitHub](https://img.shields.io/badge/GitHub-YASHGUPTA11122004-181717?style=flat-square&logo=github)](https://github.com/YASHGUPTA11122004)
[![No API Key](https://img.shields.io/badge/API%20Key-Not%20Required-green?style=flat-square)](https://open-meteo.com)
[![Single File](https://img.shields.io/badge/Build-Single%20HTML%20File-orange?style=flat-square)]()

---

## Why Nimbus?

Most weather apps show you a table of numbers. Nimbus shows you the *sky*.

Every weather condition — clear sun, thunderstorm, snowfall, foggy morning, hazy dusk — is rendered as a live animated scene directly on the canvas. The UI adapts its entire mood to match what's actually happening outside your window. Open it on a stormy night and watch lightning flash. Open it on a clear afternoon and watch the sun pulse with rays.

The name **Nimbus** comes from two Latin meanings:
- The **nimbus cloud** — the dark, rain-bearing cloud type that dominates stormy skies
- The **nimbus halo** — the glowing aura of light depicted around celestial figures in classical art

Together, they represent the full emotional range of weather — from ominous to beautiful. That duality is what Nimbus the app tries to capture.

---

## Features

### 🎬 Cinematic Animated Scenes
Nine fully hand-crafted canvas animations that respond to real weather conditions:

| Condition | Scene |
|-----------|-------|
| ☀️ Clear / Sunny | Pulsing sun with volumetric rays, atmospheric glow, drifting clouds |
| 🌧️ Rain | 260 diagonal rain streaks with cloud layer |
| ⛈️ Thunderstorm | Heavy rain + randomised lightning bolt flashes |
| ❄️ Snow | 180 drifting snowflakes with wind sway |
| ☁️ Cloudy | Floating cloud masses, faint twinkling stars |
| 🌫️ Foggy | Moving horizontal mist bands |
| 🌦️ Drizzle | Light rain, separate visual from heavy rain |
| 🌙 Night | Moon with craters, twinkling starfield, subtle glow |
| 🌁 Hazy | Warm dust particles, layered haze bands |

Each scene includes film grain, vignette overlay, and per-scene color grading for a cinematic look.

### 📊 Weather Data (Powered by Open-Meteo — Free, No API Key)
- **Current conditions** — Temperature, feels like, humidity, wind speed & direction, gusts, UV index, visibility, cloud cover, pressure, dew point, precipitation
- **7-Day Forecast** — Hi/lo temperatures, condition icons, precipitation probability, animated temperature curve
- **24-Hour Hourly** — Scrollable hourly strip with temperature, condition, and rain probability
- **Air Quality** — European AQI with PM2.5, PM10, O₃, NO₂ breakdown
- **Sunrise & Sunset** — Animated arc showing current sun position in the sky

### 🎒 Life & Outdoors Overlay
- **Outfit Recommender** — 8 contextual clothing items based on temperature and conditions
- **Pollen & Allergy Forecast** — Tree, Grass, Weed, Mould levels estimated from temperature, humidity, and season
- **Activity Suitability** — 8 activities (Running, Cycling, Golf, Walking, Camping, Photography, Driving, Yoga) rated Great / OK / Poor with specific reasons

### ✨ Insights Overlay
- **Weather Quality Score** — /100 composite score from temperature, rain risk, wind, and air quality
- **Smart Tips** — Contextual advisories: heat/cold warnings, UV alerts, rain incoming, wind warnings, humidity alerts
- **Temperature Science** — Heat Index, Wind Chill, daily range, tomorrow comparison with trend indicator
- **Weekly Heatmap** — 7-day temperature grid colour-coded from cool to hot
- **Share Card** — Copy weather summary to clipboard for WhatsApp/social sharing

### ⚖️ City Comparison
- Compare current city against any number of additional cities
- Side-by-side: temperature, feels like, humidity, wind, condition, AQI
- In-overlay city search (no browser prompts)

### 📡 Live Radar
- Windy.com precipitation radar embedded and centred on current location

### 🔍 Smart Search
- City autocomplete with debounce
- Saved city chips for quick switching
- GPS auto-detect with reverse geocoding (Nominatim)
- Duplicate chip prevention by lat/lon proximity

### ⚡ Weather Alerts
- Auto-generated alerts for thunderstorms, high wind gusts, extreme UV
- Animated pulsing pill-style banners, dismissable

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Vanilla HTML, CSS, JavaScript — zero frameworks |
| Animations | HTML5 Canvas API (hand-coded, no libraries) |
| Weather Data | [Open-Meteo](https://open-meteo.com) Forecast API |
| Air Quality | [Open-Meteo](https://open-meteo.com) Air Quality API |
| Geocoding | Open-Meteo Geocoding API |
| Reverse Geocoding | [Nominatim](https://nominatim.openstreetmap.org) (OpenStreetMap) |
| Radar | [Windy.com](https://windy.com) Embed |
| Fonts | Playfair Display, Inter, JetBrains Mono (Google Fonts) |
| Hosting | GitHub Pages |

**No build step. No npm. No framework. No API key required.** A single `index.html` file.

---

## Getting Started

### View Live
👉 [yashgupta11122004.github.io/Nimbus-Weather](https://yashgupta11122004.github.io/Nimbus-Weather/)

### Run Locally
```bash
git clone https://github.com/YASHGUPTA11122004/Nimbus-Weather.git
cd Nimbus-Weather
# Just open index.html in any browser
open index.html
```

No installation, no dependencies, no configuration needed.

---

## Project Structure

```
Nimbus-Weather/
└── index.html          # The entire application — ~950 lines
```

Everything lives in a single file by design. This makes it:
- Trivially deployable to any static host
- Easy to share, fork, or embed
- Zero-dependency in the truest sense

---

## API Reference

All APIs used are completely free with no authentication required:

```
Weather:     https://api.open-meteo.com/v1/forecast
Air Quality: https://air-quality-api.open-meteo.com/v1/air-quality
Geocoding:   https://geocoding-api.open-meteo.com/v1/search
Reverse Geo: https://nominatim.openstreetmap.org/reverse
Radar:       https://embed.windy.com/embed2.html
```

---

## Screenshots

| Clear Sky | Thunderstorm | Night |
|-----------|-------------|-------|
| Sun rays, atmospheric glow | Lightning flashes, heavy rain | Moonlit starfield |

---

## Roadmap

- [ ] PWA support (offline caching, installable)
- [ ] Historical weather data tab
- [ ] Custom alert thresholds
- [ ] Dark/light theme toggle
- [ ] More language support

---

## Built By

**Yash Gupta** — [github.com/YASHGUPTA11122004](https://github.com/YASHGUPTA11122004)

*Built from scratch as a portfolio project. Every animation, every calculation, every pixel — handwritten.*

---

<div align="center">

**Nimbus Weather** &nbsp;·&nbsp; No API key &nbsp;·&nbsp; No framework &nbsp;·&nbsp; No nonsense

*"Not just a weather app. A window into the sky."*

</div>
