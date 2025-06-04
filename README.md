# Resource-Allocation-System
### Objective : The primary objective of this project is to develop an intelligent system that can:
•	Quickly allocate resources based on zone priority and urgency.
•	Reallocate resources efficiently if shortages occur.
•	Optimize delivery routes using real-time traffic and weather data.
•	Manage resources across multiple depots.
### Methodology and Algorithms Used
1. Greedy Resource Allocation : This algorithm is used to allocate available resources rapidly to the most urgent zones. By always selecting the zone with the highest priority and matching it with the depot that can fulfill its demand, we minimize allocation time.
2. Dijkstra's Algorithm (Dynamic Programming) : Dijkstra's algorithm helps identify the shortest path between depots and affected zones. In case of roadblocks or adverse conditions, it dynamically avoids the blocked routes, ensuring timely and safe delivery.
3. Backtracking-Based Reallocation : In situations where the initial allocation leaves certain zones underserved, backtracking is used to evaluate alternate resource paths and reallocate from less critical zones or surplus depots.
4. Consideration of Traffic and Weather Conditions : Blocked roads due to weather or other factors are marked in the system. These are dynamically avoided during the route calculation phase, ensuring the system adapts to changing conditions.
5. Multi-Depot Supply Chain Management : Rather than relying on a central depot, the system supports multiple depots. This decentralization improves efficiency and responsiveness.

