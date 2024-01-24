# companion
Kotlin 伴生对象(Companion)

class Person {
    companion object Test {
        fun callMe() = println("I'm called.")
    }
}

fun main(args: Array<String>) {
    Person.callMe()
}

有点类似静态函数