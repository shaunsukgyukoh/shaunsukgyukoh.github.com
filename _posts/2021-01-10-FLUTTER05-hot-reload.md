---
layout: post
title: "Flutter 05: Creating Flutter app: Hot reload"
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
article_tag1: basic
article_tag2: layout
article_section: Flutter
meta_keywords: flutter, basic, layout
published: true
---

#### Hot reload
re-run(cntl + shift + \) is cumbersome. --> hot reload allow automatic reloading as developer changes the code. 
__Stateless widgets__  is the key to hot reload.
More reusable.

- Stateless Widgets
  - The state of the widget __cannot__ change over time

- Stateful Widgets
  - The state of the widget __can__ change over time


`stless + tab` : Create custom stateless widget class

Simply saving the .dart file reflect the changes in emulator.

``` dart
void main() {
  runApp(MaterialApp(
    home: Home(), // call stateless widget
  ));
}

class Home extends StatelessWidget {
  @override // Redefine build method: This allow the build Widget below to be used instead of the build inherited from ancestor
  Widget build(BuildContext context) { // This allow automatic loading
    return Scaffold(
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
            fontFamily: "HachiMaru", // What font is called in pubspec.yaml
            // Font can be downloaded in [google fonts](https://fonts.google.com/)
            // Make fonts directory in project and drag and drop the .ttf file inside the font folder
          ),
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {},
        child: Text('click'),
        backgroundColor: Colors.blueGrey[800],
      ),
    );
  }
}
```