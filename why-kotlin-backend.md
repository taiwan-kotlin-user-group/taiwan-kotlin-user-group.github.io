## 後端開發為什麼選擇 Kotlin

## JVM 生態系

Kotlin 可以編譯成 Java ByteCode，直接使用原本 Java 的 library

### Spring Boot

Spring 框架可謂 JVM 生態系裡最舉足輕重的框架

其穩定、完整的生態系讓它被很多大企業所採用。

利用 Spring Boot 搭配 Kotlin 建立純文字 API 的程式碼如下

```kotlin
@RestController
class HomeController() {
    @GetMapping("/hello")
    fun getHello(): String {
        return "Hello"
    }
}
```

有興趣嗎？歡迎加入 kotlin.tips 的 [Kotlin 練功場 - Spring Boot 組](https://tw.kotlin.tips/dojos/springtw) 看看！

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
            assertEquals("Hello", response.content)
        }
    }
}
```
有興趣嗎？歡迎加入 kotlin.tips 的 [Kotlin 練功場 - Ktor 組](https://tw.kotlin.tips/dojos/ktortw) 看看！

## Exposed ORM 框架

利用 Exposed 框架

可以用簡潔的程式碼

和資料庫進行串接

```kotlin
object Users : IntIdTable() {
    val name = varchar("name", 50)
}

class User(id: EntityID<Int>) : IntEntity(id) {  
    companion object : IntEntityClass<User>(Users)  
 	var name by Users.name  
}

fun main() {
    transaction {  
        SchemaUtils.create(Users)  
        User.new {  
            cityId = 1
            name = "Alice"  
        }  
        User.new {  
            cityId = 2
            name = "Bob"  
        }
        User  
        .all()  
        .forEach {  
            println("name: ${it.name}")  
        }
    }
}
```

