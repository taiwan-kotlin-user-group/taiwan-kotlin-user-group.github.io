## Kotlin Data Class 範例

宣告 data class

```kotlin
data class Customer(
    val name: String,
    val email: String
)
```

### toString()
data class 內建 `toString()`

可以直接印出所有屬性內容

```kotlin
val alice = Customer("Alice", "alice@gmail.com")
println(alice)
// Customer(name=Alice, email=alice@gmail.com)
```

### hashCode()
data class 內建 `hashCode()` 

如果兩個 `Customer` 屬性一樣

`hashCode` 回傳的值也會一樣

```kotlin
val alice = Customer("Alice", "alice@gmail.com")  
val alice2 = Customer("Alice", "alice@gmail.com")  
val bob = Customer("Bob", "alice@gmail.com")  
println(alice.hashCode()) // 262425105
println(alice2.hashCode())  // 262425105
println(bob.hashCode()) // -1699360388
```

### copy()

data class 內建 `copy()` 

可以快速複製物件

```kotlin
val alice = Customer("Alice", "alice@gmail.com")
val alice2 = alice.copy()
println(alice)
// Customer(name=Alice, email=alice@gmail.com)
println(alice2)
// Customer(name=Alice, email=alice@gmail.com)
```

`copy()` 可以接收參數

允許在複製時改變部分參數值

```kotlin
val alice = Customer("Alice", "alice@gmail.com")  
val alice2 = alice.copy(email = "alice2@gmail.com")  
println(alice)
// Customer(name=Alice, email=alice@gmail.com)
println(alice2)
// Customer(name=Alice, email=alice2@gmail.com)
```

### componentN() 

data class 內建 `component1()`、`component2()`⋯⋯

可以根據宣告的順序存取屬性值

```kotlin
val alice = Customer("Alice", "alice@gmail.com")  
println(alice.component2()) // alice@gmail.com
```

### 覆寫

覆寫一些原有函數

可以讓後續撰寫的邏輯更直觀

比方說我們認定同 `name` 不同 `email` 可以視為同一人

可以覆寫 `equals`

```kotlin
data class Customer(
    val name: String,
    val email: String
) {
    override fun equals(other: Any?) =
        other is Customer && other.name == this.name
}
```

後面的程式就可以直接套用此邏輯

```kotlin
val alice = Customer("Alice", "alice@gmail.com")
val alice2 = Customer("Alice", "alice2@gmail.com")
println(alice == alice2) // true
```

-----

想看更多範例嗎？

可以看看

* [Kotlin 慣用寫法](idioms.md)
* [Kotlin 入門範例](kotlin-syntax.md)
* [Kotlin 的函數式編程慣用寫法](kotlin-functional-programming-example.md)


或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
