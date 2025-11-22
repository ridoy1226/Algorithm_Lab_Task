#  Knight Moves (BFS in a 2D Grid) — Shortest Path for a Chess Knight

##  Problem Overview

This is a classic **shortest path** problem on a chessboard.  
Given two squares **a** and **b** on an 8×8 board, the task is:

###  Find the **minimum number of knight moves** required to reach `b` from `a`.

This problem can be modeled as a **shortest path search in an unweighted graph**.

---

## Graph Modeling

| Concept | Meaning |
|---------|---------|
| **Nodes** | All 64 squares on the chessboard |
| **Edges** | A valid knight move between two squares |
| **Cost** | Each move has equal cost (1) |

Since all edges have equal weight, the ideal algorithm is:

##  **Breadth-First Search (BFS)**

---

##  What is BFS?

**Breadth-First Search (BFS)** is a graph traversal algorithm that explores nodes **level by level**.

It uses a **queue** to ensure:

- All positions reachable in *k* moves are explored before positions reachable in *k+1* moves.
- Therefore, BFS guarantees the **shortest path** in an unweighted graph.

This makes BFS perfect for the knight-moves problem.

---

##  Representing the Board & Knight Moves

Before running BFS, we need to represent how a knight moves from one square to another.

###  The 8 Possible Knight Moves

From a position `(i, j)`, a knight may move to any of these 8 squares:
(i-2, j+1)
(i-2, j-1)
(i-1, j+2)
(i-1, j-2)
(i+1, j+2)
(i+1, j-2)
(i+2, j+1)
(i+2, j-1)








###  Implementation in Code

```cpp
// kr[] stores the possible row offsets for knight moves
const int kr[] = {2, 2, -2, -2, 1, 1, -1, -1};

// kc[] stores the possible column offsets for knight moves
const int kc[] = {1, -1, 1, -1, 2, -2, 2, -2};
FUNCTION bfs_knight(startR, startC, endR, endC):

Looping i = 0 to 7,
new_r = r + kr[i] and new_c = c + kc[i] gives all valid knight moves.

 Why BFS Works Here

BFS naturally explores moves in layers:

Layer 0: starting square

Layer 1: squares reachable in 1 move

Layer 2: squares reachable in 2 moves
The first time BFS reaches the target square, we are guaranteed that it took the minimum number of moves.

 Required Arrays
Name	Purpose
dist[8][8]	Stores the minimum number of moves from start to each square
color[8][8]	Tracks node states during BFS
queue<pair<int,int>>	Holds squares to be processed
 Meaning of color values
Value	Meaning
-1	White — Unvisited
1	Gray — Currently in queue
2	Black — Fully processed


    N = 8
    DEFINE dist[N][N], color[N][N]
    DEFINE Queue Q

    // Initialization
    FOR r FROM 0 TO N-1:
        FOR c FROM 0 TO N-1:
            dist[r][c] = INFINITY
            color[r][c] = -1

    dist[startR][startC] = 0
    color[startR][startC] = 1
    ENQUEUE (startR, startC)

    // BFS Loop
    WHILE Q IS NOT EMPTY:
        (r, c) = DEQUEUE()

        IF (r, c) == (endR, endC):
            RETURN dist[r][c]   // shortest distance found

        FOR i FROM 0 TO 7:
            newR = r + kr[i]
            newC = c + kc[i]

            IF newR,newC is inside board AND color[newR][newC] == -1:
                color[newR][newC] = 1
                dist[newR][newC] = dist[r][c] + 1
                ENQUEUE(newR, newC)

        color[r][c] = 2   // mark processed

    RETURN -1   // unreachable (should not happen in 8x8 board)

