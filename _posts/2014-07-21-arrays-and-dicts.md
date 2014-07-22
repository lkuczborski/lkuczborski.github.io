---
layout: post
title: Arrays and Dictionaries with various value types in Swift
description: Xcode 6 Beta 3 brought some changes to sugar syntax for declaring Arrays and Dictionaries. Here is how you can now create an Array with different value types...
comments: true
---

Xcode 6 Beta 3 brought some changes to sugar syntax for declaring Arrays and Dictionaries.

Here is how you can now create an Array with different value types:

```swift
/* Create an Array with different value types */
var arr: [Any] = ["aString", 1.23, true]
```

And here is the same for Dictionary:

```swift
/* Create a Dictionary with different value types */
var dict: [String:Any] = ["key1":"aString", "key2":1.23, "key3":true]
```
