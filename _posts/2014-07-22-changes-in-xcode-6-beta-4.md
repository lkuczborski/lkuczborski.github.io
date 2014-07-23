---
layout: post
title: Changes in Xcode 6 Beta 4
description: Most important Swift related changes introduced in Xcode 6 Beta 4...
comments: true
---

Xcode 6 Beta 4 brought some important changes related to constantly evolving Swift Language. Below is a compilation of the most important ones.

<!--more-->

## Summary of changes

### Access Control

#### Access levels

- ``` private ```

  Can only be accessed from within the source file where they are defined.

- ``` internal ```

  Can be accessed anywhere within the target where they are defined.

- ``` public ```

  Can be accessed from anywhere within the target and from any other context that imports the current target’s module.

#### Things to remember

- Frameworks need the public API marked as public

- Implicitly-synthesized initializers for classes and structs are internal by default

- Generated header
  - contains only **public** declarations for **Frameworks**
  - contains both **public and internal** declarations for **Applications**

      ```swift
      // An example class in a framework target.
      public class ListItem: NSObject {
          public var text: String
          public var isComplete: Bool
          // Readable throughout the module, but only writeable from
          // within this file.
          private(set) var UUID: NSUUID
          public init(text: String, completed: Bool, UUID: NSUUID) {
              self.text = text
              self.isComplete = completed
              self.UUID = UUID
          }
          func refreshIdentity() {
              self.UUID = NSUUID()
          }
              // Must be public because it overrides a public method
          	  // and is itself part of a public type.
              public override func isEqual(object: AnyObject?) -> Bool {
                  if let item = object as? ListItem {
                      return self.UUID == item.UUID
              }
              return false
          }
      }
      ```

- Declarations marked private are not exposed to the Objective-C runtime if not otherwise annotated.

  -  If you need a private method or property to be callable from Objective-C, you have to add
the ``` @objc ``` attribute to the declaration explicitly.

#### Limitations

- Unit tests cannot interact with the classes and methods in an application unless they are marked public (unit test target is not part of the application module)

---

### .by() -> stride()

The .by() method for ranges has been replaced with general stride() functions.

#### Usage
- for **exlusive** ranges:

  ``` stride(from: to: by:) ```

- for **inclusive** ranges:

  ``` stride(from: through: by:) ```

#### Examples
```swift
stride(from: x, to: y, by: z)           //was: (x..<y).by(z)
stride(from: x, through: y, by: z)      //was: (x...y).by(z)
```

---

## Unicode String improvements
The ``` String ``` type now implements a grapheme cluster segmentation algorithm to
produce Characters. This means that iteration over complex strings that include combining marks, variation sequences, and regional indicators work properly.

```swift
// returns 15
countElements("a\u{1F30D}cafe\u{0301}umbrella\u{FE0E} \u{1F1E9}\u{1F1EA}”)
```

A ``` for-in ``` loop over the string produces each human visible character in sequence.

---

## Revised Declaration Modifiers
The ``` @final ```, ``` @lazy ```, ```@optional ```, and ``` @required ``` attributes have been converted to declaration modifiers, specified without an ``` @ ``` sign.

- ``` @final ``` -> ``` final ```

- ``` @lazy ``` -> ``` lazy ```

- ``` @optional ``` -> ``` optional ```

- ``` @required ``` -> ``` required ```

---

## Landmarks
Finally! Xcode now supports ``` //MARK: ```, ``` //TODO: ``` and ``` //FIXME ``` landmarks to annotate your code and
lists them in the jump bar.

---

Let me know if you think I missed something important and feel free to comment below!
