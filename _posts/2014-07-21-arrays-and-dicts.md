---
layout: post
title: Arrays and Dictionaries with various value types in Swift
comments: true
---

Xcode 6 Beta 3 brought some changes to sugar syntax for declaring Arrays and Dictionaries.

Here is how you can now create an Array with different value types:
{% highlight swift %}
var arr: [Any] = ["aString", 1, 1.23, true]
{% endhighlight %}

And here is the same for Dictionary:
{% highlight swift %}
var dict: [String:Any] = ["key1":aString", "key2":"1", "key3":1.23]
{% endhighlight %}
