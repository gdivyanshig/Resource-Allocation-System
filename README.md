# Resource-Allocation-System
#include <stdio.h>
#include <limits.h>
#include <stdbool.h>

#define MAX_ZONES 10
#define INF 99999

// Relief Zones & Supply Data
int demand[MAX_ZONES];
int supply[MAX_ZONES];
int priority[MAX_ZONES];
bool blocked[MAX_ZONES][MAX_ZONES];

int graph[MAX_ZONES][MAX_ZONES];

int minDistance(int dist[], bool visited[], int n) {
    int min = INF, min_index;
    for (int v = 0; v < n; v++) {
        if (!visited[v] && dist[v] <= min) {
            min = dist[v], min_index = v;
        }
    }
    return min_index;
}

void dijkstra(int src, int n) {
    int dist[MAX_ZONES];
    bool visited[MAX_ZONES] = {false};

    for (int i = 0; i < n; i++) dist[i] = INF;
    dist[src] = 0;

    for (int count = 0; count < n - 1; count++) {
        int u = minDistance(dist, visited, n);
        visited[u] = true;

        for (int v = 0; v < n; v++) {
            if (!visited[v] && graph[u][v] && !blocked[u][v] && dist[u] != INF && dist[u] + graph[u][v] < dist[v]) {
                dist[v] = dist[u] + graph[u][v];
            }
        }
    }

    printf("Optimal Routes from Source %d:\n", src);
    for (int i = 0; i < n; i++) {
        printf("To Zone %d: %d\n", i, dist[i]);
    }
}

void allocateResources(int n) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (priority[j] > priority[i] && supply[i] > 0 && demand[j] > 0) {
                int allocated = (supply[i] >= demand[j]) ? demand[j] : supply[i];
                supply[i] -= allocated;
                demand[j] -= allocated;
                printf("Allocated %d resources from Depot %d to Zone %d\n", allocated, i, j);
            }
        }
    }
}

void reallocateResources(int n) {
    for (int i = 0; i < n; i++) {
        if (demand[i] > 0) {
            for (int j = 0; j < n; j++) {
                if (supply[j] > 0) {
                    int allocated = (supply[j] >= demand[i]) ? demand[i] : supply[j];
                    supply[j] -= allocated;
                    demand[i] -= allocated;
                    printf("Reallocated %d resources from Depot %d to Zone %d\n", allocated, j, i);
                    if (demand[i] == 0) break;
                }
            }
        }
    }
}

int main() {
    int n;
    printf("Enter number of zones: ");
    scanf("%d", &n);
    printf("Enter supply at each depot: ");
    for (int i = 0; i < n; i++) scanf("%d", &supply[i]);
    printf("Enter demand at each zone: ");
    for (int i = 0; i < n; i++) scanf("%d", &demand[i]);
    printf("Enter priority of each zone (higher value = more priority): ");
    for (int i = 0; i < n; i++) scanf("%d", &priority[i]);
    printf("Enter road network (enter INF for no path):\n");
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            scanf("%d", &graph[i][j]);
            if (graph[i][j] == INF) blocked[i][j] = true;
        }
    }
    allocateResources(n);
    reallocateResources(n);
    int src;
    printf("Enter source depot for route optimization: ");
    scanf("%d", &src);
    dijkstra(src, n);
    return 0;
}
