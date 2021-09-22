# Kotlin 和 Javascript 的比較

對前端來說

雖然 Kotlin 可以編譯成 Javascript

但是總是覺得學習 Kotlin 很陌生

難以感覺到這麼做的好處

下面我們來比較一些 Kotlin 和 JavaScript 相似及相異的地方

讓大家可以比較一下

## 相似的地方

### `val`、`var`和 `const`、`let`
Kotlin 用 `val` 定義值（value）

用 `var` 定義可更動的變數（variable）
```kotlin
val a = 1
var b = 2
b = 42


// 編譯錯誤 Val cannot be reassigned
a = 42
```

類似 JavaScript 用 `const` 定義常數（constant）

用 `let` 定義變數
```js
const a = 1
let b = 2
b = 42


// Uncaught TypeError: Assignment to constant variable.
a = 42
```

### 函數為第一公民
兩個語言的函數

都可以作為參數或者回傳值

Kotlin
```kotlin
fun printResult(
    first: Int,
    second: Int,
    operation: (Int, Int) -> Int
) {
    println(operation(first, second))  
}  
  
val add = fun(a: Int, b: Int): Int {  
    return a + b  
}  
printResult(1, 2, add) // 3 
```

JavaScript
```js
function printResult(first, second, operation) {
    console.log(operation(first, second));  
}  
let add = function (a, b) {  
    return a + b;  
}  
  
printResult(1.0, 2.0, add); // 3
```

### 預設參數
兩個語言的函數

都可以加上預設參數

Kotlin
```kotlin
fun printResult(
    operation: (Int, Int) -> Int,
    first: Int = 0,
    second: Int = 0
) {  
    println(operation(first, second))  
}  
  
val add = fun(a: Int, b: Int): Int {  
    return a + b  
}  
printResult(add) // 0
```

JavaScript
```js
function printResult(operation, first = 0, second = 0) {
    console.log(operation(first, second));  
}  
let add = function (a, b) {  
    return a + b;  
}
  
printResult(add); // 0
```

### lambda function
兩個語言都支援匿名函數的寫法

Kotlin
```kotlin
val add = fun(a: Int, b: Int): Int {  
    return a + b  
}
```

JavaScript
```js
let add = function (a, b) {  
    return a + b;  
}
```

### arrow function
兩個語言都支援  arrow function 宣告匿名函數的寫法

Kotlin
```kotlin
val double: (Int) -> Int = { it * 2 }
```

JavaScript
```js
const double = num => num * 2;
```


### 不固定個數參數

兩個語言都支援函數可以收不固定個數參數

Kotlin 用 `vararg` 關鍵字來宣告

```kotlin
fun sum(vararg ts: Int): Int {
    var sum = 0
    for (t in ts) {
        sum += t
    }
    return sum
}

println(sum(1,2,3,4)) // 10
```

JavaScript 用 `...args` 來宣告
```javascript
function sum(...args) {
    let sum = 0;
    for (arg of args) {
        sum += arg;
    }
    return sum;
}
console.log(sum(1,2,3,4)); // 10
```

### async/await

兩個語言都支援 async/ await 語法

來處理非同步需求

Kotlin 使用 `suspend` 關鍵字和 `Deferred` 類別
```kotlin
import kotlinx.coroutines.*

suspend fun getUserGroup(): String {  
    delay(1000)  
    return "Kotlin User Group"  
}

fun main() {  
    runBlocking {  
        val group = async { getUserGroup()  }  
        println("Taiwan ")  
        println(group.await())  
    }  
}
// Taiwan
// Kotlin User Group
```

JavaScript 使用 `Promise` 物件
```js
function getUserGroup() {  
    return new Promise((resolve) => {  
        setTimeout(() => {
            resolve("Kotlin User Group");  
        }, 1000);  
    });  
}  
async function printUserGroup() {  
    const group = await getUserGroup();  
    console.log(group); // printed after 1 sec  
}  
printUserGroup();  
console.log("Taiwan");
// Taiwan
// Kotlin User Group
```

## 不同的地方
雖然 Kotlin 和 JavaScript 有不少相似處

兩個語言其實還是有很多不同的地方

下面列出一些個人覺得重要的部分

### 編譯語言 vs 直譯語言

Kotlin 是編譯語言

需要一個編譯的過程

才能產出可運行的內容

JavaScript 則是直譯語言

可以直接執行撰寫好的程式碼

------

雖然 Kotlin 多了一個編譯過程比較繁瑣

不過有個好處是

Kotlin 可以在運作之前就找出一部分程式撰寫的錯誤

```kotlin
var name = "Alice"  
println(Alice)
// 編譯錯誤 Unresolved reference: Alice
```

類似問題 JavaScript 會在運行階段

才會找出錯誤

### 不使用分號 vs 使用分號

Kotlin 預設不使用分號

使用換行作為語句結尾

```kotlin
// IDE 提示 Redundant semicolon 
val a = 1;
```

JavaScript 可以不用分號，但是有時會導致誤判

```js
1 + 1
-1 + 1 === 0 ? alert(0) : alert(2)
// alert(2)
// 等同 1 + 1 -1 + 1 === 0 ? alert(0) : alert(2)
```

### `fun` vs `function`

Kotlin 用 `fun` 關鍵字宣告函數

```kotlin
fun hello() {
    println("hello")
}
```

JavaScript 則是用 `function` 關鍵字宣告函數

```js
function hello() {
    console.log("hello");
}
```

### 強型別語言 vs 弱型別語言

Kotlin 是強型別語言

宣告函數參數時必須要撰寫回傳型態

```kotlin
fun add(a: Float, b: Float): Float {  
    return a + b  
}

add(0.1f + 0.2f) // 0.3
```

JavaScript 是弱型別語言

宣告函數時不需要撰寫型態

```js
function add(a, b) {
    return a + b;
}
```

撰寫時 JavaScript 比較方便

不過使用時如果沒有注意

可能會有意外的錯誤

```js
function add(a, b) {
    return a + b;
}

add(1.0, 2.0); // 3
add("1.0", "2.0"); // 1.02.0
add(0.1, 0.2); // 0.30000000000000004
```

### null-safe vs not null

Kotlin 為了避免 `null` 產生錯誤

變數預設是不會變成 `null` 的

```kotlin
var name: String = null
// 編譯錯誤 
// Null can not be a value of a non-null type String
```

即使有人使用可以為 `null` 的型態，編譯器也會進行檢查，避免對這個變數進行操作

```kotlin
val name: String? = null    // 刻意宣告 name 可以為 null
println(name.length())      // 無法通過編譯
```

JavaScript 通常需要針對變數是否為 `null` 進行檢查

```js
let name = null;
console.log(name.length);
// Uncaught TypeError: 
// Cannot read properties of null (reading 'length')
```

### extension function vs prototype

Kotlin 使用 extension function 的方式

來擴充原生型態的類別

```kotlin
fun Int.isEven():Boolean = this % 2 == 0 
println(42.isEven()) // true
```

JavaScript 則使用 prototype 的方式

```js
Number.prototype.isEven = function() {  
    return this % 2 === 0;  
};  
console.log((42).isEven()); // true
```


### 單行函數

Kotlin 允許單行函數的宣告方式

```kotlin
fun isEven(a: Int): Boolean = a % 2 == 0
```

JavaScript 目前不支援類似做法

### 命名參數

Kotlin 允許宣告函數時加上參數名稱

以提升程式可讀性

並可省略位置不在後面有預設值的參數

```kotlin
fun printResult(
    first: Int = 0,
    second: Int = 0,
    operation: (Int, Int) -> Int
) {  
    println(operation(first, second))  
}  
  
val add = fun(a: Int, b: Int): Int {  
    return a + b  
}  
printResult(operation=add) // 0
```

JavaScript 目前不支援類似做法

### Passing trailing lambdas

在  Kotlin 內，如果函數的最後一個參數為 lambda 函數，可以將這個函數的內容寫在 `{}` 內

```kotlin
fun printResult(  
    first: Int = 0,  
    second: Int = 0,  
    operation: (Int, Int) -> Int  
) {  
    println(operation(first, second))  
}  
printResult(1, 2) { a: Int, b: Int -> a + b } // 3
```

如果除了最後的 lambda 參數

其他參數均使用預設值

可以將 `()` 省略

```kotlin
fun printResult(  
    first: Int = 0,  
    second: Int = 0,  
    operation: (Int, Int) -> Int  
) {  
    println(operation(first, second))  
}  
printResult{ a: Int, b: Int -> a + b } // 0
```

JavaScript 目前不支援類似做法

------

這種方式在 Kotlin 前端應用上很常使用

可以用類似 Markup Language 的方式建立畫面

以 Ktor 框架舉例

```kotlin
get("/html-dsl") {  
    call.respondHtml {  
        body {  
            h1 { +"Taiwan Kotlin User Group" }  
            ul {  
                for (n in 1..10) {  
                    li { +"$n" }  
                }  
            }  
        }  
    }  
}
```

還有想知道的嗎？歡迎看看 [Kotlin 語法特色](kotlin-syntax.md) 的介紹！
