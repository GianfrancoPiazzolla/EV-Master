# ⚡ EV Master

**EV Master** is an all-in-one Web App designed for Electric Vehicle (EV) drivers. It allows users to analyze real-world consumption, estimate residual range, plan trips based on external conditions, and calculate charging costs and times.

---

## 🚀 Key Features

The tool is divided into intelligent modules that interact with your data:

* **📊 Travel & Consumption Statistics**: Calculates real consumption in kWh/100km, efficiency (Km/kWh), and compares costs against Internal Combustion Engine (ICE) equivalents.
* **🔋 Residual Autonomy**: A visual battery interface that estimates remaining kilometers based on your current driving efficiency and a custom "minimum buffer".
* **🛣️ Trip Estimator**: Predicts future trip consumption by adjusting your baseline data according to:
* External Temperature (°C).
* Average Speed (Km/h).
* Heating or Air Conditioning usage.


* **🔌 Charging Calculator**: Estimates the time and cost required to reach a target State of Charge (SOC).
* **💾 Vehicle Presets**: Save and delete specific vehicle profiles (e.g., Battery Capacity, ICE efficiency) to switch between different EVs quickly.
* **🧮 Quick Calculator**: A built-in calculator with a "computation tape" to keep track of quick math during trip planning.

---

## 📐 Calculation Logic

The app utilizes empirical correction factors for estimations:

* **Efficiency**: Derived from the ratio of energy used (based on % drop and battery capacity) to the distance traveled.
* **Environmental Impact**: The Trip Estimator applies penalties for low temperatures and high speeds to provide a realistic "worst-case" scenario.

---

## 🛠️ Tech Stack

Built to be fast, lightweight, and dependency-free:

* **HTML5**: Semantic structure.
* **CSS3**: Modern layout using Flexbox, Grid, and Custom Properties for the dark-themed UI.
* **JavaScript (ES6+)**: Logic for state management and calculations.
* **LocalStorage**: Used to persist user inputs and vehicle presets directly in the browser.
* **PWA Ready**: Includes metadata for mobile installation and a Service Worker template for offline capabilities.

---

## 📦 Installation & Usage

No installation or backend server is required.

1. **Clone the repository**:
```bash
git clone https://github.com/your-username/ev-master.git

```


2. **Open the app**: Simply open `index.html` in any modern web browser.
   
### 📱 Mobile Use (PWA)

If hosted on a secure (HTTPS) server like GitHub Pages, you can select "Add to Home Screen" on your mobile device to use it as a full-screen standalone application.

---

## 📝 License

Distributed under the MIT License. Feel free to use, modify, and share.

---

**Developed for the sustainable mobility community.**
*If you find this tool helpful, please leave a ⭐ on GitHub!*
