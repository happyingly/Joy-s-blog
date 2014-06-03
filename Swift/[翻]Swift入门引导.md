###Swift入门引导

####本文翻译自`The Swift Programming Language`中的`A Swift Tour`

依照惯例，学一门语言从Hello World开始。

在Swift中，只需要这么一句话
	
	println("Hello, world")
	
如果之前你学过C或Objective-C，肯定对这句代码不陌生，在Swift中，这句代码就是一个完成的程序了。

你不需要为这个功能引入诸如输入输出或者字符串处理的库。

写在全局的代码就是程序的入口，不需要`main`函数

也不需要写分号


###赋值

######用`let`声明常量 用`var`声明变量

虽然在编译期不需要知道常量的值，但是还是要给常量赋个值。然后就可以到处用它了。

	var myVariable = 42
	myVariable = 50
	let myConstant = 42
	
赋值必须要左右类型一致，但是不需要明确的声明类型，创建常量或者变量的初始化就决定了这个变量或常量的类型。例如myVariable是整型的，因为初始化的值是整型的。


######如果初始化没有提供足够信息（或者没有初始化值），可以在变量后面指定一个类型，用冒号隔开
	
	let implicitInteger = 70
	let implicitDouble = 70.0
	let explicitDouble : Double = 70


#####值不能直接转换成别的类型，如果需要转换，要新建一个实例来存放新的值

	let label = "The width is"
	let width = 94
	let widthLabel = label + String(width)


#####有一种简单的方法在字符串中添加数据：把值写在圆括号中，圆括号前加上反斜杠`\`.例如：
	
	let apples = 3
	let oranges = 5
	let appleSummary = "I have \(apples) apples."
	let orangesSummary = "I have \(apples + oranges) pieces of fruit."

使用`\()`可以包含一个浮点型计算

#####用`[]`创建一个数组or字典,用下标或者key来获得数据

	var shoppingList = ["catfish", "water", "tulips", "blue paint"]
	
	shoppingList[1] = "bottle of water"
	
	var occupations = [
		"malcolm" : "Captain",
		"Kaylee" :	"Mechanic",
	]
	
	occupations["Jayne"] = "Public Relations"
	
#####使用初始化语句创建空数组or空字典
	
	let emptyArray = String[]()
	let emptyDictionary = Dictionary<String, Float>()

如果类型已经声明的话，可以直接写`[]`（字典用`[:]`）来赋空值

###条件控制和循环

可以使用`if`和`switch`做条件控制，使用`for` `for-in` `while` `do-while`来做循环

#####if语句
判断条件和循环中使用的变量可以自由选择是否用圆括号括起来，但是代码执行是肯定要用大括号括起来的。

	let individualScores = [75, 43, 103, 87, 12]
	var teamScore = 0
	for score in individualScores {
		if score > 50 {
			teamScore += 3
		} else {
			teamScore += 1
		}
	}
	teamScore

在`if`条件中，判断语句必须是一个`布尔值`，这意味着类似`if score { ... }`会报错，而不是默认和0比较

`if`后面跟着`let`和一个变量，代表这个变量可能丢失, 这些可能丢失的变量称为可选的，一个可选的变量要么含有值要么为`nil`，如果是`nil`就表示这个变量丢失了。

在初始化语句后面加上`?`表示这个变量是可选的。

	var optionalString:String? = "Hello"
	optionalString == nil
	
	var optionalName: String? = "John Appleseed"
	var greeting = "Hello!"
	if let name = optionalName {
		greeting = "Hello, \(name)"
	}
	
如果`optionalName`为空，if块条件不满足于是跳过了，最好在if后加上else来做不同的处理

#####Switch语句
`switch`支持任何类型的数据和多种表达式，没有限制必须是整型,例如

	let vegetable = "red pepper"
	switch vegetable {
		case "calery":
			let vegetableComment = "Add some raisins and make ants on a log."
		case "cucumber", "watercress":
			let vegetableComment = "That would make a good tea sandwich."
		case let x where x.hasSuffix("pepper"):
			let vegetableComment = "Is it a spicy \(x)?"
		default:
			let vegetableComment = “Everything tastes good in soup.”
	}

`switch`的进入对应的`case`执行完语句之后，不会继续往下走，因此不需要再写`break`了

#####for-in语句

可以自己定义键值对的名称然后用for-in来遍历字典，例如：
	
	let interestingNumbers = [
		"Prime": [2, 3, 5, 7, 11, 13],
		"Fibonacci": [1, 1, 2, 3, 5, 8],
		"Square": [1, 4, 9, 16, 25],
	]
	
	var largest = 0
	
	for (kind, numbers) in interestingNumbers {
		for (number in numbers) {
			if number > largest {
				largest = number
			}
		}
	}
	largest
	
#####while语句
使用`while`来重复执行代码，直到循环条件发生改变，有两种写法

	var n = 2
	while n < 100 {
		n = n * 2
	}
	n
	
	var m = 2
	do {
		m = m * 2
	} while m < 100
	m
	
也可以在循环中用下标，要么使用`..`来表示一个下标的范围，要么就直接准确的指出范围，下列两个for表达的意思是一致的
	
	var firstForLoop = 0
	for i in 0..3 {
		firstForLoop += i
	}
	firstForLoop
	
	var secondForLoop = 0
	for var i = 0; i < 3; ++i {
		secondForLoop += 1
	}
	secodeForLoop

使用`..`表示的区间会遗漏上限，例如`0..3`表示`0,1,2`，但是`...`则不会遗漏，例如`0...3`表示`0, 1, 2, 3`

###函数和闭包

#####使用`func`来声明一个函数。通过函数名和传入的参数来调用函数。

使用`->`把返回值同函数名称、属性类型区分开。

	func greet(name:String, day:String) -> String {
		return "Hello \(name), today is \(day)."
	}
	greet("Bob", "Tuesday")
	
	注：这个函数表示声明了一个名字叫greet的函数，返回值是String类型，有两个String类型的参数，参数名分别是name和day

#####使用数组来返回多个值
	
	func getGasPrices() -> (Double, Double, Double) {
		return (3.59, 3.69, 3.79)
	}
	getGasPrices()
	
#####也可以传入一系列数据做参数
	for sumOf(numbers:Int...) -> Int {
		var sum = 0
		for number in numbers {
			sum += number
		}
		return sum
	}
	sumOf()
	sumOf(42, 597, 12)

#####还可以嵌套函数
嵌套的函数可以访问函数内部声明的变量

	func returnFifteen() -> Int {
		var y = 10
		func add() {
			y += 5
		}
		add()
		return y
	}
	returnFifteen()

#####返回值是函数的函数
函数的first-class类型的，意味着一个函数可以把另外一个函数作为其返回值

	func makeIncrementer() -> (Int -> Int) {
		func addOne(number : Int) -> Int {
			return 1 + number
		}
		return addOne
	}
	var increment = makeIncrementer()
	increment(7)
	
#####把一个函数作为一个函数的参数传入
	
	func hasAnyMatches(list : Int[], condition: Int -> Bool) -> Bool {
		for item in list {
			if condition(item) {
				return true
			}
		}
		return false
	}
	
	func lessThanTen(number: Int) -> Bool {
		return number < 10
	}
	
	var numbers = [20, 19, 7, 12]
	hasAnyMatches(numbers, lessThanTen)

#####闭包
函数实际上是一种特殊的闭包, 也可以通过`{}`写一个没有函数名的闭包, 使用`in`来分隔参数和返回值

	numbers.map({
		(number: Int) -> Int in
		let result = 3 * number
		return result		
	})

有很多方式可以写出更简洁的闭包， 当一个闭包的类型是已知的，例如一个delegate的回调，则可以忽略参数（或返回值，两者都忽略也可）的类型
	
	numbers.map({ number in 3 * number})

也可以通过下标代替名字来取用参数，这个在短闭包中很好用
	
	sort([1, 5, 3, 12, 2]){ $0 > $1 }

###类和对象
#####创建类
使用`class`来创建一个类，其他变量常量声明在类的块中，例如

	class Shape {
		var numberOfSides = 0
		func simpleDescription() -> String {
			return "A shape with \(numberOfSides) sides."
		}
	}

如下所示来创建类对象,使用点语法来访问实例的参数和方法
	
	var shape = Shape()
	shape.numberOfSides = 7
	var shapeDescription = shape.simpleDescription()

#####初始化
但是这个Shape类少了一个很重要的东西，初始化方法。使用`init`来创建一个
	
	class NamedShape {
		var numberOfSides: Int = 0
		var name : String
		
		init(name: String) {
			self.name = name
		}
		
		func simpleDescription() -> String {
			return "A shape with \(numberOfSides) sides."
		}
	}

提醒：self.用来区分是类对象的属性还是传入的参数，而且每个属性都需要赋值（要么在初始化的时候要么在类中声明的时候）

如果需要在对象被释放之后做一些事情，则需要使用`deinit`

#####子类覆写父类方法
子类继承父类的话是在类名后面加上`: 父类名`, 如果子类继承的是标准根类则不需要显示声明。

如果子类要覆写父类的实现需要在实现前加上关键字`override`表示覆写了这个方法，如果不加这个，会被编译器报错。

	class Square: NamedShape {
		var sideLength: Double
		
		init(sideLength: Double, name: String) {
			self.sideLength = sideLength
			super.init(name: name)
			numberOfSides = 4
		}
		
		func area() -> Double {
			return sideLength * sideLength
		}
		
		override func simpleDescription() -> String {
			return "A square with sides of length \(sideLength)."
		}
	}
	
	let test = Square(sideLength: 5.2, name: "my test square")
	test.area()
	test.simpleDescription()

#####Get和Set方法
处理直接存储属性，属性还可以有get和set方法
	
	class EquilateralTriangle: NamedShape {
		var sideLength: Double = 0.0
		
		init(sideLength: Double, name: String) {
			self.sideLength = sideLength
			super.init(name: name)
			numberOfSides = 3
		}
		
		var perimeter: Double {
		get {
			return 3.0 * sideLength
		}
		
		set {
			sideLength = newValue / 3.0
		}
		}
		
		override func simpleDescription() -> String {
			return "An equilateral triangle with sides of length \(sideLength)."
		}
	}
	
	var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
	triangle.perimeter
	triangle.perimeter = 9.9
	triangle.sideLength

在`perimeter`的set方法中，有一个内部变量（所有新值都叫这个）叫`newValue`, 你可以在set之后给它换个名字

注意：`EquilateralTriangle`类的初始化有三个步骤：
	
	1、为子类声明的属性赋值
	2、调用父类的初始化方法
	3、改变被父类预设好的属性的值。任何其他的工作如get set方法也已经在这一步上执行完了

#####willSet和didSet
如果你不需要计算属性值但是需要在set方法运行前（或后）执行一些代码，请使用`willSet`和`didSet`。例如，确保三角形的边长总是和四边形的边长相等
	
	class TriangleAndSquare {
		var triangle: EquilateralTriangle {
		willSet {
			square.sideLength = newValue.sideLength
		}
		}
		var square: Square {
		willSet {
			triangle.sideLength = newValue.sideLength
		}
		}
		init(size: Double, name: String) {
			square = Square(sideLength: size, name: name)
			triangle = EquilateralTriangle(sideLength: size, name: name)
		}
	}
	var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
	triangleAndSquare.square.sideLength
	triangleAndSquare.triangle.sideLength
	triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
	triangleAndSquare.triangle.sideLength

#####用于外部和内部的方法属性
类的方法和函数有一个重要的不同，函数中的参数名称只能用于这个函数，但是调用类方法时也可以使用它的参数名称（除了第一个参数）。当你调用方法时，方法会有个相同的属性名，你也可以指定一个别名用于方法内部(下面的例子中，numberOfTimes用于外部，times用于内部，这俩其实是一个参数)
	
	class Counter {
		var count: Int = 0
		func incrementBy(amount: Int, numberOfTimes times: Int) {
			count += amount * times
		}
	}
	var counter = Counter()
	counter.incrementBy(2, numberOfTimes: 7)
	

#####方法，属性，下标的nil
之前说过可选的变量值，在等号前面加上`?`即可，这个也可以用于方法、属性和下标，如果`?`之前的值就是nil,则`?`之后的任何等式（或值）都会被忽略了，然后整个表达式固定返回为nil。
	
	let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
	let sideLength = optionalSquare?.sideLength


###枚举和结构体
#####枚举
使用`enum`来创建一个枚举，枚举可以有与之关联的方法

	enum Rank: Int {
		case Ace = 1
		case Two, Three, Four, Five, Six, Seven, Eight, Nine, Ten
		case Jack, Queen, King
		func simpleDescription() -> String {
			switch self {
			case .Ace:
				return "ace"
			case .Jack:
				return "jack"
			case .Queen:
				return "queen"
			case .King:
				return "king"
			default:
				return String(self.toRaw())
			}
		}
	}
	
	let ace = Rank.Ace
	let aceRawValue = ace.toRaw()
	
在上述例程中，枚举的原始数据类型为`Int` 因此只能指定第一个原始数据，剩下的数据会被依序赋值。也可以使用字符串或者浮点数作为枚举的原始值

使用`toRaw`和`fromRaw`函数在原始值和枚举值之间转换
	
	if let convertedRank = Rank.frowRaw(3) {
		let threeDescription = convertedRank.simpleDescription()
	}

枚举的成员值是实值，和原始值无关。一些情况下原始值意义不大，可以不用理它

	enum Suit {
		case Spades, Hearts, Diamonds, Clubs
		func simpleDescription() -> String {
			switch self {
			case .Spades:
				return "spades"
			case .Hearts:
				return "hearts"
			case .Diamonds:
				return "diamonds"
			case .Clubs:
				return "clubs"
			}
		}
	}
	let hearts = Suit.Hearts
	let heartsDescription = hearts.simpleDescription()	
注意:枚举值`Hearts`的两种使用方式：给`hearts`赋值时必须写全`Suit.Hearts`因为给常量初始化的时候常量不知道类型是什么，但是在枚举内部使用的时候, 可以使用`.Hearts`因为已经知道类型一定是这个枚举

#####结构体

使用`struct`来创建一个结构体。结构体和类很相似，例如方法和初始化。最大的不同在于结构体按值传递（传入之后拷贝一份），类按引用传递。

	struct Card {
		var rank: Rank
		var suit: Suit
		func simpleDescription() -> String {
			return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
		}
	}
	let threeOfSpades = Card(rank: .Three, suit: .Spades)
	let threeOfSpadesDescription = threeOfSpades.simpleDescription()
	

一个枚举成员的实例可以关联值，同一个枚举成员的实例可以关联不同的值。创建实例时提供关联值。

关联值和原始数据是不同的，一个枚举成员的原始数据和它的全部实例是一致的，是定义枚举的时候指定的原始值。

例如，以向服务器请求日出和日落时间为例，服务器要么返回请求信息的响应，要么返回错误信息

	enum ServerResponse {
		case Result(String, String)
		case Error(String)
	}

	let success = ServerResponse.Result("6:00 am", "8.09 pm")
	let failure = ServerResponse.Error("Out of cheese")
	
	switch success {
	case let .Result(sunrise, sunset):
		let serverResponse = "Sunrise is at \(sunrise) and sunset is at \(sunset)."
	case let .Error(error):
		let serverResponse = "Failure... \(error)"
	}
	
要注意日出和日落时间是如何从`ServerResponse`值中取出并作为`switch`case的匹配项的。

###协议和扩展
#####协议
使用`protocol`定义一个协议
	
	protocol ExampleProtocol {
		var simpleDescription: String { get }
		mutating func adjust()
	}

类，枚举和结构体都可以继承协议（即实现这个协议）

	Class SimpleClass: ExampleProtocol {
		var simpleDescription: String = "A very simple class."
		var anotherProperty: Int = 69105
		func adjust() {
			simpleDescription += "  Now 100% adjusted."
		}
	}
	var a  = SimpleClass()
	a.adjust()
	let aDescription = a.simpleDescription
	
	struct SimpleStructure: ExampleProtocol {
		var simpleDescription: String = "A simple structure"
		mutating func adjust()  {
			simpleDescription += "(adjested)"
		}
	}
	var b = SimpleStructure()
	b.adjust()
	let bDescription = b.simpleDescription

注意`SimpleStructure`的声明中`mutating`关键字的使用，这标记一个方法可以修改结构体，而`SimpleClass`不需要给任何方法加这个标记，因为在类中的方法总是可以修改这个类

#####扩展
使用`extension`为已经存在的类型增加功能，例如新方法和已计算的属性。可以使用扩展来增加协议一致性。

	extension Int: ExampleProtocol {
		var simpleDescription: String {
		return "The number \(self)"
		}
		mutating func adjust() {
			self += 42
		}
	}
	7.simpleDescription
	
还可以像其他已命名的类型一样使用协议名称，例如，要创建一个有不同类型对象但是都遵循同一个协议的集合。当你使用协议类型的值时，协议定义以外的方法是不可用的。

	let protocolValue: ExampleProtocol = a
	protocolValue.simpleDescription
	// protocolValue.anotherProperty // 会报错

虽然变量`protocolValue`拥有运行时类型`SimpleClass`,编译器会视为`ExampleProtocol`的已知类型。

###泛型
在尖括号中写一个名字来表示普遍的函数或类型（模板）
	
	func repeat<ItemType>(item: ItemType, times: Int) -> ItemType[] {
		var result = ItemType[]()
		for i in 0..times {
			result += item
		}
		return result
	}
	repeat("knock", 4)

可以产生一个函数和方法的模板，和类、枚举、结构体一样
	
	enum OptionalValue<T> {
		case None
		case Some(T)
	}
	var possibleInteger: OptionalValue<Int> = .None
	possibleInteger = .Some(100)

在类型名后面使用`where`来指明需求。例如，需要一个类型来实现一个协议，需要两个一致的类型，或者需要一个类，它有特殊的父类。
	
	func anyCommonElements <T, U where T: Sequence, U: Sequence, T.GeneratorType.Element: Equatable, T.GeneratorType.Element == U.GeneratorType.Element> (lhs: T, rhs: U) -> Bool {
		for lhsItem in lhs {
			for rhsItem in rhs {
				if lhsItem == rhsItem {
					return true
				}
			}
		}
		return false
	}
	anyCommonElements([1, 2, 3], [3])

在这个简单的例子中，`<T: Equatable>`和`<T where T: Equatable>`是一样的，`where`可以忽略，冒号后接一个协议名或类名.

		