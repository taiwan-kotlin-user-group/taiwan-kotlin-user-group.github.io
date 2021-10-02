## Ktor 簡介

歡迎來學 Ktor！一個精簡的異步後端框架

## 什麼是 Ktor

Ktor 是一個 Kotlin 言的框架，由 Kotlin 的開發公司 JetBrains 所建立，可以簡單的建立一個異步（asynchronous）處理的後端伺服器。

## 為什麼要學 Ktor

能異步處理需求的後端框架和語言不少，為什麼要學習 Ktor 呢？

以下我們歸納出幾點學習 Ktor 的理由

### 精簡

立基於 Kotlin 語言的特性，我們能很精簡的撰寫出想要的功能，不需要大量的冗餘程式碼。

### 官方支援

由於 Ktor 是 Kotlin 語言的開發公司 JetBrains 所建立，所以在和 Kotlin 的搭配以及 IntelliJ Idea 這個 IDE 上的搭配度都非常的好。

### 容易使用
透過 Ktor 的設計，不管是建立 API 或者撰寫網頁顯示，都非常的容易使用

比方說，建立 Hello World 的路徑是

```kotlin
get("/hello") {
    call.respondText(
		"HELLO WORLD!", 
		contentType = ContentType.Text.Plain
	)
}
```

## 課程
**行前準備**

* [開發工具](tool.md)

**啟程**

* 建立專案
* 建立 code style 檢查
* 新增路徑
* 建立 json response
* 撰寫環境變數

**串接資料庫**

* 透過 exposed 串接資料庫
* 用戶登入功能

**前端模板**

* DSL
* freeMarker

**進階討論**

* 建立 log
* 自動測試
* 上傳檔案
* 串接第三方 API

## 參考資料

* <https://ktor.io/>
* <https://tw.kotlin.tips/>
* <https://ktor.guide/>
* <https://github.com/JetBrains/Exposed/wiki>
