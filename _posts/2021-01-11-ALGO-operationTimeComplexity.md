---
layout: post
title: "Algorithm: Time complexity of various operations in Python"
date: 2021-01-08
categories:
  - Algo
tags:
  - tips
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
article_tag2: tipss
article_section: Algo
meta_keywords: algo, basic, tips
published: true
---

# Time complexity of various iterable operations in Python

# List

|Operation|Average Case|Operation|Average Case|
|---|---|---|---|
| copy | O(n) | __arr.append(v)__ | O(1) |
| __arr.pop(i)__ | O(1) | arr.pop(1) | O(n) |
| __.insert(i, v)__ | O(n) | get | O(1) |
| set | O(1) | __arr.remove(v)__ | O(n) |
| iteration | O(n) | get slice | O(k) |
| del slice | O(n) | set slice | O(k+n) |
| extend | O(k) | __arr.sort()__ | O(n log n) |
| multiply | O(nk) | __x in s__ | O(n) |
| __min(arr)/max(arr)__ | O(n) | __len(arr)__ | O(1) |
| __arr.reverse()__ | O(n) | __arr.count(v)__ | O(n) |

# collections.deque

|Operation|Average Case|Operation|Average Case|
|---|---|---|---|
| copy | O(n) | append | O(1) |
| appendleft | O(1) | pop | O(1) |
| popleft | O(1) | extend | O(k) |
| extendleft | O(k) | rotate | O(k) |
| remove | O(n) |  |  |

# set

|Operation|Average Case|Worst Case|notes|
|---|---|---|---|
| x in s | O(1) | O(n) | |
| union s\|t | O(len(s)+len(t)) |  | |
| intersection s&t | O(min(len(s), len(t)) | O(len(s) * len(t)) | replace "min" with "max" if t is not a set|
| multi intersection s1&s2&..&sn | | (n-1)*O(l) where l is max(len(s1),...,len(sn))| |
| difference s-t | O(len(s)) |  | |
| s.difference_update(t) | O(len(t)) |  | |
| symmetric differece s^t | O(len(s)) | O(len(s) * len(t)) | |
| s.symmetric_difference_update(t) | O(len(t))  | O(len(t) * len(s)) | |

# dict

|Operation|Average Case|Operation|Average Case|
|---|---|---|---|
| k in d | O(1) | copy | O(n) |
| get item | O(1) | set item | O(1) |
| delete item | O1() | iteration | O(n) |

Referece: <https://wiki.python.org/moin/TimeComplexity>