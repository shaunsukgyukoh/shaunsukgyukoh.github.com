---
layout: post
title: "Flutter 16: Flutter Package (http) and using API"
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

## Flutter Package (http)

Allow easier handling on http request to 3rd party APIs.

packages can be found in [pub.dev](https://pub.dev/) and each package has installation guide. Simlpy adding dependecies in `pubspec.yaml` will do the install

Dummy data cab be generated w/ [{JSON} Placeholder](https://jsonplaceholder.typicode.com/)

``` dart
// loading.dart
import 'package:flutter/material.dart';
import 'package:http/http.dart';
import 'dart:convert'; // To use jsonDecode() function

class Loading extends StatefulWidget {
  @override
  _LoadingState createState() => _LoadingState();
}

class _LoadingState extends State<Loading> {
  void getData() async {

    Response response = await get('https://jsonplaceholder.typicode.com/todos/1'); // using http package's get function where Response type is provided in http package as well.
    // print(response.body); // returns String looks like map
    /*
    I/flutter (17044): {
    I/flutter (17044):   "userId": 1,
    I/flutter (17044):   "id": 1,
    I/flutter (17044):   "title": "delectus aut autem",
    I/flutter (17044):   "completed": false
    I/flutter (17044): }
    */

    Map data = jsonDecode(response.body);
    print(data); // I/flutter (17044): {userId: 1, id: 1, title: delectus aut autem, completed: false}
    print(data['userId']); // 1
  }

  @override
  void initState() {
    super.initState();
    getData();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Text('loading screen'),
    );
  }
}
```

## Using [World time API](http://worldtimeapi.org/)

  - Canonical Timezone List -> select -> choose json 
  > http://worldtimeapi.org/api/timezone/Asia/Seoul

  - Address is used for `get()` and the response is as shown in above link

    ``` dart
    import 'package:flutter/material.dart';
    import 'package:http/http.dart';
    import 'dart:convert'; // To use jsonDecode() function

    class Loading extends StatefulWidget {
    @override
    _LoadingState createState() => _LoadingState();
    }

    class _LoadingState extends State<Loading> {
        void getTime() async {
            // make the request
            Response response = await get('http://worldtimeapi.org/api/timezone/Asia/Seoul');
            Map data = jsonDecode(response.body);
            // print(data);

            // get properties from data
            String datetime = data['datetime'];
            String offset = data['utc_offset'].substring(1,3); // substring to parse desired digits
            //print(datetime);
            //print(offset);

            // create DateTime obj.
            DateTime now = DateTime.parse(datetime);
            now = now.add(Duration(hours: int.parse(offset))); // .add method is non-destructive: need another assignment; int.parse() convert String to Int
            print(now);

        }

        @override
        void initState() {
            super.initState();
            getTime();
        }

        @override
        Widget build(BuildContext context) {
            return Scaffold(
            body: Text('loading screen'),
            );
        }
    }
    ```

  - Make World time custom class for better re-usablility
    - Can be imported into any file or widget that need to use it in the future.

``` dart
// loading.dart
import 'package:flutter/material.dart';
import 'package:project02_world_time/services/world_time.dart';

class Loading extends StatefulWidget {
  @override
  _LoadingState createState() => _LoadingState();
}

class _LoadingState extends State<Loading> {

  String time = 'loading';

  void setupWorldTime() async {
    WorldTime instance = WorldTime(location: 'Seoul', flag: 'korea.png', url: 'Asia/Seoul');
    await instance.getTime(); // To use await for the custom function, we have to add 'Future<type>' keyword in front of getTime() function.
    print(instance.time);
    setState(() {
      time = instance.time;
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
        child: Text(time),
      ),
    );
  }
}
```

``` dart
// world_time.dart
import 'package:http/http.dart';
import 'dart:convert';

class WorldTime {

  String location; // location name for the UI
  String time; // time in that location
  String flag; // url to an asset flag icon
  String url; // location url for API endpoint

  WorldTime({ this.location, this.flag, this.url});

  Future<void> getTime() async {
    // make the request
    Response response = await get('http://worldtimeapi.org/api/timezone/$url');
    Map data = jsonDecode(response.body);
    // print(data);

    // get properties from data
    String datetime = data['datetime'];
    String offset = data['utc_offset'].substring(1,3); // substring to parse desired digits
    //print(datetime);
    //print(offset);

    // create DateTime obj.
    DateTime now = DateTime.parse(datetime);
    now = now.add(Duration(hours: int.parse(offset))); // .add method is non-destructive: need another assignment; int.parse() convert String to Int

    time = now.toString(); // set the time property


  }
}

// Example of creating new instance
// WorldTime instance = WorldTime(location: 'Seoul', flag: 'korea.png', url: 'Asia/Seoul');
// instance.getTime();
```