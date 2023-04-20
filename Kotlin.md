# Kotlin

## 目录

-   [一、for循环](#一for循环)
-   [二、标准函数](#二标准函数)
    -   [1、let()](#1let)
    -   [2、with()](#2with)
    -   [3、run()](#3run)
    -   [4、apply()](#4apply)
-   [三、高阶函数](#三高阶函数)
    -   [1、语法结构](#1语法结构)
-   [四、委托](#四委托)
    -   [1、类委托](#1类委托)
    -   [2、属性委托](#2属性委托)
    -   [3、自定义lazy函数](#3自定义lazy函数)
-   [五、infix函数](#五infix函数)
    -   [1、语法](#1语法)
    -   [2、例子](#2例子)
-   [六、泛型的高级特性](#六泛型的高级特性)
    -   [1、对泛型进行实例化](#1对泛型进行实例化)
    -   [2、泛型的协变](#2泛型的协变)
-   [七、协程](#七协程)
    -   [1、协程创建——作用域构建器](#1协程创建——作用域构建器)

# 一、for循环

-   使用for in关键字
    ```kotlin
    for (item in array){
      
    }
    ```
-   repeat语法
    ```kotlin
    repeat(10){
      println(it) 
    }
    ```

# 二、标准函数

## 1、let()

```kotlin
val testString = "123"
//用于判断空
testString?.let {
    println(it)
}
```

## 2、with()

> 传入对象，在块内连续调用该对象的方法，让代码变得更加整洁

```kotlin
val list = 0 until 10
val num = with(StringBuilder()) {
    for (i in list) {
        append(i).append("\n")
    }
    //最后一行是函数的返回值
    toString()
}
println(num)
```

## 3、run()

> 功能与with()函数相同

```kotlin
val list = 0 until 10
val num = StringBuilder().run {
    for (i in list) {
        append(i).append("\n")
    }
    //最后一行是函数的返回值
    toString()
}
println(num)
```

## 4、apply()

> 用法与run()函数基本一致，区别在于最后一行不是返回值，返回值为对象本身

```kotlin
val list = 0 until 10
val num: StringBuilder = StringBuilder().apply {
    for (i in list) {
        append(i).append("\n")
    }
}
println(num.toString())
```

# 三、高阶函数

> 一个函数接受另一个函数作为参数，获取返回值类型是另一个函数

## 1、语法结构

ClassName.(String, Int) → Uint

```kotlin
fun example(func: (String, Int) -> Unit) {
  func("hello",123)
}
```

# 四、委托

> 操作对象不会自己不会去处理某段逻辑，而是会把工作委托给另一个辅助对象去处理

## 1、类委托

> 将一个类的具体实现委托给另一个类去完成

```kotlin
class MySet<T>(private val helperSet: HashSet<T>) : Set<T> by helperSet {

    fun helloWorld() = println("hello world")

    override fun isEmpty() = false
}
```

## 2、属性委托

> 将一个属性的具体实现委托给另一个类去完成

```kotlin
class MyClass {
    val p by Delegate()
}

class Delegate {
    private var propValue: Any? = null
    operator fun getValue(myClass: MyClass, prop: KProperty<*>): Any? {
        return propValue
    }

    operator fun setValue(myClass: MyClass, prop: KProperty<*>, value: Any?) {
        propValue = value
    }
}

```

## 3、自定义lazy函数

```kotlin
class Later<T>(val block: (T) -> T) {
    private var value: T? = null

    @Synchronized
    operator fun getValue(myClass: Any?, prop: KProperty<*>): T? = value?.let { block(it) }

    @Synchronized
    operator fun setValue(myClass: Any?, prop: KProperty<*>, value: T?) {
        this.value = value?.let { block(it) }
        println(this.value)
    }
}
//顶层函数
fun <T> later(block: (T) -> T) = Later(block)

class Person(name: String, private val age: Int) {
    var name: String? by later {
        it + "123"
    }

    init {
        this.name = name
    }
}

fun main() {
    val person = Person("xgd", 123)
    println(person.name)
}
```

# 五、infix函数

## 1、语法

infix 函数不能定义成顶层函数，它必须是某个类的成员函数，可以使用拓展函数的方式将它定义到某个类中；其次，infix函数必须且只能接收一个参数，这个参数的类型是没有限制的

## 2、例子

```kotlin
fun main() {
    val xgd = Person("xgd", 12)
    if (xgd be "xgd") {
        println("123")
    }
}

class Person(private var name: String, private var age: Int) {
    infix fun be(myName:String) = myName==this.name
}
```

# 六、泛型的高级特性

## 1、对泛型进行实例化

> 可以将内联函数中的泛型进行实例化(使用inline关键字)；在声明泛型的地方必须加上reified关键字来表示泛型要进行实例化

```kotlin
fun main() {
    val type1 = getGenericType<String>()
    var type2 = getGenericType<Int>()
    println("$type1 $type2")
}

inline fun <reified T> getGenericType() =T::class.java
```

## 2、泛型的协变

> 假如定义了一个MyClass\<T>的泛型类，其中A是B的子类型，同时MyClass\<A>是MyClass\<B>的子类型，那么可以称MyClass在T这个泛型上是协变的

```kotlin
fun main() {
    var student = SimpleData<Student>(Student())
    handleSimpleData(student)
}

fun handleSimpleData(data: SimpleData<Person>) {
    var get = data.get()
}

class SimpleData<out T>(private val data: T) {
    fun get(): T {
        return data
    }
}

open class Person {

}

class Student : Person() {

}
```

# 七、协程

> 在编程语音层面实现并发编程，不依赖于操作系统调度

## 1、协程创建——作用域构建器

1.  GlogalScope.launch——创建一个顶层协层作用域
2.  runBlocking——创建一个协层作用域，但是会阻塞当前线程，会影响性能
3.  launch——在当前作用域下创建一个子作用域
4.  coroutineScope——可以在任何挂起函数中调用，并继承当前作用域并创建子作用域，与runBlocking类似，但仅会阻塞当前协程
