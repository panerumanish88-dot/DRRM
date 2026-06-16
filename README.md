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

1. Priority Scoring
Formula:

P = 0.5 × (severity / 5)  +  0.3 × (people / max_people)  +  0.2 × access_difficulty
Component	Weight	Rationale
Severity	50%	Directly reflects immediate danger to life
Population (normalised)	30%	More people = greater total need
Access Difficulty	20%	Hard-to-reach areas may need priority scheduling
Example — Flood Zone A:

severity     = 5   → S_norm = 5/5   = 1.0
people       = 250 → N_norm = 250/400 = 0.625   (max is Landslide Area C with 400)
access       = 1   (difficult)

P = 0.5(1.0) + 0.3(0.625) + 0.2(1)
  = 0.5 + 0.1875 + 0.2
  = 0.8875  → HIGH PRIORITY (red marker, pulse animation)
Time complexity: O(n log n) — one pass to find max, then sort

2. Dijkstra's Shortest Path
Purpose: Find optimal route from a relief center to an affected area.

Steps:

Initialise all node distances to ∞; source node distance = 0
Add all nodes to an unvisited set
Pick the unvisited node with the smallest known distance
For each neighbour, compute tentative distance (current + edge weight)
If tentative < stored, update it and record the predecessor
Mark current node as visited; stop if it is the destination
Reconstruct path by backtracking through the predecessor map
Key details:

Nodes = all relief centers + all affected areas
Edges = road connections (blocked roads are excluded entirely from the graph)
Edge weight = distance_km or travel_time_minutes depending on useTime flag
Time complexity: O(V²) with Set — sufficient for small networks; upgradeable to O((V+E) log V) with a binary heap
3. Multi-Stop Routing (TSP Nearest-Neighbour)
Finding the exact shortest route visiting N areas is NP-hard (Travelling Salesman Problem). The nearest-neighbour heuristic gives a good approximation in polynomial time:

Start at the relief center
Run Dijkstra to every unvisited area; pick the nearest
Move there, mark visited
Repeat until all areas are visited
Return to the starting center
Quality: Typically within 20–25% of optimal. For 3–10 areas (typical disaster scenario) this is excellent performance with near-instant computation.

Time complexity: O(N²) where N = number of selected areas

4. Resource Allocation
Proportional distribution when supply cannot fully meet demand:

ratio = min(totalAvailable / totalRequired, 1.0)  // per resource type
allocation = Math.floor(area.required × ratio)
If supply ≥ demand, ratio = 1.0 and all needs are fully met. If supply < demand, every area gets the same proportional share.

🐛 Troubleshooting
Symptom	Cause	Fix
Map shows 0 for all counts	Frontend loaded before backend started	Start backend first; click Refresh Map
Map is blank / no tiles	No internet connection	OpenStreetMap tiles require internet access
CORS error in browser console	Backend not running or wrong port	Verify server is on port 3000; check API_URL in app.js
Route says "No route found"	All paths between nodes are blocked	Unblock a road or add an alternative connection
Priority scores are all 0	Priorities not computed yet	Click "Calculate All Priorities" on Priority Scoring tab
Map looks wrong after tab switch	Leaflet cannot measure hidden container	Already fixed — invalidateSize() fires on tab activation
"Module not found" on start	Dependencies not installed	Run cd backend && npm install
Port 3000 already in use	Another process using the port	Change PORT=3001 in .env and update API_URL in app.js
🚀 Future Enhancements
 Real MongoDB / MongoDB Atlas integration (interface is already compatible)
 Real-time updates with Socket.io — push road-status changes to all dashboards instantly
 Route visualisation drawn on the map as a highlighted polyline
 Mobile responsive layout improvements
 JWT authentication with role-based access (field worker / coordinator / admin)
 Real-time satellite imagery integration (ISRO NDEM API)
 Machine learning for disaster severity prediction
 Multi-vehicle route optimisation
 SMS / WhatsApp integration for field updates
 Blockchain-based supply chain tracking
 IoT sensor integration
 Multi-language support
 A* pathfinding upgrade using GPS coordinates as heuristic
 2-opt improvement for multi-stop route quality
📄 License
This project is licensed under the MIT License.

👥 Authors
ManishPaneru — Initial work and development 📧 panerumanish88@gmail.com

🙏 Acknowledgments
India Disaster Resource Network (IDRN) for data references
National Disaster Management Authority (NDMA) for operational guidelines
OpenStreetMap contributors for map tile data
Leaflet.js team for the excellent open-source mapping library
MongoDB and Express.js communities for documentation
Made with ❤️ for disaster relief operations



Made with ❤️ by **Manish Paneru**
