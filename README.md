EV Master is a high-performance web-based calculator designed for Electric Vehicle (EV) owners. It provides real-time insights into driving efficiency, remaining range, and cost comparisons with Internal Combustion Engine (ICE) vehicles. Built as a lightweight, single-file web application, it features a modern dark-themed interface with glassmorphism effects and is PWA-ready for mobile devices.

KEY FEATURES

Dynamic Autonomy Tracking: Instantly calculates expected residual range based on actual consumption and a user-defined battery buffer.

Advanced Trip Statistics:

Consumption Metrics: Displays efficiency in both kWh/100Km and Km/kWh.

Cost Analysis: Calculates total trip cost and cost per kilometer based on local energy prices.

Energy Monitoring: Tracks total kWh consumed and energy remaining at the set safety limit.

ICE Comparison Engine: Compares EV efficiency against fuel prices to show equivalent Km/L and the distance an ICE vehicle would travel with the same budget.

Interactive Battery Visualization: Features a visual battery gauge that updates in real-time, highlighting the Start point and Buffer limit.

Built-in Chronology Calculator: A specialized utility with a computation tape history to assist in multi-step trip planning.

Persistent Settings: Automatically saves vehicle specifications, battery capacity, and energy costs to localStorage.

TECHNICAL OVERVIEW

Frontend: Pure HTML5 and CSS3 using custom properties for theme management.

Logic: Vanilla JavaScript (ES6+) with no external dependencies.

Responsiveness: Mobile-first design using CSS Grid and Flexbox, optimized for desktop and handheld displays.

PWA Integration: Includes support for manifest.json and Service Workers for offline capabilities and home-screen installation.

CORE CALCULATIONS

The application performs precise calculations using the following logic:

Residual Autonomy: Remaining Km = (Traveled Km / Used %) * (Current % - Buffer %).

Equivalent Fuel Efficiency: Eq Km/L = (Fuel Price / kWh Price) * EV Efficiency (Km/kWh).

GETTING STARTED

Clone the repository to your local machine.

Open index.html in any modern web browser.

The app is ready to use immediately without further configuration.
