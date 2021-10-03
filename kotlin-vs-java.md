## Kotlin 和 Java 的比較

## 相似的地方

### 強型別語言

兩者都是強型別語言，在管理大型專案上，可以減少型別錯亂所產生的錯誤。

### JVM based

一般的流程來說，Java 語言撰寫完畢之後

會先編譯成 Java bytecode，然後透過 JVM 運行

Kotlin 一樣可以在撰寫完畢後

編譯成 Java bytecode，然後透過 JVM 運行

## 不同的地方

除了這些相似的地方，Kotlin 語言和 Java 相比，還有很多明顯的不同

### 不使用分號 vs 使用分號

Kotlin 預設不使用分號

使用換行作為語句結尾

```kotlin
// IDE 提示 Redundant semicolon 
val a = 1;
```

Java 必須使用分號結尾

```java
System.out.println("Hello World")  // error: ';' expected
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

Java 通常需要針對變數是否為 `null` 進行檢查

```java
String name = null;
System.out.println(name.length());
// NullPointerException
```

### 支持型別推論

Kotlin 宣告的變數，可以根據寫入的值推論型別

```kotlin
val name = "Hello World"    // 根據寫入的值，將 name 型別推論為 String
println(name.length())      // 呼叫 String.length()
```

Java 目前則不支援型別推論

```java
name = "Hello World" // error: cannot find symbol
```

### Data Classes

Kotlin 建立了 `data class`關鍵字，可以快速的建立一個 POJO 物件

```kotlin
data class Customer(
    val name: String,
    val email: String
)
```

類似的物件 Java 寫法如下
```java
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
```

### Singleton object
用 `object` 關鍵字宣告單例物件

看起來更加簡潔

```kotlin
object ThisIsASingleton {
    val name: String = "Taiwan Kotlin User Group"
}
```

類似邏輯 Java 寫法如下

```java
public class ThisIsASingleton {  
    private static final ThisIsASingleton instance = new ThisIsASingleton();  
    private static final String name = "Taiwan Kotlin User Group";  
    private ThisIsASingleton(){}  
    public static ThisIsASingleton getInstance() {  
        return instance;  
    }  
}
```

### Extension Functions

Kotlin 可以針對任何類別直接撰寫擴充函數

不需要更改原本類別的原始碼

```kotlin
fun Int.plusTwice(other: Int) = this + other * 2
println(5.plusTwice(2)) // 9
```

Java 目前不支援這種做法，必須定義處理該類別的某個 Handler 來進行其他邏輯的運算。

### Coroutine
Kotlin 目前實作 coroutine 

可以用 coroutine 的方式切換執行緒

```kotlin
fun main() = runBlocking {
    launch { // 啟動 coroutine
        delay(1000L) // 等一秒鐘
        println("World!") // 印出 "World!"
    }
    println("Hello") // 先印出 "Hello"
}
```

Java 目前未實作 coroutine

必須自己撰寫切換執行緒的邏輯
