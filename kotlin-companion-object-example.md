## Kotlin Companion Object 範例

除了在 [Kotlin Object 範例](kotlin-object-example.md) 

提到全域物件的用法

有時候我們會需要某個類別

和某個全域物件進行關聯

這時我們可以用 `companion object` 關鍵字宣告

```kotlin
class MyClass {
    companion object Factory {
        var number = 0
        fun create(): MyClass = MyClass()
    }
}
```

使用時可以像存取靜態函數這樣

直接呼叫 `MyClass.number` 或 `MyClass.create()`

```kotlin
MyClass.number++  
println(MyClass.number) // 1
MyClass.create() // 建立 MyClass
```

雖然看起來像是靜態屬性或靜態函數

但是 `companion object` 是一個實體物件

所以實體物件能做的事都可以實現

比方說繼承某個介面

```kotlin
interface Factory<T> {
    fun create(): T
}

class MyClass {
    companion object : Factory<MyClass> {
        override fun create(): MyClass = MyClass()
    }
}

val f: Factory<MyClass> = MyClass
```

-----

想看更多範例嗎？

可以看看

- [Kotlin 慣用寫法](idioms.md)
- [Kotlin 入門範例](kotlin-syntax.md)
- [kotlin Data Class 範例](kotlin-data-class-example.md)
- [kotlin Enum Class 範例](kotlin-enum-class-example.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
