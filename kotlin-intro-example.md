## Kotlin 入門範例
下面提供 Kotlin  的一些入門範例

## Hello world
```kotlin
fun main() {                        
    println("Hello, World!")
}
```

Kotlin 程式的進入點是 `main()` 函數
 
`main()` 可以不宣告參數和回傳值
 
`println()` 印出一段文字並換行
 
該特別注意的是， 程式每行結尾建議不加分號
 
## 函數
 
```kotlin
fun printMessage(message: String): Unit {
	println(message)
}
```
 
宣告函數的關鍵字為 `fun`

每個參數都需要宣告型態

如果沒有回傳值，可以標記為 `Unit` 或不標記回傳值型態
 
### 預設參數
 
```kotlin
fun printWelcomeMessage(name: String = "World") {
	println("Hello $name!")
}
```
 參數 `name` 預設值為 `"World"`

### 單行函數

```kotlin
fun multiply(x: Int, y: Int) = x * y
```

省略回傳型態

實際回傳型態由編譯器協助推斷

### 內綴函數
用 `infix` 關鍵字宣告

```kotlin
infix fun Int.plus(number: Int) = this + number
```

使用方式如下

```kotlin
2 plus 2 // 4
```

也可以宣告在類別裡面，讓程式更易讀

```kotlin
class Person(val name: String) {
    val likedPeople = mutableListOf<Person>()
    infix fun likes(other: Person) {
        likedPeople.add(other) 
	}
}

val alice = Person("Alice")
val bob = Person("Bob")
alice likes bob    
```
 
### 參數不固定個數
利用 `vararg` 關鍵字，可以建立沒有固定個數參數的函數
 
```kotlin
fun helloAllPeople(vararg names: String) {
    for (name in names) {
	    println("Hello $name")
	}
}
```

可以把 `names` 視為 `Array<String>` 進行操作

函數的呼叫方式如下

```kotlin
helloAllPeople("Alice", "Bob", "Carol", "Dave")
```

如果你剛好有一群元素要放入這個函數，可以利用 `*` 前綴

```kotlin
val boys = arrayOf("Bob", "Dave")  
helloAllPeople("Alice", *boys, "Carol")
```

## 變數

用 `val` 關鍵字宣告不可更動的值（value）

用 `var` 關鍵字宣告可更動的變數（variable）

```kotlin
val num: Int = 1 
var init: String = "initial"
```

沒有特別宣告的話

Kotlin 會對變數型態進行推斷

```kotlin
var num = 1 // 判斷 num 為 Int
num = "two" // Type mismatch.
```

如果一開始沒有對 `var` 給值

在嘗試讀取該變數時會出現錯誤

```kotlin
var name: String
println(name) // Variable 'name' must be initialized
```
## Null Safety
 
Kotlin 預設變數型態不接受 `null`

```kotlin
var name: String  
name = null // 編譯錯誤
```
 
嘗試對可接受 `null` 的變數進行操作
 
會出現編譯錯誤
 
```kotlin
var name: String? = "Alice"  
name.length // 編譯錯誤
name?.length // 編譯成功
```

## 類別

宣告類別用 `class` 關鍵字

特別注意建立物件時不使用 `new` 關鍵字

```kotlin
class Customer

val customer = Customer()
```

宣告類別屬性

```kotlin
class Contact(val id: Int, var email: String)
val contact = Contact(1, "alice@gmail.com")
```

存取屬性

```kotlin
contact.id
```

更新屬性

```kotlin
contact.email = "bob@gmail.com"
```
 
## 泛型

舉例來說，一個列表 `List` 的取出物件 `get()` 邏輯

和內含的元素本身是獨立的

這類函數在宣告時可以不定義元素的型態

我們可以用泛型（generics）的方式來處理

舉例，我們建立一個自己的 `Stack` 類別

```kotlin
class Stack<E>(vararg items: E) {
}
```

會在建立物件時定義 `E` 的類別

```kotlin
Stack(1, 2, 3) // Stack<Int>
Stack("Alice", "Bob") //Stack<String>
```
 
### 泛型函數

類似的邏輯也可以用在函數上

```kotlin
fun <E> getList(a: E, b: E) = listOf(a, b)
```

會在呼叫時定義 `E` 的類別

```kotlin
getList(1, 2, 3) // List<Int>
getList("Alice", "Bob") // List<String>
```

## 繼承

Kotlin 預設類別不可被繼承

如果希望某個類別可以被繼承

要透過 `open` 關鍵字標記

再透過 `:` 符號處理繼承

```kotlin
open class Animal {  
    open fun say() {  
    }  
}  
class Dog: Animal() {  
    override fun say() {  
        println("Woof")  
    }  
}  
Dog().say() // Woof
```
----

想了解更多嗎？

可以看看 

* [Kotlin 語法特色](kotlin-syntax.md)
* [Kotlin 慣用寫法](idioms.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
