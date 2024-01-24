# until的相当于 i=>min && i<max
 for (i in 1 until 5){
    println("$i")
}//1,2,3,4

# step的相当于 i++

for (i in 2..10 step 3){
        println("$i")
}
# downTo的相当于 i–
for (i in 10 downTo 1){
    println("$i")
}
# in的相当于 i>=min && i <=max
var num=5;
if (num in 1..10){
    println("$num")
}