## Kotlin Object 範例

物件導向程式內

類別（class）通常像是藍圖

物件（object）則是根據藍圖建立的個體

如果我們單純需要物件

可以直接用 `object` 宣告

```kotlin
val date = object {                                              
	val day = "01"
	val month = "01"
	val year = "2021"
	fun getDate() = "${year}-${month}-${day}"
}
println(date.year) // 2021  
println(date.getDate()) // 2021-01-01
```

如果我們需要一個全域的物件（參考：單例模式）

我們可以直接在頂層宣告

```kotlin
object Date {  
    var day = "01"  
    var month = "01"  
    var year = "2021"  
    fun getDate() = "${year}-${month}-${day}"  
}  

println(Date.year) // 2021
Date.month = "02"  
println(Date.getDate()) // 2021-02-01

```

-----

想看更多範例嗎？

可以看看

- [Kotlin 慣用寫法](idioms.md)
- [Kotlin 入門範例](kotlin-syntax.md)
- [Kotlin 的函數式編程慣用寫法](kotlin-functional-programming-example.md)
- [kotlin Data Class 範例](kotlin-data-class-example.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
