---
layout: post
title: "Algorithm: Shortest Path"
date: 2021-02-04
categories:
  - Algo
tags:
  - Shortest Path
author_profile: true
read_time: true
comments: true
share: true
related: true
popular: true
toc: true
toc_sticky: true
toc_label: 목차
article_tag1: shortest path
article_tag2: dijkstra
article_tag3: floyd warshall
article_tag4: bellman ford
article_section: Algo
meta_keywords: algo, Shortest Path, Dijkstra, Floyd-Warshall, Bellman-Ford
published: true
---

# Shortest Path Algorithm

- more frequent in finding shortest length than finding all path
- Many ways to question
  - __one to one__ (Very frequent) -> Dijkstra, Bellman-Ford
  - one to every (not frequent)
  - every to every (frequent) -> Floyed-Warshall

## Dijkstra algo.

- One node to every node
- Greedy: Select unvisited node w/ min. cost in every step.
- Path must be always positive length (in oppose to B1ellman-Ford)
- Processed node in each step must be set as final -> Assure shortest path for one node in each step.
- Must check every element in shortest path table in each step to select shortest path node using priority queue (min heap q) 
- Total complexity: O(E log V)


Mechanism
1. Set start node
2. Init shortest path table w/ INF
3. Select shortest path node among unvisited nodes
4. Calculate cost from selected node toward another node and set shortest path table.
5. repeat 3, 4

Using heapq
``` python
import heapq

def heapsort(iterable):
    h = []
    result = []

    for v in iterable:
        heapq.heappush(h, value)

    for i in range(len(h)):
        result.append(heapq.heappop(h))
    return result

result = heapsort([1, 5, 2, 4, 3])
print(result)
```

src code: [Dijkstra](https://github.com/shaunsukgyukoh/TeamNote/blob/main/ShortestPath/dijkstra.md)

## Floyed-Warshall algo.

- Every node to Every node
- DP: D_ab = min(D_ab, D_ai + D_ib)
- Use 2D table to store shortest path
- Count every path through certain node in each step. -> Save all shortest path in 2D list
- Permutation(V-1, 2) calculations for each step
- For each node, search every node(3 nested loops): O(N^3) --> # of V, E must be very small

e.g.)  a to b path through i:  

D23 = min(D_23, D_2i + D_i3)  
D24 = min(D_24, D_2i + D_i4)  
D32 = min(D_32, D_3i + D_i2)  
D34 = min(D_34, D_3i + D_i4)  
D42 = min(D_42, D_4i + D_i2)  
D43 = min(D_43, D_4i + D_i3)
  
src code: [Floyed-Warshall](https://github.com/shaunsukgyukoh/TeamNote/blob/main/ShortestPath/floyedWarshall.md)

## Bellman-Ford algo.

- One node to every node
- Path can be negative length

Condition:

1. No cycle -> max |V|-1 edges
2. Repeat until there's no nodes to update min distance.
3. If updating w/ infinite negative cost (negative cycle), escape loop

- O(|V||E|)

src code: [Bellman-Ford](https://github.com/shaunsukgyukoh/TeamNote/blob/main/ShortestPath/bellmanFord.md)

## Traveling Salesman Problem (TSP)

- Travel all nodes only once and return to start node w/ lowest cost.
  - Hamiltonian Cycle: Find if there exist a tour that visits every city exactly once
  - TSP: Finding minimum weight Hamiltonian Cycle.

- Naive
  1. Consider city 1 as the starting and ending point. Since the route is cyclic, we can consider any point as a starting point.
  2. Generate all (n-1)! permutations of cities.
  3. Calculate the cost of every permutation and keep track of the minimum cost permutation.
  4. Return the permutation with minimum cost.

- Using Backtracking
  1. Consider city 1 as the starting and ending point. Since the route is cyclic, we can consider any point as starting point.
  2. Start traversing from the source to its adjacent nodes in dfs manner.
  3. Calculate cost of every traversal and keep track of minimum cost and keep on updating the value of minimum cost stored value.
  4. Return the permutation with minimum cost.

  src code: [TSP](https://github.com/shaunsukgyukoh/TeamNote/blob/main/ShortestPath/tsp.md)

## Minimum Spanning Tree (MST)

Spanning tree: Partial graph that includes all nodes w/o cycle

||Graph|Tree|
|-|-|-|
|Direction|Directed/Undirected|Directed|
|Cycle|Cyclic/Acyclic|Acyclic|
|Root node|X|O|
|nodal relation|none|parent/child
|model|network|hierchy|

### Kruskal's algo

- GREEDY algo
- Disjoint: sets w/o any common element (e.g. {1,2,4,6} and {3,5})
- Union-Find algo: Find root node
- O(E log E)

- Steps:
  1. Sort all edges
  2. Include in set beginning from shortest edge
      - If cycle occurs, do not include in set
  3. repeat 2 for all edges.


### Primm's algo

## DAG (Topological Sort)

- Directed Acyclic Graph