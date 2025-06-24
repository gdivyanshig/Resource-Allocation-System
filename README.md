# 🚨 Disaster Relief Resource Allocation & Route Optimization 

This project is a C-based simulation of **resource allocation and path optimization** in a disaster-affected region. It handles:
- Dynamic allocation based on **supply-demand priorities**
- Reallocation if priority-based allocation fails
- **Shortest path routing** using Dijkstra’s Algorithm
- Handling of **blocked roads** via adjacency matrix and custom logic

---

## 🧠 Features

- 📦 Allocates resources from supply depots to demand zones
- 🎯 Honors zone **priority levels** during allocation
- 🔁 Reallocates leftover supplies after first pass
- 🗺️ Optimizes routes using **Dijkstra’s algorithm**
- ❌ Supports road blockage using `INF` to block paths

---

## 🛠 Requirements

- A C compiler (e.g., `gcc`, `clang`)
- Terminal or IDE that supports standard C

---

### Objective : The primary objective of this project is to develop an intelligent system that can:
-	Quickly allocate resources based on zone priority and urgency. 
-	Reallocate resources efficiently if shortages occur.
-	Optimize delivery routes using real-time traffic and weather data.
-	Manage resources across multiple depots.

---

### Methodology and Algorithms Used
1. Greedy Resource Allocation : This algorithm is used to allocate available resources rapidly to the most urgent zones. By always selecting the zone with the highest priority and matching it with the depot that can fulfill its demand, we minimize allocation time.
2. Dijkstra's Algorithm (Dynamic Programming) : Dijkstra's algorithm helps identify the shortest path between depots and affected zones. In case of roadblocks or adverse conditions, it dynamically avoids the blocked routes, ensuring timely and safe delivery.
3. Fallback-Based Reallocation : After the initial priority-based allocation, if some zones still require resources, a secondary reallocation loop checks all remaining depots for leftover supplies.
4. Road Blockage and Dynamic Path Adjustment : The system treats blocked or impassable roads (due to traffic, weather, etc.) as INF in the input graph. These are dynamically avoided in both allocation and routing, making the model adaptable to real-time road conditions.
5. Multi-Depot Supply Chain Management : Rather than relying on a central depot, the system supports multiple depots. This decentralization improves efficiency and responsiveness.
