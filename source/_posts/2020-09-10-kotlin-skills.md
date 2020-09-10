---
title: kotlin_skills
date: 2020-09-10 09:02:48
tags:
---


## 1. functions as parameters （函数作为入参）
假设有两个数，要将他们合并为一个数，合并的方式不同，此时就可以使用函数入参的方式
```kotlin
fun <T, R> Collection<T>.fold(
    initial: R, 
    combine: (acc: R, nextElement: T) -> R
): R {
    var accumulator: R = initial
    for (element: T in this) {
        accumulator = combine(accumulator, element)
    }
    return accumulator
}
```
#### 使用
```kotlin
 val items = listOf(1, 2, 3, 4, 5)

// Lambdas are code blocks enclosed in curly braces.
items.fold(0, { 
    // When a lambda has parameters, they go first, followed by '->'
    acc: Int, i: Int -> 
    print("acc = $acc, i = $i, ") 
    val result = acc + i
    println("result = $result")
    // The last expression in a lambda is considered the return value:
    result
})

// Parameter types in a lambda are optional if they can be inferred:
val joinedToString = items.fold("Elements:", { acc, i -> acc + " " + i })

// Function references can also be used for higher-order function calls:
val product = items.fold(1, Int::times)

/**
acc = 0, i = 1, result = 1
acc = 1, i = 2, result = 3
acc = 3, i = 3, result = 6
acc = 6, i = 4, result = 10
acc = 10, i = 5, result = 15
joinedToString = Elements: 1 2 3 4 5
product = 120
*/
```

## 2. 扩展函数
可以为已有的类添加方法，使其有新的功能
```kotlin
// 将 Boolean 值转成 0 或 1
fun Boolean.toInt() = if (this) 1 else 0

// usage
True.toInt()
```

## 3. let, run, also, apply, with 的使用
### 3.1 let
`let` 最后一行是`let`代码块的返回值，如果最后一行是一个值，则`let`有返回值，否则是一个`Unit`，即无返回值
{% codeblock %}
    val name = "Jack"

    val a = name.let {
        it.length
    }
    // a = 4

    val a = name.let {
        it.length
        print("xyz")
    }
    // Unit
{% endcodeblock %}

`let`的代码块里带有一个内置的`it`实例，代表调用`let`代码块的实例本身

### 3.2 run
`run` 和 `let` 类似，不过没有了`it`，可以再代码块里直接访问实例本身的属性，同样最后一行是返回值
{% codeblock lang:kotlin %}
    val name = "Jack"

    val a = name.run {
        length
    }
    // a = 4

    val a = name.run {
        length
        print("xyz")
    }
    // Unit
{% endcodeblock %}


### 3.3 also
`also`和`let`类似，只不过不需要指定返回，默认返回实例本身，所以多数情况下`let`和`also`可以相互替换。 `also`同样含有`it`指向调用实例本身
{% codeblock lang:kotlin %}
    val count = 10

    val result = count.also {
        it + 1
        print("xyz")
    }

    println(result) // result = 10
{% endcodeblock %}


### 3.4 apply
`apply`和`run`类似，无需指定返回值，相比于`also`, `apply`可以直接使用实例的属性；相比于`run`，无需指定返回值
{% codeblock lang:kotlin %}
    val name = "Jack"

    val result = name.apply {
        println(length + 1)
    }

    println(result)
{% endcodeblock %}

### 3.5 with
`with`用于改变实例的属性，而无需使用`.`来调用
{% codeblock lang:kotlin %}
    data class Person(var name: String, var gender: String)

    val person = Person("Jack", "male")

    with(person) {
        name = "Rose"
        gender = "female"
    }
    println(person)
{% endcodeblock %}
