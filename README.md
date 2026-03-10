# ⚡ EV Master

> **A simple but powerful web-based calculator designed for Battery Electric Vehicle (BEV) owners.**  
> No backend, no installation, no account — just open and use.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PWA Ready](https://img.shields.io/badge/PWA-Ready-brightgreen)](https://web.dev/progressive-web-apps/)
[![HTML5](https://img.shields.io/badge/HTML5-Single--File-orange)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![No dependencies](https://img.shields.io/badge/dependencies-none-blue)]()

---

## 📖 Table of Contents

- [Overview](#-overview)
- [Features at a Glance](#-features-at-a-glance)
- [Detailed Feature Reference](#-detailed-feature-reference)
  - [🔢 Main Input Panel](#-main-input-panel)
  - [📊 Stats Tab](#-stats-tab)
  - [🔋 Autonomy Tab](#-autonomy-tab)
  - [🗺️ Trip Estimator Tab](#️-trip-estimator-tab)
  - [⚡ Charging Calculator Tab](#-charging-calculator-tab)
  - [🏎️ Speed vs Range Tab](#️-speed-vs-range-tab)
  - [🧮 Battery Health Tab](#-battery-health-tab)
  - [🌿 CO₂ Savings Tab](#-co₂-savings-tab)
  - [📍 Trip Log Tab](#-trip-log-tab)
  - [🧮 Quick Calculator Tab](#-quick-calculator-tab)
- [🚗 Vehicle Presets](#-vehicle-presets)
- [🌗 Theme System](#-theme-system)
- [💾 Persistence & Storage](#-persistence--storage)
- [📱 Progressive Web App (PWA)](#-progressive-web-app-pwa)
- [⚙️ Technical Architecture](#️-technical-architecture)
- [🚀 Getting Started](#-getting-started)
- [📜 License](#-license)

---

## 🌟 Overview

**EV Master** is a fully self-contained, single-file HTML application that provides a comprehensive suite of tools for electric vehicle owners. It lets you calculate real-world consumption from an actual drive, estimate future trip costs, plan charging sessions, monitor battery degradation over time, and compare your EV's environmental impact against a conventional ICE vehicle — all without any server, framework, or internet connection required.

All data is persisted locally in the browser via `localStorage`, so your vehicle profiles, trip history, and preferences survive page reloads and browser restarts.

---

## ✨ Features at a Glance

| 🏷️ Feature | 📝 Description |
|---|---|
| 📊 **Real Consumption Stats** | Calculates true kWh/100Km from actual SoC delta and distance |
| 🔋 **Animated Battery Visual** | Live graphical battery bar with buffer and start markers |
| 🗺️ **Trip Estimator** | Projects future trip cost/SoC using temperature, speed & HVAC factors |
| ⚡ **Charging Calculator** | Estimates time and cost for any SoC target and charger power |
| 🏎️ **Speed vs Range Chart** | Canvas-drawn aerodynamic drag curve across speed intervals |
| 🏷️ **SoH Estimator** | Calculates State of Health from measured vs WLTP range with arc gauge |
| 🌿 **CO₂ Comparison** | Computes EV vs ICE emissions using configurable grid intensity |
| 📍 **Trip Log** | Persistent history of up to 50 logged trips with averages |
| 🧮 **Quick Calculator** | Standalone calculator with history tape and SoC↔Km converter |
| 🚗 **Vehicle Presets** | Save/load named vehicle profiles (capacity, WLTP range, ICE reference) |
| 🌗 **Dark / Light Theme** | Full theme switcher with smooth CSS transitions |
| 📱 **PWA Support** | Installable on mobile home screen via Web App Manifest + Service Worker |
| 💾 **Local Persistence** | All state auto-saved to `localStorage`; zero data leaves the device |
| 📋 **Export Summary** | One-click clipboard copy of a full trip summary as plain text |

---

## 🔍 Detailed Feature Reference

---

### 🔢 Main Input Panel

The left-hand panel (or top panel on mobile) is the primary data entry area. Every field has both a **numeric input** and a synchronized **range slider** for quick adjustment. All values immediately re-compute and re-render the entire UI on change.

| 🏷️ Field | ⚙️ Default | 📐 Range | 📝 Description |
|---|---|---|---|
| 🟢 **Starting battery SoC** | 100% | 0–100% | Battery charge at the start of the recorded drive |
| 🟡 **Current battery SoC** | 80% | 0–100% | Battery charge at the end of the recorded drive |
| 📏 **Traveled distance** | 50 Km | 0–500 Km | Actual distance covered during the recorded drive |
| 🛡️ **Minimum SoC buffer** | 10% | 0–100% | Reserved charge level — never counted as usable range |
| 🔋 **Usable battery capacity** | 75 kWh | 10–150 kWh | The usable (net) battery capacity of the vehicle |
| 📄 **WLTP rated range** | 400 Km | 50–1000 Km | Manufacturer's official WLTP range — used for SoH and WLTP ratio |
| 💶 **Electricity price** | 0.25 €/kWh | 0.01–1.50 €/kWh | Cost of electricity — used for all trip cost calculations |
| ⛽ **Fuel price** | 1.70 €/L | 1.00–3.00 €/L | Petrol/diesel price for ICE cost equivalence comparisons |
| 🚗 **ICE fuel efficiency** | 15 Km/L | 5–40 Km/L | Reference ICE vehicle efficiency for cost/CO₂ comparison |
| 🌫️ **Grid CO₂ intensity** | 233 g/kWh | 0–900 g/kWh | Average CO₂ emissions per kWh from the electrical grid |
| 💨 **ICE CO₂ emissions** | 120 g/Km | 50–400 g/Km | CO₂ output per Km of the reference ICE vehicle |

> ℹ️ **Validation:** The main calculator requires `startBattery > currentBattery` and `kilometersTraveled > 0`. If the inputs are invalid, all dependent tabs display a "no results" placeholder automatically.

---

### 📊 Stats Tab

The **Stats** tab is the primary output screen, displaying a grid of computed metrics derived from the main input panel.

Computed values shown:

- **⚡ Consumption** — Real-world efficiency in `kWh/100Km`, calculated as:  
  `consumptionKwh100km = (energyUsedKwh / kilometersTraveled) × 100`

- **🏁 Efficiency** — Inverse metric in `Km/kWh`:  
  `efficiencyKmKwh = kilometersTraveled / energyUsedKwh`

- **🔌 Energy used** — Actual kWh drawn from the battery:  
  `energyUsedKwh = (usedPct / 100) × batteryCapacity`

- **💰 Trip cost** — Total electricity cost for the recorded drive:  
  `tripCost = energyUsedKwh × kwhPrice`

- **📏 Cost per Km** — Granular cost metric in `€/Km`

- **🗺️ Remaining range** — Estimated distance drivable from current SoC down to the minimum buffer:  
  `remainingRange = (currentBattery - minBattery) × kmPerPercent`

- **🌍 Projected full range** — Extrapolated full-charge real-world range:  
  `fullRangeReal = kmPerPercent × 100`

- **📊 WLTP ratio** — How your real range compares to the manufacturer's claim:  
  `wltpRatio = (fullRangeReal / wltpRange) × 100%`

- **⛽ ICE equivalent cost** — How many Km an ICE car could travel for the same money

- **📐 Equivalent ICE efficiency** — EV efficiency expressed as equivalent `L/100Km`:  
  `equivalentEfficiency = (fuelPrice / kwhPrice) × efficiencyKmKwh`

- **💸 ICE cost per kWh equivalent** — Effective cost of petrol per kWh of energy

- **🔋 Buffer energy** — kWh stored below the minimum SoC threshold

- **📍 Km per % SoC** — Granular consumption indicator

- **⛽ Equivalent ICE refuel cost** — The total petrol cost an ICE vehicle would incur to cover the same distance:  
  `iceRefuelCost = (kilometersTraveled / fuelConsumption) × fuelPrice`

- **💚 BEV vs ICE cost gain** — The monetary saving achieved by driving electric instead of the reference ICE vehicle:  
  `bevVsIceCostGain = iceRefuelCost - tripCost`

A **📋 Copy Summary** button exports all key metrics as a formatted plain-text block directly to the clipboard for easy sharing.

---

### 🔋 Autonomy Tab

The **Autonomy** tab provides a visual and numerical representation of the current battery status.

**🎨 Animated Battery Visual:**
- A horizontal battery widget fills proportionally to the current SoC percentage
- The fill color transitions dynamically: **green** (>30%) → **amber** (15–30%) → **red** (<15%)
- A **red dashed vertical marker** (`Buffer`) shows where the minimum SoC threshold is
- A **blue dashed vertical marker** (`Start`) shows where the drive started
- A large percentage label below updates in real time

**📐 Residual Autonomy Figures:**
- Displays the main remaining range figure prominently in large typography
- Shows the usable remaining SoC percentage (current minus buffer)

---

### 🗺️ Trip Estimator Tab

The **Trip Estimator** predicts what a *future* trip will cost and consume, using the **real baseline consumption** derived from the last recorded drive as the starting point. It applies three adjustment multipliers:

| 🏷️ Factor | 📐 Formula | 📝 Notes |
|---|---|---|
| 🌡️ **Temperature** | `1 + (20 - T) × 0.015` for T < 20°C; `1 - (T - 20) × 0.005` for T > 20°C | Cold weather increases consumption; hot weather slightly reduces it |
| 🏎️ **Speed** | Quadratic penalty above 90 Km/h; sub-linear benefit below 90 Km/h | Models aerodynamic drag increase at high speed |
| ❄️ **HVAC (Heating/AC)** | `× 1.15` when enabled | Adds 15% consumption overhead when climate control is active |

**Inputs for the estimator:**
- 📏 Trip distance (0–1000 Km)
- 🌡️ External temperature (−20°C to +50°C)
- 🚗 Average speed (10–250 Km/h)
- ❄️ Use Heating/AC checkbox

**Outputs:**
- ⚡ Adjusted consumption (kWh/100Km)
- 🔋 Estimated energy required (kWh)
- 📊 SoC that will be consumed (%)
- 🏁 Estimated final SoC on arrival (%)

> ⚠️ This tab requires the main calculator to have valid data first (baseline consumption must be established).

---

### ⚡ Charging Calculator Tab

The **Charging Calculator** estimates charging duration and costs for a given charger power and SoC range.

**Inputs:**
- ⚡ Average charging power (1–350 kW) — supports everything from home wallboxes to ultra-rapid DC chargers
- 🔋 Starting SoC (0–100%)
- 🎯 Target SoC (0–100%)
- 📡 Energy transfer efficiency (70–100%) — accounts for AC/DC conversion losses

**Calculation logic:**
```
kwhAdded       = ((targetSoc - startSoc) / 100) × batteryCapacity
kwhTransferred = kwhAdded / (transferEfficiency / 100)   ← includes wall-to-battery losses
timeHours      = kwhTransferred / chargePower
pctPerHour     = (chargePower × efficiency / batteryCapacity) × 100
```

**Outputs:**
- ⏱️ Total charging time (hours and minutes)
- ⚡ Net energy added to battery (kWh)
- 🔌 Gross energy drawn from the grid (kWh, includes efficiency losses)
- 💰 Net charging cost (€)
- 💸 Gross charging cost (€, including losses)
- 📈 Charge rate (% SoC per hour)
- 🏷️ Charger type badge (Slow / Fast / Rapid / Ultra-rapid) — automatically inferred from power level

> ℹ️ Note: Assumes a **linear charging curve**. Real-world charging slows above ~80% SoC on most vehicles.

---

### 🏎️ Speed vs Range Tab

The **Speed vs Range** tab renders an interactive **canvas chart** showing how estimated range changes across driving speeds, modelling aerodynamic drag using a v² scaling law.

**How it works:**
- Uses the baseline real consumption (from the main calculator) as the reference point at a reference speed (~90 Km/h)
- Applies an aerodynamic correction factor for each speed step: `adjustedCons = baseCons × (speed / refSpeed)²`  
  (with a small rolling-resistance floor to avoid unrealistically low values at very low speeds)
- Draws a smooth curve from ~30 Km/h to 200+ Km/h
- Shows a **data table** below the chart with speed/range pairs at fixed intervals (e.g. 50, 80, 90, 110, 130, 150 Km/h)

The chart **re-draws automatically** on window resize and whenever the tab becomes visible.

---

### 🧮 Battery Health Tab

The **Battery Health (SoH) Estimator** helps you track the long-term degradation of your battery pack.

**Methodology:**  
Compares the *measured real-world range* you actually experience at full charge against the vehicle's WLTP rated range to derive an estimated State of Health percentage:
```
SoH = (measuredRange / wltpRange) × 100%
```

**🎨 Arc Gauge Visual:**
- An SVG semi-circular arc gauge fills from 0% to the computed SoH
- Color transitions: 🟢 green (>80%), 🟡 amber (60–80%), 🔴 red (<60%)
- Smooth animated transition on value change

**📋 SoH Session Log:**
- Each time SoH is computed, a session entry is saved with the **date**, **measured range**, and **SoH %**
- Log entries persist across sessions via `localStorage`
- A 🗑️ **Clear Log** button wipes the history after confirmation

---

### 🌿 CO₂ Savings Tab

The **CO₂** tab quantifies the environmental benefit (or lack thereof) of driving electric versus a conventional ICE vehicle, based on your personal grid carbon intensity.

**Calculations:**
```
evCO2Trip    = energyUsedKwh × gridCo2      (grams)
iceCO2Trip   = kilometersTraveled × iceCo2  (grams)
co2Saved     = iceCO2Trip - evCO2Trip       (grams)
co2SavedPct  = (co2Saved / iceCO2Trip) × 100
```

**Outputs:**
- 🔌 CO₂ emitted by the EV for this trip (g and kg)
- 🚗 CO₂ that the reference ICE vehicle would have emitted (g and kg)
- 🌿 CO₂ saved vs ICE (g, kg, and percentage)
- 📊 EV CO₂ per Km (g/Km)

> 💡 The result adapts to your local electricity grid: a coal-heavy grid will show less savings than a renewable-heavy one. You can customise the `Grid CO₂ intensity` field in the main panel.

---

### 📍 Trip Log Tab

The **Trip Log** provides persistent historical tracking of your drives.

**Logging:**
- Click **📍 Log Current Trip** to save the current calculator state as a timestamped entry
- Each entry records: 📅 date/time, 📏 distance (Km), ⚡ consumption (kWh/100Km), 💰 trip cost (€)
- The log holds up to **50 entries** (oldest automatically removed when the cap is reached)
- The app automatically switches to the Trip Log tab after logging

**Log Display:**
- All entries listed in reverse chronological order (newest first)
- Each entry has a ✕ **delete button** to remove individual records
- When 2+ entries exist, an **averages summary** is shown below the list:
  - 📏 Total Km logged (sum)
  - ⚡ Average consumption (mean kWh/100Km)
  - 🔢 Number of trips logged

---

### 🧮 Quick Calculator Tab

An always-available **standalone calculator** embedded within the app for ad-hoc arithmetic while planning your drives.

**Calculator Features:**
- Standard 4-function arithmetic: `+`, `−`, `×`, `÷`
- Parentheses support for complex expressions: `(`, `)`
- Decimal point input
- `C` (clear all) and `←` (backspace/delete last character) keys
- Supports chaining operations (result becomes input for next operation)
- Error handling for invalid expressions

**📜 History Tape:**
- Every completed calculation is appended to a scrollable **history tape** on the right
- Each entry shows the full expression and its result
- History is session-only (not persisted to `localStorage`)

**⚡ SoC ↔ Km Converter (bonus tool):**
A two-way live converter embedded below the calculator:
- Enter a **SoC %** → instantly see the corresponding **Km range**
- Enter a **Km distance** → instantly see the required **SoC %**
- Uses the `Km per % SoC` ratio computed from the main calculator
- Updates in real time as you type

> ℹ️ The converter requires valid main calculator data to function (Km/% must be established first).

---

## 🚗 Vehicle Presets

Vehicle profiles allow you to switch between multiple EVs (or configurations) instantly without re-entering data.

**Each preset stores:**
- 🔋 Usable battery capacity (kWh)
- 📄 WLTP rated range (Km)
- ⛽ ICE reference fuel consumption (Km/L) — for cost/CO₂ comparisons

**Operations:**
- **💾 Save** — prompts for a name and saves the current values as a new named profile
- **📂 Load** — select a preset from the dropdown to instantly apply its values and recompute all tabs
- **🗑️ Delete** — removes the selected preset after confirmation

Presets are persisted in `localStorage` along with the rest of the application state.

---

## 🌗 Theme System

EV Master supports both **dark** and **light** themes with smooth animated transitions.

- The theme toggle button (☀️ / 🌙) is permanently visible in the top-right corner of the header
- The active theme is stored in `localStorage` and restored on next visit
- All colors are defined via **CSS custom properties** (`--bg-dark`, `--accent-blue`, etc.), making the theme toggle a single `data-theme` attribute switch on `<body>`

| 🎨 Variable | 🌑 Dark | ☀️ Light |
|---|---|---|
| Background | `#020617` | `#ffffff` |
| Card | `#0f172a` | `#e9e9e9` |
| Accent Blue | `#60a5fa` | `#65addd` |
| Accent Green | `#34d399` | `#047857` |
| Accent Red | `#f87171` | `#b91c1c` |
| Accent Amber | `#fbbf24` | `#b45309` |
| Accent Purple | `#fd78d1` | `#ff62cb` |

---

## 💾 Persistence & Storage

All application state is automatically saved to **`localStorage`** under the key `evMasterState` as a JSON object. This includes:

| 🏷️ Key | 📝 Description |
|---|---|
| `startBattery`, `currentBattery`, `kilometersTraveled`, `minBattery` | Core drive inputs |
| `batteryCapacity`, `wltpRange` | Vehicle specs |
| `kwhPrice`, `fuelPrice`, `fuelConsumption` | Pricing configuration |
| `gridCo2`, `iceCo2` | Emissions factors |
| `tripDistance`, `externalTemp`, `averageSpeed`, `useHeatingAc` | Estimator inputs |
| `chargePower`, `chargeStartSoc`, `chargeTargetSoc`, `transferEfficiency` | Charging inputs |
| `theme` | UI theme preference (`'dark'` or `'light'`) |
| `presets` | Named vehicle profiles (object map) |
| `selectedPreset` | Last selected preset name |
| `tripLog` | Array of up to 50 logged trip objects |
| `healthLog` | Array of SoH session records |

State is saved on **every input change** — no manual save button required.

---

## 📱 Progressive Web App (PWA)

EV Master is configured as a **fully installable PWA**:

- **`manifest.json`** — defines app name (`EV Master`), icons (192×192 and larger), theme color (`#000000`), display mode, and start URL
- **`sw.js`** — a Service Worker is registered on page load for offline caching support
- **Meta tags** — includes `apple-mobile-web-app-capable`, `apple-mobile-web-app-status-bar-style`, and `mobile-web-app-capable` for full-screen experience on iOS and Android
- **`favicon.ico`** and **`icon-192x192.png`** — app icons for home screen and browser tab

To install on mobile: open the URL in your browser → tap **"Add to Home Screen"** → launch as a standalone app.

---

## ⚙️ Technical Architecture

| 🏷️ Aspect | 📝 Details |
|---|---|
| 🗂️ **Structure** | Single self-contained HTML file — all CSS and JS are inline |
| 🔧 **Runtime** | Vanilla JavaScript (ES6+), no frameworks or libraries |
| 🎨 **Styling** | Pure CSS with custom properties; responsive grid layout |
| 📐 **Layout** | CSS Grid — single column on mobile, `5fr / 7fr` two-column on ≥1024px |
| 📊 **Chart** | Native HTML5 `<canvas>` API (no Chart.js or similar) |
| 💾 **Storage** | Browser `localStorage` only — zero server communication |
| 📱 **PWA** | Web App Manifest + Service Worker registration |
| ♿ **Inputs** | All numeric fields are paired with `<input type="range">` sliders, synced bidirectionally |
| 🔄 **State** | Single `state` object; any change triggers a full `updateUI()` re-render cycle |

---

## 🚀 Getting Started

No installation or build step required.

```bash
# Clone the repository
git clone https://github.com/GianfrancoPiazzolla/EV-Master.git

# Open the app
cd EV-Master
open index.html
```

Or simply **open `index.html`** directly in any modern browser (Chrome, Firefox, Safari, Edge).

For PWA installation with offline support, serve the files over HTTP/HTTPS (e.g. via `npx serve .` or any static file server) so the Service Worker can register correctly.

---

## 👤 Author

**Gianfranco Piazzolla**  
🔗 [GitHub Profile](https://github.com/GianfrancoPiazzolla)

---

## 📜 License

Distributed under the **MIT License**. Feel free to use, modify, and share.

---

> 🌱 *Developed for the sustainable mobility community. If you find this tool helpful, please leave a ⭐ on GitHub!*
