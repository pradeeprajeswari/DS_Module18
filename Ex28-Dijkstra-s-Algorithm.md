# Ex28 Dijkstra’s Algorithm
## DATE: 08/05/25
## AIM:
To write a C Program to implement Dijkstra's Algorithm to find the shortest path

## Algorithm

1. Initialize Constants and Variables  
   - Define `INFINITY = 9999`, `MAX = 10`.  
   - Declare graph matrix `G[MAX][MAX]`, and arrays for `distance`, `visited`, and `pred`.

2. Input Graph and Starting Node  
   - Read number of nodes `n`, then input adjacency matrix `G[i][j]`.  
   - Replace `0` with `INFINITY` to indicate no direct edge.  
   - Read the starting node `u`.

3. Set Up for Dijkstra's Algorithm 
   - Initialize `distance[i]` with `G[u][i]`, set `pred[i] = u`, and mark all nodes unvisited.  
   - Mark the start node as visited and set its distance to 0.

4. Compute Shortest Paths 
   - Repeat for `n-1` nodes:  
     - Select the nearest unvisited node.  
     - Mark it visited and update distances of its unvisited neighbors if a shorter path is found.

5. Display Results
   - For each node (except the start), print the shortest distance from the start and trace the path using `pred[]`.


## Program:
```
/*
Program to implement Dijkstra's Algorithm 
Developed by: PRADEEP E
RegisterNumber:  212223230149
*/
```
```
#include <stdio.h>
#define INFINITY 9999
#define MAX 10

void dijkstra(int G[MAX][MAX], int n, int startnode);

int main()
{
    int G[MAX][MAX], i, j, n, u;
    scanf("%d", &n);
    for (i = 0; i < n; i++)
        for (j = 0; j < n; j++)
            scanf("%d", &G[i][j]);
    scanf("%d", &u);
    dijkstra(G, n, u);
    return 0;
}

void dijkstra(int G[MAX][MAX], int n, int startnode)
{
    int cost[MAX][MAX], distance[MAX], pred[MAX];
    int visited[MAX], count, mindistance, nextnode, i, j;

    // Create the cost matrix
    for (i = 0; i < n; i++)
        for (j = 0; j < n; j++)
            cost[i][j] = (G[i][j] == 0) ? INFINITY : G[i][j];

    // Initialize pred[], distance[], and visited[]
    for (i = 0; i < n; i++)
    {
        distance[i] = cost[startnode][i];
        pred[i] = startnode;
        visited[i] = 0;
    }

    distance[startnode] = 0;
    visited[startnode] = 1;
    count = 1;

    while (count < n - 1)
    {
        mindistance = INFINITY;
        for (i = 0; i < n; i++)
        {
            if (!visited[i] && distance[i] < mindistance)
            {
                mindistance = distance[i];
                nextnode = i;
            }
        }

        visited[nextnode] = 1;

        for (i = 0; i < n; i++)
        {
            if (!visited[i])
            {
                if (mindistance + cost[nextnode][i] < distance[i])
                {
                    distance[i] = mindistance + cost[nextnode][i];
                    pred[i] = nextnode;
                }
            }
        }
        count++;
    }

    // Print the path and distance of each node
    for (i = 0; i < n; i++)
    {
        if (i != startnode)
        {
            printf("Distance of node %d = %d\n", i, distance[i]);
            printf("Path = %d", i);
            j = i;
            while (j != startnode)
            {
                j = pred[j];
                printf(" <- %d", j);
            }
            printf("\n");
        }
    }
}
```

## Output:

![image](https://github.com/user-attachments/assets/121d86c2-a203-4174-aa9d-5389b62714ef)

## Result:
Thus, the Program to implement Dijkstra's Algorithm to find the shortest path is implemented successfully.
