---
layout: post
title: "Flutter 03: Android studio setup"
date: 2021-01-08
categories:
  - Flutter
tags:
  - framework
author_profile: true
read_time: true
comments: true
share: true
related: true
popular: true
toc: true
toc_sticky: true
toc_label: 목차
article_tag1: framework
article_section: Language
meta_keywords: flutter, dart, language
published: true
---

## Creating Flutter app in Android studio

1. Open Android studio  
<img src="/assets/images/flutter/flutter000.PNG" width="30%" height="40%">
1. Configure - AVD Manager - Create Virtual Device...  
<img src="/assets/images/flutter/flutter001.PNG" width="30%" height="60%">
1. Select hardware - Next - Select System Image - Next
  - Adding more hardware
    2. Download skin <https://developer.samsung.com/galaxy-emulator-skin/guide.html>
    2. Unzip in `Android Studio > plugins > android > lib > device-art-resources`
    2. New Hardware Profile -> add appropriate device name, screen size, resolution, RAM  
    <img src="/assets/images/flutter/flutter006.PNG" width="40%" height="40%">
    2. Scroll down and set Default skin folder to the ones you downloaded.  
    <img src="/assets/images/flutter/flutter007.PNG" width="40%" height="40%">
    2. Finish  

1. Change Graphics --> Hardware - GLES 2.0 for __faster rendering__ --> Finish  
<img src="/assets/images/flutter/flutter002.PNG" width="40%" height="40%">  
This is the screen when you are done with emulator setup  
<img src="/assets/images/flutter/flutter003.PNG" width="40%" height="40%">
1. From initial Android Studio : Create New Flutter Project - Flutter Application - Next
1. If Flutter SDK path is empty: put flutter path (e.g. D:\src\flutter) - Next - Finish  
<img src="/assets/images/flutter/flutter004.PNG" width="40%" height="40%">
1. Choose virtual machine and run (shift + F10) (It take some time for the first run)
1. We will work on main.dart 99% of the time.  
<img src="/assets/images/flutter/flutter004.PNG" width="40%" height="40%">
1. If you want to re-run press cntl + shift + \