## Kotlin Sealed Class 範例

宣告 sealed class

```kotlin
sealed class Mammal(val name: String) 
```

## 特性
sealed class 限制只能被同一個 package 的類別繼承

```kotlin
package demo

import Mammal

class Demo(name: String) : Mammal(name) // 編譯錯誤
```

由於這個特性

sealed class 跟 enum 一樣

可以讓編譯器確定資料的可能個數

如果在條件式內列舉所有可能

就不需要宣告 `else`

```kotlin
class Cat(name: String) : Mammal(name)
class Dog(name: String) : Mammal(name)

fun greetMammal(mammal: Mammal): String {
    return when (mammal) {                                          
        is Dog -> "GoodBoy ${mammal.name}"
        is Cat -> "Hello ${mammal.name}"
    }
}

```

-----

想看更多範例嗎？

可以看看

- [Kotlin 的函數式編程慣用寫法](kotlin-functional-programming-example.md)
- [kotlin Data Class 範例](kotlin-data-class-example.md)
- [kotlin Data Class 範例](kotlin-enum-class-example.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
