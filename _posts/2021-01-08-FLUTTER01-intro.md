---
layout: post
title: "Flutter 01: Intro and setup"
date: 2021-01-08
categories:
  - Flutter
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
article_section: Flutter
meta_keywords: flutter, basic, setup
published: true
---

## Installation

1. Download and install git for windows <https://git-scm.com/download/win>
> Check box using git in command prompt or PowerShell
1. Make "src" directory for flutter in C:\src
> Do not install Flutter in a directory like C:\Program Files\ that requires elevated privileges.
1. Git clone flutter inside src directory using window's power shell.  
   win + R --> cmd
   ``` shell
   C:\Users\asd123> cd ../../src
   C:\src\> git clone https://github.com/flutter/flutter.git -b stable
   ```
1. Update flutter path

   2. Window's Start search bar: env (환경)
   2. Edit environment variables for your account
   2. User variables -> Path -> edit
   2. Add `C:\src\flutter\bin`

1. Android toolchain
    ``` shell
    C:\src\flutter> flutter doctor --android-licenses
    ```
1. Install Android Studio and install Dart, Flutter pulgins in <https://developer.android.com/studio>

1. Install VS Code and install Dart, Flutter extensions in <https://code.visualstudio.com/>

Reference: <https://flutter.dev/docs/get-started/install/windows>