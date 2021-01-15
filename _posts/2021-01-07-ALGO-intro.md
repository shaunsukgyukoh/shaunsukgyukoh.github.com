---
layout: post
title: "Algorithm: Intro and setup"
date: 2021-01-07
categories:
  - Algo
tags:
  - basic
  - setup
author_profile: true
read_time: true
comments: true
share: true
related: true
popular: true
toc: true
toc_sticky: true
toc_label: 목차
article_tag1: basic
article_tag2: setup
article_section: Algo
meta_keywords: algo, basic, setup
published: true
---

# Preparing algo competition

## frequent question types
- Implementation
  - Parsing
  - Hashing
  - Sort
  - __Simulation__
  - __String / RE (Regular Expression)__
  - Bitmasking
  - __Set / Map by tree or hash__
- Search
  - Graph
  - __DFS / BFS__
  - Full search (Backtrack)
  - MST
- Data structure
  - Stack
  - Queue
  - __Deque__
  - Heap
  - Tree
- Algorithm
  - __Greedy__
  - __DP__
  - Binary search
  - __Dijkstra__
  - Union Find
- Mathematics
  - __Prime numbers__
  - Euclidean
  - Geometry
  - Number theory
  - Linear Algebra

## Figuring out what algo should be used and which standard library to use
Depending on input number N, We have to figure out complexity to select correct methods that will satisfy time and memory limit.  
Python calculates about __20,000,000 per sec__.  
2^10 ~ 1000 : OK  
2^20 ~ 1M : OK
2^30 ~ 10 Billion (1,000,000,000) : TLE

- If time limit : < 1 sec.
  - N = 500   : Can use __O(N^3)__
  - N = 2000  : Can use __O(N^2)__
  - N = 100,000 : Use __O(N _log_ N)__
  - N = 10,000,000 : Must use __O(N)__

- Remember Standard library functions' complexity and make use of it.  
[Check out complexities for iterable functions in Python](https://shaunsukgyukoh.github.io/algo/ALGO-operationTimeComplexity/)

- checking time consumption in Python
  ``` python
  import time
  st = time.time()
  process()
  print(time.time() - st)
  ```

## Languages
- C++: Better for recursion, data structure
- Python: Better for string, sort, parsing

## Error Types
- CE: Compile Error --> Correct __grammer error__ 문법오류
- TLE: Time Limit Exceeded --> Need __optimization__ 시간초과 (최적화 필요)
- MLE: Memory Limit Exceeded --> Need __optimization__  메모리 초과 (최적화 필요)
- RE: Runtime Error 과정 오류
  1. div by 0
  2. index out of bound
  3. inf loop (TLE)
- WA: Wrong Answer 틀림
  1. limit and up/down check 제한 및 대소관계 (이상이하초과미만 minmax)
  2. Exception handling 예외처리 (예: 단, 없는경우 -1 출력)
  3. Input / output (공백, 양식 ,순서, 정렬유무)
  4. TLE / MLE 시간제한 / 메모리제한
  5. Correct algorithm? 알고리즘 맞는가?
  6. Is this the logic I thought of? 내가 생각한 로직대로 구현했나?
  7. Unnecessary loop? 불필요한 반복문 있나?
  8. Duplciation handle 중복처리


## VS Code setup
Most of free online IDE such as [repl.it](https://repl.it) are generally open to public. This means that your solutions can be caught as cheating in competetion. (Paid account may have private sessions). Therefore, I will use VS Code for solving problems.  
In Windows, I/O redirection is not supported. Install WSL2(Windows Subsystem for Linux 2) for I/O redirection support in VS Code. Linux and Mac does not need any optional action.  
1. Install _Python_ extension.  
2. In VS Code, press `cntl + p` or `cmd + p`  and search for _launch.json_ and add __args__ line for I/O redirection.  
launch.json:
``` json
"version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Current File",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "args": ["<", "in.txt", ">", "out.txt"]
        }
    ]
```
Now I/O redirection is activated for your VS Code system.  
3. Create __input.txt__ and __output.txt__. Open both files and locate them as shown in the picture. This will allow you to check the output immediately.

<img src="/assets/images/algo/algo000.PNG">