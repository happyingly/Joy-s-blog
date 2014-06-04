###Strings and Characters

**String** 是一个有序的字符集合，例如 "hello, world", "albatross"。Swift 字符串通过 **String** 类型来表示，也可以表示为 **Character** 类型值的结合。

Swift 的 **String** 和 **Character** 类型提供了一个快速的，兼容 Unicode 的方式来处理代码中的文本信息。创建和操作字符串的语法与 C的操作方式相似，轻量并且易读。字符串连接操作只需要简单地通过 `+` 号将两个字符串相连即可。与 Swift 中其他值一样，是否可更改字符串的值，取决于其被定义为常量还是变量。

尽管语法简易，但 **String** 类型是一种快速、现代化的字符串实现。每一个字符串都是由独立编码的 Unicode 字符组成，并提供了在多种 Unicode 声明中访问这些字符的支持。

**String** 也可以用于在常量、变量、文字和表达式中进行字符串插值，这使得创建用于展示、存储和打印的字符串变得轻松自如。

> 注意：
> Swift 的 **String** 类型与 Foundation NSString 类进行了无缝桥接。如果您在利用 Cocoa 或 Cocoa Touch 中的 Foundation 框架进行工作，整个 NSString API 都可以调用您创建的任意 String 类型的值，您额外还可以在任意 API 中使用本章介绍的 **String** 特性。您也在任意要求传入NSString 实例作为参数的 API 中使用 **String** 类型的进行替换。
>
>更多关于在 Foundation 和 Cocoa 中使用 **String** 的信息请查看 [Using Swift with Cocoa and Objective-C](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/BuildingCocoaApps/index.html#//apple_ref/doc/uid/TP40014216)。
