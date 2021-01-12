---
layout: post
title: "Flutter 09: Creating Flutter app: Rows and Columns"
date: 2021-01-10
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

## Creating Flutter app: Rows and Columns

Expand our layout: Create multiple widgets on page at once.

#### Rows

- Row have `children` property (not `child`).
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
          Text("Hello world"), // Each widgets are comma separated as usual
          FlatButton(
            onPressed: () {},
            color: Colors.amber,
            child: Text("Click"),
          ),
          Container(
            color: Colors.cyan,
            padding: EdgeInsets.all(30.0),
            child: Text("inside container"),
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
<img src="/assets/images/flutter/flutter017.PNG" width="50%" height="100%">

- Spacing  
<img src="https://www.oreilly.com/library/view/mastering-css/9781787281585/assets/a44451c0-7a19-46bd-aa19-aff2e1c78239.jpg" width="50%" height="50%">  
Reference: <https://www.oreilly.com/library/view/mastering-css/9781787281585/e13a0b13-1d1b-4ace-aa36-ea7c18442213.xhtml>
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
        mainAxisAlignment: MainAxisAlignment.spaceEvenly, // Must be in Row widget: not inside of any other widgets
        crossAxisAlignment: CrossAxisAlignment.start, // Must be in Row widget: not inside of any other widgets
        children: <Widget>[
          Text("Hello world"), // Each widgets are comma separated as usual
          FlatButton(
            onPressed: () {},
            color: Colors.amber,
            child: Text("Click"),
          ),
          Container(
            color: Colors.cyan,
            padding: EdgeInsets.all(30.0),
            child: Text("inside container"),
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

#### Columns

- Main axis and cross axis are swapped from row's axis. i.e., Main becomes vertical and cross becomes horizontal.

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
        crossAxisAlignment: CrossAxisAlignment.stretch,
        children: <Widget>[
          Container(
            color: Colors.cyan,
            padding: EdgeInsets.all(20.0),
            child: Text("one"),
          ),
          Container(
            color: Colors.red,
            padding: EdgeInsets.all(30.0),
            child: Text("two"),
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

- Row and column can be nested.

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
          Container(
            color: Colors.cyan,
            padding: EdgeInsets.all(20.0),
            child: Text("one"),
          ),
          Container(
            color: Colors.red,
            padding: EdgeInsets.all(30.0),
            child: Text("two"),
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
<img src="/assets/images/flutter/flutter018.PNG" width="50%" height="100%">