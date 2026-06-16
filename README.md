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


Map Features (New in v1.1)
✅ Green markers for relief centers with inventory popup
✅ Colour-coded area markers — Red (high priority), Orange (medium), Blue (low) with animated pulse on critical zones
✅ Blue polylines for open roads with distance/time tooltip
✅ Red dashed lines for blocked roads
✅ Layer toggles — show/hide centers, areas, or roads independently
✅ Fit All button to zoom map to encompass all data points
✅ Auto-refresh — map updates whenever data changes (add/remove/simulate)
✅ Dark tile theme — OpenStreetMap tiles filtered to match the command-centre aesthetic

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

Basic Workflow
1. Dashboard & Map

Open the app — the Network Overview Map loads automatically
Green dots = relief centers, coloured dots = affected areas, lines = roads
One dashed red line is visible by default (Road #7 is blocked in sample data)
2. Compute Priorities

Click the Priority Scoring tab
Click "Calculate All Priorities"
Areas are ranked by urgency score; map markers update colour instantly:
🔴 Red = High priority (score ≥ 0.7) — animated pulse ring
🟠 Orange = Medium priority (score ≥ 0.4)
🔵 Blue = Low priority (score < 0.4)
3. Plan a Route

Click the Route Planning tab
Select a relief center and an affected area
Optionally check "Optimize by Time" instead of distance
Click "Find Shortest Route" — the path is shown as a visual node chain
4. Multi-Stop Route

On the same tab, use the right panel to select multiple areas
Click "Plan Multi-Stop Route" — uses nearest-neighbour TSP heuristic
5. Add New Data

Click the Resource Management tab
Fill in any of the three forms (Add Center / Add Area / Add Road)
New entries appear in the dashboard lists and on the map immediately
6. What-If Simulation

Click the What-If Analysis tab
Select a road and choose Block or Unblock
Click "Run Simulation" — see how priorities would change without saving
The map updates to show the simulated road status
Sample Scenario (Built-in Data)
Entity	Details
Central Relief Hub	Lat 27.1767, Lng 78.0081 · 1000 food, 2000 water, 500 medical
North District Warehouse	Lat 27.25, Lng 78.10 · 800 food, 1500 water, 400 medical
Flood Zone A	Severity 5, 250 people, Difficult access
Village Beta	Severity 3, 150 people, Easy access
Landslide Area C	Severity 4, 400 people, Difficult access
Road #7	Village Beta ↔ Landslide Area C — BLOCKED by default


---

# 🗺️ Network Overview Map

The map is the centrepiece of the Dashboard tab. Here is how it works technically.

Initialisation
Leaflet is loaded from a CDN — no npm install required:

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.css"/>
<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.js"></script>
Layer System
Three independent L.layerGroup() instances allow toggling:

Layer	Contents	Style
centerLayer	Relief center markers	Green static circles
areaLayer	Affected area markers	Red/Orange/Blue by priority; pulse ring on high
routeLayer	Road polylines	Blue solid (open), Red dashed (blocked)
Correct Loading Order
Roads need coordinates to draw lines. The loading sequence is enforced with await:

async function loadAllData() {
  await loadCenters();  // populates locCoords for center IDs
  await loadAreas();    // populates locCoords for area IDs (id+1000)
  await loadRoads();    // all coordinates ready — road lines draw correctly
}
Tab Switch Fix
When the Dashboard tab is hidden, Leaflet cannot measure the container. On re-activation:

if (targetTab === 'dashboard' && networkMap) {
  setTimeout(() => networkMap.invalidateSize(), 50);
}


---

# 📡 API Documentation

Base URL: http://localhost:3000

All endpoints return a consistent JSON envelope:

{ "success": true,  "count": 3, "data": [ ... ] }
{ "success": false, "error": "Descriptive error message" }
Relief Centers
Method	Endpoint	Description
GET	/centers	Get all relief centers
GET	/centers/:id	Get a single center by ID
POST	/centers	Add a new relief center
PUT	/centers/:id	Update an existing center
DELETE	/centers/:id	Delete a center
POST /centers body:

{
  "name": "Dehradun Hub",
  "latitude": 30.3165,
  "longitude": 78.0322,
  "total_food_kits": 750,
  "total_water_units": 1500,
  "total_medical_kits": 250
}
Affected Areas
Method	Endpoint	Description
GET	/areas	Get all areas (includes priority_score if computed)
GET	/areas/:id	Get a single area by ID
POST	/areas	Add a new affected area
PUT	/areas/:id	Update an existing area
DELETE	/areas/:id	Delete an area
POST /areas body:

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
Roads
Method	Endpoint	Description
GET	/roads	Get all road connections
POST	/roads	Add a new road connection
PUT	/roads/:id	Update a road (e.g. block/unblock)
DELETE	/roads/:id	Delete a road
POST /roads body:

{
  "from_location_id": 1,
  "to_location_id": 1001,
  "distance_km": 15.5,
  "travel_time_minutes": 45,
  "is_blocked": false
}
Analytics & Routing
Method	Endpoint	Description
POST	/compute-priorities	Calculate and store priority scores for all areas
POST	/allocate-resources	Compute proportional resource allocation
GET	/routes?centerId=1&areaId=2&useTime=false	Find shortest single route
POST	/routes/multi-stop	Find multi-stop route
POST	/simulate	Run what-if simulation (non-destructive)
GET /routes query params:

Param	Type	Description
centerId	Integer	Relief center ID
areaId	Integer	Affected area ID (raw, not graph ID)
useTime	Boolean	true = optimise by time, false = by distance
POST /routes/multi-stop body:

{
  "centerId": 1,
  "areaIds": [1, 2, 3],
  "useTime": false
}
POST /simulate body:

{
  "roadId": 7,
  "blocked": true
}
Quick Test (curl)
# Health check
curl http://localhost:3000/

# Get all centers
curl http://localhost:3000/centers

# Compute priorities
curl -X POST http://localhost:3000/compute-priorities

# Find route (center 1 to area 2, by distance)
curl "http://localhost:3000/routes?centerId=1&areaId=2&useTime=false"

# Block road #7
curl -X PUT http://localhost:3000/roads/7 \
     -H "Content-Type: application/json" \
     -d '{"is_blocked": true}'


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


