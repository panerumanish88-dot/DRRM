# 🚨 Disaster Relief Command Center

<p align="center">
  <img src="https://img.shields.io/badge/Node.js-v18+-green?style=for-the-badge&logo=node.js">
  <img src="https://img.shields.io/badge/Express.js-4.18+-black?style=for-the-badge&logo=express">
  <img src="https://img.shields.io/badge/JavaScript-ES6+-yellow?style=for-the-badge&logo=javascript">
  <img src="https://img.shields.io/badge/Leaflet.js-Interactive%20Maps-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/MongoDB-Ready-success?style=for-the-badge&logo=mongodb">
  <img src="https://img.shields.io/badge/License-MIT-brightgreen?style=for-the-badge">
</p>

<p align="center">
  <b>Full-Stack Disaster Relief Resource Allocation & Route Optimization Platform</b>
</p>

<p align="center">
Helping NGOs, Government Agencies and Emergency Response Teams efficiently manage relief operations during disaster situations.
</p>

---


### 📋 Table of Contents

- Features
- Tech Stack
- System Architecture
- Project Structure
- Installation & Setup
- Usage
- Network Overview Map
- API Documentation
- Algorithms
- Troubleshooting
- Future Enhancements
- License

---

# ✨ Features

## Core Functionality

| Feature | Description |
|----------|------------|
| 🗺️ Network Overview Map | Interactive Leaflet.js map showing centers, areas, and roads |
| 🎯 Priority Scoring Engine | Automatically ranks affected areas using weighted scoring |
| 📦 Resource Management | Track inventories and resource requirements |
| 🛣️ Route Optimization | Dijkstra's shortest path computation |
| 🔀 Multi-Stop Routing | Nearest-Neighbour TSP heuristic |
| 📊 Dashboard Analytics | Real-time statistics and monitoring |
| 🔄 What-If Simulation | Block/unblock roads and test impact |
| 💾 Data Persistence | In-memory storage with MongoDB-ready structure |
| 🔌 REST API | Complete backend API |


## 🗺️ Map Features (v1.1)

The **Network Overview Map** provides a real-time visual representation of relief operations, enabling responders to monitor resources, affected areas, and transportation networks efficiently.

### Key Features

| Feature | Description |
|----------|------------|
| 🟢 Relief Center Markers | Interactive green markers displaying inventory information through popups |
| 🔴🟠🔵 Priority-Based Area Markers | Color-coded affected areas based on urgency level (High, Medium, Low) |
| ✨ Critical Area Highlighting | Animated pulse effect for high-priority zones requiring immediate attention |
| 🛣️ Open Road Visualization | Blue polylines showing active road connections with distance and travel-time details |
| 🚫 Blocked Road Detection | Red dashed lines indicating inaccessible or blocked routes |
| 🎛️ Layer Controls | Toggle visibility of relief centers, affected areas, and road networks independently |
| 🎯 Fit-All Navigation | Instantly zoom and center the map to display the entire operational network |
| 🔄 Auto Refresh | Automatically updates whenever centers, areas, roads, or simulations change |
| 🌙 Command Center Theme | Dark-themed OpenStreetMap styling optimized for emergency operations dashboards |

### Visual Indicators

| Element | Meaning |
|----------|---------|
| 🟢 Green Marker | Relief Center |
| 🔴 Red Marker | High Priority Area |
| 🟠 Orange Marker | Medium Priority Area |
| 🔵 Blue Marker | Low Priority Area |
| 🔵 Blue Line | Open Road |
| 🚫 Red Dashed Line | Blocked Road |

### Benefits

✅ Improved Situational Awareness

✅ Faster Decision Making

✅ Real-Time Network Monitoring

✅ Better Route Planning

✅ Enhanced Disaster Response Coordination
---

# 🛠️ Tech Stack

## Backend

| Component | Technology |
|------------|------------|
| Runtime | Node.js |
| Framework | Express.js |
| Database | In-Memory Database |
| Future Upgrade | MongoDB |
| Middleware | cors, dotenv |
| Dev Server | nodemon |

## Frontend

| Component | Technology |
|------------|------------|
| Structure | HTML5 |
| Styling | CSS3 |
| Logic | Vanilla JavaScript |
| Mapping | Leaflet.js |
| API Calls | Fetch API |

---

# 🏗️ System Architecture

```text
CLIENT (Browser)
│
├── HTML5
├── CSS3
├── JavaScript
└── Leaflet.js
        │
        ▼
EXPRESS.JS SERVER
│
├── REST APIs
├── Priority Engine
├── Routing Engine
└── Resource Manager
        │
        ▼
DATABASE
│
├── Relief Centers
├── Affected Areas
└── Road Network
```

Node ID Convention
Centers use their raw IDs (1, 2, 3...). Areas are stored in the routing graph as area.id + 1000 (e.g. area #1 → node 1001). This prevents ID collisions when both types share the same graph — used consistently across database.js, routingEngine.js, and the frontend map.

# 📁 Project Structure

```text
DRRM/
│
├── backend/
│   ├── server.js
│   ├── database.js
│   ├── priorityScorer.js
│   ├── routingEngine.js
│   ├── package.json
│   └── .env
│
├── frontend/
│   ├── index.html
│   ├── app.js
│   └── style.css
│
├── API.md
├── ALGORITHMS.md
└── README.md
```

# 📦 Installation & Setup

## Prerequisites

- Node.js v18+
- npm
- Modern Browser

## Install Dependencies

```bash
cd backend
npm install
```

## Start Server

```bash
npm run dev
```

Server:

```text
http://localhost:3000
```

---

# 🚀 Usage

## Basic Workflow

### 1️⃣ Dashboard & Network Overview

After launching the application, the **Network Overview Map** loads automatically.

#### Map Indicators

🟢 **Green Markers** → Relief Centers

🔴 **Red Markers** → High Priority Areas

🟠 **Orange Markers** → Medium Priority Areas

🔵 **Blue Markers** → Low Priority Areas

🛣️ **Blue Lines** → Open Roads

🚫 **Red Dashed Lines** → Blocked Roads

> By default, **Road #7** is blocked in the sample dataset.

---

### 2️⃣ Calculate Priority Scores

Navigate to the **Priority Scoring** tab and click:

```text
Calculate All Priorities
```

The system evaluates all affected areas using:

- Disaster Severity
- Population Impact
- Accessibility Difficulty

#### Priority Levels

| Level | Score Range | Color |
|---------|------------|---------|
| High | ≥ 0.7 | 🔴 Red |
| Medium | ≥ 0.4 | 🟠 Orange |
| Low | < 0.4 | 🔵 Blue |

Map markers update automatically after scoring.

---

### 3️⃣ Route Planning

Navigate to the **Route Planning** tab.

#### Steps

1. Select a Relief Center
2. Select an Affected Area
3. Choose Routing Mode:
   - Distance Optimized
   - Time Optimized
4. Click **Find Shortest Route**

The system computes the shortest path using **Dijkstra's Algorithm**.

---

### 4️⃣ Multi-Stop Route Optimization

For deliveries involving multiple locations:

1. Select multiple affected areas
2. Click:

```text
Plan Multi-Stop Route
```

The application uses a **Nearest-Neighbour TSP Heuristic** to generate an efficient delivery sequence.

---

### 5️⃣ Resource Management

Navigate to the **Resource Management** tab.

You can:

✅ Add Relief Centers

✅ Add Affected Areas

✅ Add Road Connections

Changes are reflected instantly across:

- Dashboard
- Analytics
- Network Map

---

### 6️⃣ What-If Simulation

Navigate to the **What-If Analysis** tab.

#### Available Actions

- Block a Road
- Unblock a Road

Click:

```text
Run Simulation
```

The simulation updates network conditions without permanently modifying stored data.

Perfect for testing emergency scenarios before taking action.

---

# 📋 Sample Scenario

The project comes with preloaded demonstration data.

| Entity | Details |
|----------|----------|
| Central Relief Hub | 1000 Food Kits, 2000 Water Units, 500 Medical Kits |
| North District Warehouse | 800 Food Kits, 1500 Water Units, 400 Medical Kits |
| Flood Zone A | Severity 5 • 250 People • Difficult Access |
| Village Beta | Severity 3 • 150 People • Easy Access |
| Landslide Area C | Severity 4 • 400 People • Difficult Access |
| Road #7 | Blocked by Default |

---

# 🗺️ Network Overview Map

The interactive map serves as the operational center of the application.

## Key Features

✅ Real-Time Network Visualization

✅ Relief Center Tracking

✅ Priority-Based Area Highlighting

✅ Road Status Monitoring

✅ Layer Visibility Controls

✅ Interactive Popups

✅ Auto Refresh on Data Changes

---

## Map Layer System

| Layer | Purpose | Style |
|---------|---------|---------|
| centerLayer | Relief Centers | 🟢 Green Markers |
| areaLayer | Affected Areas | 🔴🟠🔵 Priority Colors |
| routeLayer | Road Network | 🔵 Open / 🔴 Blocked |

---

## Data Loading Sequence

Roads require valid coordinates before rendering.

```javascript
async function loadAllData() {
  await loadCenters();
  await loadAreas();
  await loadRoads();
}
```

This ensures all routes are drawn correctly.

---

## Dashboard Resize Fix

Leaflet cannot correctly calculate dimensions when hidden inside inactive tabs.

```javascript
if (targetTab === "dashboard" && networkMap) {
  setTimeout(() => networkMap.invalidateSize(), 50);
}
```

This guarantees proper map rendering whenever the Dashboard tab becomes active.

---

# 📡 API Documentation

### Base URL

```text
http://localhost:3000
```

---

## Standard Response Format

### Success Response

```json
{
  "success": true,
  "count": 3,
  "data": [...]
}
```

### Error Response

```json
{
  "success": false,
  "error": "Descriptive error message"
}
```

---

## Relief Centers API

| Method | Endpoint | Description |
|---------|----------|-------------|
| GET | /centers | Get all relief centers |
| GET | /centers/:id | Get center by ID |
| POST | /centers | Create center |
| PUT | /centers/:id | Update center |
| DELETE | /centers/:id | Delete center |

### Example Request

```json
{
  "name": "Dehradun Hub",
  "latitude": 30.3165,
  "longitude": 78.0322,
  "total_food_kits": 750,
  "total_water_units": 1500,
  "total_medical_kits": 250
}
```

---

## Affected Areas API

| Method | Endpoint |
|---------|----------|
| GET | /areas |
| GET | /areas/:id |
| POST | /areas |
| PUT | /areas/:id |
| DELETE | /areas/:id |

### Example Request

```json
{
  "name": "Kedarnath Village",
  "latitude": 30.7346,
  "longitude": 79.0669,
  "people_count": 500,
  "severity": 5,
  "access_difficulty": 1,
  "required_food_kits": 300,
  "required_water_units": 600,
  "required_medical_kits": 100
}
```

---

## Roads API

| Method | Endpoint |
|---------|----------|
| GET | /roads |
| POST | /roads |
| PUT | /roads/:id |
| DELETE | /roads/:id |

### Example Request

```json
{
  "from_location_id": 1,
  "to_location_id": 1001,
  "distance_km": 15.5,
  "travel_time_minutes": 45,
  "is_blocked": false
}
```

---

## Analytics & Routing APIs

| Method | Endpoint | Purpose |
|---------|----------|---------|
| POST | /compute-priorities | Calculate priorities |
| POST | /allocate-resources | Allocate resources |
| GET | /routes | Find shortest route |
| POST | /routes/multi-stop | Multi-stop routing |
| POST | /simulate | Scenario simulation |

---

## Quick API Testing

### Health Check

```bash
curl http://localhost:3000/
```

### Get Centers

```bash
curl http://localhost:3000/centers
```

### Compute Priorities

```bash
curl -X POST http://localhost:3000/compute-priorities
```

### Find Route

```bash
curl "http://localhost:3000/routes?centerId=1&areaId=2&useTime=false"
```

### Block Road

```bash
curl -X PUT http://localhost:3000/roads/7 \
-H "Content-Type: application/json" \
-d '{"is_blocked": true}'
```


---


# 🧮 Algorithms

## 1️⃣ Priority Scoring Engine

The system automatically ranks affected areas based on urgency using a weighted scoring formula.

### Formula

```text
P = 0.5 × (Severity / 5)
  + 0.3 × (Population / Max Population)
  + 0.2 × Access Difficulty
```

### Weight Distribution

| Factor | Weight | Purpose |
|----------|----------|----------|
| Severity | 50% | Measures immediate danger to life |
| Population Impact | 30% | Higher population means greater demand |
| Accessibility Difficulty | 20% | Hard-to-reach areas may require priority scheduling |

### Example Calculation

```text
Flood Zone A

Severity = 5
Population = 250
Max Population = 400
Access Difficulty = 1

P = 0.5(1.0)
  + 0.3(0.625)
  + 0.2(1)

P = 0.8875
```

🔴 Result: **High Priority Area**

### Complexity

```text
O(n log n)
```

---

## 2️⃣ Route Optimization (Dijkstra Algorithm)

Used to determine the shortest and most efficient route between relief centers and affected areas.

### Process

1. Initialize source node distance as `0`
2. Set all other node distances to `∞`
3. Select the nearest unvisited node
4. Update neighboring distances
5. Repeat until destination is reached
6. Reconstruct the shortest path

### Key Features

✅ Distance-Based Routing

✅ Travel-Time Optimization

✅ Blocked Road Avoidance

✅ Dynamic Network Support

### Complexity

```text
O(V²)
```

Future optimization can reduce complexity to:

```text
O((V + E) log V)
```

using a Priority Queue (Min Heap).

---

## 3️⃣ Multi-Stop Route Planning

The system uses the **Nearest Neighbour TSP Heuristic** to efficiently visit multiple affected areas.

### Workflow

```text
Start at Relief Center
        ↓
Find Nearest Area
        ↓
Visit Area
        ↓
Find Next Nearest Area
        ↓
Repeat Until Complete
        ↓
Return to Base
```

### Benefits

✅ Fast Execution

✅ Near-Optimal Routes

✅ Suitable for Emergency Logistics

### Complexity

```text
O(N²)
```

---

## 4️⃣ Resource Allocation Engine

When resources are limited, supplies are distributed proportionally among affected areas.

### Formula

```text
ratio = min(totalAvailable / totalRequired, 1.0)

allocation = required × ratio
```

### Example

```text
Available Food Kits = 500
Required Food Kits = 1000

Ratio = 500 / 1000 = 0.5

Area Requirement = 200

Allocated = 200 × 0.5 = 100 Kits
```

### Benefits

✅ Fair Distribution

✅ Prevents Resource Starvation

✅ Supports Large-Scale Operations

---

# 🐛 Troubleshooting

| Issue | Possible Cause | Solution |
|---------|---------|---------|
| Dashboard shows zero data | Backend not running | Start backend and refresh |
| Map tiles not loading | No internet connection | Check network connectivity |
| CORS error | Incorrect API endpoint | Verify backend URL and port |
| Route not found | Roads are blocked | Unblock roads or add alternate routes |
| Priority scores remain zero | Priorities not computed | Run "Calculate Priorities" |
| Dependencies missing | npm packages not installed | Run `npm install` |
| Port already in use | Another service using port 3000 | Change PORT in `.env` |

---

# 🚀 Future Enhancements

### Database & Infrastructure

- MongoDB Atlas Integration
- Redis Caching Layer
- Docker Deployment Support

### Real-Time Features

- Socket.io Live Updates
- Real-Time Road Status Monitoring
- Multi-User Collaboration

### Security

- JWT Authentication
- Role-Based Access Control (RBAC)
- Audit Logging

### AI & Analytics

- Disaster Severity Prediction
- Demand Forecasting
- Resource Optimization using ML

### Routing Improvements

- A* Pathfinding Algorithm
- Multi-Vehicle Route Optimization
- Route Visualization on Interactive Map
- 2-Opt Route Refinement

### Integrations

- WhatsApp Notifications
- SMS Alerts
- IoT Sensor Data Integration
- Satellite Imagery Support

### User Experience

- Mobile Responsive Dashboard
- Offline Mode Support
- Multi-Language Support

---

# 📄 License

Licensed under the **MIT License**.

---

# 👨‍💻 Author

### Manish Paneru

📧 **Email:** panerumanish88@gmail.com

🔗 **GitHub:** https://github.com/panerumanish88-dot

💻 Full Stack Developer | DSA Enthusiast | Open Source Learner

---

# 🙏 Acknowledgments

- India Disaster Resource Network (IDRN)
- National Disaster Management Authority (NDMA)
- OpenStreetMap Contributors
- Leaflet.js Community
- MongoDB Community
- Express.js Community

---

⭐ If you found this project useful, consider giving it a star.

**Made with ❤️ by Manish Paneru**


