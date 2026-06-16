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

## 📖 Overview

Disaster Relief Command Center is a full-stack web application built to improve disaster response operations through intelligent resource allocation, priority-based decision making, and route optimization.

The system enables authorities and NGOs to:

- Identify high-priority affected areas
- Allocate limited resources efficiently
- Monitor road connectivity
- Optimize delivery routes
- Simulate disaster scenarios
- Visualize operations on an interactive map

---

## 🌟 Key Features

### 🗺️ Interactive Disaster Network Map
- Real-time visualization using Leaflet.js
- Relief centers and affected area tracking
- Road network monitoring
- Blocked road detection
- Layer visibility controls

### 🎯 Priority Scoring Engine
Automatically ranks affected areas using:

- Disaster Severity
- Population Impact
- Accessibility Difficulty

### 📦 Resource Allocation System
- Food kit management
- Water inventory management
- Medical supply tracking
- Proportional resource distribution

### 🛣️ Route Optimization
- Dijkstra's Shortest Path Algorithm
- Distance optimization
- Travel-time optimization
- Blocked road avoidance

### 🔀 Multi-Stop Route Planning
- Nearest Neighbour TSP Heuristic
- Efficient multi-location delivery planning

### 📊 Dashboard Analytics
- Real-time statistics
- Priority rankings
- Resource summaries
- Network monitoring

### 🔄 What-If Simulation
- Block roads temporarily
- Test operational impact
- Non-destructive scenario analysis

---

## 📸 Screenshots

### Dashboard

> Add dashboard screenshot here

![Dashboard](images/dashboard.png)

---

### Network Overview Map

> Add map screenshot here

![Map](images/network-map.png)

---

### Route Planning

> Add route planning screenshot here

![Routing](images/routing.png)

---

## 🛠️ Tech Stack

### Frontend

| Technology | Purpose |
|------------|----------|
| HTML5 | Structure |
| CSS3 | Styling |
| JavaScript ES6+ | Application Logic |
| Leaflet.js | Interactive Mapping |

### Backend

| Technology | Purpose |
|------------|----------|
| Node.js | Runtime Environment |
| Express.js | REST API Framework |

### Database

| Technology | Purpose |
|------------|----------|
| In-Memory Database | Current Storage |
| MongoDB | Future Upgrade |

### Development Tools

- Git
- GitHub
- Nodemon
- Postman

---

## 🏗️ System Architecture

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

## 📂 Project Structure

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

## 🚀 Installation

### Clone Repository

```bash
git clone https://github.com/panerumanish88-dot/DRRM.git
```

### Move Into Project

```bash
cd DRRM/backend
```

### Install Dependencies

```bash
npm install
```

### Start Server

```bash
npm run dev
```

Server runs at:

```text
http://localhost:3000
```

---

## 🚀 Usage

### Step 1
Start Backend Server

### Step 2
Open Frontend

### Step 3
Calculate Priority Scores

### Step 4
Allocate Resources

### Step 5
Generate Delivery Routes

### Step 6
Run Simulations

---

## 🧮 Algorithms Used

### Priority Scoring Formula

```text
P = 0.5 × (Severity / 5)
  + 0.3 × (Population / Max Population)
  + 0.2 × Access Difficulty
```

### Dijkstra's Algorithm

Used for:

- Shortest path calculation
- Route optimization
- Blocked road avoidance

Complexity:

```text
O(V²)
```

### Multi-Stop Routing

Nearest Neighbour TSP Heuristic

Benefits:

- Fast computation
- Good route approximation
- Suitable for emergency logistics

### Resource Allocation

```text
Allocation = Required × Ratio
```

Ensures fair distribution when resources are limited.

---

## 🔌 REST API Highlights

### Centers

```http
GET /centers
POST /centers
PUT /centers/:id
DELETE /centers/:id
```

### Areas

```http
GET /areas
POST /areas
PUT /areas/:id
DELETE /areas/:id
```

### Roads

```http
GET /roads
POST /roads
PUT /roads/:id
DELETE /roads/:id
```

### Analytics

```http
POST /compute-priorities
POST /allocate-resources
POST /simulate
```

### Routing

```http
GET /routes
POST /routes/multi-stop
```

---

## 🚀 Future Enhancements

- MongoDB Atlas Integration
- JWT Authentication
- Socket.io Real-Time Updates
- Mobile Responsive Dashboard
- Satellite Data Integration
- AI-Based Severity Prediction
- Multi-Vehicle Route Optimization
- WhatsApp Notifications
- IoT Sensor Integration
- A* Pathfinding Upgrade

---

## 👨‍💻 Author

### Manish Paneru

📧 Email: panerumanish88@gmail.com

🔗 GitHub: https://github.com/panerumanish88-dot

💻 Full Stack Developer | DSA Enthusiast | Open Source Learner

---

## 📄 License

This project is licensed under the MIT License.

---

## ⭐ Support

If you found this project useful, consider giving it a star.

Made with ❤️ by **Manish Paneru**
