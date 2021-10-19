## Kotlin KDoc 註解範例

```kotlin
/**
 * *members* 的集合
 *
 * 這個類別單純展示如何撰寫 KDoc 註解
 *
 * @param T 集合內元素的型態
 * @property name 集合的名稱
 * @constructor 建立空集合
 */
class Group<T>(val name: String) {
    /**
     * 在集合內增加新 [member]
     * @return 集合增加後的大小
     */
    fun add(member: T): Int { ... }
}
```

### 支援的標籤
- `@param name`
  - 函數或者類別的參數資訊，也可以寫成 `@param[name] description`
- `@return`
  - 回傳值資訊
- `@constructor`
  - 建構子資訊
- `@receiver`
  - 標記延伸函數（extension function）的接收者
- `@property name`
  - 類別的屬性資訊
- `@throws class`
  - 可能拋出的例外或錯誤
- `@exception class`
  - 可能拋出的例外或錯誤
- `@sample identifier`
  - 該元件的使用範例
- `@see identifier`
  - 補充說明資訊
- `@author`
  - 作者資訊
- `@since`
  - 記錄這段程式碼加入時的專案版本
- `@suppress`
  - 將這段 KDoc 移出文件外，可以用在不對外的 API 註解上

KDoc 不支援 `@deprecated` 標籤

要標記某個元件為棄用

可以使用 `@Deprecated` 這個 Annotation Class

（參考 [[Kotlin Annotation Class 範例]]）
### Inline markup

KDoc 可以使用 Markdown 格式撰寫內文

```kotlin
/**
 * Markdown 範例
 *
 * 這段程式有**以下流程**
 * - 首先⋯⋯
 * - 接著⋯⋯
 * - 最後⋯⋯
 */
```

### Links to elements

KDoc 支援直接用 `[]` 標記其他元件

像是類別、方法、屬性、參數的名稱

```kotlin
/**
 * Returns the value of this [Float] number as a [BigDecimal].
 *
 * The number is converted to a string and then the string is converted to a [BigDecimal].
 */
public inline fun Float.toBigDecimal()
```

## 實際案例

[Ktor](kotlin-ktor-intro.md) 內

`Application` KDoc 註解如下

```kotlin
/**
 * Represents configured and running web application, capable of handling requests.
 * It is also the application coroutine scope that is cancelled immediately at application stop so useful
 * for launching background coroutines.
 *
 * @param environment Instance of [ApplicationEnvironment] describing environment this application runs in
 */
```

針對內部方法

比方說 `dispose()`

也有 KDoc 註解說明該函數的邏輯

```kotlin
/**
 * Called by [ApplicationEngine] when [Application] is terminated
 */
public fun dispose()
```

-----

想看更多範例嗎？

可以看看

- [Kotlin 慣用寫法](idioms.md)
- [Kotlin 入門範例](kotlin-syntax.md)
- [Kotlin 的協變和反變](kotlin-covariance-contravariance.md)
- [kotlin Data Class 範例](kotlin-data-class-example.md)

加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
