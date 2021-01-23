---
layout: post
title: "Flutter 13: Card class"
date: 2021-01-23
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

## Card class

- Creating a function that returns widget

``` dart
class _FriendsListsState extends State<FriendsLists> {
  List<Friend> friends = [
    Friend(name: 'sso', age: 22),
    Friend(name: 'tam2burin', age: 522),
    Friend(name: 'yoosona', age: 6),
  ];

  Widget friendTemplate(friend){
    return Card(
      margin: EdgeInsets.fromLTRB(16.0, 16.0, 16.0, 0.0),
      child: Padding(
        padding: const EdgeInsets.all(12.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: [
            Text(
              friend.name,
              style: TextStyle(
                fontSize: 18.0,
                color: Colors.grey[600],
              ),
            ),
            SizedBox(height: 5.0,),
            Text(
              friend.age,
              style: TextStyle(
                fontSize: 14.0,
                color: Colors.grey[800],
              ),
            ),
          ],
        ),
      ),
    );
  }

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
        children: friends.map((friend) => friendTemplate(friend)).toList(), // if you want to output var which requre property, must cover w/ curly braces
      ),
    );
  }
}
```

- Extracting Widgets

Flutter Outline -> right click on widget -> Extract widget
> This automatically makes stless widget

<img src = "/assets/images/flutter/flutter024.PNG" width="50%" height="50%">

``` dart
// main.dart

  Widget friendTemplate(friend){
    return FriendCard(friend);
  }


class FriendCard extends StatelessWidget {
  // const FriendCard({
  //   Key key,
  // }) : super(key: key);

  // Make a constructor
  final Friend friend; // `Final` set this var as final and declare that it's not gonna be changed over time, Thus, allow us to use in stless widget
  FriendCard({ this.friend});

  @override
  Widget build(BuildContext context) {
    ...

```

- Delete template widget and directly use stless widget inside map function

``` dart
// main.dart
class _FriendsListsState extends State<FriendsLists> {
  List<Friend> friends = [
    Friend(name: 'sso', age: 22),
    Friend(name: 'tam2burin', age: 522),
    Friend(name: 'yoosona', age: 6),
  ];

  // Delete
  //Widget friendTemplate(friend){
  //  return FriendCard(friend: friend);
  //}

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
        children: friends.map((friend) => FriendCard(friend: friend)).toList(),
      ),
    );
  }
}
```

- Save widget as separate file to make it re-usable for other files.

  - Create another dart file in lib directory and add import.

  ``` dart
  // friend_card.dart
  import 'package:flutter/material.dart';
  import 'package:flutter_app_learning_board/friend.dart';

  class FriendCard extends StatelessWidget {

    // const FriendCard({
    //   Key key,
    // }) : super(key: key);

    final Friend friend; // Final set this var as final and not gonna be changed later, Thus, allow us to use in stless widget
    FriendCard({ this.friend});


    @override
    Widget build(BuildContext context) {
      return Card(
        margin: EdgeInsets.fromLTRB(16.0, 16.0, 16.0, 0.0),
        child: Padding(
          padding: const EdgeInsets.all(12.0),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: [
              Text(
                friend.name,
                style: TextStyle(
                  fontSize: 18.0,
                  color: Colors.grey[600],
                ),
              ),
              SizedBox(height: 5.0,),
              Text(
                friend.age.toString(),
                style: TextStyle(
                  fontSize: 14.0,
                  color: Colors.grey[800],
                ),
              ),
            ],
          ),
        ),
      );
    }
  }
  ```

  - Add `import 'package:flutter_app_learning_board/friend_card.dart';` in `main.dart` to use it.

- Using function as paramter

  ``` dart
  // friend_card.dart
  import 'package:flutter/material.dart';
  import 'package:flutter_app_learning_board/friend.dart';

  class FriendCard extends StatelessWidget {
    final Friend friend;
    final Function delete; // Passing function as parameter
    FriendCard({ this.friend, this.delete});

    @override
    Widget build(BuildContext context) {
      return Card(
        margin: EdgeInsets.fromLTRB(16.0, 16.0, 16.0, 0.0),
        child: Padding(
          padding: const EdgeInsets.all(12.0),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: [
              Text(
                friend.name,
                style: TextStyle(
                  fontSize: 18.0,
                  color: Colors.grey[600],
                ),
              ),
              SizedBox(height: 5.0,),
              Text(
                friend.age.toString(),
                style: TextStyle(
                  fontSize: 14.0,
                  color: Colors.grey[800],
                ),
              ),
              SizedBox(height: 5.0,),
              // apply function
              FlatButton.icon(onPressed: delete, icon: Icon(Icons.delete), label: Text('delete')),
            ],
          ),
        ),
      );
    }
  }
  ```

  ``` dart
  // main.dart
  import 'package:flutter/material.dart';
  import 'package:flutter_app_learning_board/friend.dart';
  import 'package:flutter_app_learning_board/friend_card.dart';

  void main() => runApp(MaterialApp(
    home: FriendsLists(),
  ));

  class FriendsLists extends StatefulWidget {
    @override
    _FriendsListsState createState() => _FriendsListsState();
  }

  class _FriendsListsState extends State<FriendsLists> {
    List<Friend> friends = [
      Friend(name: 'sso', age: 22),
      Friend(name: 'tam2burin', age: 522),
      Friend(name: 'yoosona', age: 6),
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
          children: friends.map((friend) => FriendCard(
            friend: friend,
            delete: (){  // making function as parameter for the custom widget
              setState((){
                friends.remove(friend);
              });
            }
          )).toList(),
        ),
      );
    }
  }
  ```

