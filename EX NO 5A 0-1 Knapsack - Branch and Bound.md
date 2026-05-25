
# EX 5A 0/1 Knapsack Problem - Branch&Bound 
## DATE: 18.05.26
## AIM:
To Write a Java program to solve 0/1 Knapsack problem using Branch and Bound Approach.
You are heading a college entrepreneurship cell that can invest in up to N student‑startups.

For each startup i you know: cost[i]  — the amount (in ₹ lakh) required to join the showcase profit[i] — the estimated profit (in ₹ lakh) you’ll gain if it succeeds You have a total budget of B ₹ lakh. Pick a subset of startups so that the sum of costs ≤ B and the sum of profits is maximised.

Because N can be as large as 50, a plain exhaustive search (2^N) is too slow.

The recommended approach is Branch & Bound with a fractional‑knapsack upper bound (but any algorithm that meets the constraints is accepted). 

Input Format

N

B

cost[1] cost[2] … cost[N]

profit[1] profit[2] … profit[N]

1 ≤ N ≤ 50

1 ≤ B ≤ 1 000 000

1 ≤ cost[i], profit[i] ≤ 10 000 

Output Format

maxProfit

For example:


# Algorithm

### 1. Input:

- Read number of items `N` and bag capacity `B`.

- Read the `cost` and `profit` of each item.

### 2. Initialization:

- Create `Item` objects storing `cost`, `profit`, and `profit-to-cost ratio`.

- Sort items in **descending order of ratio** (profit per cost).

### 3. Bounding Function:

- Define a `bound()` function to calculate the **upper bound of profit** that can be achieved from a given node using fractional knapsack logic.

### 4. Branch and Bound Logic:

- Use a queue to explore possible item selections.

- For each node (state), generate two branches:

  - **Include** the next item.

  - **Exclude** the next item.

- Update `maxProfit` if a valid higher profit is found.

- Add nodes to the queue only if their bound is greater than current `maxProfit`.

### 5. Output:

- After exploring all possible branches, print the **maximum achievable profit**.  

## Program:
```
/*
Program to implement Reverse a String
Developed by: SARISH VARSHAN V
Register Number:  212223230196
*/

import java.util.*;

public class Main {

    static class Item {
        int cost, profit;
        double ratio;
        Item(int c, int p) { cost = c; profit = p; ratio = (double) p / c; }
    }

    static class Node {
        int level, profit, cost;
        double bound;
    }

    static int N, B;
    static Item[] items;

    static double bound(Node u) {
        if (u.cost >= B) return 0;
        double profitBound = u.profit;
        int j = u.level + 1, totWeight = u.cost;

        while (j < N && totWeight + items[j].cost <= B) {
            totWeight += items[j].cost;
            profitBound += items[j].profit;
            j++;
        }

        if (j < N)
            profitBound += (B - totWeight) * items[j].ratio;

        return profitBound;
    }

    static int knapsack() {
        Arrays.sort(items, (a, b) -> Double.compare(b.ratio, a.ratio));

        Queue<Node> q = new LinkedList<>();
        Node u = new Node(), v = new Node();
        u.level = -1; u.profit = 0; u.cost = 0;
        double maxProfit = 0;
        q.add(u);

        while (!q.isEmpty()) {
            u = q.poll();
            if (u.level == N - 1) continue;

            v.level = u.level + 1;

            // include item
            v.cost = u.cost + items[v.level].cost;
            v.profit = u.profit + items[v.level].profit;

            if (v.cost <= B && v.profit > maxProfit)
                maxProfit = v.profit;

            v.bound = bound(v);
            if (v.bound > maxProfit)
                q.add(new Node(){{
                    level=v.level; cost=v.cost; profit=v.profit; bound=v.bound;
                }});

            // exclude item
            v.cost = u.cost;
            v.profit = u.profit;
            v.bound = bound(v);
            if (v.bound > maxProfit)
                q.add(new Node(){{
                    level=v.level; cost=v.cost; profit=v.profit; bound=v.bound;
                }});
        }
        return (int) maxProfit;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        N = sc.nextInt();
        B = sc.nextInt();
        int[] cost = new int[N], profit = new int[N];
        for (int i = 0; i < N; i++) cost[i] = sc.nextInt();
        for (int i = 0; i < N; i++) profit[i] = sc.nextInt();

        items = new Item[N];
        for (int i = 0; i < N; i++) items[i] = new Item(cost[i], profit[i]);

        System.out.println(knapsack());
    }
}
```

## Output:
<img width="691" height="233" alt="image" src="https://github.com/user-attachments/assets/70a347ec-6842-4f63-bb8b-179f0040451e" />



## Result:
The program successfully solved 0/1 Knapsack problem using branch & bound and output is verified. 
