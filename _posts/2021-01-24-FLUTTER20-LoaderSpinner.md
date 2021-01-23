---
layout: post
title: "Flutter 20: Loader / Spinner"
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

## Loader / Spinner

<https://pub.dev/packages/flutter_spinkit/install>

``` dart
import 'package:flutter/material.dart';
import 'package:project02_world_time/services/world_time.dart';
import 'package:flutter_spinkit/flutter_spinkit.dart'; // Using spinner

class Loading extends StatefulWidget {
  @override
  _LoadingState createState() => _LoadingState();
}

class _LoadingState extends State<Loading> {

  void setupWorldTime() async {
    WorldTime instance = WorldTime(location: 'Seoul', flag: 'korea.png', url: 'Asia/Seoul');
    await instance.getTime(); // To use await for the custom function, we have to add 'Future<type>' keyword in front of getTime() function.
    Navigator.pushReplacementNamed(context, '/home', arguments: { // using arguments property to send data to /home route
      'location': instance.location,
      'flag': instance.flag,
      'time': instance.time,
    });
  }

  @override
  void initState() {
    super.initState();
    setupWorldTime();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.blue[900],
      body: Center(
        child: SpinKitRotatingCircle( // Using spinner
          color: Colors.white,
          size: 50.0,
        ),

      ),
    );
  }
}

```
