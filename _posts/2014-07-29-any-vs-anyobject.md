---
layout: post
title: Any vs. AnyObject
description: Two special type aliases for working with non-specific types in Swift
comments: true
---

Swift provides two special type aliases for working with non-specific types:

- ```AnyObject``` can represent an instance of any class type.
- ```Any``` can represent an instance of any type at all, apart from function types.

<!--more-->

Let's assume we have ```Movie``` class...

```swift
class Movie {
    let title: String
    init(_ title: String) {
        self.title = title;
    }
    func simpleDescription() -> String {
        return "Title: \"\(title)\"."
    }
}
```

There is one interesting thing in the above example – the ```_``` sign:	

- **We can use ```_``` sign when we want to omit providing parameter name in ```init``` method.** 

	In this case we can create ```Movie``` object like this...

	```swift
	Movie("Forrest Gump")
	```

	...instead of

	```swift
	Movie(title: "Forrest Gump")
	```

If we would like to create an array holding ```Movie``` instances and also some other class type instances, we can do it like this:

```swift
var anyObjectThings = [AnyObject]()
```

As we want to hold only class instances we don't have to use [Any] type alias.

-

We than append new ```Movie``` object to the array like this: 

```swift
anyObjectThings.append(Movie("Forrest Gump"))

println((anyObjectThings[0] as Movie).simpleDescription()) 
// returns "Title: "Forrest Gump"."
```

We use [Any] when we want to support more than just class types, for eg.:

```swift
var anyThings = [Any]()

anyThings.append(42)
anyThings.append(3.14159)
anyThings.append("hello")
anyThings.append((3.0, 5.0))
anyThings.append(Movie("Godzilla"))
```
Also see my previous blog post on creating Arrays and Dictionaries with various value types [here](/2014/07/21/arrays-and-dicts).

**Apple warns to use ```Any``` and ```AnyObject``` only when you explicitly need the behavior and capabilities they provide.** It is always better to be specific about the types you expect to work with in your code.

There are however cases when you will have to use this type aliases for eg. when working with Cocoa APIs, it is common to receive an array with a type of ```[AnyObject]```, or "an array of values of any object type". This is because Objective-C does not have explicitly typed arrays like Swift does.