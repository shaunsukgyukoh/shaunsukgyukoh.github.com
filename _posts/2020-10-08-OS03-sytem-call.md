---
layout: post
title: "OS 03: System Call"
date: 2020-10-08
categories:
  - General CS
tags:
  - os
author_profile: true
read_time: true
comments: true
share: true
related: true
popular: true
toc: true
toc_sticky: true
toc_label: 목차
article_tag1: os
article_section: General CS
meta_keywords: general cs, os
published: true
---

## Relationship between OS, app, and H/W

* OS give permission and allocate memory that app requests (Manage H/W resources)
* OS provide CPU time that app requests 
* OS give permissions for using I/O devices that app requests

## OS provide interfaces

* For **user** interface
    - Shell
        + A program that allow user to manipulate OS functions and services
        + CLI / GUI

* For **APP** interface
    - API (Application Programming Interface)
        + Provide functions
        + open()
    - Usually provided as library format
        + C library <https://www.gnu.org/software/libc>

* System Call
    - OS provide command / function called **system call** to use OS's functions requested by APP
    - Most API consists of calling **system call**

    <img src="/assets/images/os/os007.png">

## If want to make OS?

    1. Implement OS (kernel)
    2. Implement sys. call
    3. Implement C API (library)
    4. Implement Shell program
    5. Develop application programs