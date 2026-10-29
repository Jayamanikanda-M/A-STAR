# ExpNo 4: Implement A* search algorithm for a Graph

# Name: JAYAMANIKANDA M

# Register Number: 212225230113

# Aim:

To Implement A* Search algorithm for a Graph using Python 3.

# Algorithm:

1. Initialize the open list


2. Initialize the closed list put the starting node on the open list (you can leave its f at zero)


3. while the open list is not empty


a) find the node with the least f on the open list, call it "q"


b) pop q off the open list


c) generate q's 8 successors and set their parents to q


d) for each successor


i) if successor is the goal, stop search

```
ii) else, compute both g and h for successor


successor.g = q.g + distance between successor and q


successor.h = distance from goal to successor (This can be done using many ways, we will discuss three heuristics- Manhattan, Diagonal and Euclidean Heuristics)


successor.f = successor.g + successor.h


iii) if a node with the same position as successor is in the OPEN list which has a lower f than successor, skip this successor


iv) if a node with the same position as successor is in the CLOSED list which has a lower f than successor, skip this successor otherwise, add the node to the open list

```
end (for loop)


e) push q on the closed list


end (while loop)



# Program:

```python
from collections import defaultdict

H_dist = {}

def aStarAlgo(start_node, stop_node):
    open_set = set([start_node])
    closed_set = set()
    g = {}
    parents = {}
    g[start_node] = 0
    parents[start_node] = start_node

    while len(open_set) > 0:
        n = None

        for v in open_set:
            if n is None or g[v] + heuristic(v) < g[n] + heuristic(n):
                n = v

        if n is None:
            print("Path does not exist!")
            return None

        if n == stop_node:
            path = []
            while parents[n] != n:
                path.append(n)
                n = parents[n]
            path.append(start_node)
            path.reverse()
            print("Path found: {}".format(path))
            return path

        for (m, weight) in get_neighbors(n):
            if m not in open_set and m not in closed_set:
                open_set.add(m)
                parents[m] = n
                g[m] = g[n] + weight
            else:
                if g[m] > g[n] + weight:
                    g[m] = g[n] + weight
                    parents[m] = n
                    if m in closed_set:
                        closed_set.remove(m)
                        open_set.add(m)

        open_set.remove(n)
        closed_set.add(n)

    print("Path does not exist!")
    return None

def get_neighbors(v):
    return Graph_nodes.get(v, [])

def heuristic(n):
    return H_dist.get(n, 0)

graph = defaultdict(list)
n, e = map(int, input().split())

for _ in range(e):
    while True:
        line = input().strip()
        if line:
            break
    u, v, cost = line.split()
    cost = float(cost)
    graph[u].append((v, cost))
    graph[v].append((u, cost))

for _ in range(n):
    while True:
        line = input().strip()
        if line:
            break
    node, h = line.split()
    H_dist[node] = float(h)

Graph_nodes = graph
start_node = max(H_dist, key=H_dist.get)
goal_node = min(H_dist, key=H_dist.get)
aStarAlgo(start_node, goal_node)

```

*(Extracted from program text)*

# Sample Graph I
<img width="1012" height="652" alt="image" src="https://github.com/user-attachments/assets/f9912523-6226-482e-936e-5fd5f8528aca" />


# Sample Input

10 14

A B 6

A F 3

B D 2

B C 3

C D 1

C E 5

D E 8

E I 5

E J 5

F G 1

G I 3

I J 3

F H 7

I H 2

A 10

B 8

C 5

D 7

E 3

F 6

G 5

H 3

I 1

J 0

# Sample Output
<img width="582" height="426" alt="image" src="https://github.com/user-attachments/assets/13731027-ec32-487e-889e-d8ee6855b079" />


Path found: ['A', 'F', 'G', 'I', 'J']

Execution Successful

# Sample Graph II
<img width="993" height="627" alt="image" src="https://github.com/user-attachments/assets/0868220c-4f42-46f7-a877-df3fc40d7713" />


# Sample Input

6 6

A B 2

B C 1

A E 3

B G 9

E D 6

D G 1

A 11

B 6

C 99

E 7

D 1

G 0

# Sample Output
<img width="410" height="252" alt="image" src="https://github.com/user-attachments/assets/73ae8e6b-6f69-4ada-8325-919f3e0d215a" />


Path found: ['C', 'B', 'G']

Code Execution Successful

 # Result:
 The Python program to Implement A * Search algorithm for a Graph has been executed successfully
.
