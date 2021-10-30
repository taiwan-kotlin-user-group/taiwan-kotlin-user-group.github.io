## Kotlin 專案命名常規

### 套件命名
套件（package）命名使用小寫

不使用底線（`org.example.project`）。

通常不鼓勵在命名內使用超過一個單字

如果必須使用的話，可以直接連在一起

或使用駝峰式命名（`org.example.myProject`）。

### 類別命名

類別（class）或物件（object）命名

使用大寫開頭的駝峰式命名：

```kotlin
open class DeclarationProcessor { /*...*/ }

object EmptyDeclarationProcessor : DeclarationProcessor() { /*...*/ }
```

### 函數命名

函數、屬性、本地變數的命名

使用小寫開頭的駝峰式命名，不使用底線：

```kotlin
fun processDeclarations() { /*...*/ }
var declarationCount = 1
```

例外：建立實體用的工廠函數（factory function）

可以直接使用抽象回傳型態

作為函數名稱：


```kotlin
interface Foo { /*...*/ }

class FooImpl : Foo { /*...*/ }

fun Foo(): Foo { return FooImpl() }
```

### 測試函數命名

在測試內，並且**僅可以**在測試內

可以使用包含空格的命名 

並以「\`」符號包圍函數名稱

注意：這種命名方式在 Android 運行上不支援

測試程式碼也允許函數名稱內使用底線

```kotlin
class MyTestCase {
     @Test fun `ensure everything works`() { /*...*/ }
     
     @Test fun ensureEverythingWorks_onAndroid() { /*...*/ }
}
```

### 屬性命名

常數，也就是以 `const` 標記的屬性

或者包含不可更動資料，最頂層的屬性或物件

應使用全大寫，以底線分隔的命名方式（[screaming snake case](https://en.wikipedia.org/wiki/Snake_case)）：

```kotlin
const val MAX_COUNT = 8
val USER_NAME_FIELD = "UserName"
```

Names of top-level or object properties which hold objects with behavior or mutable data 

應使用小寫開頭的駝峰式命名：

```kotlin
val mutableCollection: MutableSet<String> = HashSet()
```

屬性用來儲存針對單例物件的參照時

可以使用 `object` 宣告的命名方式：

```kotlin
val PersonComparator: Comparator<Person> = /*...*/
```

### 列舉常數命名

列舉（enum）常數的命名

依據使用場景

可使用使用全大寫，以底線分隔的命名方式（[screaming snake case](https://en.wikipedia.org/wiki/Snake_case)）：

```kotlin
enum class Color { RED, GREEN }`
```

或者使用大寫開頭的駝峰式命名：

```kotlin
enum class Color { Red, Green }`
```
 
   
### 暫存屬性命名

如果類別內有兩個屬性

兩個屬性基本相同

一個來自外部傳入

另一個則是本地的私有屬性

可以在本地的私有屬性名稱前加上底線標記：

```kotlin
class C {
    private val _elementList = mutableListOf<Element>()

    val elementList: List<Element>
         get() = _elementList
}
```

### 選擇好名稱

類別的名稱一般是名詞或名詞子句

解釋這個類別**是什麼**：
- `List`
- `PersonReader`

方法（method）的名稱一般是動詞或動詞子句

解釋這個方法**做什麼**：
- `close`
- `readPersons`

#### 方法行為

方法的命名應該要能看出是否會更動傳入的物件

比方說 `sort` 會將傳入的集合排序好

`sorted` 則應該不更動原有集合

回傳一個排序好的集合複本

#### 目的

命名應該要能清楚地看出目的

所以最好避免無意義的單字

比方說 `Do`，`Wrapper`

#### 縮寫
使用縮寫時

如果縮寫是兩個字母

應使用全大寫

比方說 `IOStream`

如果縮寫超過兩個字母

則不應使用全大寫

比方說 `XmlFormatter`，`HttpInputStream`

-----

更多命名範例

請參考 [不好的 Kotlin 專案命名範例](kotlin-bad-naming-example.md) 進行對比

-----

想看更多範例嗎？

可以看看

- [Kotlin 慣用寫法](idioms.md)
- [Kotlin 入門範例](kotlin-syntax.md)
- [Kotlin 的函數式編程慣用寫法](kotlin-functional-programming-example.md)
- [Kotlin Data Class 範例](kotlin-data-class-example.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
