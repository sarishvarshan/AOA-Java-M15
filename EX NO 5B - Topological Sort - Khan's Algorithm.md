
# EX 5B Topological Sort - Khan's Algorithm
## DATE: 18.05.26
## AIM:
To write a Java program to for given constraints.
Problem Description:
A software development team is preparing for a product release. The release consists of multiple tasks, each dependent on other tasks being completed first. You are to determine a valid order in which all tasks can be completed. If it's not possible due to cyclic dependencies, output that the release cannot be scheduled.

Each task is labeled from 0 to n-1. The dependencies are provided in the form of pairs [a, b] which means task a depends on task b.

Implement a program to find a valid task execution order using topological sort.

Input Format:

An integer n — number of tasks.

An integer m — number of dependencies.

m lines follow with two integers a and b — representing a depends on b.

Output Format:

If a valid order exists, print the task numbers in a possible execution order (space-separated).

If not, print "Release cannot be scheduled".

<img width="341" height="363" alt="image" src="https://github.com/user-attachments/assets/f0355541-4f66-49da-bcd3-171a799a7c1f" />

# Algorithm

### 1. Input:

- Read the number of tasks `n` and the number of dependency pairs `m`.

- Read each dependency pair and store them in a 2D array.

### 2. Graph Construction:

- Create an adjacency list to represent task dependencies.

- Maintain an `indegree` array to count incoming edges for each task.

### 3. Initialization:

- Add all tasks with `indegree = 0` (no dependencies) to a queue.

### 4. Topological Sorting:

- Repeatedly remove a task from the queue, add it to the order list, and decrease the indegree of its dependent tasks.

- If a dependent task’s indegree becomes `0`, add it to the queue.

### 5. Output:

- If all tasks are processed, print the valid order of execution.

- Otherwise, display `"Release cannot be scheduled"` if a cycle (dependency conflict) exists.

## Program:
```
/*
Program to implement Reverse a String
Developed by: SARISH VARSHAN V
Register Number:  212223230196
*/

import java.util.*;

public class prog{

    public static List<Integer> findTaskOrder(int n, int[][] dependencies) {
       //Write your code
       List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        int[] indegree = new int[n];
        for (int[] d : dependencies) {
            int a = d[0], b = d[1];
            graph.get(b).add(a);
            indegree[a]++;
        }

        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < n; i++)
            if (indegree[i] == 0) q.add(i);

        List<Integer> order = new ArrayList<>();
        while (!q.isEmpty()) {
            int node = q.poll();
            order.add(node);
            for (int nei : graph.get(node)) {
                indegree[nei]--;
                if (indegree[nei] == 0) q.add(nei);
            }
        }

        if (order.size() != n) return null; // cycle detected
        return order;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(); // number of tasks
        int m = sc.nextInt(); // number of dependencies

        int[][] dependencies = new int[m][2];
        for (int i = 0; i < m; i++) {
            dependencies[i][0] = sc.nextInt(); // a
            dependencies[i][1] = sc.nextInt(); // b
        }

        List<Integer> result = findTaskOrder(n, dependencies);

        if (result == null) {
            System.out.println("Release cannot be scheduled");
        } else {
            for (int task : result) {
                System.out.print(task + " ");
            }
        }
    }
}
```

## Output:
<img width="984" height="536" alt="image" src="https://github.com/user-attachments/assets/846ffaf4-da14-49ed-a110-a50fcb17f551" />



## Result:
The program successfully implemented and the expected output is verified.
