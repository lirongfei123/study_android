fun describe(obj: Any): String = 
    when (obj) { 
        1          -> "One" 
        "Hello"    -> "Greeting" 
        is Long    -> "Long" 
        !is String -> "Not a string" 
        else       -> "Unknown" 
    } 
//调用describe这个方法，就会根据参数的不同返回String类型的不同值



override fun getModule(
        s: String,
        reactApplicationContext: ReactApplicationContext
    ): NativeModule? {
        when (s) {
            ScreensModule.NAME -> return ScreensModule(reactApplicationContext)
        }
        return null
    }
