---
description: ⭐️⭐️⭐️⭐️⭐️
---

# implicit与implicitly区别？

1. implicit是一个关键字，功能比较多，如隐式参数/值，隐式转换。
2. implicitly是一个内置方法，作为隐式参数/值使用时两种没有区别，但是，implicit修饰的隐式参数需要定义在方法签名上，而使用implicitly不需要。

直接使用implicit声明隐式参数jsonCodec

```scala
  def stringCodec(implicit jsonCodec:JsonCodec[Json]): JsonCodec[String] =
    jsonCodec.map(json => json.noSpaces)(string =>
      parse(string) match {
        case Left(_)      => throw new RuntimeException("ApiJsonCoded")
        case Right(value) => value
      }
    )
```

使用implicitly，不需要声明jsonCodec，编译器最终会将implicitly\[JsonCodec\[Json]]展开成类似implicit def stringCodec(implicit evidence$1:JsonCodec\[Json]): JsonCodec\[String]的函数

```scala
  val stringCodec: JsonCodec[String] =
    implicitly[JsonCodec[Json]].map(json => json.noSpaces)(string =>
      parse(string) match {
        case Left(_)      => throw new RuntimeException("ApiJsonCoded")
        case Right(value) => value
      }
    )
```

它们没有本质上的好坏，通常，如果是透传一个类似locale这种的隐式参数（方法体内不直接使用隐式参数值），使用implicit更方便，如果是需要直接使用该参数，比如本例子对JsonCodec调用了map方法，那么使用implicitly就能少写一个参数在方法签名中。 不过，直接定义会使得方法签名更加容易阅读，所以对外接口通常使用implicit。本例子实际上的是用于JSON隐式转换的，不会被外部主动调用，使用implicitly更好。

答到1.2及格，答完例子所述，满分
