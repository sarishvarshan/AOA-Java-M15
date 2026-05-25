
# EX 5D Flower Planting.
## DATE: 18.05.26
## AIM:
To write a Java program to for given constraints.
You are given n gardens, labelled from 1 to n.

You also have a list called paths, where each element paths[i] = [xi, yi] represents a bidirectional road connectingthe  garden xi and garden yi.

You want to plant one flower in each garden, and there are exactly 4 types of flowers labelled as 1, 2, 3, and 4.

Your goal is to plant flowers such that:

No two connected gardens (i.e., connected via a path) have the same flower type.

Return any valid flower assignment as an array where:

answer[i] is the flower type planted in the (i+1) ᵗʰ garden

It is guaranteed that:

No garden is connected to more than 3 other gardens

A valid flower assignment always exists

<img width="177" height="292" alt="image" src="https://github.com/user-attachments/assets/36aa40cb-1cdd-4746-b1a6-fc51ce6e96aa" />

# Algorithm

### 1. Input:

- Read the number of gardens `n` and the number of paths `m`.

- Read each path pair `(u, v)` that connects two gardens.

### 2. Graph Construction:

- Create an adjacency list for all gardens.

- For every path `(u, v)`, add each garden to the other's adjacency list.

### 3. Initialization:

- Create an integer array `flowers[n]` to store the flower type (`1–4`) assigned to each garden.

- Each garden can have one of four flower types.

### 4. Assignment Logic:

- For each garden `i`, check all adjacent gardens.

- Mark the flower types already used by its neighbors and assign the first available flower type to garden `i`.

### 5. Output:

- Print the final flower type assigned to each garden in order.
## Program:
```
/*
Program to implement Reverse a String
Developed by: SARISH VARSHAN V
Register Number:  212223230196
*/

import java.util.*;

public class GardenFlowerPlanner {

    public static int[] assignFlowers(int n, int[][] paths) {
       @SuppressWarnings("unchecked")
        // Type Your Code Here.
        List<Integer>[] adj = new ArrayList[n];
        for (int i = 0; i < n; i++) adj[i] = new ArrayList<>();

        for (int[] p : paths) {
            adj[p[0] - 1].add(p[1] - 1);
            adj[p[1] - 1].add(p[0] - 1);
        }

        int[] res = new int[n];
        for (int i = 0; i < n; i++) {
            boolean[] used = new boolean[5];
            for (int nei : adj[i]) used[res[nei]] = true;
            for (int c = 1; c <= 4; c++)
                if (!used[c]) { res[i] = c; break; }
        }
        return res;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(); 
        int m = sc.nextInt(); 

        int[][] paths = new int[m][2];
        for (int i = 0; i < m; i++) {
            paths[i][0] = sc.nextInt();
            paths[i][1] = sc.nextInt();
        }
        int[] result = assignFlowers(n, paths);

        for (int flower : result) {
            System.out.print(flower + " ");
        }
        System.out.println();
    }
}
```

## Output:
<img width="726" height="462" alt="image" src="https://github.com/user-attachments/assets/43edcf15-60ea-43dd-8d3a-d8538d6675b9" />



## Result:
The program successfully implemented and the expected output is verified.
