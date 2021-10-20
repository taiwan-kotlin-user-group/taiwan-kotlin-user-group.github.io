## Kotlin Koin 簡介
Koin 是一個協助在 Kotlin 專案內建立依賴注入的框架

可以用簡潔的語法

快速的協助我們將依賴元件注入到使用元件的程式裡

## 什麼是依賴注入

在專案裡面

不可避免的會有元件和元件之間的互動

我們可能會想用組合的方式

在元件內宣告底層元件進行使用

```kotlin
class Calculator {  
    fun count() = println("呼叫 Calculator.count()")  
}  
  
class Printer {  
    fun print() = println("呼叫 Printer.print()")  
}  
  
fun mainLogic() {  
    val calculator = Calculator()  
    val printer = Printer()  
    calculator.count() // 呼叫 Printer.print()  
    printer.print() // 呼叫 Printer.print()  
}
```

這樣的缺點是

當我們想切換成其他元件時

就必須要更改 `mainLogic()` 內的程式碼

### 依賴注入

我們可以修改一下我們的程式碼

```kotlin
interface CalculatorInterface {  
    fun count()  
}  
  
class Calculator : CalculatorInterface {  
    override fun count() = println("呼叫 Calculator.count()")  
}  
  
interface PrinterInterface {  
    fun print()  
}  
  
class Printer : PrinterInterface {  
    override fun print() = println("呼叫 Printer.print()")  
}  
  
fun mainLogic(
    calculator: CalculatorInterface = Calculator(),
    printer: PrinterInterface = Printer()
) {
    calculator.count() // 呼叫 Calculator.count()
    printer.print() // 呼叫 Printer.print()
}
```

使用預設參數的方式為

```kotlin
val mainLogic = MainLogic()  
mainLogic()
```

如果我們需要切換成其他元件時

只要該元件實作了 `CalculatorInterface` 和 `PrinterInterface`

就可以使用在 `mainLogic()` 內

```kotlin
class NewCalculator : CalculatorInterface {  
    override fun count() = println("呼叫 NewCalculator.count()")  
}

class NewPrinter : PrinterInterface {  
    override fun print() = println("呼叫 NewPrinter.print()")  
}

val mainLogic = MainLogic(NewCalculator(), NewPrinter())  
mainLogic()
```

這樣的缺點是

如果我們的注入有多層的話

那麼就必須自己維護這些注入的參數

## Koin 的用法

透過 Koin 框架

可以讓上述的流程變得更簡潔

```kotlin
interface CalculatorInterface {
    fun count()
}

class Calculator : CalculatorInterface {
    override fun count() = println("呼叫 Calculator.count()")
}

interface PrinterInterface {
    fun print()
}

class Printer : PrinterInterface {
    override fun print() = println("呼叫 Printer.print()")
}

class MainLogic : KoinComponent {
    private val calculator by inject<CalculatorInterface>()
    private val printer by inject<PrinterInterface>()
    operator fun invoke(
    ) {
        calculator.count() // 呼叫 CalculatorInterface.print()
        printer.print() // 呼叫 PrinterInterface.print()
    }
}
```

使用時我們透過 Koin 

協助我們綁定 `CalculatorInterface` 和 `PrinterInterface`

對應的實作

```kotlin
val myModule = module {
    single { Calculator() as CalculatorInterface }
    single { Printer() as PrinterInterface }
}
startKoin {
    modules(myModule)
}
val mainLogic = MainLogic()
mainLogic() 
// 呼叫 Calculator.count()
// 呼叫 Printer.print()
```

如果想切換對應的實作

只要調整 `module`

```kotlin
val myNewModule = module {
    single { NewCalculator() as CalculatorInterface }
    single { NewPrinter() as PrinterInterface }
}
startKoin {
    modules(myNewModule)
}
val mainLogic = MainLogic()
mainLogic() 
// 呼叫 NewCalculator.count()
// 呼叫 NewPrinter.print()
```

這樣一來

我們就可以將所有依賴關聯放在同一處

並且隨著我們的需求切換對應元件了

### 參考資料
- https://insert-koin.io/

-----

想看更多範例嗎？

可以看看

- [Kotlin Ktor 簡介](kotlin-ktor-intro.md)
- [Kotlin Exposed 簡介](kotlin-exposed-intro.md)
- [Kotlin Mockk 簡介](kotlin-mockk-intro.md)
- [Kotlin 的函數式編程慣用寫法](kotlin-functional-programming-example.md)
- [kotlin Data Class 範例](kotlin-data-class-example.md)

加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
