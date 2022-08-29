---
description: ⭐️⭐️⭐️
---

# Int和Integer区别？Int.box()的使用场景？

1. Int是Scala的整数类型，Integer是Java的整数类型，且Integer是包装类型，Int不是。
2. Int不能new，不能为null，直接对应虚拟机的int类型。Scala通过RichInt提供Int上的拓展操作，所以Int是加强版的int。
3. Int基本不能与Integer混用，特别是使用Scala编写spring和mybatis应用。因为Int不能为null，这会导致反射和get/set不可用等一系列问题。由于Integer可以为null，还可能导致Scala代码出现短路。
4. Int.box()或Boolean等类型的box方法，在调用Java库时可能是必须的。已知场景是netty的option设定时，必须使用Boolean.box(false)，Boolean.box(true)，不能使用Scala的值类型。

答到1.2及格

答全，满分
