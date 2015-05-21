# Hprose for Swift

[![Join the chat at https://gitter.im/hprose/hprose-swift](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/hprose/hprose-swift?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

*Hprose* is a High Performance Remote Object Service Engine.

It is a modern, lightweight, cross-language, cross-platform, object-oriented, high performance, remote dynamic communication middleware. It is not only easy to use, but powerful. You just need a little time to learn, then you can use it to easily construct cross language cross platform distributed application system.

*Hprose* supports many programming languages, for example:

* AAuto Quicker
* ActionScript
* ASP
* C++
* Dart
* Delphi/Free Pascal
* dotNET(C#, Visual Basic...)
* Golang
* Java
* JavaScript
* Node.js
* Objective-C/Swift
* Perl
* PHP
* Python
* Ruby
* ...

Through *Hprose*, You can conveniently and efficiently intercommunicate between those programming languages.

This project is the implementation of Hprose for Swift.

In fact, Swift can be using with Cocoa and Objective-C, so we don't need to
rewrite hprose in Swift again. We only need to use [Hprose for Objective-C](https://github.com/hprose/hprose-objc) in
Swift.

To use Hprose for Objective-C in Swift, you should to create a `Bridging-Header.h` like this:
```c
#ifndef BridgingHeader_h
#define BridgingHeader_h
#import "Hprose.h"
#endif
```

Then you can use hprose in Swift now. for example:

```swift
import Foundation

class User:NSObject {
    var name: String = ""
    var age: Int = 0
    var married: Bool = false
    var birthday: NSDate?
    var sex: Int = 0
}

@objc protocol Hello {
    func hello(name:String) -> String
    func sum(a:Int, b:Int, c:Int) -> Int
    func swapKeyAndValue(dict: [String: String]) -> [String: String]
    func getUserList() -> Array<User>;
}

HproseClassManager.registerClass(User.self, withAlias: "User")
var client = HproseHttpClient("http://www.hprose.com/example/index.php")
var h: AnyObject! = client.useService(Hello)
println(h.hello("world"))
println(h.hello("hprose"))
println(h.hello("中文"))
println(h.sum(1,b:2,c:3))
println(h.swapKeyAndValue([
    "January": "Jan",
    "February": "Feb",
    "March": "Mar",
    "April": "Apr"
]));
var sexStrings = ["Unknown", "Male", "Female", "InterSex"];
var users = h.getUserList();
for user in users {
    println(user.name)
    println(user.age)
    println(user.married)
    println(user.birthday)
    println(sexStrings[user.sex])
}
```

The full example is here: https://github.com/hprose/hprose-objc/tree/master/examples/swiftExam
