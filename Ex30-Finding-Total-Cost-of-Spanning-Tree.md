# Ex30 Finding Total Cost of Spanning Tree
## DATE: 15/05/25
## AIM:
To write a C Program to implement Prim's Algorithm for finding Total Cost of spanning tree.
## Algorithm

1. Initialize Variables: Define `infinity = 9999`, `MAX = 20`, and declare the adjacency matrix `G[MAX][MAX]`, MST matrix `spanning[MAX][MAX]`, and integer `n`.

2. Input Graph Data: Read the number of vertices `n` and edge weights into `G[i][j]`.

3. Run `prims()` Function:
   - Initialize `cost[][]`, `spanning[][]`, `distance[]`, `from[]`, and `visited[]`.
   - While there are edges left to add to the MST, find the vertex with the smallest `distance[]`, update the MST, and adjust `distance[]` for unvisited vertices.

4. Print MST: After the `prims()` function completes, print the `spanning[][]` matrix representing the minimum spanning tree.

5. Display Total Cost: Output the `min_cost` of the spanning tree, which is the total minimum cost.


## Program:
```
/*
Program to find and display the priority of the operator in the given Postfix expression
Developed by: PRADEEP E
RegisterNumber:  212223230149
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

    printf("\nTotal cost of spanning tree = %d\n", total_cost);
    return 0;
}

int prims()
{
    int cost[MAX][MAX];
    int distance[MAX], from[MAX], visited[MAX];
    int min_cost = 0, no_of_edges = n - 1;
    int i, j, u, v, min_distance;

    // Create cost matrix and initialize spanning tree matrix
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {
            if (G[i][j] == 0)
                cost[i][j] = infinity;
            else
                cost[i][j] = G[i][j];
            spanning[i][j] = 0;
        }
    }

    // Initialize distance, visited, and from arrays
    distance[0] = 0;
    visited[0] = 1;
    for (i = 1; i < n; i++)
    {
        distance[i] = cost[0][i];
        from[i] = 0;
        visited[i] = 0;
    }

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
        visited[v] = 1;
        no_of_edges--;
        min_cost += cost[u][v];

        for (i = 1; i < n; i++)
        {
            if (visited[i] == 0 && cost[i][v] < distance[i])
            {
                distance[i] = cost[i][v];
                from[i] = v;
            }
        }
    }

    return min_cost;
}
```

## Output:

![image](https://github.com/user-attachments/assets/551b82e4-0ef7-413c-91cc-c3d55c6e454d)



## Result:
Thus the C program to implement Prim's Algorithm for finding Total Cost of spanning tree is implemented successfully.
