## Kotlin 正規表達式慣用寫法

## 取代字串前後的文字

在 Java 內，可以使用 [replaceFirst()](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html#replaceFirst(java.lang.String,java.lang.String)) 和 [replaceAll()](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html#replaceAll(java.lang.String,java.lang.String)) 
函數。

`replaceAll()` 接收正規表達式做為參數

我們可以用 `##$` 來替換字串結尾為 `##` 的內容

```java
String input = "##place##holder##";
String result = input.replaceFirst("##", "").replaceAll("##$", "");
System.out.println(result); // place##holder
```


在 Kotlin 內，可以使用 [removeSurrounding()](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/remove-surrounding.html) 函數

取代字串前後的 `##`

```kotlin
fun main() {
    val input = "##place##holder##"
    val result = input.removeSurrounding("##")
    println(result) // place##holder
}
```

## 取代字串中出現的某個樣式

在 Java 內，可以使用 [Pattern](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/regex/Pattern.html)
類別和 [Matcher](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/regex/Matcher.html) 類別

比方說我們想隱藏資料內的用戶名和密碼

```java
String input = "login: Pokemon5, password: 1q2w3e4r5t";
Pattern pattern = Pattern.compile("\\w*\\d+\\w*");
Matcher matcher = pattern.matcher(input);
String replacementResult = matcher.replaceAll(it -> "xxx");
System.out.println("Anonymized input: '" + replacementResult + "'");
// Anonymized input: 'login: xxx, password: xxx'
```


在 Kotlin 內，可以使用 [Regex](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/) 類別

來簡化正規表達式操作

另外，利用[原始字串](https://kotlinlang.org/docs/basic-types.html#string-literals)可以減少我們使用反斜線的次數

```kotlin
fun main() {
    val input = "login: Pokemon5, password: 1q2w3e4r5t"
    val regex = Regex("""\w*\d+\w*""") // raw string
    val replacementResult = regex.replace(input, replacement = "xxx")
    println("Anonymized input: '$replacementResult'")
	  // Anonymized input: 'login: xxx, password: xxx'
}
```

-----

想看更多範例嗎？

可以看看

- [Kotlin 慣用寫法](idioms.md)
- [Kotlin 入門範例](kotlin-syntax.md)
- [Kotlin 的函數式編程慣用寫法](kotlin-functional-programming-example.md)
- [Kotlin 和 Java 的比較](kotlin-vs-java.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
