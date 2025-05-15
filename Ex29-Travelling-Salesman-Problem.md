# Ex29 Travelling Salesman Problem
## DATE: 12/05/25
## AIM:
To write a C Program to implement Travelling Salesman Problem for finding shortest path.
## Algorithm

1. Initialize Global Variables  
   - `a[10][10]`: Cost matrix (travel cost between cities).  
   - `visited[10]`: Flags for visited cities (all initially 0).  
   - `n`: Number of cities, and `cost = 0`: Total minimum cost.

2. Input Data – `get()` Function  
   - Reads number of cities `n` and fills the `a[i][j]` cost matrix.  
   - Initializes all cities as **not visited**.

3. Find Minimum Cost Path – `mincost(city)`  
   - Marks the current city as visited and prints it.  
   - Finds the next city with the **least cost** using `least(city)`.  
   - If all cities are visited, returns to the starting city.  
   - Updates total `cost` and **recursively continues** from the next city.

4. Select Least Cost City – `least(city)`  
   - Checks all unvisited neighbors of the current city.  
   - Picks the city with the **minimum travel cost** and returns it.  
   - Adds the intermediate cost for each decision.

5. Display Result – `put()`  
   - Prints the **total minimum cost** after all cities are visited and returned.

6. Main Function Execution  
   - Calls `get()` → `mincost(0)` → `put()` in sequence.  
   - Begins from city `0` and completes the tour.


## Program:
```
/*
Program to implement Travelling Salesman Problem for finding shortest path
Developed by: PRADEEP E
RegisterNumber:  212223230149
*/
```
```
#include <stdio.h>

int a[10][10], visited[10], n, cost = 0;

void get()
{
    int i, j;
    scanf("%d", &n);
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
            scanf("%d", &a[i][j]);
        visited[i] = 0;
    }
}

int least(int c)
{
    int i, nc = 999;
    int min = 999, kmin;

    for (i = 0; i < n; i++)
    {
        if ((a[c][i] != 0) && (visited[i] == 0))
        {
            if (a[c][i] + a[i][0] < min)
            {
                min = a[c][i] + a[i][0];
                kmin = a[c][i];
                nc = i;
            }
        }
    }

    if (min != 999)
        cost += kmin;
    return nc;
}

void mincost(int city)
{
    int ncity;
    visited[city] = 1;
    printf("%d --> ", city + 1);
    ncity = least(city);

    if (ncity == 999)
    {
        ncity = 0;
        printf("%d", ncity + 1);
        cost += a[city][ncity];
        return;
    }

    mincost(ncity);
}

void put()
{
    printf("\n\nMinimum cost: %d\n", cost);
}

int main()
{
    get();
    mincost(0);
    put();
    return 0;
}
```

## Output:

![image](https://github.com/user-attachments/assets/cba89abe-c91d-4dd9-9101-0b6508c93555)



## Result:
Thus, the C program to implement Travelling Salesman Problem for finding shortest path is implemented successfully.
