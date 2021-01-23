---
layout: post
title: "Flutter 15: Widget cycles"
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

## Widget cycles

Stateless|Stateful|
---|---|
State doesn't change over time: every data inside must be constant | State CAN change over time|
Build function only runs once when it's created| setState() triggers the build function |

- Stateful widget

  - initState()
    - called only once when the widget is created
    - Subscribe to streams or any object that could change our widget data.|

  - Build()
    - Builds the widget tree
    - A build is triggered every time we use setState()

  - Dispose()
    - When the widget / state object is removed

``` dart
// choose_location.dart
import 'package:flutter/material.dart';

class ChooseLocation extends StatefulWidget {
  @override
  _ChooseLocationState createState() => _ChooseLocationState();
}

class _ChooseLocationState extends State<ChooseLocation> {

  int counter = 0;

  @override
  void initState() { // fires once when we load it
    super.initState();
    print('initState function ran');
  }



  @override
  Widget build(BuildContext context) { // fires every time we build
    print('build function ran');
    return Scaffold(
      backgroundColor: Colors.grey[200],
      appBar: AppBar(
        backgroundColor: Colors.blue[900],
        title: Text('Choose location'),
        centerTitle: true,
        elevation: 0,
      ),
      body: RaisedButton(
        onPressed: (){
          setState(() { // trigger build widget to update data on screen
            counter += 1;
          });
        },
        child: Text('counter is $counter'),
      )
    );
  }
}
```
