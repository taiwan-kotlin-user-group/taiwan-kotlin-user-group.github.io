## Kotlin Delegation 範例

在軟體開發上

委派（delegation）模式是一個很有用的模式

比方說 Java 的實作

```java
interface Print {
	void print();
}

class Delegate implements Print {
	void print() { 
		System.out.print("被委派者"); 
	}
}

class Delegator implements Print {
	Delegate delegate = new Delegate();
	void print() {
		delegate.print();
	} 
}

Printer printer = new Printer();
printer.print(); // 被委派者
```

在 Kotlin 內，內建支援委派的原生語法

寫起來更加直觀

```kotlin
interface Print {
    fun print()
}

class Delegate : Print {
    override fun print() = println("被委派者");
}

class Delegator(delegate: Delegate) : Print by delegate

val delegate = Delegate()  
Delegator(delegate).print() // 被委派者
```

-----

想看更多範例嗎？

可以看看

- [Kotlin 慣用寫法](idioms.md)
- [Kotlin 的函數式編程慣用寫法](kotlin-functional-programming-example.md)
- [kotlin Data Class 範例](kotlin-data-class-example.md)
- [kotlin Enum Class 範例](kotlin-enum-class-example.md)
- [kotlin Sealed Class 範例](kotlin-sealed-class-example.md)

或加入 kotlin.tips 的 [Kotlin 讀書會](https://tw.kotlin.tips/study-jams) ！
