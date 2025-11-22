# 🌟 Bicoloring (BFS) — Problem Analysis & Solution

## 📘 Problem: Graph Bicoloring

Can a graph be colored using **only two colors**, such that no two **adjacent nodes** share the same color?  
In other words, we must determine whether the graph is **bicolorable**.

This is the same as checking whether the graph is a **bipartite graph**.

---

## 🎯 Core Concept: Bipartite Graph

A graph is **bipartite** if:

- Its vertices can be divided into two **disjoint sets** (Set A and Set B)
- Every edge connects a vertex from Set A to Set B
- No edge exists between vertices of the same set

A bipartite graph can always be colored using **two colors** (e.g., White and Black).

---

## 🚫 When is Bicoloring NOT Possible?

Bicoloring is **not possible** if the graph contains an:

### 🔺 Odd-Length Cycle

Example:  
A **triangle (3-cycle)** cannot be bicolored because:

- If Node 1 = White  
- Node 2 = Black  
- Node 3 must be White  
- But Node 3 is adjacent to Node 1 → ❌ conflict

So the graph becomes **NOT BICOLORABLE**.

---

## 🔍 Solution Approach: Breadth-First Search (BFS)

We use **BFS** to traverse the graph and try to assign alternating colors (0 and 1) to each node.

### ✔ Steps of the Algorithm

1. **Initialization**  
   - All nodes are marked as **uncolored** (`-1`).

2. **Start BFS**  
   - Begin from node `0`  
   - Assign color `0`  
   - Push it into the queue

3. **Coloring during BFS**  
   For each node `u` popped from the queue:
   - Each neighbor `v` should get **opposite color** = `1 - color[u]`

4. **Conflict Check**  
   If any neighbor `v` already has the **same color** as `u` →  
   ➜ Graph contains an **odd cycle**  
   ➜ **NOT BICOLORABLE**

5. **If BFS completes without conflict:**  
   ➜ **BICOLORABLE**

---

## 💻 Pseudocode

```pseudocode
FUNCTION isBicolorable(n, adjList):

    DECLARE colors[n]
    FOR i FROM 0 TO n-1:
        colors[i] = -1   // -1 means Uncolored

    DECLARE queue

    colors[0] = 0       // Start with node 0 having color 0
    queue.push(0)

    WHILE queue is not empty:
        u = queue.pop()
        neighborColor = 1 - colors[u]

        FOR each neighbor v in adjList[u]:

            IF colors[v] == -1:
                colors[v] = neighborColor
                queue.push(v)

            ELSE IF colors[v] == colors[u]:
                RETURN false   // Conflict → Odd cycle detected

    RETURN true
