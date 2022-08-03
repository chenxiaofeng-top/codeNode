### 程序入口:

```kotlin
//在类之外，不能在class里面
//不带参数
fun main() {
    println("Hello world!")
}
//带参数
fun main(args: Array<String>) {
    println(args.contentToString())
}
```

### 系统输出：

```kotlin
//java System.out.println("Hello ");
print("Hello ")
```

### 方法

```kotlin
//定义
fun sum(a: Int, b: Int): Int {
    return a + b
}
//只有return一行可以简写成
fun sum(a: Int, b: Int) = a + b
```

### 变量

```kotlin
//常量
val a: Int = 1  // immediate assignment
val b = 2   // 类型推导
val c: Int  // Type required when no initializer is provided
c = 3       // 延迟赋值，只能赋值一次

//变量
var x = 5 // `Int` type is inferred
x += 1

//可空变量,在类型后加一个"?"
val c: Int?
```

### class定义

```kotlin
//最简单定义的一个类
class Shape
//使用，跟js很类型，不需new 
var shape = Shape();

//类的属性，height，length，perimeter，都是Rectangle的属性
class Rectangle(var height: Double, var length: Double) {
    var perimeter = (height + length) * 2
}
//使用
var rectangle = Rectangle(1.0, 2.0)
println("The perimeter is ${rectangle.perimeter} ${rectangle.height}")

//类默认是不能继承，如果可以继承，则需要加上open
//Shape的构造方法在继承里写
open class Shape
class Rectangle(var height: Double, var length: Double): Shape() {
    var perimeter = (height + length) * 2
}

```

### 字符串

```kotlin
//拼接
var a = 1
val s1 = "a is $a" 
val s2 = "${s1.replace("is", "was")}, but now is $a"

```

### 条件语句

```kotlin
fun maxOf(a: Int, b: Int): Int {
    if (a > b) {
        return a
    } else {
        return b
    }
}
//简写
fun maxOf(a: Int, b: Int) = if (a > b) a else b
```

### for 循环

```kotlin
val items = listOf("apple", "banana", "kiwifruit")
for (item in items) {
    println(item)
}
//或着
for (index in items.indices) {
    println("item at $index is ${items[index]}")
}
```

### while 循环

```kotlin
val items = listOf("apple", "banana", "kiwifruit")
var index = 0
while (index < items.size) {
    println("item at $index is ${items[index]}")
    index++
}
```

### when 表达式

```kotlin
fun describe(obj: Any): String =
    when (obj) {//跟switch类似，但有kotlin特性，不需要在后面加break
        1          -> "One"
        "Hello"    -> "Greeting"
        is Long    -> "Long"
        !is String -> "Not a string"
        else       -> "Unknown"
    }
```

### 范围表达式

```kotlin
//1..y+1 表示1到10这个范围
val x = 10
val y = 9
//在判断中返回true或着false
if (x in 1..y+1) {
    println("fits in range")
}
//在for中返回值
for (x in 1..5) {
    print(x)
}

//输出13579
for (x in 1..10 step 2) {
    print(x)
}
println()

//x in 9 downTo 0 输出963
//下面输出9630
for (x in 9 downTo 0 step 3) {
    print(x)
}
```

### lambda 表达式

```kotlin
val fruits = listOf("banana", "avocado", "apple", "kiwifruit")
fruits
    .filter { it.startsWith("a") }
    .sortedBy { it }
    .map { it.uppercase() }
    .forEach { println(it) }
//输出:
//APPLE
//AVOCADO
```

### 类型转换

```kotlin
//隐式转换 
if (obj is String) {
        // `obj` is automatically cast to `String` in this branch
    	//java  中需要增加强制类型转换的代码，但kotlin,在if判断为ture时，就自动转换
        return obj.length
  }
```

