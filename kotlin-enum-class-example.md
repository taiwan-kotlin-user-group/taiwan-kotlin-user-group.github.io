## Kotlin Enum Class 範例

類似其他語言有的列舉

Kotlin 設計了 `enum class` 的語法

宣告 enum class

```kotlin
enum class Direction {
    NORTH, SOUTH, EAST, WEST
}
```

宣告後可以透過類別名存取

```kotlin
val direction = Direction.NORTH
println(direction) // NORTH
```

由於 enum 的宣告

可以讓編譯器確定資料的可能個數

如果在條件式內列舉所有可能

就不需要宣告 `else`

```kotlin
val message = when (direction) {
	Direction.NORTH -> "facing north"
	Direction.SOUTH -> "facing south"
	Direction.EAST -> "facing east"
	Direction.WEST -> "facing west"
}
```

enum 也可以加上屬性和函數

透過分號來區分常數和其他區塊

```kotlin
enum class Color(val rgb: Int) {
    RED(0xFF0000),
    GREEN(0x00FF00),
    BLUE(0x0000FF),
    PINK(0xFFCCCC);

    fun containsRed() = (this.rgb and 0xFF0000 != 0)
}
```

宣告後我們就可以對變數正常存取

```kotlin
val red = Color.RED
println(Integer.toHexString(red.rgb)) // ff0000
println(red.containsRed()) // true
```

也可以直接宣告常數後存取

```kotlin
println(Color.BLUE.containsRed()) // false
println(Color.PINK.containsRed()) // true
```

------

想看更多範例嗎？

可以看看

- [Kotlin Data Class 範例](kotlin-data-class-example.md)
- [Kotlin 慣用寫法](idioms.md)
- [Kotlin 入門範例](kotlin-syntax.md)
- [Kotlin 的函數式編程慣用寫法](kotlin-functional-programming-example.md)
- [kotlin Data Class 範例](kotlin-data-class-example.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
