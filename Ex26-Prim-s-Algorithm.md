# Ex26 Prim’s Algorithm

## DATE: 28/04/25
## AIM:
To write a C program to implement Prim's Algorithm for finding Total Cost of tree.

## Algorithm


1. Initialize Constants and Variables
   - Define `infinity = 9999` and `MAX = 20`.  
   - Declare global matrices `G[MAX][MAX]`, `spanning[MAX][MAX]`, and integer `n`.

2. Read Graph Input in `main()`  
   - Read number of vertices `n`.  
   - Input the adjacency matrix `G[i][j]` using `scanf`.

3. Define `prims()` Function
   - Convert `G` to `cost[][]` matrix (replace 0s with infinity).  
   - Initialize arrays: `visited[]`, `distance[]`, and `from[]`.

4. Construct Minimum Spanning Tree
   - Repeat for `n-1` edges:  
     - Find the minimum unvisited vertex.  
     - Add the edge to `spanning[][]`.  
     - Update distances and mark vertex as visited.

5. Output the Result
   - Print the `spanning[][]` matrix and the total cost returned by `prims()`.

## Program:
```
/*
Program to implement Prim's Algorithm
Developed by: 
RegisterNumber:  
*/
```
```
#include <stdio.h>
#include <stdlib.h>

#define infinity 9999
#define MAX 20

int G[MAX][MAX], spanning[MAX][MAX], n;

int prims();

int main()
{
    int i, j, total_cost;

    scanf("%d", &n);
    for (i = 0; i < n; i++)
        for (j = 0; j < n; j++)
            scanf("%d", &G[i][j]);

    total_cost = prims();

    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
            printf("%d ", spanning[i][j]);
        printf("\n");
    }

    printf("\nTotal cost of spanning tree = %d", total_cost);
    return 0;
}

int prims()
{
    int cost[MAX][MAX];
    int u, v, min_distance, distance[MAX], from[MAX];
    int visited[MAX], no_of_edges, i, j, min_cost;

    // Create cost matrix and initialize spanning tree
    for (i = 0; i < n; i++)
        for (j = 0; j < n; j++)
        {
            if (G[i][j] == 0)
                cost[i][j] = infinity;
            else
                cost[i][j] = G[i][j];
            spanning[i][j] = 0;
        }

    distance[0] = 0;
    visited[0] = 1;

    for (i = 1; i < n; i++)
    {
        distance[i] = cost[0][i];
        from[i] = 0;
        visited[i] = 0;
    }

    min_cost = 0;
    no_of_edges = n - 1;

    while (no_of_edges > 0)
    {
        min_distance = infinity;
        for (i = 1; i < n; i++)
        {
            if (visited[i] == 0 && distance[i] < min_distance)
            {
                v = i;
                min_distance = distance[i];
            }
        }

        u = from[v];

        spanning[u][v] = distance[v];
        spanning[v][u] = distance[v];
        no_of_edges--;
        visited[v] = 1;

        for (i = 1; i < n; i++)
        {
            if (visited[i] == 0 && cost[i][v] < distance[i])
            {
                distance[i] = cost[i][v];
                from[i] = v;
            }
        }

        min_cost += cost[u][v];
    }

    return min_cost;
}
```

## Output:

![image](https://github.com/user-attachments/assets/29cb3c21-0913-4917-9156-bb943c7ccb31)



## Result:
Thus, the C program to implement Prim's Algorithm for finding Total Cost of tree is implemented successfully.
