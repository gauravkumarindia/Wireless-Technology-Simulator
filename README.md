# WirelessNet Sim Lab — Drag • Connect • Simulate

An interactive React-based wireless network planning simulator with drag-and-drop device & tower placement, algorithm-based resource allocation, and real-time performance visualization.

[React](https://img.shields.io/badge/React-18-blue)
[License](https://img.shields.io/badge/License-MIT-green)
[Status](https://img.shields.io/badge/Status-Active-brightgreen)

### 🔗 Live Demo
> Host the `build` or drop the artifact HTML file into any static host (Vercel, Netlify, GitHub Pages).

---

## ✨ Features

### 1. Select Mobile Devices (Drag & Drop)
Drag from palette to canvas:
- **📱 Smartphone** – 8 Mbps demand, high mobility
- **💻 Laptop** – 20 Mbps demand, medium power
- **📟 IoT Sensor** – 1 Mbps demand, low power
- **🥽 AR Headset** – 35 Mbps demand, high QoS requirement

Each device calculates path loss and signal strength based on distance.

### 2. Select Tower / Base Station
- **🏗️ Macro Tower** – Range: 300px, Capacity: 150 Mbps, Freq: 2.4 GHz
- **📡 Small Cell** – Range: 150px, Capacity: 80 Mbps, Freq: 3.5 GHz
- **📶 5G mmWave** – Range: 100px, Capacity: 300 Mbps, Freq: 28 GHz

Visual coverage circles, dashed for weak zones. Reposition by dragging, double-click to delete.

### 3. Choose Algorithm
Select scheduling strategy in right panel:

| Algorithm | Principle | Fairness | Throughput | Use Case |
|-----------|-----------|----------|------------|----------|
| **Round Robin** | Equal time slots per user | High | Low | Baseline fairness test |
| **Max CQI / Max Throughput** | Best channel gets all resources | Low | Very High | Throughput maximization |
| **Proportional Fair** | `score = instantaneous_rate / avg_rate` | Medium | High | Industry standard (LTE/5G) |
| **Weighted Fair (QoS-aware)** | Priority: AR > Laptop > Smartphone > IoT | Medium | High | QoS / slice simulation |

> Formula displayed: `Path Loss (dB) = -30 - 20*log10(d+1) - freq_factor`

### 4. Simulate and Get Results
Click **▶ Run Simulation**

**Visualization:**
- Connection lines color-coded by signal: Green > -70 dBm (Strong), Yellow -85 to -70 dBm, Red < -85 dBm
- Pulsing animation during simulation
- Nearest tower association within range check

**Metrics Calculated:**
- Avg Throughput (Mbps)
- Avg Latency (ms) = `10 + distance*0.1 + congestion_factor`
- Jain's Fairness Index: `(sum x)^2 / (n * sum x^2)`
- Coverage % and Connected Devices
- Total Capacity Utilization

**Results Panel:**
- Stat cards, bar chart (allocated vs demand), detailed table per device (Tower, Distance, Signal, Allocated, Latency, Status)
- Export to JSON, Reset

---

## 🚀 Getting Started

### Installation
```bash
git clone https://github.com/yourusername/wireless-sim-lab.git
cd wireless-sim-lab
npm install
npm start
```

### Build for Production
```bash
npm run build
# deploy /build to GitHub Pages / Vercel / Netlify
```

### GitHub Pages Deploy
```bash
npm install --save-dev gh-pages
# add to package.json: "homepage": "https://yourusername.github.io/wireless-sim-lab"
npm run deploy
```

---

## 🧠 How It Works

1. **Placement:** HTML5 Drag API – palette items set `dataTransfer`, canvas handles `onDrop` → creates object `{id, type, subtype, x, y}`
2. **Signal Model:** Simple log-distance path loss, frequency penalty for mmWave
3. **Association:** Device scans towers in range → if none, marked `Disconnected`
4. **Allocation:** Algorithm distributes tower capacity:
   - RR: `capacity / connected_count`
   - Max CQI: sort by signal strength descending, allocate full demand until capacity ends
   - PF: score with historical average (simulated as demand)
   - WF: weight by device priority

---

## 🗂️ Project Structure
```
/src
  App.jsx        # Main simulator (palette, canvas, controls, results)
  index.css      # Tailwind + grid background + animations
/public
  index.html
README.md
```

---

## 🛠️ Tech Stack
- **React 18** (Hooks: useState, useRef, useMemo)
- **Tailwind CSS** for styling / glassmorphism / neon theme
- **Pure JS** – No D3, no Chart.js (lightweight div-based bars)
- Drag & Drop: Native HTML5 API + mouse move for repositioning

---

## 📸 Screenshots
Add yours:
```
/screenshots/canvas-empty.png
/screenshots/simulation-run.png
/screenshots/results-panel.png
```

---

## 🔮 Future Improvements
- [ ] Interference modeling & SINR
- [ ] User mobility / handover simulation
- [ ] Shadowing & wall penetration loss
- [ ] 4G vs 5G vs WiFi 6 comparison mode
- [ ] Heatmap of signal strength
- [ ] Save/load topology

---

## 🤝 Contributing
PRs welcome! Please open an issue first for major changes.

```bash
git checkout -b feature/new-algorithm
git commit -m "feat: add EDF scheduler"
git push origin feature/new-algorithm
```


---

## 👨‍💻 Author
Built for wireless communication education & network planning demos.
If you use this for teaching, please star ⭐ the repo!

**Enjoy simulating!** Drag • Connect • Simulate.
