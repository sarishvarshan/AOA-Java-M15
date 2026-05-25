
# EX 5E Minimum Spanning Tree -Boruvka's Algorithm
## DATE: 18.05.26
## AIM:
To write a Java program to for given constraints.
Boruvka's Algorithm - Minimum Spanning Tree

Find the MST using Boruvka's Algorithm for a weighted undirected graph.
<img width="292" height="235" alt="image" src="https://github.com/user-attachments/assets/06246b27-37a9-40a8-bd7a-37a1d5187cd1" />

# Algorithm

### 1. Input:

- Read number of vertices `V` and edges `E`.

- For each edge, read its source `src`, destination `dest`, and weight `w`.

- Store all edges in a list.

### 2. Initialization:

- Set up a `parent[]` array for Disjoint Set Union (DSU).

- Initially, each vertex is its own parent.

- Initialize `numTrees = V` (number of connected components) and `MSTweight = 0`.

### 3. Finding Cheapest Edges:

- For every iteration (while more than one tree exists):

  - Initialize an array `cheapest[]` to store the minimum-cost edge for each component.

  - For each edge, find the sets of its two vertices.

  - Update `cheapest` for both sets if the current edge has a smaller weight.

### 4. Building the MST:

- For each vertex, pick its `cheapest` edge (if any).

- If the two endpoints belong to different sets, include the edge in the MST, print it, and merge the sets using `union()`.

- Decrease `numTrees` after each successful merge.

### 5. Output:

- Continue until only one tree (MST) remains.

- Print each chosen edge and finally display the **Total Weight of MST**.

## Program:
```
/*
Program to implement Reverse a String
Developed by: SARISH VARSHAN V
Register Number:  212223230196
*/

import java.util.*;

public class BoruvkaMST {
    static int[] parent;

    static int find(int i) {
        if (parent[i] != i)
            parent[i] = find(parent[i]);
        return parent[i];
    }

    static void union(int x, int y) {
        parent[find(x)] = find(y);
    }

    
    static int boruvkaMST(int V, List<Edge> edges) {
        //Type your code here
        parent = new int[V];
        for (int i = 0; i < V; i++) parent[i] = i;

        int numTrees = V;
        int MSTweight = 0;

        while (numTrees > 1) {
            Edge[] cheapest = new Edge[V];

            // Find the cheapest edge for each component
            for (Edge e : edges) {
                int set1 = find(e.src);
                int set2 = find(e.dest);
                if (set1 == set2) continue;
                if (cheapest[set1] == null || e.weight < cheapest[set1].weight)
                    cheapest[set1] = e;
                if (cheapest[set2] == null || e.weight < cheapest[set2].weight)
                    cheapest[set2] = e;
            }

            // Add the cheapest edges to MST
            for (int i = 0; i < V; i++) {
                Edge e = cheapest[i];
                if (e != null) {
                    int set1 = find(e.src);
                    int set2 = find(e.dest);
                    if (set1 != set2) {
                        System.out.println("Edge: " + e.src + "-" + e.dest + " Weight: " + e.weight);
                        MSTweight += e.weight;
                        union(set1, set2);
                        numTrees--;
                    }
                }
            }
        }

        return MSTweight;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int V = sc.nextInt();
        int E = sc.nextInt();

        List<Edge> edges = new ArrayList<>();
        for (int i = 0; i < E; i++) {
            edges.add(new Edge(sc.nextInt(), sc.nextInt(), sc.nextInt()));
        }

        int totalWeight = boruvkaMST(V, edges);
        System.out.println("Total Weight of MST: " + totalWeight);

        sc.close();
    }
}

class Edge {
    int src, dest, weight;
    Edge(int s, int d, int w) {
        src = s; dest = d; weight = w;
    }
}
```

## Output:
<img width="912" height="497" alt="image" src="https://github.com/user-attachments/assets/261a889c-fe6b-4195-85e2-c33690b4cf86" />



## Result:
The program successfully implemented and the expected output is verified.
