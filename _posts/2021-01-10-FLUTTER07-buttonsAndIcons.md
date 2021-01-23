---
layout: post
title: "Flutter 07: Buttons and icons"
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

## Buttons and icons

#### Icons

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
      body: Center(
        child: Icon(
          Icons.airport_shuttle,
          color: Colors.lightBlue,
          size: 50.0,
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

#### Buttons

<img src="/assets/images/flutter/flutter012.PNG" width="30%" height="60%">

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
      body: Center(
        child: RaisedButton( // Shows shadow that it's raised from the background
          // FlatButton is also available
          onPressed: () {
            print("Hi. I'm mee6!");
          }, // onPressed takes function as a value: Action when button is pressed
          child: Text("Click me"), // Child is used when you nest properties
          color: Colors.green[300],
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

#### Button with icon

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
      body: Center(
        child: RaisedButton.icon(
          onPressed: () {
            print("Hi. I'm mee6!");
          }, // onPressed takes function as a value: Action when button is pressed
          icon: Icon(
            Icons.mail,
          ),
          label: Text("Mail me"),
          color: Colors.amber[300],
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

#### Icon button

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
      body: Center(
        child: IconButton(
          onPressed: () {
            print("Hi. I'm mee6!");
          },
          icon: Icon(
            Icons.alternate_email, // @
          ),
          color: Colors.blue[300],
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