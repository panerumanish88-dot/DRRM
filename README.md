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

# 🚨 Disaster Relief Command Center

Full-Stack Web Application: Express.js + In-Memory DB (MongoDB-ready) + Vanilla JavaScript + Leaflet.js

A data-driven disaster relief resource allocation and route optimization system that helps NGOs and authorities prioritize affected locations, allocate limited resources efficiently, and compute optimal delivery routes during emergencies.

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

### 1. Dashboard & Map

- Open application
- View relief centers and affected areas
- Monitor road network

### 2. Compute Priorities

- Calculate urgency scores
- Rank affected regions

### 3. Route Planning

- Select center and area
- Generate shortest path

### 4. Multi-Stop Routing

- Select multiple destinations
- Generate optimized route

### 5. Simulation

- Block or unblock roads
- Observe operational impact

---

# 🗺️ Network Overview Map

### Features

✅ Relief Center Tracking

✅ Priority-Based Area Markers

✅ Open & Blocked Road Visualization

✅ Layer Controls

✅ Auto Refresh

✅ Interactive Popups

---

# 📡 API Documentation

## Centers

```http
GET /centers
POST /centers
PUT /centers/:id
DELETE /centers/:id
```

## Areas

```http
GET /areas
POST /areas
PUT /areas/:id
DELETE /areas/:id
```

## Roads

```http
GET /roads
POST /roads
PUT /roads/:id
DELETE /roads/:id
```

## Analytics

```http
POST /compute-priorities
POST /allocate-resources
POST /simulate
```

## Routing

```http
GET /routes
POST /routes/multi-stop
```

---

# 🧮 Algorithms

## Priority Scoring

```text
P = 0.5 × (Severity / 5)
  + 0.3 × (Population / Max Population)
  + 0.2 × Access Difficulty
```

## Dijkstra Algorithm

Used for:

- Shortest Path
- Route Optimization
- Blocked Road Avoidance

Complexity:

```text
O(V²)
```

## Multi-Stop Routing

Nearest-Neighbour TSP Heuristic

## Resource Allocation

```text
Allocation = Required × Ratio
```

---

# 🐛 Troubleshooting

| Problem | Solution |
|----------|----------|
| Backend not responding | Start server with npm run dev |
| CORS Error | Verify backend port |
| Map not loading | Check internet connection |
| No route found | Unblock roads or add connections |

---

# 🚀 Future Enhancements

- MongoDB Atlas Integration
- JWT Authentication
- Socket.io Real-Time Updates
- Mobile Responsive Dashboard
- AI-Based Severity Prediction
- Multi-Vehicle Route Optimization
- WhatsApp Notifications
- IoT Sensor Integration
- A* Pathfinding Upgrade

---

# 👨‍💻 Author

### Manish Paneru

📧 panerumanish88@gmail.com

🔗 https://github.com/panerumanish88-dot

💻 Full Stack Developer | DSA Enthusiast | Open Source Learner

---

# 📄 License

This project is licensed under the MIT License.

---

# ⭐ Support

If you found this project useful, consider giving it a star.

Made with ❤️ by **Manish Paneru**

Made with ❤️ by **Manish Paneru**
