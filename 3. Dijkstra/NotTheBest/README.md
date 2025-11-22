# 🚀 Second Shortest Path (Modified Dijkstra Algorithm)

Robin lives in a village that has **N intersections** and **R bidirectional roads**.  
He needs to travel from `1 → N`, but instead of taking the **shortest path**, he wants to take the **second-shortest path**.

---

## 🧠 Problem Definition

The **second-shortest path** is defined as:

- A path that is **longer than the shortest path**
- But **shorter than all other possible paths**
- Reusing edges is allowed
- Graph contains **positive weights only**

For each test case, we must output:


---

## 🔍 Algorithm Overview — Modified Dijkstra

For every node, we maintain **two distances**:

- `dist1[v]` → shortest distance to node `v`
- `dist2[v]` → second-shortest distance to node `v`

### ✔ Relaxation Rules

1️⃣ If the new path is **shorter than dist1[v]**:  
- Update `dist2[v] = dist1[v]`  
- Update `dist1[v] = new_dist`

2️⃣ Else if: 

→ Update `dist2[v] = new_dist`

The priority queue ensures that smaller distances are always processed first.

---

## 📌 Input Format


- `T` = number of test cases  
- `N` = intersections (1–5000)  
- `R` = roads (1–100000)  
- `w` = weight (1–5000)  

---

## 📌 Output Format
2
3 3
1 2 100
2 3 200
1 3 50
4 4
1 2 100
2 4 200
2 3 250
3 4 100

### Output
Case 1: 150
Case 2: 450

---




