---
layout: post
title: "Flutter 06: Images"
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

## Images

#### Network image

NetworkImage("URL") : Use network image

1. Way 1
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
        child: Image.asset("assets/sso.jpg"),
          image: NetworkImage('https://upload.wikimedia.org/wikipedia/commons/b/b9/Caspar_David_Friedrich_-_Wanderer_above_the_sea_of_fog.jpg'), // Using network image
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

1. Way 2
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
        child: Image.network('https://upload.wikimedia.org/wikipedia/commons/b/b9/Caspar_David_Friedrich_-_Wanderer_above_the_sea_of_fog.jpg'),
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

#### Asset image

- AssetImage("dir") : Use asset image
  1. Create `assets` directory and put images files inside it.
  <img src="/assets/images/flutter/flutter010.PNG" width="100%" height="100%">  

  2. Edit `pubspec.yaml` to use assets
  > Every asset images should be declared inside the .yaml file in order to use it.
 
  <img src="/assets/images/flutter/flutter011.PNG" width="50%" height="50%">


1. Way 1
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
        child: Image(
          image: AssetImage("assets/sso.jpg"),
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

1. Way 2
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
        child: Image.asset("assets/sso2.jpg"),
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