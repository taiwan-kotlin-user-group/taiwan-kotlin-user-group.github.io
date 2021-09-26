## 為什麼選擇 Kotlin


## 精簡

精簡的語法，讓閱讀與維護更加簡單。

建立 POJO（Plain Old Java Object）類別，用 `data class` 關鍵字即可

```kotlin
data class Customer(
    val name: String,
    val email: String,
    val company: String
)
```

建立單例模式（Singleton），用 `object` 關鍵字即可

```kotlin
object ThisIsASingleton {
    val name: String = "Taiwan Kotlin User Group"
}
```

### 函數式編程

引入函數式編程的語法，讓程式更精簡，也更好閱讀

過濾所有的正數

```kotlin
list.filter { it > 0 }
```

交換兩個變數

```kotlin
a = b.also { b = a }
```

## 安全

編譯階段就避免 `null` 產生問題

減少 `NullPointerException` 出現

讓程式出錯的機會更少

```kotlin
var output: String
output = null   // 無法通過編譯
```

```kotlin
val name: String? = null    // 刻意宣告 name 可以為 null
println(name.length())      // 無法通過編譯
```

-----

想了解更多嗎？

可以看看 

* [Kotlin 語法特色](kotlin-syntax.md)
* [Kotlin 慣用寫法](idioms.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
