# Unit 3

## Question 1 1. Floyds Algorithm 2. Multi stage Graph 3. Prim's Algorithm 4. Kruskal's Algorithm 5. Dijkstra Algorithm

### 1. Floyd's Algorithm

**Concept**: Floyd's Algorithm, also known as Floyd-Warshall Algorithm, is used to find the shortest paths between all pairs of vertices in a weighted graph. It is capable of handling graphs with positive or negative edge weights but no negative weight cycles.

**Steps**:

1. **Initialization**: Start with a matrix representing distances between each pair of vertices. If there's no direct edge between two vertices, set the distance to infinity.
2. **Update Paths**: Iteratively update the distances by considering each vertex as an intermediate point.
3. **Final Matrix**: The final matrix represents the shortest distances between all pairs of vertices.

**Algorithm**:

```python
def floyd_warshall(graph):
    n = len(graph)
    dist = list(map(lambda i: list(map(lambda j: j, i)), graph))

    for k in range(n):
        for i in range(n):
            for j in range(n):
                dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])

    return dist
```

**Time Complexity**:

- **All cases**: \( O(n^3) \)

### 2. Multi-Stage Graph

**Concept**: A multi-stage graph is a directed graph where vertices are divided into stages. The edges are only allowed between vertices of consecutive stages. The goal is typically to find the shortest path from a source vertex in the first stage to a destination vertex in the last stage.

**Steps**:

1. **Identify stages**: Divide vertices into stages.
2. **Compute Shortest Path**: Use dynamic programming to compute the shortest path by considering all possible transitions between stages.

**Example**:
Consider a multi-stage graph with vertices divided into 4 stages. Compute the shortest path from vertex 1 in the first stage to vertex 10 in the last stage using dynamic programming.

### 3. Prim's Algorithm

**Concept**: Prim's Algorithm is used to find the Minimum Spanning Tree (MST) of a weighted undirected graph. It starts with a single vertex and grows the MST by adding the cheapest edge from the tree to a vertex not yet in the tree.

**Steps**:

1. **Initialize**: Start with an arbitrary vertex and add it to the MST.
2. **Grow MST**: Add the smallest edge connecting a vertex in the MST to a vertex outside the MST.
3. **Repeat**: Repeat until all vertices are included in the MST.

**Algorithm**:

```python
import heapq

def prim(graph, start):
    mst = []
    visited = set([start])
    edges = [(cost, start, to) for to, cost in graph[start].items()]
    heapq.heapify(edges)

    while edges:
        cost, frm, to = heapq.heappop(edges)
        if to not in visited:
            visited.add(to)
            mst.append((frm, to, cost))
            for to_next, cost_next in graph[to].items():
                if to_next not in visited:
                    heapq.heappush(edges, (cost_next, to, to_next))

    return mst
```

**Time Complexity**:

- **Using min-heap (priority queue)**: \( O(E \log V) \)

### 4. Kruskal's Algorithm

**Concept**: Kruskal's Algorithm is used to find the Minimum Spanning Tree (MST) of a graph. It works by sorting all the edges and adding them one by one to the MST, ensuring no cycles are formed.

**Steps**:

1. **Sort Edges**: Sort all edges by their weights.
2. **Add Edges**: Add edges to the MST in increasing order of their weights, ensuring no cycles are formed using a union-find data structure.
3. **Repeat**: Repeat until the MST contains \( V-1 \) edges.

**Algorithm**:

```python
class DisjointSet:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n

    def find(self, u):
        if self.parent[u] != u:
            self.parent[u] = self.find(self.parent[u])
        return self.parent[u]

    def union(self, u, v):
        root_u = self.find(u)
        root_v = self.find(v)
        if root_u != root_v:
            if self.rank[root_u] > self.rank[root_v]:
                self.parent[root_v] = root_u
            elif self.rank[root_u] < self.rank[root_v]:
                self.parent[root_u] = root_v
            else:
                self.parent[root_v] = root_u
                self.rank[root_u] += 1

def kruskal(graph):
    edges = []
    for u in range(len(graph)):
        for v, weight in graph[u].items():
            edges.append((weight, u, v))
    edges.sort()

    ds = DisjointSet(len(graph))
    mst = []

    for weight, u, v in edges:
        if ds.find(u) != ds.find(v):
            ds.union(u, v)
            mst.append((u, v, weight))

    return mst
```

**Time Complexity**:

- **Using union-find**: \( O(E \log V) \)

### 5. Dijkstra's Algorithm

**Concept**: Dijkstra's Algorithm is used to find the shortest paths from a single source vertex to all other vertices in a weighted graph with non-negative weights.

**Steps**:

1. **Initialize**: Set the distance to the source vertex to 0 and to all other vertices to infinity.
2. **Relax Edges**: Iteratively relax the edges by updating the shortest known distance to each vertex.
3. **Repeat**: Repeat until all vertices are processed.

**Algorithm**:

```python
import heapq

def dijkstra(graph, start):
    n = len(graph)
    dist = {i: float('inf') for i in range(n)}
    dist[start] = 0
    pq = [(0, start)]

    while pq:
        current_dist, u = heapq.heappop(pq)
        if current_dist > dist[u]:
            continue
        for v, weight in graph[u].items():
            distance = current_dist + weight
            if distance < dist[v]:
                dist[v] = distance
                heapq.heappush(pq, (distance, v))

    return dist
```

**Time Complexity**:

- **Using min-heap (priority queue)**: \( O((V + E) \log V) \)

### Conclusion

These algorithms are fundamental tools in graph theory and are widely used in various applications. They demonstrate the power of algorithm design techniques, especially the divide-and-conquer and greedy approaches, in solving complex problems efficiently.
