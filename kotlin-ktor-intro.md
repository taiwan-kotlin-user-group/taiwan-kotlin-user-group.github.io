## Kotlin Ktor 簡介

Ktor 是一個 Kotlin 語言的後端框架

由 Kotlin 的開發公司 JetBrains 所建立

可以簡單的建立一個異步（asynchronous）處理的後端伺服器

## 為什麼學 Ktor

能異步處理需求的後端框架和語言不少

為什麼要學習 Ktor 呢？

以下我們整理出幾點學習 Ktor 的理由

### 精簡

立基於 Kotlin 語言的特性

我們能很精簡的撰寫出想要的功能

不需要大量的冗餘程式碼。

### 官方支援

由於 Ktor 是 Kotlin 語言的開發公司 JetBrains 所建立

所以在和 Kotlin 的搭配

以及 IntelliJ Idea 這個 IDE 上的搭配度都非常的好

### 容易使用

透過 Ktor 的設計

不管是建立 API 或者撰寫網頁顯示

都非常的容易使用

比方說，建立 Hello World 的路徑是

```kotlin
get("/hello") {
    call.respondText(
		"HELLO WORLD!", 
		contentType = ContentType.Text.Plain
	)
}
```

### 異步處理

利用 Kotlin 內建的 coroutine

Ktor 可以很簡單的對需求進行非同步處理

比方說，先存取 `http://localhost/path1`

不等回傳就繼續存取 `http://localhost/path2`

等回傳後分別將回傳值存入 `firstRequestContent` 和 `secondRequestContent`

```kotlin
val client = HttpClient(CIO)
val firstRequest: Deferred<String> = async { client.get("http://localhost/path1") }
val secondRequest: Deferred<String> = async { client.get("http://localhost/path2") }
val firstRequestContent = firstRequest.await()
val secondRequestContent = secondRequest.await()
```

-----

想看更多範例嗎？

可以看看

* [Kotlin 慣用寫法](idioms.md)
* [Kotlin 入門範例](kotlin-syntax.md)
* [Kotlin 的函數式編程慣用寫法](kotlin-functional-programming-example.md)


加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) 

或 kotlin.tips 的 [Ktor 練功坊](https://tw.kotlin.tips/dojos/ktortw) ！
