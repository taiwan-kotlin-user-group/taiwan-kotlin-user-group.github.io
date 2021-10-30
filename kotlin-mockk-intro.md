## Kotlin Mockk 簡介

Kotlin Mockk 是一個協助在測試環境中

製造 test double 的框架

## 用法
### mock
宣告 Car 的 mock 物件 `car`

希望 `car` 收到 `drive(Direction.NORTH)`時

固定回傳 `Outcome.OK`

```kotlin
val car = mockk<Car>()

every { car.drive(Direction.NORTH) } returns Outcome.OK

```

### patial mock

宣告 Car 的 mock 物件 `car`

希望 `car` 收到 `drive(Direction.NORTH)`時

固定回傳 `Outcome.OK`

如果收到 `drive(Direction. SOUTH)` 時

行為和原本 Car 類別一樣

```kotlin
val car = mockk<Car>()

every { car.drive(Direction.NORTH) } returns Outcome.OK
every { car.drive(Direction.SOUTH) } answers { callOriginal() }
```


### spy

宣告 Car 的 `spyk` 物件 `car`

在程式執行完之後

確認是否被呼叫 `drive(Direction.NORTH)`

```kotlin
val car = spyk(Car())
car.drive(Direction.NORTH)
verify { car.drive(Direction.NORTH) }
```

## 參考資料
- https://mockk.io/

-----

想看更多範例嗎？

可以看看

* [Kotlin Exposed 簡介](kotlin-exposed-intro.md)
* [Kotlin Ktor 簡介](kotlin-ktor-intro.md)
* [Kotlin 慣用寫法](idioms.md)
* [Kotlin 入門範例](kotlin-syntax.md)
* [Kotlin 的函數式編程慣用寫法](kotlin-functional-programming-example.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
