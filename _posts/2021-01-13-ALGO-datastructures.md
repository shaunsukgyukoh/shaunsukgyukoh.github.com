---
layout: post
title: "Algorithm: Data structures"
date: 2021-01-13
categories:
  - Algo
tags:
  - basic
  - data structures
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
article_tag2: data structures
article_section: Algo
meta_keywords: algo, basic, data structures
published: true
---

# Data structures

Complexity
<img src="https://www.bigocheatsheet.com/img/big-o-cheat-sheet-poster.png">  
Reference: <https://www.bigocheatsheet.com/>

## Array

- Usage: Using same type of data
- Pro: access fast
- Con: add/del hard

## Queue

- Usage: Multi-tasking scheduling (OS)
- Pro: -
- Con: -
- Enqueue @ TAIL
- Dequeue @ HEAD

## Stack

- Usage: Computer internal process' function call 
- Pro: Simple structure -> easy to implement, fast read/write
- Con: maximum # of data must be set. If max # is larger than usage -> waste of memory.
- Push @ HEAD
- Pop @ TAIL

## Singly-Linked List

- Pro: Don't need to pre-allocate memory: Can connect data far away from src
- Con: 
  1. Need extra space for connecting: memory inefficient.
  2. Slow finding connecting info.
  3. Need extra connecting step when add/delete data in middle.

## Doubly-Linked List

- Pro: Better accessability

## Hash Table

- Usage:
  1. When need lot of searching.
  2. When need lot of write/del/read.
  3. When need cache (Easy to check duplicate).

- Pro:
  1. O(1) in data read/write
  2. Easy to check duplicate

- Con:
  1. Need lot of memory
  2. Need extra data structure to avoid same address collision for multiple keys.

## Heap

- Usage: Complete Binary Tree that can fast search min and max value.

- Heap vs Binary Tree  
  - Same: Both are binary tree  
  - Difference:  

  |Heap |Binary Tree|
  |---|---|
  |Each nodes' value is greater than or equal to child node (for __MAX__ heap) (Heap doesn't have rule about which child is large or small)  |left child < parent < right child |
  | For finding max/min  | For Searching |
