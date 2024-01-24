 fun speedUp() {
        check(isStarted) {
            "Engine is not started, cannot be speed up now"
        }

        //speed up the engine
}


fun createNewFileV2(file: File?): Boolean {
    check(isDiskMounted) {
        "Disk is not mounted"
    }
    requireNotNull(file) {
        "file is null"
    }
    file.createNewFile()
    assert(file.exists()) {
        "createNewFileV2 file($file) does not exist"
    }
    return true
}
# require
require(boolean) 用来检测方法的参数，当参数boolean为false时，抛出 IllegalArgumentException
fun readFileContent(file: File?): String {
    //判断file不能为null
    requireNotNull(file)
    //判断文件必须可读，并提供错误的信息
    require(file.canRead()) {
        "readFileContent file($file) is not readable"
    }
    //read file content
    return "Your file content"
}
# check
class Engine {
    var isStarted = false
    fun speedUp() {
        check(isStarted) {
            "Engine is not started, cannot be speed up now"
        }
        //speed up the engine
    }
}
# assert

fun makeFile(path: String) {
    val file = File(path)
    file.createNewFile()
    assert(file.exists()) {
        "make File($file) failed"
    }
}

# 使用顺序
先使用 check检测对象的状态

再使用 require检测方法的参数合法性

执行操作后，使用 assert校验结果

