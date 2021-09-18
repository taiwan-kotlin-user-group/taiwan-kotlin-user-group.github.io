## 後端開發為什麼選擇 Kotlin

## JVM 生態系

Kotlin 可以編譯成 Java ByteCode，直接使用原本 Java 的 library


## Ktor 網頁框架

### 全 Kotlin

利用 Kotlin 語法簡潔的特性，Ktor 的程式碼非常簡潔易懂

用 Ktor 建立純文字 API 的程式碼如下

```kotlin
import io.ktor.routing.*
import io.ktor.response.*

routing {
    get("/hello") {
        call.respondText("Hello")
    }
}
```

### 自動測試

```kotlin
@Test
fun testRoot() {
    withTestApplication({ module(testing = true) }) {
        handleRequest(HttpMethod.Get, "/").apply {
            assertEquals(HttpStatusCode.OK, response.status())
            assertEquals(".toString()", response.content)
        }
    }
}
```

## Exposed ORM 框架

