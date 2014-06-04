###Swift语法(一)语法基础

Swift是一个为iOS和OS X应用开发而产生的新编程语言,尽管如此，如果你有C和Objective-C上的开发经验，用起Swift来应该会感觉很熟悉

Swift自定义了一套对应C和Objective-C的基础类型，其中包括`Int`(对应整型)，`Double`和`Float`(对应浮点型)，`Bool`（对应布尔值）,‘String’(对应文本数据),还提供了数组和字典的对应类型，关于Swift中的数组和字典，将在后续的`集合类型`中详述

同C一样, Swift使用变量来存储和引用值，也大范围使用常量，Swift中的常量比C中的常量更加安全和整洁。

除了相似的类型，Swift还有几种Objective-C中不存在的高级类型,如元组（创建和传递成组数据,作为函数的返回值返回，注：返回的是一个元组，但是其中可以存多个数据）

Swift还拥有可选类型，可以处理数据缺失的情况（译者注：譬如网络请求的时候返回了空值）,可选值表示的意思是`我不能保证我有值，且值是XXX`可选值的概念类似于Objective-C中使用nil,但是这个可以用于任何类型，不仅仅是类。Swift中的可选值比Objective-C中的nil更加安全也更加生动，也更加触及Swift的核心功能。

可选值概念充分体现了Swift是一个类型安全的语言。Swift帮助开发者理清代码中能够工作的值的类型。如果你有个变量是一个`String`，可选值能保护代码免于因为传入`Int`而报错。也能够帮助开发者在开发阶段尽早的捕获和修复错误。

###常量和变量
常量和变量把常量(变量)名称(例如`maximumNumberOfLoginAttempts`或`welcomeMessage`)和某个类型的值(例如数字`10`或者字符串`"Hello"`)联系在一起。常量的值设置后不能改变，变量就可以随便变。

#####常量和变量的声明
常量和变量在使用前必须声明。

声明常量用关键字`let`，声明变量用关键字`var`
	
	let maximumNumberOfLoginAttempts = 10
	var currentLoginAttempt = 0

上述代码的意思是：
	
	声明一个叫做maximumNumberOfLoginAttempts的新常量，给它赋值10
	声明一个叫做currentLoginAttempt的新变量，赋值0

在上述例子中，被允许的最大登录重试数被声明为一个常量，因为最大值不能改变。但是当前登录重试数被声明为一个变量，因为这个数值会随着登录失败开始重试而增加。

你可以在一行中声明多个常量或变量，如下
	
	var x = 0.0, y = 0.0, z = 0.0

如果程序中有一个值`过去，现在，将来`都不会改变，就把它声明成常量吧，把需要改变的数才声明称变量。

#####指定类型声明
当声明一个常量或变量时，可以指定声明某个类型，以便于清晰的表述常量或变量中值的类型。

在常量和变量的后面加一个`:` 再加上这个常量或变量想存储的值的类型。

下面的例子声明了一个叫`welcomeMessage`的变量并指明这个变量存储的是`String`类型
	
	var welcomeMessage: String

这个`welcomeMessage`变量现在可以存储任何字符串值而不会报错了

	welcomeMessage = "Hello"
	
注:练习中需要声明变量类型的情况很少见，如果为一个常量或变量赋初值，Swift将推断这个变量或常量使用的是初值的类型，详情请见`类型安全和类型推断`

在上面的例子中，没有提供初始值，但是`welcomeMessage`变量被事先声明了类型，系统也将从中推断出类型。

#####为常量和变量取名
你可以为常量和变量取各式各样的名字，几乎涵盖所有字符，包括如下的

	let π = 3.14159
	let 你好 = “你好世界”
	let 🐶🐮 = “dogcow”

但是名字里不能包括`数学符号` `箭头` `私用(或非法)Unicode编码` `描线或描框字符` 
也不能以`数字`开头，包含数字是允许的

一旦声明了一个变量或常量（已经声明类型），就不能用同样的名字再次声明它(或改变成别的类型)，也不允许变量改成常量，常量改成变量。

注：如果需要让常量和变量使用保留关键字做名字，可以用```包围这个关键字，就可以做名字来使用，但是不推荐不提倡这么做

可以用兼容的类型来给已知的变量赋值。如下，`friendlyWelcome`的值从`Hello`变为`Bonjour`

	var friendlyWelcome = "Hello"
	friendlyWelcome = "Bonjour"

不像变量，常量一旦赋值就不能改变。尝试改变将会报错：
	
	let languageName = "Swift"
	languageName = "Swift++" // 将报错
	
#####打印常量和变量
可以用`println`来打印常量和变量
	
	println(friendlyWelcome)

`println`是一个全局函数，可以打印值，并自动换行，如果在Xcode上工作，这个语句将会在控制台上打印（还有一个方法是`print`，打印之后不换行）

`println`打印任何`String`值
	
	println("This is a string")

也可以打印很多复杂的Log,类似于Cocoa's `NSLog`

还有一种用法，说明很长很无趣，看例子就知道了：(friendlyWelcome是字符串)
	
	println("The current value of friendlyWelcome is \(friendlyWelcome)")
	
#####注释
两种，一种是`双斜杠` `//`
还有一种是`\*` `*\`

注：Swift的`\**\`注释可以嵌套  `\* \* *\ *\`这样也完全可以

#####分号
Swift不需要在代码语句的最后写分号，如果你想，也可以写。

但是，如果想在一行中写两行语句，则一定要在第一行语句的末尾加分号

	let cat = "🐱"; println(cat)
	// prints "🐱"

###整数
整数是没有小数的数字，例如42和-23.整数包含有符号数和无符号数。

Swift提供8位 16位 32位 64位的符号数和无符号数。这些整数的命名习惯和C类似。

8位的无符号数类型是UInt8， 32位的符号数类型是Int32.

#####整数域
每个整数类型都可以通过`min`和`max`来访问整数类型是最小值和最大值
	
	let minValue = UInt8.min // minValue = 0,类型是UInt8
	let maxValue = UInt8.max // maxValue = 255，类型是UInt8
	
这些属性值都是大小合适的数字类型(例如上例中的UInt8)，因此也可以用于其他表达式

#####Int类型
很多情况下，不需要刻意选择整数类型。Swift提供一个额外的整数类型`Int`，随着平台的不同会自动变成对应的整数类型。例如：

	32位上，Int等同于Int32
	64位上，Int等同于Int64

除非需要指定整型位数，否则尽量使用`Int`.

#####UInt类型
Swift也提供一个无符号数UInt
	
	32位上，UInt等同于UInt32
	64位上，UInt等同于UInt64

#####浮点数
浮点数指的是有小数部分的数，例如3.14159,0.1和 -273.15

浮点型可以拥有超过整数类型的数字范围，也可以存储超过整型范围的数

浮点型有两类`Float`（32位浮点数，精确到6位小数） `Double`(64位浮点数，至少精确到15位小数)

#####类型安全和类型推测
Swift是类型安全的语言，一个类型安全的语言鼓励开发者把代码的类型变得清晰。如果代码期待收到一个字符串类型，开发者就不应该错误地传入一个整型。

因为Swift是类型安全的，所以编译代码时会进行类型检查，并把所有的不匹配类型标记为错误。这使得开发者能在开发阶段尽早捕获并修复错误。

类型检查帮助开发者避免不同类型的错误，但是这不意味这开发者需要为每一个变量和常量声明类型。如果没有明确指出值的类型，Swift也会使用类型推测来判断出合适的类型，类型推测能够使编译器在编译器自动推测类型，检查开发者提供的数值。

因为类型推测，Swift需要比C或Objective-C更多更广的类型声明。变量和常量都需要明确的声。

当开发者初始化一个常量或变量的时候，类型推测非常有用，这个在指定一个字面量（例如42或3.14159）的时候就已经做完了

例如，如果你给一个新常量赋值42，但是没有指明常量类型，Swift会推测你希望常量是`Int`型，因为42是`Int`型

	let meaningOfLife = 42

如果你赋了一个浮点数的值但是没有指明是Float型，那么Swift会推测希望创建`Double`
	
	let pi = 3.14159

如果一个表达式中既有整数又有浮点数，那么会推测这个表达式是`Double`型

	let anotherPi = 3 + 0.14159

#####数字字面量
数字字面量有几种写法
	
	无前缀的数字，有0b前缀的二进制数字，有0o前缀的八进制数字，有0x前缀的十六进制数字

	let decimalInteger = 17
	let binaryInteger = 0b10001
	let octalInteger = 0o21
	let hexadecimalInteger = 0x11

浮点数字面值可以是数字（没有前缀），或者十六进制数（带0x前缀）。小数点两边的进制必须相等，也可以指明一个大写或小写e（十进制）或者大写或小写p（十六进制）
	
带`exp`的十进制数：

	1.25e2 = 1.25 * 10²或125.0
	1.25e-2 = 1.25 * 10-² 或0.0125

带`exp`的十六进制数:
	
	0xFp2 = 15 * 2²或60.0
	0xFp-2 = 15 * 2-² 或3.75

下面都表示12.1875
	
	let decimalDouble = 12.1875
	let exponentDouble = 1.21875e1
	let hexadecimalDouble = 0xC.3p0

数字字面量可以包含一些附加信息以便于阅读，所有的整数和浮点数都可以用0填充也可以包含下划线来辅助阅读。
	let paddedDouble = 000123.456
	let oneMillon = 1_000_000
	let justOverOneMillon = 1_000_000.000_000_1

###数字类型转换
通常在程序用表示数字会用`Int`型，虽然知道他们非负，使用默认数字类型意味着数字常量和变量立即操作并可以匹配整数字面量

#####整数转换
每一种整型常量或变量可以存储的数字区间都不一样，一个`Int8`常量或变量能够存储`-128`到`127`，`UInt8`型则可以存储`0`到`255`当数字存储在不适合的数字类型中时系统会报错。

	let cannotBeNegative: UInt8 = -1 // 无符号数不能存储-1，会报错
	let tooBig: Int8 = Int8.max + 1 // 这个数超过了Int8可存储的最大值，报错

因为每个数字类型能够存储不同数据范围的数，所以最好找到最优存储类型，这样可以防止出现隐蔽的格式转换错误。

要把一个数字类型转换成新的数字类型，需要先新建一个新的想要的数字类型，然后初始化.如下，有一个`UInt16`类型的常量`twoThousand`，还有一个`UInt8`的常量，他们不是一个类型的，于是创建一个新的`UInt16`，将`UInt8`转换成`UInt16`

	let twoThousand: UInt16 = 2_000
	let one: UInt8 = 1
	let twoThousandAndOne = twoThousand + UInt16(one)

因为等号两边都是`UInt16`所以可以进行赋值

#####整数与浮点数互相转换
整数和浮点数之间进行类型转换，必须明确表示：
	
	let three = 3
	let pointOneFourOneFiveNine = 0.14159
	let pi = Double(three) + pointOneFourOneFiveNine

常量`three`用来创建`Double`类型，因此等号两边都是相同类型，就可以赋值了。


从浮点型转换成整型的操作总是可以的
	
	let integerPi = Int(pi)

但是浮点型转换成整数之后，小数点后面的数字都被截断了，`4.75`转换之后变成`4`，`-3.9`转换之后变成`-3`

###类型别名
类型别名允许给一个已知的类型定义别名，使用`typealias`即可

主要用途是更加表意

	typealias AudioSample = UInt16

定义别名之后可以和正式名称一样使用，替换也可

	var maxAmplitudeFound = AudioSample.min

###布尔值
Swift也有基本的布尔值`Bool` 有两个值`true` `false`
	
	let orangesAreOrange = true
	let turnipsAreDelicious = false

如果赋值的时候赋了`true` 或 `false`, 系统会自动把类型设置为布尔，而不需要特别指定

布尔值可以用于`if`语句

if turnipsAreDelicious {
	println("Mmm, tasty turnips!")
} else {
	println("Eww, turnips are horrible.")
}

关于`if`的具体细节请参见后续章节`控制流`

Swift的类型安全可以防止非布尔值替代`Bool`，下列例子会编译错误：

	let i = 1
	if i { // 报错
		
	}
	
但是这样就对了：

	let i = 1
	if i == 1 {
		// 编译成功
	}

`i == 1`的结果是`Bool`因此符合判断要求，关于`i == 1`详见`基础操作`

###元组
元组把多个值集合起来作为一个集体，一个元组可以存放各种类型，而且不要求每个类型都一样

下面有个例子，`(404, "Not Found")`就是一个表示HTTP状态码的数组，一个HTTP状态码像web服务器请求之后返回得到的。404 Not Found表示这个页面不存在

	let http404Error = (404, "Not Found") // http404Error 类型是(Int, String)

这个元组把一个数字和一个字符串聚合在一起，可以描述其为类型是`(Int, String)`的元组

可以创建拥有任意类型和数量的元祖，例如`(Int, Int, Int)`或`(String, Bool)`

也可以分解元祖的内容，分开赋值给常量or变量，如下:
	
	let (statusCode, statusMessage) = http404Error
	println("The status code is \(statusCode)")
	println("The status code is \(statusMessage)")

如果值需要元祖中某一部分的值，不想要的值用`_`代替

	let (justTheStatusCode, _）= http404Error
	println("The status code is \(justTheStatusCode)") 
	// 结果是 The status code is 404

还可以用下标来访问元祖的某个元素
	
	println("The status code is \(http404Error.0)")
	// 打印 The status code is 404
	println("The status message is \(http404Error.1)")
	// 打印 The status message is Not Found

还可以给元祖中各个元素命名
	
	let http200Status = (statusCode: 200, description: "OK")

如果给元祖中的元素命了名，可以直接用这个名称来访问数据
	
	println("The status code is \(http200Status.statusCode)")
	// 打印 The status code is 200
	println("The status message is \(http200Status.descripiton)")
	// 打印 The status message is OK

元祖主要用于做函数的返回值，用元祖也很好的描述了网络返回状态。想了解更多信息，详见`多返回值函数`

注：元祖用于存储临时的成组关联值时很好用，但是不适用于复杂的数据结构，如果需要长期使用，新建一个类或者结构体比元祖更好，详见"类和结构体"

###可选值
当一个值可能丢失时，可以使用可选来标记这个值，换言之，可选的意思表示
	
	这个值存在，并等于x

或
	
	这个值不存在

注：可选值这个概念在C和Objective-C中不存在,Objective-C中比较接近的做法是一个方法要么返回nil要么返回对象，nil的意思就是指一个有效值的丢失。但是nil只存在于对象中，在结构体，基于C的类型，或者枚举中都不存在。对这些类型，Objective-C的一种处理是返回一种特殊类型`NSNotFound`。这种方式是假定了方法的调用者知道存在这样的特殊值且会检查它。Swift的可选值对任何类型都有效.

举例说明，Swift的`String`类型有一个方法`toInt`，这个可以把`String`转换成`Int`。但是，不是任何字符串都能转换成整型，`hello,world`就不行

	let possibleNumber = "123"
	let covertedNumber = possibleNumber.toInt()

因为`toInt`可能会失败，因此可能会返回`Int的可选值`而不是`Int`。整型的可选值写成`Int?`而不是`Int`。上述例子可能是`Int`也可能`没有值`。

#####If语句和强制展开(forced upwrapping)
可以用`if`语句来判断是否是可选值。

如果不存在，则使用else来分开处理

	if convertedNumber {
		println("\(possibleNumber) has an integer value of \(convertedNumber)")
	} else {
		println("\(possibleNumber) could not be converted to an integer")
	}
	
关于`if`语句的详细信息，参见`控制流`

注：尝试使用`!`访问不存在的可选值，以便于触发运行时错误。在使用`!`之前总是要确认这个可选值中包含非空值。

#####可选值绑定（optional binding）
使用可选值绑定来确定是否这个可选值含有值，如果含有值，把这个值作为一个临时变量或常量, 在块中调用这个临时的变量或常量，可选值绑定可以和`if` `while`结合来判断一个值是否是可选的，含有值则把这个值赋给临时的变量或常量。预知后事如何，详见`控制流`

可选值绑定怎么写，见下面：

	if let constantName = someOptional {
		statements
	}

还可以使用可选值绑定来修改之前的例子

	if let actualNumber = possibleNumber.toInt() {
		println("\(possibleNumber) has an integer value of \(actualNumber)")
	} else {
		println("\(possibleNumber) could not be converted to an integer")
	}
上面例子可以表述为：
	
	如果`possibleNumber.toInt()`可选的`Int`中含有值，会将这个值赋值给`actualNumber`,如果条件成立，常量`actualNumber`就在if成立的块中可用，这个常量已经初始化并且不再需要再加上`!`来获得值。上述例子中，`actualNumber`只是简单的用于打印
	
如果想用变量，只需要把`if let`改成`if var`就行了

#####nil
给可选值变量赋空值的方式就是给它一个`nil`

	var serverResponseCode: Int? = 404
	// serverResponseCode包含实值404
	serverResponseCode = nil
	// 现在serverResponseCode不含有值了

注：`nil`不能给非可选值的常量或变量赋值，如果需要表示在某种情况下会有空值，把这个常量或变量改成可选值吧

如果定义一个不带默认值的可选的常量或变量，它们将自动赋值nil
	
	var surveyAnswer: String?
	// surveyAnswer自动赋了空值nil

注：Swift中的nil不等同于Objective-C中的nil，在Objective-C中nil是一个指向不存在对象的指针。但是Swift中nil不是一个指针，它是某个类型的值的空缺。任何类型的可选值都可以被设为nil,而不仅仅是对象。

#####隐式可选值(Implicitly unwrapped optional)
综上所述，可选值指明了一个允许赋空值的常量或变量，可选值能够被`if`语句判断是否存在值，也可以结合可选值绑定有条件的展开来访问可选值，如果可选值存在的话

有时候一些可选值初始化之后总是有值，这种情况下，可以不必每次都检查，因为总是安全的。

多种类型的可选值可以被定义为限制打开的可选值，只要在类型后面加上感叹号`(String!)`取代之前的`(String?)`即可

当一个可选值的值在初始化之后肯定存在，就能够确定的猜想任何时候这个隐式可选值都存在。它主要的用途在于类初始化中，详情请见`不能拥有的引用和隐式可选值属性`

一个隐式可选值离开那些场景的话也就是正常的可选值，也可以像非可选的值一样使用，而不需要每次都展开可选值。下面的例子展现了可选值String和隐式可选值String之间的不同

	let possibleString: String? = "An optional string"
	println(possibleString!) // 需要加感叹号才能直接访问
	let assumedString: String! = "An implicitly unwrapped optional string."
	println(assumedString) //没有感叹号也可以访问

可以认为隐式可选值作为允许访问的可选值，任何时候使用都会自动展开。与其每次使用可选值的时候在可选值后面放感叹号，还不如声明的时候放一次，之后都可以直接调用

注：当你访问一个不含值的隐式可选值，将会有运行时错误，这个和使用一般的未赋值的可选值一样

还可以像一般的可选值一样用`if`检查是否含有值

	if assumedString {
		pringln(assumedString)
	}

同样，也可以使用可选值绑定来检查
	
	if let definiteString = assumedString {
		println(definiteString)
	}
	
	
注：隐式可选值本不应该用于一个可能为nil的变量，如果需要在变量的生命周期中随时检查nil的变量就应该使用正常的可选值

###断言
可选值使开发者在可能存在或不存在的时候检查值，并在无值的时候能够从容应对。一些情况下，如果可选值不存在或者提供的值不满足某些条件，代码可能很难处理。这时候，开发者可以触发断言，结束运行，来完善缺失的条件

#####带断言调试
断言在运行期检查逻辑条件是否为真。

如果位真，代码继续运行，否则，程序被终止

如果代码在编译环境下运行触发了断言，例如在Xcode中编译和运行应用，可以看到断言发生的位置和当时状态。断言本身也能提供一些合适的调试信息。

要写断言，调用全局函数`assert`。传入一个表达式以及当这个表达式为假时的描述信息。

	let age = -3
	assert(age >= 0, "A person's age cannot be less than zero")

在上面的例子中，如果`age >= 0 `判断为假，程序会终止

断言也可以不写描述信息，下面的例子就展示了一个无描述信息的情况：

	asert(age >= 0)

#####何时使用断言
当条件可能为假时就可以使用断言。使用断言的场景包括:

- 传入整数下标，且可能越界
- 向一个函数传入一个值，但是值非法
- 可选值当前是nil 但是实际上需要一个非空的值来保障程序运行

详情参见`下标和函数`


	


	
	
	
	
	
