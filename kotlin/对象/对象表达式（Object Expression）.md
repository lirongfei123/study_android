```
interface AA {
    fun a()
}

fun main(args: Array<String>) {

    val aa = object : AA {
        override fun a() {
            println("a invoked")
        }
    }

    aa.a()
}

```

# 不实现任何接口和类，并且在匿名内部类中添加方法
```
fun main(args: Array<String>) {

    val obj = object  {
        fun a() {
            println("a invoked")
        }
    }

    obj.a()  //打印：a invoked
}
```
# 实现多个接口和类
```
fun main(args: Array<String>) {
    val cc = object : AA, BB() {
        override fun a() {

        }

        override fun b() {

        }

    }

    cc.a()
    cc.b()

}
```