---
layout: post
title: "Flutter 16: Asynchronous code"
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

## Asynchronous code

- Async: starts now and finishes some time in future
- Asynchronous code must be non-blocking
  - while the request has been made, rest of the code could carry-on

``` dart
class _ChooseLocationState extends State<ChooseLocation> {

int counter = 0;
void getData() async { // using async function

    // simulate network request for a username
    String username = await Future.delayed(Duration(seconds: 3), () { // use await keyword to wait till finish
    return 'sso';
    });

    // simulate network request to get bio of the username
    String bio = await Future.delayed(Duration(seconds: 2), () { // bio depends on username --> use await to do it
    return 'Afreeca BJ and youtuber';
    });

    print('$username - $bio');
}

@override
void initState() { // fires once when we load it
    super.initState();
    getData();
    print('initState function ran');
}



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
    body: RaisedButton(
        onPressed: (){
        setState(() { // trigger build widget to update data on screen
            counter += 1;
        });
        },
        child: Text('counter is $counter'),
    )
    );
}
}
```