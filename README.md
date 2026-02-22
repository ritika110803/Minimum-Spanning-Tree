Prim’s Algorithm in C (Minimum Spanning Tree)

This project implements *Prim’s Algorithm* in C to find the *Minimum Spanning Tree (MST)* of a weighted, undirected graph using an *Adjacency Matrix* representation.

---

 Project Description

This program:

* Uses an adjacency matrix to represent a weighted graph
* Implements *Prim’s Algorithm*
* Finds the Minimum Spanning Tree (MST)
* Prints the edges included in the MST along with their weights

The graph contains *5 vertices*, defined using a constant:

c
#define V 5


---

What is a Minimum Spanning Tree (MST)?

A *Minimum Spanning Tree* is:

* A subset of edges
* That connects all vertices
* Without cycles
* With the *minimum possible total edge weight*

Prim’s Algorithm is a *greedy algorithm* that builds the MST step-by-step.

---

Graph Used in This Program

The program uses the following weighted graph:


       2
   (0)------(1)
    | \        \
    |  \        5
    6   3        \
    |    \        (4)
   (3)------(2)
       7


Adjacency Matrix Representation:

text
0 2 0 6 0
2 0 3 8 5
0 3 0 0 7
6 8 0 0 9
0 5 7 9 0


---

Source Code

c

#include <stdio.h>

#include <limits.h>

#define V 5 // Number of vertices in the graph

// Function to find the vertex with the minimum key value, from the set of vertices not yet included in MST

int minKey(int key[], int mstSet[]) {
    
    int min = INT_MAX, min_index;

    for (int v = 0; v < V; v++)
        
        if (mstSet[v] == 0 && key[v] < min)
            min = key[v], min_index = v;

    return min_index;
}

// Function to print the constructed MST stored in parent[]

void printMST(int parent[], int graph[V][V]) {
    
    printf("Edge \tWeight\n");
    for (int i = 1; i < V; i++)
        printf("%d - %d \t%d\n", parent[i], i, graph[i][parent[i]]);
}

// Function to construct and print MST for a graph represented with adjacency matrix

void primMST(int graph[V][V]) {
    
    int parent[V]; // Array to store constructed MST
    int key[V];    // Key values used to pick minimum weight edge in cut
    int mstSet[V]; // To represent set of vertices included in MST

    // Initialize all keys as INFINITE and mstSet[] as false
    
    for (int i = 0; i < V; i++) {
        key[i] = INT_MAX;
        mstSet[i] = 0;
    }

    // Always include first vertex in MST. Make key 0 so that this vertex is picked as first vertex.
    
    key[0] = 0;
    
    parent[0] = -1; // First node is always root of MST

    // The MST will have V vertices
    
    for (int count = 0; count < V - 1; count++) {
        
        // Pick the minimum key vertex from the set of vertices not yet included in MST
        
        int u = minKey(key, mstSet);

        // Add the picked vertex to the MST Set
        
        mstSet[u] = 1;

        // Update key value and parent index of the adjacent vertices of the picked vertex.
        
        for (int v = 0; v < V; v++)
            
            // graph[u][v] is non zero only for adjacent vertices of u
           
            // mstSet[v] is false for vertices not yet included in MST
            
            // Update the key only if graph[u][v] is smaller than key[v]
            
            if (graph[u][v] && mstSet[v] == 0 && graph[u][v] < key[v]) {
                
                parent[v] = u;
                key[v] = graph[u][v];
            }
    }

    // Print the constructed MST
    
    printMST(parent, graph);
}

// Driver code

int main() {
    
    /* Let us create the following graph
       (0)------(1)
      / |        |
     /  |        |
    (3)------(2)
    */
    
    int graph[V][V] = {
        {0, 2, 0, 6, 0},
        {2, 0, 3, 8, 5},
        {0, 3, 0, 0, 7},
        {6, 8, 0, 0, 9},
        {0, 5, 7, 9, 0}
    };

    // Print the MST
    
    primMST(graph);

    return 0;
}    
---

How to Compile and Run

Using GCC

1. Save the file as:


prim.c


2. Compile:

bash
gcc prim.c -o prim


3. Run:

bash
./prim


(On Windows: prim.exe)

---

Sample Output


Edge    Weight
0 - 1   2
1 - 2   3
0 - 3   6
1 - 4   5


This represents the edges included in the Minimum Spanning Tree.

---

Time and Space Complexity

| Type             | Complexity |
| ---------------- | ---------- |
| Time Complexity  | O(V²)      |
| Space Complexity | O(V²)      |

Where:

* *V* = Number of vertices

---

Concepts Covered

* Graph Data Structure
* Weighted Undirected Graph
* Greedy Algorithm
* Minimum Spanning Tree (MST)
* Adjacency Matrix
* Key and Parent Arrays

---

How Prim’s Algorithm Works

1. Start from an arbitrary vertex (here vertex 0)
2. Pick the minimum weight edge connecting the tree to a new vertex
3. Add that vertex to the MST
4. Repeat until all vertices are included

---

Possible Improvements

* Implement using adjacency list + min heap → O(E log V)
* Allow user input for graph
* Print total cost of MST
* Convert to dynamic vertex size instead of fixed #define V
* Add visualization support

---

Learning Outcome

After completing this project, you will understand:

* Difference between MST and shortest path
* How greedy algorithms work
* Graph representation using adjacency matrix
* Practical use cases (network design, cable wiring, road planning)

---
