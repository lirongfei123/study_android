# let
当需要定义一个变量在一个特定的作用域时，可以考虑使用 let 函数。当然，更多的是用于避免 Null 判断。

在 let 函数内部，用 it 指代调用 let 函数的对象，并且最后返回最后的计算值

any.let {
    // 用 it 指代 any 对象
    // todo() 是 any 对象的共有属性或方法
    // it.todo() 的返回值作为 let 函数的返回值返回
    it.todo() 
}
// 另一种用法
any?.let {
    it.todo() // any 不为 null 时才会调用 let 函数
}

fun main() {
  val result = "Test".let {
    println(it) // Test
    3 * 4 // result = 12
  }
  println(result) // 12
}
# with
和 let 类似，又和 let 不同，with 最后也包含一段函数块，也是将最后的计算的结果返回。

但是 with 不是以拓展的形式存在的。其将某个对象作为函数的参数，并且以 this 指代。

首先来看 with 的一般结构：
```
whith(any) {
  // todo() 是 any 对象的共有属性或方法
  // todo() 的返回值作为 with 函数的返回值返回
  todo() 
}
```
## 具体使用
class Person(val name: String, val age: Int)

fun main() {
    val chengww = Person("chengww", 18)
    val result = with(chengww) {
        println("Greetings. My name is $name, I am $age years old.")
        3 * 4 // result = 12
    }
    println(result)
}

在 let 函数的实际使用中，我们对 textView 进行空判断，但是每次函数调用的时候还是要使用 it 对象去调用。
如果我们使用 with 函数的话，由于代码块中传入的是 this，而不是 it，那么我们就可以直接写出函数名（属性）来进行相应的设置：
```
if (textView == null) return
with(textView) {
	text = "TextSetInTextView"
	setTextColor(ContextCompat.getColor(this@TestActivity, R.color.colorAccent))
	textSize = 18f
}
```
# run
刚刚说到，我们想能有 let 函数那样又优雅的判空，又能有 with 函数省去同一个对象多次设置属性的便捷写法。
没错，就是这就非我们 run 函数莫属了。run 函数基本是 let 和 with 的结合体，对象调用 run 函数，接收一个 lambda 函数为参数，传入 this 并以闭包形式返回，返回值是最后的计算结果。
```
textView?.run {
	text = "TextSetInTextView"
	setTextColor(ContextCompat.getColor(this@TestActivity, R.color.colorAccent))
	textSize = 18f
}

```
像上面这个例子，在需要多次设置属性，但设置属性后返回值不是改对象（或无返回值：Unit）不能链式调用的时候，就非常适合使用 run 函数。

# apply
apply 函数和 run 函数很像，但是 apply 最后返回的是调用对象自身。
```
val result = any.apply {
  // todo() 是 any 对象的共有属性或方法
  todo() 
  3 * 4 // 最后返回的是 any 对象，而不是 12
}

println(result) // 打印的是 any 对象

```
由于 apply 函数返回的是调用对象自身，我们可以借助 apply 函数的特性进行多级判空。

# also
没错，和 let 函数类似，唯一的区别就是 also 函数的返回值是调用对象本身，在上例中 also 函数将返回 school.mClass.student.name。
```
val result = any.also {
    // 用 it 指代 any 对象
    // todo() 是 any 对象的共有属性或方法
    it.todo() 
  	3 * 4 // 将返回 any 对象，而不是 12
}
```