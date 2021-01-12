---
layout: post
title: "Flutter 02: Dart"
date: 2021-01-08
categories:
  - Flutter
tags:
  - language
  - dart
author_profile: true
read_time: true
comments: true
share: true
related: true
popular: true
toc: true
toc_sticky: true
toc_label: 목차
article_tag1: language
article_tag2: dart
article_section: Flutter
meta_keywords: flutter, dart, language
published: true
---

## Dart

- Flutter uses Dart developed by Google.
- Dart is statically typed language : when var declared, can't change type afterward.

``` dart
void main() {
  int age = 30; // Variable declaration and assignment
  String name = greeting(); // Using Function
  print(name); // Printing
  name = "chun-kim";
  print(name); // Can change value if type is same
  bool isNight = false;
  name = greetingArrow(); // Using arrow function
  print(name);
  
  
  dynamic name2 = "Ken"; // Dynamic type is available but not recommended in order to reduce error. Use it only when you need to do it
  print(name2);
  name2 = 23;
  print(name2); // Check automatic type change
  
  List names = ["lew", "ken", "mario"]; // Using array list like python
  print(names);
  names.add("luigi"); // .remove is also available
  print(names);
  names.add(30); // Adding different type does not give an error : but not a good practice
  print(names);
  List<String> namesType = ["yohi", "brian", "kazuya"]; // Type specification is a good practice: only String can be element
  print(namesType);
  // namesType.add(30); // error
  
  User user1 = User(); // create user object.
  print(user1.username);
  user1.login();
  
  User user2 = User(); // create user2 object.
  print(user2.username); // give same name since we define it in class --> need constructor
  
  User2 user3 = User2("Hwarang", 20); // obj. w/ constructor
  print(user3.username);
  print(user3.age);
  
  SuperUser su = SuperUser("Jin", 20);
  print(su.username);
  su.publish();
}

String greeting() {
  return "hello";
}

// Dart support arrow functions
String greetingArrow() => "helloArrow";

// Class is a blueprint of an object like any other languages
class User { // Naming convention: uppercase for first letter 
  
  // Properties
  String username = "mario";
  int age = 25;
  
  // Methods
  void login(){
    print("user logged in");
  }
} // This is just a blueprint: does not create obj

class User2 {
  String username;
  int age;
  
  // Constructor: special function that runs when we instantiate a class
  User2(String username, int age){ // parameter name can be anything (e.g. String u, int a)
    this.username = username;
    this.age = age;
  }
  
  void login(){
    print("user logged in");
  }
}

// Inheritance is when we have a class that inherits from another class
class SuperUser extends User2{ // Inherit from user and extend more methods
  SuperUser(String username, int age) : super(username, age); // super() calls constructor in User2 class
  
  // Can add more methods
  void publish(){
    print("published update");
  }
}

```

Referece: <https://www.youtube.com/watch?v=1ukSR1GRtMU&list=PL4cUxeGkcC9jLYyp2Aoh6hcWuxFDX6PBJ>