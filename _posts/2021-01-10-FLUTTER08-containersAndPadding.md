---
layout: post
title: "Flutter 08: Creating Flutter app: Containers and padding"
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

## Creating Flutter app: Containers and padding

#### Container widget

- One of simplest __layout__ widgets that flutter offers.
- Wraps around other widgets
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
      body: Container(
        color: Colors.grey[900], // background color
        child: Text("Heloo"), // Container restrict it self to child widget

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
<img src="/assets/images/flutter/flutter013.PNG" width="30%" height="60%">  
- Container restrict it self to child widget  
<img src="/assets/images/flutter/flutter014.PNG" width="30%" height="60%">

- Padding and margin
  - Padding is __INSIDE__ Spacing
  - Margin is __OUTSIDE__ Spacing

- If you want padding to a `Container()` widget or to margin it, use padding property inside `Container()` widget.
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
      body: Container(
        // Padding is INSIDE Spacing
        //padding: EdgeInsets.all(20.0), // EdgeInsets control the spacing (padding and margin) inside Flutter
        //padding: EdgeInsets.symmetric(horizontal: 30.0, vertical: 10.0),
        padding: EdgeInsets.fromLTRB(10.0, 20.0, 30.0, 40.0),
        // Margin is OUTSIDE Spacing
        margin: EdgeInsets.all(30.0),
        color: Colors.grey[900], // background color
        child: Text("Heloo"), // Container restrict it self to child widget

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
<img src="/assets/images/flutter/flutter015.PNG" width="30%" height="60%">

- If you want padding a simple widget such as `Text()` widget, use Padding() widget.
> Padding() widget does not allow margin or color. It only takes padding itself.
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
      body: Padding( 
        padding: EdgeInsets.all(90.0),
        child: Text("Heloo"),
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
<img src="/assets/images/flutter/flutter016.PNG" width="30%" height="60%">
