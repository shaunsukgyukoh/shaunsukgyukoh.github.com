---
layout: post
title: "Flutter 12: Stateful widgets"
date: 2021-01-22
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

## Stateful widgets

- Recall that the stateful widget change the states over time: State obj saves the states.

`stful + tab` : Create custom stateless widget class

- To use variable -> use `"$varName"`

- Whenever you want to update the data inside Stateful widget, use `setState((){})`


``` dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: IdCard(),
  ));
}

class IdCard extends StatefulWidget {
  @override
  _IdCardState createState() => _IdCardState();
}

class _IdCardState extends State<IdCard> {

  int id_level = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.grey[900],
      appBar: AppBar(
        title: Text("ID card"),
        centerTitle: true,
        backgroundColor: Colors.grey[850],
        elevation: 0.0, // remove shadow
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: (){
          // id_level += 1; // This itself does not update the screen
          setState((){ // Need setState() to update the screen
            id_level += 1;
          });
        },
        child: Icon(Icons.add),
        backgroundColor: Colors.grey[850],
      ),
      body: Padding(
        padding: EdgeInsets.fromLTRB(30.0, 40.0, 30.0, 0.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              "Level",
              style: TextStyle(
                color: Colors.grey,
                letterSpacing: 2.0,
              ),
            ),
            SizedBox(height: 10.0),
            Text(
              "$id_level",
              style: TextStyle(
                color: Colors.amberAccent[200],
                letterSpacing: 2.0,
                fontSize: 28.0,
                fontWeight: FontWeight.bold,

              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

- Using list update

  - `List<String>` can be updated w/ `Column()` widget and `map()` method, where `map((parameter) {function})` method cycle through a list of data and apply functions to each data and returns __iterable__

``` dart
class _FriendsListsState extends State<FriendsLists> {
  List<String> friends = [
    'sso',
    'tam2burin',
    'yoosona',
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.grey[200],
      appBar: AppBar(
        title: Text("My friends"),
        centerTitle: true,
        backgroundColor: Colors.redAccent,
      ),
      body: Column(
        children: friends.map((name) => Text(name)).toList(),
      ),
    );
  }
}
```
  - If you want to associate another property to the lists (such as age, sex, .. ), it is better to create new class rather than declaring Lists for all the additional properties.

    - This modularization is also better design as the project gets larger.
    
    - Make another `.dart` file for new obj class in `lib` directory, and add `import 'package:flutter_app_learning_board/friend.dart';` in main.dart

    ``` dart
    class Friend {
      String name;
      int age;

      // // Way 1
      // Friend(String name, int age){ // Constructor
      //   this.name = name;
      //   this.age = age;
      // }

      // // Way 2: named parameter
      // Friend({String name, int age}){ // Constructor
      //   this.name = name;
      //   this.age = age;
      // }

      // Way 3: Simpler way 2
      Friend({this.name, this.age});

    }
    /*
    // making new Friend obj.
    Friend myFriend = Friend("Hi", 21);

    // another way to assign values: named parameter: param order does not matter
    Friend myFriend = Friend(name: "Hi", age: 21);
    */
    ```