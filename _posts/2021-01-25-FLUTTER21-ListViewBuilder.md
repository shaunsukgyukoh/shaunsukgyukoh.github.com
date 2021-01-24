---
layout: post
title: "Flutter 21: List View Builder"
date: 2021-01-25
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

## List View Builder

``` dart
// choose_location.dart
import 'package:flutter/material.dart';
import 'package:project02_world_time/services/world_time.dart';

class ChooseLocation extends StatefulWidget {
  @override
  _ChooseLocationState createState() => _ChooseLocationState();
}

class _ChooseLocationState extends State<ChooseLocation> {

  List<WorldTime> locations = [
    WorldTime(location: 'Seoul', flag: 'korea.png', url: 'Asia/Seoul'),
    WorldTime(location: 'Tokyo', flag: 'japan.png', url: 'Asia/Tokyo'),
    WorldTime(location: 'Taipei', flag: 'taiwan.png', url: 'Asia/Taipei'),
    WorldTime(location: 'Hong Kong', flag: 'hongkong.png', url: 'Asia/Hong_Kong'),
    WorldTime(location: 'Shanghai', flag: 'china.png', url: 'Asia/Shanghai'),
    WorldTime(location: 'Moscow', flag: 'russia.png', url: 'Europe/Moscow'),
    WorldTime(location: 'Los Angeles', flag: 'usa.png', url: 'America/Los_Angeles'),
    WorldTime(location: 'New York / Ohio', flag: 'usa.png', url: 'America/New_York'),
    WorldTime(location: 'Chicago', flag: 'usa.png', url: 'America/Chicago'),
  ];

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
      body: ListView.builder(
        itemCount: locations.length,
        itemBuilder: (context, index) {
          return Padding(
            padding: const EdgeInsets.symmetric(vertical: 2, horizontal: 4),
            child: Card(
              child: ListTile(
                onTap: () {
                  print(locations[index].location);
                },
                title: Text(locations[index].location),
                leading: Image(
                  width: 50,
                  height: 50,
                  image: AssetImage('assets/images/${locations[index].flag}') // Make sure '/' is not in front of 'assets' in path
                ),
              ),
            ),
          );
        },
      )
    );
  }
}

```