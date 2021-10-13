## Kotlin 的協變和反變

### 泛型需要補充的地方

Kotlin 的泛型（generic）非常好用

我們可以在撰寫函數時

先不定義參數的型別

使用時才定義

```kotlin
class Box<T>(t: T) { var content = t }

val box = Box(1)  
val box2 = Box(1.0)  
println(box.content::class.simpleName) // Int
println(box2.content::class.simpleName) // Double
```

不過有的情境下

泛型定義會有不夠充分的地方

需要加上其他的方式補充

### 協變（Covariance）

假設我們定義

```kotlin
interface Box<T> {  
    fun setBoxContent(content: T)  
    fun getBoxContent(): T  
}
```

利用 `Box` 介面我們嘗試定義以下函數

```kotlin
fun demo(box: Box<Int>) {  
    val bigBox: Box<Number> = box  
}
```

這段程式會無法通過編譯

因為 `Number` 是 `Int` 的父類別（parent class）

如果我們後續呼叫

```kotlin
bigBox.setContent(1.0)
```

嘗試將 `Double` 寫入 `Box<Int>`

就會導致出錯

在 Kotlin 內，我們可以透過將泛型宣告成 `out T`

並移除包含參數輸入的 `setContent()`

來避免這個問題

```kotlin
interface Box<out T> {  
    fun getBoxContent(): T  
}  
  
  
fun demo(box: Box<Int>) {  
    val bigBox: Box<Number> = box
}
```


### 反變（Contravariance）

假設我們定義

```kotlin
interface Box<T> {  
    fun setBoxContent(content: T)  
    fun getBoxContent(): T  
}
```

利用 `Box` 介面我們嘗試定義以下函數

```kotlin
fun demo(box: Box<Number>) {  
    val bigBox: Box<Int> = box  
}
```

這段程式一樣會無法通過編譯

因為如果我們後續呼叫

```kotlin
bigBox.getBoxContent()
```

我們可能會拿到某個繼承 `Number` 類別的物件

但是不一定會拿到 `Box<Int>` 呼叫 `getBoxContent()` 

預期拿到的 `Int`

在 Kotlin 內，我們可以透過將泛型宣告成 `in T`

並移除包含參數輸出的 `getContent()`

來避免這個問題

```kotlin
interface Box<in T> {
    fun setBoxContent(content: T)  
}  
  
  
fun demo(box: Box<Number>) {
    val bigBox: Box<Int> = box  
}
```

## 實際應用

在 Kotlin 內 `Comparable` 介面的宣告為

```kotlin
public interface Comparable<in T> {
    public operator fun compareTo(other: T): Int
}
```

這樣的宣告允許以下寫法

```kotlin
fun demo(comparable: Comparable<Number>) {  
    val smallComparable: Comparable<Int> = comparable  
}
```


## 總結

`out` 關鍵字，用來定義參數僅能輸出

允許我們將比較「小」的型別（`Box<Int>`）

指派給比較「大」的型別（`Box<Number>`）

-----

`in` 關鍵字，用來定義參數僅能輸入

允許我們將比較「大」的型別（`Box<Number>`）

指派給比較「小」的型別（`Box<Int>`）

-----
想看更多範例嗎？

可以看看

- [Kotlin 慣用寫法](idioms.md)
- [Kotlin 入門範例](kotlin-syntax.md)
- [Kotlin 的函數式編程慣用寫法](kotlin-functional-programming-example.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
