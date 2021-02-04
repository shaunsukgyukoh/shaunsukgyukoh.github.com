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