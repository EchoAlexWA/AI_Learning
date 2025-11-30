# Lecture Summary Comp9814

## Search
- **Uninformed Search**: No information about the goal state is used. Examples include:
  - Breadth-First Search (BFS)
  - Depth-First Search (DFS)
  - Uniform Cost Search (UCS)
- **Informed Search**: Uses heuristics to estimate the cost to reach the goal. Examples include:
  - A* Search

### BFS
```
function BFS(start):
    create an empty queue Q
    create an empty set visited
    Q.enqueue(start)
    visited.add(start)

    while Q is not empty:
        node = Q.dequeue()
        if node is goal:
            return success

        for each neighbor in node.neighbors:
            if neighbor not in visited:
                visited.add(neighbor)
                Q.enqueue(neighbor)

    return failure
```

### DFS
```
function DFS(start):
    create stack S
    create empty visited set
    S.push(start)

    while S not empty:
        node = S.pop()
        if node is goal:
            return success

        if node not in visited:
            visited.add(node)
            for neighbor in node.neighbors (any order):
                S.push(neighbor)

    return failure

```
recursion version:
```
DFS(node):
    if node is goal: return true
    visited.add(node)

    for each neighbor in node.neighbors:
        if neighbor not in visited:
            if DFS(neighbor) == true:
                return true

    return false
```
  
### UCS
```
function UCS(start):
    create priority queue PQ ordered by g
    PQ.insert(start, g(start)=0)
    create empty dictionary cost
    cost[start] = 0

    while PQ not empty:
        node = PQ.pop()    // lowest g-value

        if node is goal:
            return success

        for each (neighbor, step_cost) of node:
            new_cost = cost[node] + step_cost

            if neighbor not in cost or new_cost < cost[neighbor]:
                cost[neighbor] = new_cost
                PQ.insert(neighbor, new_cost)

    return failure
```

### Greedy Best-First Search
```
function Greedy(start):
    PQ ordered by h(n)
    PQ.insert(start)

    visited = empty set

    while PQ not empty:
        node = PQ.pop()   // lowest h

        if node is goal:
            return success

        if node not in visited:
            visited.add(node)

            for neighbor in node.neighbors:
                PQ.insert(neighbor)

    return failure

```

### A* Search
```
function Astar(start):
    PQ ordered by f(n) = g(n) + h(n)
    PQ.insert(start, f=0+h(start))
    g[start] = 0

    while PQ not empty:
        node = PQ.pop()   // lowest f

        if node is goal:
            return success

        for each (neighbor, step_cost):
            new_g = g[node] + step_cost

            if neighbor not in g or new_g < g[neighbor]:
                g[neighbor] = new_g
                f = new_g + h(neighbor)
                PQ.insert(neighbor, f)

    return failure
```
