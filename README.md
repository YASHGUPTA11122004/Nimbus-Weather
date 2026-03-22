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
| 🌙 Night | Moon with craters, twinkling starfield, subtle halo |
| 🌁 Hazy | Warm dust particles, layered haze bands |

Each scene includes film grain texture, radial vignette, and per-scene colour grading overlay. The sun is drawn with 3 layered radial gradients (outer halo → mid glow → soft core) — not a flat disc.

---

### 📊 Current Weather
Always visible on the main screen:
- **Temperature** — large cinematic display with °C / °F toggle
- **Feels Like** — apparent temperature
- **Hi / Lo** — today's max and min
- **Condition** — full label + one-line description (e.g. "Brilliant clear skies all day.")
- **Location** — city name
- **Date & Time** — live clock, updates every second

**Right-side float cards (always visible):**
- Wind speed (km/h) + direction + gust speed
- Humidity % + dew point temperature
- UV Index with colour-coded severity (Low → Extreme)
- Visibility (km) + cloud cover %
- Air Quality — European AQI ring chart + label
- Sunrise & Sunset — animated arc with live sun position

---

### 📅 7-Day Forecast
- Daily condition icon, hi/lo temperatures, precipitation probability %
- Animated bezier temperature curve connecting all 7 days with gradient fill
- "Today" and "Tomorrow" highlighted
- Precipitation % shown when above 15%

---

### 🕐 24-Hour Hourly Forecast
- Horizontally scrollable strip with visible scrollbar
- Each card shows: time, condition icon, temperature, rain probability
- "Now" card highlighted
- Full 24 hours from current time

---

### 📋 Details Tab
Six additional data points:
- Atmospheric Pressure (hPa) + trend indicator (▲ High / → Normal / ▼ Low)
- UV Index + severity label
- Cloud Cover %
- Precipitation mm (last hour)
- Dew Point + comfort label (Dry / Comfortable / Humid / Very Humid)
- Wind Gust speed + compass direction

---

### 🌬️ Air Quality
- European AQI score with animated SVG ring chart
- PM2.5, PM10, O₃ (Ozone), NO₂ (Nitrogen Dioxide) values
- Colour-coded: Good / Moderate / Unhealthy* / Unhealthy

---

### 🌙 Moon Phase
- Current phase icon (🌑 → 🌘)
- Phase name (New Moon, Waxing Crescent, Full Moon, etc.)
- Illumination % + progress bar

---

### 🌅 Sunrise & Sunset
- SVG arc with golden gradient showing day progress
- Animated sun dot at current position on the arc
- Exact sunrise and sunset times

---

### 🎒 Life & Outdoors Overlay

**Outfit Recommender**
- 8 clothing items dynamically chosen based on temperature range
- Banner with specific advice text, current temp, humidity, and condition

**Pollen & Allergy Forecast**
- Tree, Grass, Weed, Mould pollen levels
- Estimated from temperature, humidity, and month/season
- Colour-coded bars: Low / Moderate / High

**Activity Suitability**
- 8 activities: Running, Cycling, Golf, Walking, Camping, Photography, Driving, Yoga
- Rated: ✓ Great / ~ OK / ✗ Poor with a specific reason for each

---

### ✨ Insights Overlay

**Weather Quality Score**
- Composite score out of 100
- Factors: temperature comfort, rain risk, wind, air quality
- Colour-coded ring chart

**Smart Contextual Tips** (up to 8, auto-generated from live data)
- Heat Advisory (temp > 35°C)
- Cold Advisory (temp < 5°C)
- Sun Protection needed (UV ≥ 6)
- Poor Air Quality warning (AQI > 100)
- Rain Coming (>70% chance in next 3 hours)
- Wind Warning (gusts > 55 km/h)
- High Humidity alert (> 80%)
- Best outdoor window recommendation

**Temperature Science**
- Daily temperature range
- Heat Index — Rothfusz formula, activates when temp > 27°C
- Wind Chill — activates when temp < 10°C
- Tomorrow's high with trend badge (▲ / ▼ / →)
- 7-day total rainfall in mm
- Moon phase + illumination %

**Weekly Temperature Heatmap**
- 7-cell grid, colour-coded from cool to hot
- Hover any cell to see exact date and temperature

**Share Weather Card**
- Formatted weather summary ready to paste
- One-click copy to clipboard (WhatsApp / Twitter / anywhere)

---

### ⚖️ City Comparison Overlay
- Compare your city against any number of additional cities
- Side-by-side: Temperature, Feels Like, Humidity, Wind, Condition, AQI
- Built-in city search with autocomplete — no browser popups
- Remove any city with one click

---

### 📡 Live Precipitation Radar
- Windy.com radar embedded and centred on current location
- Regional zoom showing live rainfall patterns

---

### 🔍 Search & Location
- City autocomplete with 260ms debounce
- Saved city chips — one click to switch
- GPS auto-detect via browser geolocation
- Reverse geocoding (Nominatim) to get city name from coordinates
- Duplicate prevention using lat/lon proximity (0.05° radius)

---

### ⚡ Weather Alerts
- Auto-generated for: severe thunderstorm, high wind gusts (> 60 km/h), extreme UV (≥ 8)
- Animated pulsing banners at the top of the screen
- Each alert individually dismissable

---

### ⚙️ UI & Settings
- **°C / °F toggle** — all temperatures switch instantly everywhere
- **Live clock** — updates every second
- **Branded loading screen** — animated progress bar on first load
- **Toast notifications** — non-intrusive action feedback
- **Resize handling** — canvas scenes reinitialise on window resize

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Vanilla HTML, CSS, JavaScript — zero frameworks |
| Animations | HTML5 Canvas API — hand-coded, no libraries |
| Weather Data | [Open-Meteo](https://open-meteo.com) Forecast API |
| Air Quality | [Open-Meteo](https://open-meteo.com) Air Quality API |
| Geocoding | Open-Meteo Geocoding API |
| Reverse Geocoding | [Nominatim](https://nominatim.openstreetmap.org) (OpenStreetMap) |
| Radar | [Windy.com](https://windy.com) Embed |
| Fonts | Playfair Display · Inter · JetBrains Mono (Google Fonts) |
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
open index.html
```

No installation, no dependencies, no configuration needed.

---

## Project Structure

```
Nimbus-Weather/
├── index.html      # The entire application (~950 lines)
├── README.md       # This file
└── TECHNICAL.md    # Internal architecture guide for developers & AI assistants
```

---

## API Reference

All APIs are free, no authentication required:

```
Weather:      https://api.open-meteo.com/v1/forecast
Air Quality:  https://air-quality-api.open-meteo.com/v1/air-quality
Geocoding:    https://geocoding-api.open-meteo.com/v1/search
Reverse Geo:  https://nominatim.openstreetmap.org/reverse
Radar:        https://embed.windy.com/embed2.html
```

---

## Roadmap

- [ ] PWA support — offline caching, installable on mobile
- [ ] Historical weather data tab
- [ ] Custom alert thresholds
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
