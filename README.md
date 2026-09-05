# AutoLight-Civic

**AutoLight-Civic** is an AI-driven, next-generation Smart City Municipal Streetlighting and Automated Maintenance Operations Platform. Designed for modern urban municipal corporations, AutoLight replaces traditional static streetlights with adaptive PWM dimming mesh networks, automated Computer Vision (YOLO) fault detection, graph-based maintenance crew routing (NetworkX TSP), and comprehensive ESG/Carbon footprint telemetry with downloadable municipal compliance reports.



## 🌟 Key Features

### 1. ⚡ Adaptive Municipal Streetlighting Mesh
- **Standby Mode (20% PWM / 20W):** Dynamic baseline reduction when corridors are idle.
- **Motion-Triggered Ramping:** Real-time 100% active illumination on motion detection, plus **60% predictive downstream light cascading** for approaching vehicles/pedestrians.
- **Heavy Fog / Monsoon Amber Mode:** Adaptive 3000K anti-glare color temperature shifts based on ambient humidity and visibility metrics.
- **Emergency Green Corridor Override:** Instant priority lighting corridors for ambulances and fire engines.

### 2. 👁️ Computer Vision & Dark-Patch Fault Detection
- Synthetic **YOLOv8 + OpenCV** inference simulation for live camera streams (`CAM-01`, `CAM-02`, `CAM-03`).
- **Dark-Patch ROI Luminance Analysis:** Automated detection of burnt-out LEDs and circuit trips, instantly generating geotagged critical fault tickets.

### 3. 🚚 Autonomous Maintenance Crew Dispatch & TSP Routing
- Built-in **NetworkX + Haversine spatial graph solver** for Traveling Salesperson Problem (TSP) route optimization.
- Automatically calculates the shortest turn-by-turn repair dispatch route from the Central Depot through all active fault locations, minimizing fuel usage and transit times.

### 4. 📊 ESG & Sustainability Telemetry Dashboard
- Real-time tracking of kWh energy saved vs. 100W static baseline lighting grids.
- Computes CO₂ emission offset (kg/tonnes), monetary electricity cost savings (₹/INR), and Carbon Credits accrued.
- **Automated PDF Export:** Generates official municipal compliance reports (built with ReportLab) ready for government tenders and ESG audits.

### 5. 🗺️ Live Digital Twin & Real-time Web Platform
- Built with **React 18**, **Leaflet**, and **Recharts**.
- Full WebSocket support (`/ws`) for live bidirectional telemetry updates and grid state streaming.
- Built-in **Simulation Control Panel** for live demoing: inject traffic motion, trigger fixture faults, adjust weather parameters, and toggle emergency overrides.



## 🏗️ System Architecture

```mermaid
graph TD
    subgraph Frontend Client
        UI[React 18 + Vite Web App]
        Map[Leaflet Digital Twin Map]
        ESG[ESG & Compliance Dashboard]
        WSClient[WebSocket Listener]
    end

    subgraph Backend Core (FastAPI)
        API[FastAPI REST & WS Endpoints]
        Sim[Background Simulation Loop]
        CV[CV & Dark-Patch Analyzer]
        Path[NetworkX TSP Route Optimizer]
        ESGEng[ESG Metric Calculator]
        PDFGen[ReportLab PDF Engine]
    end

    subgraph Database
        DB[(SQLite / SQLModel autolight.db)]
    end

    UI -->|REST Requests| API
    UI -->|Live Feeds| WSClient
    API <-->|SQLModel| DB
    API <-->|WebSocket Stream| WSClient
    Sim -->|Grid Ramping & Faults| DB
    CV -->|Synthetic Frames & Dark Patch| API
    Path -->|Haversine Graph Solve| DB
    ESGEng -->|Calculate Savings| DB
    PDFGen -->|PDF Report Byte Stream| API
