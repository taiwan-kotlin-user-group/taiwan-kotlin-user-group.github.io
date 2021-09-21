# Kotlin 語法特色

以下來分享一些我們認為 Kotlin 語法上值得關注的特色

## data class
用 `data` 宣告純資料物件（POJO，Plain Old Java Object）

看起來更加簡潔
```kotlin
data class Customer(
    val name: String,
    val email: String
)
/*
Java 寫法
public class Customer {
 	public String name; 
 	public String email;
	
	public Customer(String name, String email) {
		this.name = name;
		this.email = email;
	}
	
	public String name() { 
	 	return this.name;
	}
	
	public String email() { 
	 	return this.email; 
	}
	// ...
}
*/
```
## var and val
用 `val` 宣告不可更改的值

用 `var` 宣告可以更改的變數

讓意外更動常數的機會降低

```kotlin
val a = 1
var b = 2
b = 42


// 編譯錯誤 Val cannot be reassigned
a = 42
```

## fun vs function
用 `fun` 關鍵字宣告函數

看起來更加簡潔

```kotlin
fun main() {
}

/*
等同 Java
public static void main() {
}
*/
```

## default class are final
類別宣告預設為 `final`

避免超長繼承鏈的出現

```kotlin
class Base(p: Int) 


/*編譯錯誤
This type is final, so it cannot be inherited from
*/
class Derived(p: Int) : Base(p)
```

## `:` vs extends
使用 `:` 宣告繼承

看起來更加簡潔

```kotlin
open class Base(p: Int) 

class Derived(p: Int) : Base(p)
```

## no semicolon
不用分號做結尾

看起來更簡潔

也避免常見的漏打分號錯誤

```kotlin
val a = 1


// IDE 提示 Redundant semicolon 
val a = 1;
```

## single return can skip curly brackets
如果函數只有單行

可省略 `{}` 

看起來更加簡潔

```kotlin
fun double(x: Int): Int = x * 2

/*
等同於
fun double(x: Int): Int {
	return x * 2 
}
*/
```
## if expression
Kotlin 的 `if` 是表達式

可以直接用在變數賦值

```kotlin
val c = if (a > b) a else b
```

`if` 還可以直接放在函數回傳內

搭配上單行函數的寫法更加簡潔

```kotlin
fun bigger(a: Int, b: Int) = if (a > b) a else b
```
## when expression
引入 `when` 表達式

比起 `switch` 更好看懂

並且避免常見的漏打 `break;` 錯誤

```kotlin
when (x) {
    1 -> println("x == 1")
    2 -> println("x == 2")
    else -> {
        println("x is neither 1 nor 2")
    }
}
/*
等同 Java
switch(x) {
  	case 1:
		System.out.println("x == 1");
    break;
  	case 2:
    	System.out.println("x == 2");
    break;
  	default:
		System.out.println("x is neither 1 nor 2");
}
*/
```

`when` 和 `if` 一樣可以直接用在變數賦值

```kotlin
val state = when (x % 3) {  
    0 -> "is a multiple of 3"  
 	1 -> "divided by 3 have remainder of 1"  
 	2 -> "divided by 3 have remainder of 2"  
 	else -> {  
        throw ArithmeticException("impossible!!") 
    }  
}
```

也可以直接放在函數回傳內

```kotlin
fun getState(x: Int): String = when (x % 3) {  
    0 -> "is a multiple of 3"  
 	1 -> "divided by 3 have remainder of 1"  
 	2 -> "divided by 3 have remainder of 2"  
 	else -> {  
        throw ArithmeticException("impossible!!")  
    }  
}
```
## Singleton object
用 `object` 關鍵字宣告單例物件

看起來更加簡潔

```kotlin
object ThisIsASingleton {
    val name: String = "Taiwan Kotlin User Group"
}
/*
Java 寫法
public class ThisIsASingleton {  
    private static final ThisIsASingleton instance = new ThisIsASingleton();  
 	private static final String name = "Taiwan Kotlin User Group";  
 	private ThisIsASingleton(){}  
    public static ThisIsASingleton getInstance() {  
        return instance;  
 	}  
}
*/
```
## Elvis Operator
引入 `?.` 和 `?:`

讓程式可以寫得更簡潔

```kotlin
val b = a?.length ?: -1
// 等同 val b: Int = if (a != null) a.length else -1
```
## Type Inference
Kotlin 可以在編譯時推理變數型態

讓程式不需宣告型態

寫法更加簡潔
```kotlin
val str = "hello"
// 等同 val str : String = "hello"
```
## Type Aliases
引入 `typealias` 關鍵字

讓程式語意更清晰

```kotlin
typealias CreditCardNumber = String
val aliceCardNumber: CreditCardNumber = "1234****"
```

## Named Arguments
可在呼叫函數時使用參數命名

讓程式的語意更清晰

並避免順序錯誤導致程式錯誤

```kotlin
fun reformat(
    str: String,
    normalizeCase: Boolean = true,
    upperCaseFirstLetter: Boolean = true,
    divideByCamelHumps: Boolean = false,
    wordSeparator: Char = ' ',
) { /*...*/ }

reformat(
    "String!",
    normalizeCase = false,
    upperCaseFirstLetter = false,
    divideByCamelHumps = true,
    wordSeparator = '_'
)
```

參數命名也讓我們可省略所有含預設值參數

只列出我們需要更動的參數

```
reformat("String!", upperCaseFirstLetter = false)

/*
等同
reformat(
    "String!",
    true,
    false,
    false,
    ' '
)
*/
```

## Null Check

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
## Pretty Lambda
好閱讀的 lambda 函數宣告法

讓程式邏輯易懂又好讀

```kotlin

val printInteger = fun Int.() { println(this) }  
numbers.forEach { printInteger(it) }

/*
等同 Java
import java.util.function.Consumer;

Consumer<Integer> printInteger = (n) -> { System.out.println(n); };
    numbers.forEach( printInteger );
*/
```
## String Interpolation
字串樣板讓程式在字串處理時更加易懂

且不容易出現空白錯誤

```kotlin
val bestLanguage = "Kotlin"
println("Taiwan $bestLanguage User Group")

/*
等同 Java
String bestLanguage = "Kotlin";  
System.out.println(
	"Taiwan " 
	+ bestLanguage 
	+ " User Group"
);
*/
```

## Operator Overloading

除了函數可以多載

我們也可以用 `operator` 關鍵字對符號多載

讓我們的程式更好撰寫

```kotlin
data class Counter(val dayIndex: Int) {  
    operator fun plus(increment: Int): Counter {  
        return Counter(dayIndex + increment)  
    }  
}

val counter = Counter(3)  
println(counter + 4)
// Counter(dayIndex=7)
```
## Infix Notation

引入 `infix` 關鍵字

讓我們可以宣告更易懂的函數

```kotlin
infix fun Int.shouldEqualTo(actual: Int) {  
    assertEquals(this, actual)  
}

add(2, 2) shouldEqualTo 4

// 等同 assertEquals(4, add(2, 2))
```
## Destructuring Declaration
Kotlin 可以直接解構物件

讓程式邏輯更加簡潔

```kotlin
data class Customer(
    val name: String,
    val email: String
)

val (name, email) = customer

/*
等同
val name = customer.name
val email = customer.email
*/
```

也可以解構 `Map` 物件

```kotlin
val map = mapOf("Alice" to 21, "Bob" to 25)
for ((name, age) in map) {
    println("$name is $age years old")          
}
```

想了解更多 Kotlin 的語法特點嗎？

歡迎加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！

#Kotlin #TKUG
