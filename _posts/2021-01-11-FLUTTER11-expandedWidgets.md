---
layout: post
title: "Flutter 11: Expanded widgets"
date: 2021-01-11
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

## Expanded widgets

- If you want to use as much as space available (leftover) to the widgets, use `Expanded()` widget. Simply use shorcut or outline to wrap a widget and edit the name to `Expanded` will do.

<img src="/assets/images/flutter/flutter022.PNG" width="100%" height="80%">  
<img src="/assets/images/flutter/flutter023.PNG" width="100%" height="80%">  

- `Expanded()` widgets can have `flex:` property (portion of width that we want to associate with this `Expanded()` widget)

- `Expanded()` widget is also useful for containing images within the boundaries of screen.

``` dart
class Home extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Hello Shaun!"),
        centerTitle: true,
        backgroundColor: Colors.cyan[300],
      ),
      body: Row(
        children: <Widget>[
          Expanded( // Contain child images
            flex: 4,
            child: Image.asset('assets/sso.jpg'),
          ), // Too large -> Wrap over rest of the widgets
          Expanded( // Fill the space
            flex: 3, // Portion of space
            child: Container(
              padding: EdgeInsets.all(30.0),
              color: Colors.pinkAccent[200],
              child: Text('2'),
            ),
          ),
          Expanded(
            flex: 2,
            child: Container(
              padding: EdgeInsets.all(30.0),
              color: Colors.cyan[200],
              child: Text('1'),
            ),
          ),
          Expanded(
            flex: 1,
            child: Container(
              padding: EdgeInsets.all(30.0),
              color: Colors.amberAccent[200],
              child: Text('3'),
            ),
          ),
        ],
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