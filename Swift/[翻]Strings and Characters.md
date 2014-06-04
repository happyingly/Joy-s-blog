###Strings and Characters

**String** 是一个有序的字符集合，例如 "hello, world", "albatross"。Swift 字符串通过 **String** 类型来表示，也可以表示为 **Character** 类型值的结合。

Swift 的 **String** 和 **Character** 类型提供了一个快速的，兼容 Unicode 的方式来处理代码中的文本信息。创建和操作字符串的语法与 C的操作方式相似，轻量并且易读。字符串连接操作只需要简单地通过 `+` 号将两个字符串相连即可。与 Swift 中其他值一样，是否可更改字符串的值，取决于其被定义为常量还是变量。

尽管语法简易，但 **String** 类型是一种快速、现代化的字符串实现。每一个字符串都是由独立编码的 Unicode 字符组成，并提供了在多种 Unicode 声明中访问这些字符的支持。

**String** 也可以用于在常量、变量、字面量和表达式中进行字符串插值，这使得创建用于展示、存储和打印的字符串变得轻松自如。

> 注意：
> 
> Swift 的 **String** 类型与 Foundation NSString 类进行了无缝桥接。如果您在利用 Cocoa 或 Cocoa Touch 中的 Foundation 框架进行工作，整个 NSString API 都可以调用您创建的任意 String 类型的值，您额外还可以在任意 API 中使用本章介绍的 **String** 特性。您也在任意要求传入NSString 实例作为参数的 API 中使用 **String** 类型的进行替换。
>
>更多关于在 Foundation 和 Cocoa 中使用 **String** 的信息请查看 [Using Swift with Cocoa and Objective-C](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/BuildingCocoaApps/index.html#//apple_ref/doc/uid/TP40014216)。

##### 字符串字面量

您可以在您的代码中包含一段预定义的字符串值作为字符串字面量。字符串字面量是由双引号包裹着的具有固定顺序的文本字符集。

字符串字面量可以用于为常量和变量提供初始值。

```
let someString = "Some string literal value"
```

**注意**：`someString` 变量通过字符串字面量进行初始化，Swift 因此推断其为 **String** 类型。

字符串字面量可以包含以下特殊字符：

*	转移特殊字符\0(空字符)、\\\\(反斜线)、\t(水平制表符)、\n(换行符)、\r(回车符)、\"(双引号)、\'(单引号)。
*	单字节 Unicode 标量，写成\xnn，其中 nn 为两位十六进制数。
*	双字节 Unicode 标量，写成\unnnn，其中 nnnn 为四位十六进制数。
*	四字节 Unicode 标量，写成\Unnnnnnnn，其中 nnnnnnnn 为八位十六进制数。

下面的代码为各种特殊字符的使用示例。

wiseWords 常量包含了两个转移特殊字符 - 双括号；dollarSign、blackHeart 和 sparklingHeart 常量演示了三种不同格式的 Unicode 标量：

```
let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
// "Imagination is more important than knowledge" - Einstein
let dollarSign = "\x24"        // $,  Unicode scalar U+0024
let blackHeart = "\u2665"      // ♥,  Unicode scalar U+2665
let sparklingHeart = "\U0001F496"  // 💖, Unicode scalar U+1F496
```

##### 初始化空字符串

为了构造一个很长的字符串，可以创建一个空字符串作为起点。可以将空的字符串字面量赋值给变量，也可以初始化一个新的 **String** 实例：

```
var emptyString = ""               // empty string literal
var anotherEmptyString = String()  // initializer syntax
// 这两个字符串都为空，并且两者等价
```

您可以通过检查其 **Boolean** 类型的 `isEmpty` 属性来判断该字符串是否为空：

```
if emptyString.isEmpty {
    println("Nothing to see here")
}
// 打印 "Nothing to see here"
```

##### 字符串可变性

您可以通过将一个特定字符串分配给一个变量来对其进行修改，或者分配给一个常量来保证其不会被修改：

```
var variableString = "Horse"
variableString += " and carriage"
// variableString 现在为 "Horse and carriage"
let constantString = "Highlander"
constantString += " and another Highlander"
// 这会报告一个编译错误(compile-time error) - 常量不可以被修改。
```

> 注意：
>
> 在 Objective-C 和 Cocoa 中，您通过选择两个不同的类( NSString 和 NSMutableString )来指定该字符串是否是否可以被修改，Swift中的则仅通过定义变量或者常量来决定，实现了多种类型可变性操作的统一。

##### 字符串是值类型

Swift 的 **String** 类型是值类型。如果您创建了一个新的字符串，那么当其进行常量、变量赋值操作或在函数/方法中传递时，会进行值拷贝。任何情况下，都会对已有字符串值创建新副本，并对该新副本进行传递或赋值。值类型在 [Structures and Enumerations Are Value Types](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/ClassesAndStructures.html#//apple_ref/doc/uid/TP40014097-CH13-XID_104) 中进行了说明。

> 注意：
>
> 其与 Cocoa 中的 NSString 不同，当您在 Cocoa 中创建了一个 NSString 实例，并将其传递给一个函数/方法，或者赋值给一个变量，您永远都是传递或赋值同一个 NSString 实例的一个引用。除非您特别要求其进行值拷贝，否则字符串不会进行赋值新副本操作。

Swift 默认字符串拷贝的方式保证了在函数/方法中传递的时字符串的值，其明确了无论该值来自于哪里，都是您独自拥有的。您可以放心您传递的字符串本身不会被更改。

在实际编译时，Swift编译器会优化字符串的使用，使实际的复制只发生在绝对必要的情况下，这意味着您始终可以将字符串作为值类型的同时获得极高的性能。

##### 使用字符(Characters)

Swift 的 **String** 类型表示特定序列的字符值的集合。每一个字符值代表一个 Unicode 字符。您可利用 for-in 循环来遍历字符串中的每一个字符：

```
for character in "Dog!🐶" {
    println(character)
}
// D
// o
// g
// !
// 🐶
```

for-in 循环在[For Loops](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/ControlFlow.html#//apple_ref/doc/uid/TP40014097-CH9-XID_154)中进行了详细描述。

另外，通过标明一个 **Character** 类型注解并通过字符字面量进行赋值，可以建立一个独立的字符常量或变量：

```
let yenSign: Character = "¥"
```

##### 计算字符数量

通过调用全局 `countElements` 函数并将字符串作为参数进行传递可以获取该字符串的字符数量。

```
let unusualMenagerie = "Koala 🐨, Snail 🐌, Penguin 🐧, Dromedary 🐪"
println("unusualMenagerie has \(countElements(unusualMenagerie)) characters")
// prints "unusualMenagerie has 40 characters"
```

>注意：
>
>不同的 Unicode 字符以及相同 Unicode 字符的不同表示方式可能需要不同数量的内存空间来存储，所以Swift 中的字符在一个字符串中并不一定占用相同的内存空间。因此，字符串的长度不得不通过迭代字符串中每一个字符的长度来进行计算。如果您正在处理一个长字符串，需要注意 `countElements` 函数必须遍历子妇产中的字符以精准计算字符串的长度。
>
>另外需要注意的是通过 `countElements` 返回的字符数量并不总是与包含相同字符的 NSString 的 `length` 属性相同。NSString 的 `length` 属性是基于利用utf-16表示的十六位代码单元数字，而不是基于 Unicode 字符。为了解决这个问题，NSString 的 `length` 属性在被 Swift的 **String** 访问时被成为 `utf16count`

##### Concatenating Strings and Characters

字符串和字符的值可以通过加法运算法 (+) 相加在一起并创建一个新的字符串值：

```
let string1 = "hello"
let string2 = " there"
let character1: Character = "!"
let character2: Character = "?"

let stringPlusCharacter = string1 + character1        // 等于 "hello!"
let stringPlusString = string1 + string2              // 等于 "hello there"
let characterPlusString = character1 + string1        // 等于 "!hello"
let characterPlusCharacter = character1 + character2  // 等于 "!?"
```

您也可以通过加法赋值运算符 (+=) 将一个字符串或者字符添加到一个已经存在字符串变量上：

```
var instruction = "look over"
instruction += string2
// instruction 现在等于 "look over there"

var welcome = "good morning"
welcome += character1
// welcome 现在等于 "good morning!"
```

>注意：
>
>您不能将一个字符串或者字符添加到一个已经存在的字符变量上，因为字符变量只能包含一个字符。

##### 字符串插值

字符串插值是一种全新的构建字符串的方式，可以在其中包含常量、变量、字面量和表达式。您插入的字符串字面量的每一项都被包裹在以反斜线为前缀的圆括号中：

```
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
// message is "3 times 2.5 is 7.5"
```

在上面的例子中，`multiplier` 作为 `\(multiplier)` 被插入到一个字符串字面量中。当创建字符串执行插值计算时此占位符会被替换为 `multiplier` 实际的值。

`multiplier` 的值也作为字符串中后面表达式的一部分。该表达式计算 `Double(multiplier) * 2.5` 的值并将结果 (7.5) 插入到字符串中。在这个例子中，表达式写为 `\(Double(multiplier) * 2.5)` 并包含在字符串字面量中。

>注意：
>
>您插值字符串中写在括号中的表达式不能包含非转义双引号 (") 和反斜杠 (\\)，并且不能包含回车或换行符。

##### 比较字符串

Swift 提供了三种方式来比较字符串的值：字符串相等，前缀相等和后缀相等。

###### 字符串相等

如果两个字符串以同一顺序包含完全相同的字符，则认为两者字符串相等：

```
let quotation = "We're a lot alike, you and I."
let sameQuotation = "We're a lot alike, you and I."
if quotation == sameQuotation {
    println("These two strings are considered equal")
}
// prints "These two strings are considered equal"
```

###### 前缀/后缀相等

通过调用字符串的 `hasPrefix`/`hasSuffix` 方法来检查字符串是否拥有特定前缀/后缀。两个方法均需要以字符串作为参数传入并传出 **Boolean** 值。两个方法均执行基本字符串和前缀/后缀字符串之间逐个字符的比较。

下面的例子以一个字符串数组表示莎士比亚话剧`罗密欧与朱丽叶`中前两场的场景位置：

```
let romeoAndJuliet = [
    "Act 1 Scene 1: Verona, A public place",
    "Act 1 Scene 2: Capulet's mansion",
    "Act 1 Scene 3: A room in Capulet's mansion",
    "Act 1 Scene 4: A street outside Capulet's mansion",
    "Act 1 Scene 5: The Great Hall in Capulet's mansion",
    "Act 2 Scene 1: Outside Capulet's mansion",
    "Act 2 Scene 2: Capulet's orchard",
    "Act 2 Scene 3: Outside Friar Lawrence's cell",
    "Act 2 Scene 4: A street in Verona",
    "Act 2 Scene 5: Capulet's mansion",
    "Act 2 Scene 6: Friar Lawrence's cell"
]
```

您可以利用 `hasPrefix` 方法来计算话剧中第一幕的场景数：

```
var act1SceneCount = 0
for scene in romeoAndJuliet {
    if scene.hasPrefix("Act 1 ") {
        ++act1SceneCount
    }
}
println("There are \(act1SceneCount) scenes in Act 1")
// prints "There are 5 scenes in Act 1"
```

###### 大写和小谢字符串

您可以通过字符串的 `uppercaseString` 和 `lowercaseString` 属性来访问一个字符串的大写/小写版本。

```
let normal = "Could you help me, please?"
let shouty = normal.uppercaseString
// shouty is equal to "COULD YOU HELP ME, PLEASE?"
let whispered = normal.lowercaseString
// whispered is equal to "could you help me, please?"
```







