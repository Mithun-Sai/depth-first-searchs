# ExpNo 2: Implement Depth First Search Traversal of a Graph

**Name:** Mithun SAI P
**Register Number:**

## Aim

To implement Depth First Search (DFS) traversal of a graph using Python 3.

## Theory

**Depth First Search (DFS)** for a graph is similar to Depth First Traversal of a tree. The main difference is that graphs may contain cycles, where a node may be visited more than once. A Boolean `visited` array is therefore used to avoid processing a node more than once.

A graph can have more than one possible DFS traversal depending on the order in which adjacent nodes are visited.

Depth First Search is an algorithm for traversing or searching tree or graph data structures. The algorithm starts at a root node, or an arbitrary starting node in the case of a graph, and explores as far as possible along each branch before backtracking.

### Step 1: Initialize the Stack and Visited Arrays

Initially, the stack and visited arrays are empty.

![DFS Step 1](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/640b3c6f-3ac1-49a2-a955-68da9a71f446)

### Step 2: Visit Node 0

Visit node `0` and put its adjacent nodes `1`, `2`, and `3` into the stack.

![DFS Step 2](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/86dcf7d9-1f9d-49b0-a821-5976a6e77606)

### Step 3: Visit Node 1

Node `1` is visited and removed from the stack. Its unvisited adjacent nodes are then considered.

![DFS Step 3](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/e6017942-08b1-4742-87ad-c97eb97bf985)

### Step 4: Visit Node 2

Node `2` is visited and removed from the stack. Its unvisited adjacent nodes `3` and `4` are added to the stack.

![DFS Step 4](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/6e6d123c-60ae-4f9c-a27c-c4fc7e57d57c)

### Step 5: Visit Node 4

Node `4` is at the top of the stack. It is visited and removed from the stack. There are no new unvisited adjacent nodes to add.

![DFS Step 5](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/20b76a05-5668-4da5-8189-e10fb1bb7238)

### Step 6: Visit Node 3

Node `3` is visited and removed from the stack. Its adjacent nodes have already been visited.

![DFS Step 6](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/3b88f04a-7846-4f75-89b4-22bbd5b48e52)

The stack is now empty, which means all the nodes have been visited and the DFS traversal is complete.

## Algorithm

1. Construct a graph with nodes and edges.
2. Initialize an empty stack and a visited array.
3. Insert the `START` node into the stack.
4. Visit the starting node and find its successors or neighbours.
5. Check whether each neighbouring node has been visited.
6. If a node has not been visited, visit it and continue the DFS traversal recursively.
7. Continue until there are no more unvisited nodes.
8. The DFS traversal is complete when all reachable nodes have been visited.

## Program

```python
from collections import defaultdict
import networkx as nx
import matplotlib.pyplot as plt

graph = defaultdict(list)
G = nx.Graph()

nodes, edges = map(int, input().split())

for i in range(edges):
    u, v = input().split()

    graph[u].append(v)
    graph[v].append(u)

    G.add_edge(u, v)

# Draw and save graph
pos = nx.spring_layout(G)

nx.draw(
    G,
    pos,
    with_labels=True,
    node_color="lightblue",
    edge_color="red",
    width=2,
    node_size=2000
)

plt.title("Graph")
plt.savefig("graph.png")
plt.close()


# Depth First Search
def dfs(graph, start, visited, path):
    visited[start] = True
    path.append(start)

    for neighbour in graph[start]:
        if not visited[neighbour]:
            dfs(graph, neighbour, visited, path)

    return path


# Starting node
start = input().strip()

path = []
visited = defaultdict(bool)

traversepath = dfs(graph, start, visited, path)

print("Depth First Search:")
print(traversepath)
```

## Sample Input 1

```text
8 9
A B
A C
B E
C D
B D
C G
D F
G F
F H
A
```

## Sample Output 1

```text
Depth First Search:
['a', 'b', 'e', 'd', 'c', 'g', 'f', 'h']
```

![DFS Graph Output 1](https://github.com/user-attachments/assets/34f78bed-1113-4f85-b24f-5fe360f8a2d7)

---

## Sample Input 2

```text
5 5
0 1
0 2
0 3
2 3
2 4
0
```

## Sample Output 2

```text
Depth First Search:
['0', '1', '2', '3', '4']
```

![DFS Graph Output 2](https://github.com/user-attachments/assets/09e119c0-d0f3-4a7e-a59c-6c5534b42903)

---

## Result

Thus, a graph was constructed and the Depth First Search traversal for the graph was implemented successfully.
