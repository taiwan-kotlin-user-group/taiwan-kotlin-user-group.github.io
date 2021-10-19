## Kotlin 0.1 + 0.2 是多少

如果我們在 JavaScript 內進行運算 `0.1 + 0.2`
 
```javascript
0.1 + 0.2
```
 
會得到奇怪的結果
 
```javascript
0.30000000000000004
```

這個數字是怎麼來的呢？

在 Kotlin 程式語言會不會有一樣的狀況？

## 浮點數

在多數語言裡，進行小數的運算時

會使用浮點數 `float`

或者雙倍精確度的浮點數 `double` 進行運算

浮點數的定義通常使用 **IEEE 754** 的儲存格式

花費空間是 4 Bytes

在 Kotlin 內

我們可以透過 `toRawBits()`

來實際看到儲存的資料

印成 `Int` 後的內容

```kotlin
val a = 0.1f  
println(a.toRawBits()) // 1036831949
```

由於底層的轉換會出現誤差

因此可能會導致浮點數的四則運算

出現預期外的結果

### Kotlin 會不會有一樣的狀況

Kotlin 預設的小數型態為雙倍精確度的浮點數 `Double`

一樣依照 IEEE 754 規範的儲存格式

所以也有類似的問題

```kotlin
println(0.1 + 0.2) // 0.30000000000000004
```

## 解決方式

如果使用 JavaScript

可以透過 `toFixed()` 限制浮點數的精確度

避免這個問題

```javascript
(0.1+0.2).toFixed(1) // 0.3
```

在 Kotlin 內

可以透過 `toBigDecimal()`

來避免這個問題

```kotlin
println(0.1.toBigDecimal() + 0.2.toBigDecimal()) // 0.3
```

-----

想看更多範例嗎？

可以看看

- [Kotlin 慣用寫法](idioms.md)
- [Kotlin 入門範例](kotlin-syntax.md)
- [Kotlin 的函數式編程慣用寫法](kotlin-functional-programming-example.md)
- [kotlin Data Class 範例](kotlin-data-class-example.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
如果使用 JavaScript
