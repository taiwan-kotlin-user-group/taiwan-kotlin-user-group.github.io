## Kotlin 中綴函數範例
### 什麼是中綴

我們很常使用前綴（prefix），像是 **hyper**active

和使用後綴（suffix），像是 sad**ness**

中綴（infix）的意思和前綴後綴類似

不過是夾在詞彙的中間，所以稱為中綴

### 中綴函數

在 Kotlin 內

可以宣告中綴函數

讓程式的語意化更加提升

比方說我們想加入一個中綴函數 `add`

可以這樣宣告

```kotlin
infix fun Int.add(x: Int) = this + x
```

這樣一來，程式就可以這樣撰寫

```kotlin
println(2 add 2) // 4
println(2.add(2)) // 對等的寫法
```

### 實際案例
#### 位元操作
Kotlin 的位元操作上

使用非常多的中綴函數

```kotlin
println(1 and 0) // 0
println(1 or 0) // 0
println(1 xor 0) // 1
```

#### 建立 `Pair` 物件
在[Kotlin 慣用寫法](idiom.md)內

提到建立唯讀 map 的慣用寫法是

```kotlin
val map = mapOf("a" to 1, "b" to 2, "c" to 3)
```

裡面的 `to` 就是一個中綴函數

可以快速建立 Kotlin 的 `Pair` 物件

```kotlin
public infix fun <A, B> A.to(that: B): Pair<A, B> 
    = Pair(this, that)
```

-----
想看更多範例嗎？

可以看看

- [Kotlin 入門範例](kotlin-syntax.md)
- [Kotlin 的函數式編程慣用寫法](kotlin-functional-programming-example.md)
- [Kotlin Data Class 範例](kotlin-data-class-example.md)
- [Kotlin Scope Function 範例](kotlin-scope-function-example.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
