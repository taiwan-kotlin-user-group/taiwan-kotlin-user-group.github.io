## Kotlin Exposed 簡介

![exposed logo](https://raw.githubusercontent.com/JetBrains/Exposed/master/docs/logo.png)

Exposed 是一個 Kotlin 的 ORM framework，基於 JDBC driver 上開發，由 JetBrains 官方開發與維護。

如前面所說，這個框架的目的，主要是協助我們在 Kotlin 專案裏面串接資料庫。

這個框架目前已經支援很多開發或正式使用的資料庫，比方說：
* H2
* MySQL
* MariaDB
* Oracle
* PostgreSQL
* SQL Server
* SQLite

## 為什麼要用 Exposed 框架

### 純 Kotlin
Exposed 框架是純 Kotlin 語言，所以不用擔心同一專案需要多個語言維護，導致提升開發以及維護的難度。

得益於 Kotlin 的語法，這個框架使用起來的感覺非常簡單易懂。不像部分語言受限於特性，無法完整的以物件導向方式撰寫資料庫的串接邏輯。

個人認為，比起許多語言串接資料庫的方式開發上，要好學以及容易開發很多。

### open source

Exposed 框架是 open source 的，使用 Apache License 2.0。

所以不像有的框架，需要擔心使用時的授權或費用等問題。

## 範例

### DSL
使用 DSL 存取資料庫的範例如下

```kotlin
object Cities: IntIdTable() {  
    val name = varchar("name", 50)  
}

fun main() {
    Database.connect(
		"jdbc:h2:mem:test",
		driver = "org.h2.Driver"
	)
	transaction {  
		SchemaUtils.create(Cities)  
		val id = Cities.insertAndGetId {  
			it[name] = "Taipei"  
		}  

		Cities  
			.select { Cities.id eq id }  
			.forEach {  
				println("City #$id: ${it[Cities.name]}")  
			}
	}
}
```
### DAO
使用 DAO 存取資料庫的範例如下

```kotlin
object Cities: IntIdTable() {  
    val name = varchar("name", 50)  
}

class City(id: EntityID<Int>) : IntEntity(id) {  
    companion object : IntEntityClass<City>(Cities)  
 	var name by Cities.name  
}

fun main() {
    Database.connect(
        "jdbc:h2:mem:test",
        driver = "org.h2.Driver"
    )
    transaction {
        SchemaUtils.create(Cities)
        val city = City.new {
            name = "Taipei"
        }

        println("City #${city.id}: ${city.name}")
    }
}
```

-----

有更多想知道的嗎？

歡迎加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
