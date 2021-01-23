---
layout: post
title: "Flutter 14: Map and Routing"
date: 2021-01-24
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

## Map and Routing

Map is like dict() in Python -> use keys and values

- `MaterialApp()`'s `routes:` property act as map


  ``` dart
  void main() {
    Map student = {'name' : 'sso', 'age' : 22};
    print(student['name']); // sso
  }
  ```

- Routing `Navigator.pushNamed(context, '/location');` act as STACK -> LIFO

  ``` dart
  //main.dart

  import 'package:flutter/material.dart';
  import 'package:project02_world_time/pages/choose_location.dart';
  import 'package:project02_world_time/pages/home.dart';
  import 'package:project02_world_time/pages/loading.dart';

  void main() {
    runApp(MaterialApp(
      // home: Home(), // delete since it conflicts w/ '/' in routes. --> instead, use initialRoute.
      initialRoute: '/home', // '/' is default but we can override it.
      routes: {
        '/': (context) => Loading(), // '/' indicate first route and context keep track of where we are on widget tree
        '/home': (context) => Home(),
        '/location': (context) => ChooseLocation(),
      },
    ));
  }

  ```

  ``` dart
  //home.dart
  import 'package:flutter/material.dart';

  class Home extends StatefulWidget {
    @override
    _HomeState createState() => _HomeState();
  }

  class _HomeState extends State<Home> {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        body: SafeArea(
            child: Column(
              children: [
                FlatButton.icon(
                    onPressed: () {
                      Navigator.pushNamed(context, '/location');// use .pushNamed to navigate w/ name
                    },
                    icon: Icon(Icons.edit_location),
                    label: Text('edit location'))
              ],
            )
        ), // Move text widget to safe area (not behind status bar)
      );
    }
  }
  ```

  ``` dart
  //choose_location.dart
  import 'package:flutter/material.dart';

  class ChooseLocation extends StatefulWidget {
    @override
    _ChooseLocationState createState() => _ChooseLocationState();
  }

  class _ChooseLocationState extends State<ChooseLocation> {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        backgroundColor: Colors.grey[200],
        appBar: AppBar(
          backgroundColor: Colors.blue[900],
          title: Text('Choose location'),
          centerTitle: true,
          elevation: 0,
        ),
        body: Text('choose location screen'),
      );
    }
  }
  ```