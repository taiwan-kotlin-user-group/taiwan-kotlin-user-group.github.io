# Kotlin 的函數式編程慣用寫法

下面列出 Kotlin 的函數式編程慣用寫法

## 以其他函數做參數

在 Kotlin 內我們可以定義函數

```kotlin
fun plus(x: Int, y: Int) = x + y
```

由於 Kotlin 內的函數是可以當參數或回傳值的

所以也可以設計出

接收 `(Int, Int) -> Int` 的函數作為參數

的函數

```kotlin
fun calc(x: Int, y: Int, opr: (Int, Int) -> Int) = opr(x, y)
```

使用方法如下

```kotlin
val plus = fun (x: Int, y: Int) = x + y  
calc(2, 2, plus) // 4
```

如果不想使用匿名函數的做法

也可以用 `::` 符號

```kotlin
fun plus(x: Int, y: Int) = x + y
calc(2, 2, ::plus) // 4
```

如果某個函數的最後一個參數，剛好是一個函數

可以直接將函數寫在 `{}` 內

```
calc(2, 2) { x, y -> x + y } // 4
```


## 以其他函數做回傳值

我們也可以設計某個函數

會將函數做為回傳值

```kotlin
fun plus(x: Int, y: Int) = x + y  
fun add(): (Int, Int) -> Int = ::plus

val opr = add()
opr(2, 2) // 4
```

## 匿名函數

我們可以直接宣告一個沒有名稱的函數

然後傳入變數

特別注意變數的型態如何宣告

```kotlin
fun plus(x: Int, y: Int) = x + y
val plusOne: (Int) -> Int = {x: Int -> plus(x, 1)}
plusOne(2) // 3
```

Kotlin 可以透過型態推斷，得知 `plusOne` 的型態

所以可以省略

```kotlin
val plusOne = {x: Int -> plus(x, 1)}
```

也可以反過來利用型態推斷

省略 `x` 的型態

```kotlin
val plusOne: (Int) -> Int = {x -> plus(x, 1)}
```

像這樣只有一個參數的匿名函數

我們可以用 `it` 取代掉參數的宣告

```kotlin
val plusOne:(Int) -> Int = { plus(it, 1) }
```

如果匿名函數內只有一個其他函數

可以用 `::` 符號取得

```kotlin
val add = ::plus
```

-----

想了解更多 Kotlin 的寫法嗎？

可以看看 [Kotlin 慣用寫法](idioms.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
