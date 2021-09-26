# Kotlin Scope Functions 範例

這邊我們介紹一些 Kotlin 的 scope function

## let

`let()` 會在 `{}` 直接用 `it` 存取內文物件

並回傳 `{}` 執行之後的結果

舉例來說，原先我們的程式

```kotlin
val numbers = listOf(1, 2, 3)  
println(numbers) 
```

可以改寫成

```
listOf(1, 2, 3)  
    .let { println(it) }
```

由於我們 `let()` 裡面只有一行 `println(it)`

我們可以直接呼叫 `let()` 

並將 `::println` 視為參數傳進去

```
listOf(1, 2, 3)  
    .let(::println)
```

`let()` 很常用在判斷某變數不是 `null` 才往下執行

比方說

```kotlin
if (name != null) {
	println(name.length)
}
```

可以改寫成

```kotlin
name?.let { println(it.length) }
```

可讀性大大提升

直接讀成「name exist? LET'S print it's length.」

## run

`run()` 跟 `let()` 很相近

不過 `run()` 存取內文物件的關鍵字是 `this`

可以不用透過 `it` 來存取內文物件

當我們希望能呼叫被呼叫物件的函數時

這會讓程式更簡潔易懂

原本這樣寫的程式

```kotlin
println(2.let { it.toFloat() })
```

可以簡化成

```kotlin
println(2.run { toFloat() })
```

## with

`with()` 函數的內文物件放在 `()` 裡面

傳輸到 `{}`  執行過後

回傳執行後的結果。

在 `with()` 的 `{}` 裏面

存取物件的關鍵字是 `this`，

可以不用透過 `it` 來存取被宣告的物件

可以用來執行不需回傳值的邏輯

唸成 「WITH this, DO the following 」

舉例來說

```kotlin
data class Pet(var name: String, var age: Int=0)  
  
val pet = Pet(name="Luna")  
with(pet) { println(name) }
```

直接讀成「with pet, print (it's) name.」

## apply
`apply()` 函數存取物件的關鍵字是 `this`

傳輸到 `{}`  執行過後

回傳內文物件本身。

由於執行後回傳的是物件本身

所以 `apply()` 預期 `{}` 內執行後不會有回傳值

如果我們嘗試在 `{}` 內進行回傳，會出現錯誤 

```kotlin
var a = 2  
var b = 1
a.apply { return b } 
// Type Mismatch 
// Required: Unit
// Found: Int
```

這可能會產生一點疑惑：

如果不取得 `{}` 執行內容的話

那麼 `apply()` 要用在哪種情境呢？

`apply()` 可以用在設置物件上

可以讓程式碼更簡潔

假設我們之前的邏輯是

```kotlin
data class Pet(var name: String, var age: Int=0)  
  
val pet = Pet(name="Luna")
// 改名和設置年紀
pet.name = "Bella"
pet.age = 1
```

可以用 `apply()` 改寫成

```kotlin
data class Pet(var name: String, var age: Int=0)  
  
val pet = Pet(name="Luna")
// 改名和設置年紀
pet.apply {
	name="Bella"
	age=1
}
```

這也很符合 `apply` 這個字的語意。

## also

`also()` 和 `apply()` 有個相似的部分

就是執行過後，都是回傳物件本身。

不同的地方是，`also()` 內用 `it` 存取內文物件。

這在需要將內文物件變成參數時，可以讓程式變得更簡短。

以前的

```kotlin
var list = mutableListOf(1, 2)  
list.add(3)  
list.remove(1)  
list = list.map { it * 10 }.toMutableList()  
println(list) // [20., 30]
```

可以變成這樣寫

```kotlin
mutableListOf(1, 2).apply {  
    add(3)  
    remove(1)  
}.map { it * 10 }.also { println(it) }
```

另外也可以用在變數對調

```kotlin
var a = 1  
var b = 2  
a = b.also { b = a }
println("$a, $b") // 2, 1
```

------

想看更多範例嗎？

可以看看 

* [Kotlin 入門範例](kotlin-syntax.md)
* [Kotlin 的函數式編程慣用寫法](kotlin-functional-programming-example.md)


或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
