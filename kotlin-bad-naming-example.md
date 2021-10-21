## 不好的 Kotlin 專案命名範例

下面來介紹不好的專案命名範例

### 單字母命名法

如果你用 `a`, `b`, `c` 幫變數命名

你可以保證之後的工程師無法用文字搜尋找到這些變數

另外，也沒有人能猜到他們的用途。

如果有人希望打破從 FØRTRAN 以來

用 `i`, `j`, `k` 來當作 index 的傳統

就將他們改成 `ii`, `jj`, `kk`。

### 抽象用字

在命名變數時，使用抽象的字

像是 _it_, _everything_, _data_, _handle_

_stuff_, _do_, _routine_, _perform_

可以搭配數字編號

比方說 `routineX48`，`PerformDataFunction`

`DoIt`，`HandleStuff`，`do_args_method`⋯⋯等等。

### 拼字錯誤

藉由部分的單字拼字錯誤

部分又正確

可以讓之後維護的工程師

無法用搜尋的方式快速找到該命名出現的位置

比方說 `setPintleOpen` 對應 `SetPintalClose`

#### 英美式拼法

混雜英式與美式拼法

比方說 `const COLOR` 和 `const COLOUR`

### 縮寫

大量使用未定義的縮寫

比方說用 `AppSendPL` 代表 `ApplicationSendPipeline`

#### 移除母音

找不到常用縮寫方式時

任意移除母音作為縮寫的方式

比方說用 `ApplctnSndPpln` 代表 `ApplicationSendPipeline`

#### 絕不使用縮寫

反過來也可以絕不使用縮寫

比方說 `HyperTextTransferProtocolInputStream`


### 誤導的名稱

確保每個函數都比名稱顯示

多做一點或少做一點事情

比方說 `isvalid(n: Int): Boolean`

除了驗證輸入是否合法

還可以將數字轉成二進位並存到資料庫內

-----

想看更多範例嗎？

可以看看

- [Kotlin 慣用寫法](idioms.md)
- [Kotlin 入門範例](kotlin-syntax.md)
- [Kotlin 的函數式編程慣用寫法](kotlin-functional-programming-example.md)
- [Kotlin Data Class 範例](kotlin-data-class-example.md)
- [Kotlin 專案命名常規](kotlin-naming-example.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
