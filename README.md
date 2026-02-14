# EV Master 🚗⚡

**EV Master** is a sleek, professional web-based calculator designed for Battery Electric Vehicle (BEV) owners. It provides real-time insights into driving efficiency, trip estimation, and charging costs through a modern, responsive "dark-mode" dashboard.

---

## 🌟 Key Features

### 1. 📊 Trip Statistics & Consumption
* **📉 Real-world Efficiency:** Calculates $kWh/100km$ and $km/kWh$ based on actual battery usage.
* **🛣️ Residual Autonomy:** Dynamically predicts remaining range based on the current drive's efficiency.
* **⛽ ICE Comparison:** Compares electric drive costs and efficiency against Internal Combustion Engine (ICE) equivalents, including $km/L$.

### 2. 🔮 Trip Consumption Estimator
Predicts energy requirements for future trips by applying environmental and behavioral factors to your baseline consumption:
* **🌡️ Temperature Adjustment:** Accounts for cold or hot weather impacts on battery performance.
* **💨 Aerodynamic Scaling:** Uses a non-linear factor to account for increased drag at higher average speeds.
* **❄️ HVAC Impact:** Optional toggle to factor in the energy penalty for Heating or Air Conditioning usage.

### 3. 🔌 Charging Calculator
* **⏱️ Time Estimation:** Estimates the duration required to reach a target SoC based on charger power ($kW$).
* **💰 Cost Projection:** Calculates the total cost of a charging session based on your specific energy price.

### 4. 📂 Vehicle Profiles & Persistence
* **🚗 Custom Presets:** Save and manage multiple vehicle profiles (e.g., Battery Capacity) to quickly switch between different EVs.
* **💾 Local Storage:** All inputs, settings, and presets are automatically saved locally in your browser.

### 5. 🛠️ Integrated Tools
* **🔋 Battery Visualizer:** A real-time UI component showing current charge, starting point, and safety buffers.
* **🧮 Quick Calculator:** A built-in scratchpad with a "History Tape" for manual calculations.

---

## 📐 Calculation Logic

The app utilizes empirical correction factors for estimations:

* **Efficiency**: Derived from the ratio of energy used (based on % drop and battery capacity) to the distance traveled.
* **Environmental Impact**: The Trip Estimator applies penalties for low temperatures and high speeds to provide a realistic "worst-case" scenario.

The application calculates consumption using the following relationship:

$$Consumption\ (kWh/100km) = \left( \frac{Used\ SoC\ \%}{100} \times Capacity \right) \div \frac{Distance}{100}$$

## ⚙️ Technical Overview

The application is built as a **Progressive Web App (PWA)** using a lightweight, "zero-dependency" stack:
* 📄 **HTML5**: Semantic structure.
* 🎨 **CSS3**: Modern layout using Flexbox, Grid, and Custom Properties for the dark-themed UI.
* ⚡ **JavaScript (ES6+)**: Logic for state management and calculations.
* 💾 **LocalStorage**: Used to persist user inputs and vehicle presets directly in the browser.
* 📱 **PWA Ready**: Includes metadata for mobile installation and a Service Worker template for offline capabilities.

---

## 📦 Installation & Usage
1.  🛠️ **Clone the repository (optional):**
    ```bash
    git clone https://github.com/your-username/ev-master.git
    ```
2.  🚀 **Launch the App:**
    Simply open `index.html` in any modern web browser. No server or installation is required.
3.  📱 **Install as an App:**
    If hosted on a secure (HTTPS) server like GitHub Pages, you can select "Add to Home Screen" or "Install as App" on your mobile device to use it as a full-screen standalone application.
    
---

## 📄 License

Distributed under the **MIT License**. Feel free to use, modify, and share.

---

**Developed for the sustainable mobility community.**
*If you find this tool helpful, please leave a ⭐!*
