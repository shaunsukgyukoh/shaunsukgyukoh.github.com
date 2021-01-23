---
layout: post
title: "Flutter 10: Creating Flutter app: Shortcuts and outlines"
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

## Creating Flutter app: Shortcuts and outlines


- If you want to edit widgets (such as swapping two widget), copy and paste is cumbersome.

#### Shortcuts

- When you click a widget, a lightburb will appear --> This is __Action menu__ for this widget.
  - shortcut: `alt`+`enter`
- If the lightbulb does not show up, try to make space (press enter) right above the widget.

<img src="/assets/images/flutter/flutter019.PNG" width="100%" height="100%">


- Wrap with widget example
<img src="/assets/images/flutter/flutter020.PNG" width="100%" height="80%">  

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
      body: Column(
        mainAxisAlignment: MainAxisAlignment.end, // Must be in Row widget: not inside of any other widgets
        crossAxisAlignment: CrossAxisAlignment.end,
        children: <Widget>[
          Row( // Row takes full width of the column: therefore, it is on the top of rest of container.
            children: [
              Text("Hello,"),
              Text(" world"),
              Container(
                color: Colors.pinkAccent,
                padding: EdgeInsets.all(10.0),
                child: Text("zero"),
              ),
            ],
          ),
          Container( // Edit name of widget you want to use
            child: Padding(
              padding: const EdgeInsets.all(8.0),
              child: Container(
                color: Colors.red,
                padding: EdgeInsets.all(30.0),
                child: Padding(
                  padding: const EdgeInsets.all(16.0),
                  child: Text("two"),
                ),
              ),
            ),
          ),
          Container(
            color: Colors.cyan,
            padding: EdgeInsets.all(20.0),
            child: Text("one"),
          ),
          Container(
            color: Colors.purple,
            padding: EdgeInsets.all(40.0),
            child: Text("three"),
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

#### Outlines

- When you do not see any outlines, Click on any widget while pressing `ctrl`. This will activate outline.
<img src="/assets/images/flutter/flutter021.PNG" width="100%" height="80%">  

- Simply right click to use same function as shortcut.
- Buttons above are also useful.