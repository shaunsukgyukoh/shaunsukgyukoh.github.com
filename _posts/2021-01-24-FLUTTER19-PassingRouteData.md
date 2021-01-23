---
layout: post
title: "Flutter 19: Passing Route Data"
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

## Passing Route Data

Use 3rd parameter `arguments :{}` in Navigator obj's push method.

``` dart
// loading.dart
import 'package:flutter/material.dart';
import 'package:project02_world_time/services/world_time.dart';

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
      body: Padding(
        padding: EdgeInsets.all(50.0),
        child: Text('loading'),
      ),
    );
  }
}
```
``` dart
// home.dart
import 'package:flutter/material.dart';

class Home extends StatefulWidget {
  @override
  _HomeState createState() => _HomeState();
}

class _HomeState extends State<Home> {

  Map data = {};

  @override
  Widget build(BuildContext context) {

    data = ModalRoute.of(context).settings.arguments;// recieve data

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

- Formatting

``` dart
// home.dart
import 'package:flutter/material.dart';

class Home extends StatefulWidget {
  @override
  _HomeState createState() => _HomeState();
}

class _HomeState extends State<Home> {

  Map data = {};

  @override
  Widget build(BuildContext context) {

    data = ModalRoute.of(context).settings.arguments;// recieve data
    print(data);

    return Scaffold(
      body: SafeArea(
          child: Padding(
            padding: const EdgeInsets.fromLTRB(0, 120.0, 0, 0),
            child: Column(
              children: [
                FlatButton.icon(
                    onPressed: () {
                      Navigator.pushNamed(context, '/location');// use .pushNamed to navigate w/ name
                    },
                    icon: Icon(Icons.edit_location),
                    label: Text('edit location')
                ),
                SizedBox(height: 19.0),
                Row(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: [
                    Text(
                      data['location'],
                      style: TextStyle(
                        fontSize: 28.0,
                        letterSpacing: 2.0,
                      ),
                    ),
                  ],
                ),
                SizedBox(height: 19.0),
                Text(
                  data['time'],
                  style: TextStyle(
                    fontSize: 66,
                  ),
                ),
              ],
            ),
          )
      ), // Move text widget to safe area (not behind status bar)
    );
  }
}
```
``` dart
// world_time.dart
import 'dart:math';

import 'package:http/http.dart';
import 'dart:convert';
import 'package:intl/intl.dart'; // Used for formatting datetime

class WorldTime {

  String location; // location name for the UI
  String time; // time in that location
  String flag; // url to an asset flag icon
  String url; // location url for API endpoint

  WorldTime({ this.location, this.flag, this.url});

  Future<void> getTime() async {

    try {
      // make the request
      Response response = await get('http://worldtimeapi.org/api/timezone/$url'); // add 's' to timezone to simulate error
      Map data = jsonDecode(response.body);

      // get properties from data
      String datetime = data['datetime'];
      String offset = data['utc_offset'].substring(1,3);

      // create DateTime obj.
      DateTime now = DateTime.parse(datetime);
      now = now.add(Duration(hours: int.parse(offset)));

      time = DateFormat.jm().format(now); // Widget provided by intl package
    }catch(e){
      print('caught error: $e');
      time = 'could not get time data';
    }
  }
}
```