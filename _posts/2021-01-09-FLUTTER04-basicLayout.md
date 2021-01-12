---
layout: post
title: "Flutter 04: Creating Flutter app: basic layout"
date: 2021-01-09
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
article_tag1: basic
article_tag2: layout
article_section: Flutter
meta_keywords: flutter, basic, layout
published: true
---

## Creating Flutter app: basic layout

- Putting text in home property via Text widget

``` dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    // home 은 home 스크린에 뭘 띄울지 보여줌
    home: Text("Hey Shaun!"), // 보통 여러개의 property 를 가지므로 항상 뒤에 , 붙이는게 좋은 습관임.

 )); // MyApp 이 위젯임!
}
```

- Layout setting

``` dart
import 'package:flutter/material.dart';
void main() {
  runApp(MaterialApp(
    // home 은 home 스크린에 뭘 띄울지 보여줌
    home: Scaffold( // Scaffold 위젯은 기본적인 layout 표현 (위에 Appbar 나 action 버튼같은것들)
      appBar: AppBar(
        title: Text("Hello Shaun!"),
        centerTitle: true,
      ), // Scaffold 는 appBar property를 갖고 있고 그 값은 AppBar 위젯임.
      body: Center(
        child: Text("My first app"), // 위젯을 고대로 다른 위젯한테 nested 하면 child property를 사용
      ),
      floatingActionButton: FloatingActionButton( // Highlight 은 뭔가 잘못된걸 알려줌.
        child: Text('click'),
      ),
    ),

  ));
}
```

- Putting colors and font
Flutter app have access to Matrerial color palette shown in [here](https://material.io/design/color/the-color-system.html#tools-for-picking-color, "Material color pallete")  
In backgroundColor property, color options will appear when type `Colors.`.  
cntl+ q shows more options with brackets.

Fonts can be downloaded in [google fonts](https://fonts.google.com/).  
Make fonts directory in project and drag and drop the .ttf file inside the font folder.  
<img src="/assets/images/flutter/flutter008.PNG" width="30%" height="40%">

Edit pubspec.yaml file to add assets like font. \! Must use __2 space__ indentation for pubspec.yaml.
After saving edits, popup will show in main.dart. Just press `Get dependencies`

``` dart
void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text("Hello Shaun!"),
        centerTitle: true,
        backgroundColor: Colors.cyan[300], // Material design pallet
      ),
      body: Center(
        child: Text(
          "My first app",
          style: TextStyle( // select TextStyle by clicking and cntl+q gives style options
            fontSize: 20.0,
            fontWeight: FontWeight.bold,
            letterSpacing: 2.0,
            color: Colors.grey[600],
            fontFamily: "HachiMaru", // Name of font saved in pubspec.yaml
          ),
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {},
        child: Text('click'),
        backgroundColor: Colors.blueGrey[800],
      ),
    ),
  ));
}
```