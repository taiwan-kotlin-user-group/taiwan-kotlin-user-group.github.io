## Kotlin 慣用寫法

下面列出一些常見的 Kotlin 慣用寫法

## 建立 DTO 
建立 DTO 

（或稱 POJO，Plain Old Java Object）

```kotlin
data class Customer(val name: String, val email: String)
```

建立 `Customer` 類別

並包含下列函數：

* 內含屬性的 getter
* 如果屬性為 `var` 會包含 setter
* `equals()`
* `hashCode()`
* `toString()`
* `copy()`
* 對應屬性順序的 `component1()`、`component2()`⋯⋯

## 函數參數的預設值

```kotlin
fun foo(a: Int = 0, b: String = "") { ... }
```

## 過濾 list

```kotlin
val positives = list.filter { x -> x > 0 }
```

更短的寫法

```kotlin
val positives = list.filter { it > 0 }
```

## 確認某元素是否出現在集合內

```kotlin
if ("john@example.com" in emailsList) { ... }

if ("jane@example.com" !in emailsList) { ... }
```

## 字串樣板

```kotlin
println("Name $name")
```

## 檢查變數型態

```kotlin
when (x) {
    is Foo -> ...
    is Bar -> ...
    else   -> ...
}
```

## 建立唯讀 list

```kotlin
val list = listOf("a", "b", "c")
```

## 建立唯讀 map

```kotlin
val map = mapOf("a" to 1, "b" to 2, "c" to 3)
```

## 存取 map

```kotlin
println(map["key"])
map["key"] = value
```

## 遍歷 map

```kotlin
for ((k, v) in map) {
    println("$k -> $v")
}
```

也可用來遍歷元素為 `Pair` 型態的 list

```kotlin
val list = listOf(  
    Pair("name", "Alice"),   
    Pair("age", 18)  
)  
for ((k, v) in list) {  
    println("$k -> $v")  
}
```

`k` 和 `v` 都可以換成可讀性更高的名稱

像是 `name` 和 `age`

## 某範圍內迴圈

從 1 到 100
```kotlin
for (i in 1..100) { ... }
```

從 1 到 99，不包含 100
```kotlin
for (i in 1 until 100) { ... }
```

2 4 6 8 10
```kotlin
for (x in 2..10 step 2) { ... }
```

從 10 到 1
```kotlin
for (x in 10 downTo 1) { ... }
```

## 某範圍內判斷

```kotlin
if (x in 1..10) { ... }
```

## Lazy property

```kotlin
val p: String by lazy {
    // compute the string
}
```

## 擴充函數
可在原生型態上增添新函數

```kotlin
fun String.spaceToCamelCase() { ... }

"Convert this to camelcase".spaceToCamelCase()
```

## 建立單例
建立單例（singleton）

```kotlin
object Resource {
    val name = "Name"
}
```

## 實例化抽象類別

```kotlin
abstract class MyAbstractClass {
    abstract fun doSomething()
    abstract fun sleep()
}

fun main() {
    val myObject = object : MyAbstractClass() {
        override fun doSomething() {
            // ...
        }

        override fun sleep() { // ...
        }
    }
    myObject.doSomething()
}
```

## If-not-null 縮寫
如果 `files` 不為 `null`

印出 `files.size`

```kotlin
println(files?.size)
```

## If-not-null-else 縮寫
如果 `files` 不為 `null`

印出 `files.size`

如果 `files` 為 `null`

印出 `"empty"`

```kotlin
println(files?.size ?: "empty")
```

## 為 `null` 執行特定行為
如果 `values["email"]` 為 `null`

拋出例外 `IllegalStateException("Email is missing!")`

```kotlin
val email = values["email"] ?: throw IllegalStateException("Email is missing!")
```

## 在可能為空的集合取出第一個元素

`emails` 為 `List<String>`

如果集合為空，則取出預設物件（`""`）

```kotlin
val mainEmail: String = emails.firstOrNull() ?: ""
```

## 變數不為 `null` 時執行

```kotlin
value?.let {
    // 變數不為 null 時執行此段落
}
```

## Map nullable value if not null

假設 `value` 型態是 `Int?`

`mapped` 轉換成 `List<Int>`

如果 `value` 是 `null`

把 `mapped` 設置為 `listOf(0)`

```kotlin 
val mapped = value?.let { listOf(it) } ?: listOf(0)
```

## 回傳 when 表達式

```kotlin
fun transform(color: String): Int {
    return when (color) {
        "Red" -> 0
        "Green" -> 1
        "Blue" -> 2
        else -> throw IllegalArgumentException("Invalid color")
    }
}
```

## try-catch 表達式
在 Kotlin `try-catch` 是表達式

回傳結果可以直接寫入變數

```kotlin
fun test() {
    val result = try {
        count()
    } catch (e: ArithmeticException) {
        throw IllegalStateException(e)
    }

    // Working with result
}
```

## if 表達式
在 Kotlin `if` 是表達式

回傳結果可以直接寫入變數

```kotlin
fun foo(param: Int) {
    val result = if (param == 1) {
        "one"
    } else if (param == 2) {
        "two"
    } else {
        "three"
    }
}
```

## 利用回傳 `Unit` 函數的生成器模式

`fill()` 的回傳值是 `Unit`

（對等其他語言的回傳 `void`）

下面建立大小為 `size`

全部值為 `-1` 的 `IntArray`

```kotlin
fun arrayOfMinusOnes(size: Int): IntArray {
    return IntArray(size).apply { fill(-1) }
}
```

## 單一表達式的函數

```kotlin
fun theAnswer() = 42
```

上面等同於

```kotlin
fun theAnswer(): Int {
    return 42
}
```

單一表達式函數搭配上其他慣用寫法

可以寫出更簡潔的程式

例如搭配上 `when` 表達式

```kotlin
fun transform(color: String): Int = when (color) {
    "Red" -> 0
    "Green" -> 1
    "Blue" -> 2
    else -> throw IllegalArgumentException("Invalid color")
}
```

## 對某物件內多個函數進行呼叫

利用 `with()`

```kotlin
class Turtle {
    fun penDown()
    fun penUp()
    fun turn(degrees: Double)
    fun forward(pixels: Double)
}

val myTurtle = Turtle()

// 畫出大小 100 畫素的正方形
with(myTurtle) { 
    penDown()
    for (i in 1..4) {
        forward(100.0)
        turn(90.0)
    }
    penUp()
}
```

## 設定物件屬性

利用 `apply()`

```kotlin
val myRectangle = Rectangle().apply {
    length = 4
    breadth = 5
    color = 0xFAFAFA
}
```

在處理沒有出現在建構子內的屬性時

非常方便的寫法

## Java 7 的 try-with-resources

```kotlin
val stream = Files.newInputStream(Paths.get("/some/file.txt"))
stream.buffered().reader().use { reader ->
    println(reader.readText())
}
```

## 需要泛型類別資訊的泛型函數

假設 `Gson` 和 `Gson.fromJson()`

的宣告為

```java
public final class Gson {
    // ...
    public <T> T fromJson(JsonElement json, Class<T> classOfT) throws JsonSyntaxException {
    // ...
```

使用時我們會需要 `Class<T>` 的資訊

利用 `inline fun` 和 `reified` 關鍵字

我們可以讓泛型函數內

取得泛型參數的類別資訊

```kotlin
inline fun <reified T: Any> Gson.fromJson(json: JsonElement): T = this.fromJson(json, T::class.java)
```

這邊 `<T>` 型態是 `Any`

可以放入任意類別

使用起來非常簡潔

```kotlin
Gson.fromJson<MyDataClass>(json)
```

## 可為 `null` 的 Boolean

```kotlin
val b: Boolean? = ...
if (b == true) {
    ...
} else {
    // `b` 為 false 或 null
}
```

## 交換變數

```kotlin
a = b.also { b = a }
```

## 標記程式未完成
 
利用 `TODO()` 函數

`TODO()` 執行時會拋出 `NotImplementedError` 中斷程式

`TODO()` 的回傳值是 `Nothing`

所以可以無視函數設定的回傳值

`TODO()`內可以宣告理由

```kotlin
fun calcTaxes(): BigDecimal = TODO("等會計部門回需求")
```

IntelliJ IDEA 的 kotlin plugin 認得 `TODO()`

並會自動將內容放在 TODO 工具視窗內

-----

想了解更多嗎？

可以看看 [Kotlin 語法特色](kotlin-syntax.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
