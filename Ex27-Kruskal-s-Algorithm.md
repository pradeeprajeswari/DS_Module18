# Ex27 Kruskal’s Algorithm
## DATE: 05/05/25
## AIM:
To write a C program to implement Kruskal's Algorithm for finding minimum cost

## Algorithm

1. Initialize Variables and Data Structures
   - Set `ne = 1`, `mincost = 0`.  
   - Declare `cost[9][9]` for the adjacency matrix and `parent[9]` for disjoint sets.  
   - Define helper functions: `find(int)` to find root and `uni(int, int)` to union sets.

2. Read Input  
   - Input number of vertices `n`.  
   - Fill `cost[i][j]` matrix using `scanf`.  
   - Replace `0` values with `999` (representing infinity/no edge).

3. Build Minimum Spanning Tree  
   - While `ne < n`:  
     - Find the edge with minimum weight not yet used.  
     - Use `find()` to check if it connects different trees.  
     - If so, use `uni()` to merge sets and include edge in MST.

4. Update Costs and MST Info  
   - Print selected edge and update `mincost`.  
   - Set `cost[a][b]` and `cost[b][a]` to `999` to avoid reselecting.

5. Output Final Result  
   - Print the total cost of the MST using `printf("Minimum cost = %d\n", mincost);`.


## Program:
```
/*
Program to implement Kruskal's Algorithm
Developed by: PRADEEP E
RegisterNumber:  212223230149
*/
```
```
#include <stdio.h>
#include <stdlib.h>

int i, j, k, a, b, u, v, n, ne = 1;
int min, mincost = 0, cost[9][9], parent[9];

int find(int);
int uni(int, int);

int main()
{
    scanf("%d", &n);

    for (i = 1; i <= n; i++)
    {
        for (j = 1; j <= n; j++)
        {
            scanf("%d", &cost[i][j]);
            if (cost[i][j] == 0)
                cost[i][j] = 999;
        }
    }

    while (ne < n)
    {
        min = 999;
        for (i = 1; i <= n; i++)
        {
            for (j = 1; j <= n; j++)
            {
                if (cost[i][j] < min)
                {
                    min = cost[i][j];
                    a = u = i;
                    b = v = j;
                }
            }
        }

        u = find(u);
        v = find(v);

        if (uni(u, v))
        {
            printf("%d edge (%d,%d) = %d\n", ne++, a, b, min);
            mincost += min;
        }

        cost[a][b] = cost[b][a] = 999;
    }

    printf("Minimum cost = %d\n", mincost);
    return 0;
}

int find(int i)
{
    while (parent[i])
        i = parent[i];
    return i;
}

int uni(int i, int j)
{
    if (i != j)
    {
        parent[j] = i;
        return 1;
    }
    return 0;
}
```

## Output:

![image](https://github.com/user-attachments/assets/12b2ed8b-bc94-495d-b5d3-22eabb5c0e1f)



## Result:
Thus, the C program to implement Kruskal's Algorithm for finding minimum cost is implemented successfully.
