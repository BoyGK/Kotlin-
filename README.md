（小白的学习之路，欢迎指正，持续更新中。。。）<br>
Kotlin出现到现在已经有一段时间了，之前也了解过这门语言，直到Google确定他为Android开发的官方语言，终于下定决心学习。
# 2017/7/10
## 1.<a href="http://kotlinlang.org/">Kotlin</a>简介（粘来的，了解了解哈）
  1. Kotlin是一个基于 JVM 的新的编程语言，由 JetBrains 开发。<br>
  2. Kotlin可以编译成Java字节码，也可以编译成JavaScript，方便在没有JVM的设备上运行。<br>
  3. Kotlin与Java100%兼容。<br>
  4. and so on。（Google一下就好了哈  虽然我是百度的...>-<!）<br>
  
# 2017/7/11
## 2.Kotlin入门第一课
* Intellij创建Kotlin项目和创建java项目很相似，并且支持性非常好（毕竟亲儿子）。在创建项目时，Intellij会有JVM和JavaScript两个选择，选JVM就好了（毕竟我不是搞前段开发的哈）。<br>
* Kotlin同样具有包package的概念,导包关键字import。
* 定义类型<br>
  Kotlin定义类型有两种方式，val和var <br>
  val定义的变量只读（除赋初值外不可再赋值）<br>
  var定义的变量为可变变量<br>
  例：<br>
  val a: Int = 1    //初值为1<br>
  val a: Int        //未赋初值必须声明类型<br>
  a = 1             //初次赋值<br>
  val a = 1         //推测Int<br>
  <br>
  var a： Int<br>
  a += 5<br>
* 定义函数
  函数定义fan<br>
  例：<br>
  fun sum（a： Int，b： Int）： Int //：Int返回值为int,没有返回值则不写或<strong>:Unit</strong><br>
      return a + b<br>
  }<br>
* 常用语句
  Kotlin中if{}else{}，while（）{}等和java用法一样，但是Kotlin在这些基础上做了很多添加，也就是说在Kotlin中这些语句还有新用法（还没学会哈，后续段落添加）。<br>
  Kotlin中for语句和Java中的foreach很像，例如<br>
  for（a in args）{<br>
      print（a）<br>
  }<br>
  Kotlin中没有switch了（好紧张，那该怎么办...），当然新添加了when，用法如下（找来的例子哈）：<br>
  fun cases(obj: Any) {<br>
  &nbsp;&nbsp;when (obj) {<br>
  &nbsp;&nbsp;&nbsp;&nbsp;1          -> print("One")<br>
  &nbsp;&nbsp;&nbsp;&nbsp;"Hello"    -> print("Greeting")<br>
  &nbsp;&nbsp;&nbsp;&nbsp;is Long   -> print("Long")<br>
  &nbsp;&nbsp;&nbsp;&nbsp;!is String -> print("Not a string")<br>
  &nbsp;&nbsp;&nbsp;&nbsp;else       -> print("Unknown")<br>
  &nbsp;&nbsp;}<br>
  }<br>
  有没有感觉瞬间上了不止一个档次，反正我是感觉比switch好多了<br>
* 千里之行，始于HelloWorld<br>
  fun main(args: Array<String>) {<br>
  &nbsp;&nbsp;var a: Int<br>
  &nbsp;&nbsp;&nbsp;&nbsp;val scanner: Scanner = Scanner(System.`in`)<br>
  &nbsp;&nbsp;a = scanner.nextInt()<br>
  &nbsp;&nbsp;when (a) {<br>
  &nbsp;&nbsp;&nbsp;&nbsp;1 -> println("HelloWorld")<br>
  &nbsp;&nbsp;&nbsp;&nbsp;else -> println(sum(a, 2017))<br>
  &nbsp;&nbsp;&nbsp;&nbsp;}<br>
  &nbsp;&nbsp;}<br>
　<br>
  fun sum(a: Int = 0, b: Int = 0): Int {<br>
  &nbsp;&nbsp;return a + b<br>
  }<br>
  
# 2017/7/12
## 2.Kotlin入门之简单集合遍历
fun main(args: Array<String>) { //args: Array<String>这个东西也可以写成vararg args: String，vararg这个东西就是相当于Java的String...<br>
　　val arrays = args.flatMap {<br>
　　　　it.split("_")<br>
　　}<br>
/\*<br>
split 大家一定很熟悉，java中常用来拆分字符串，Kotlin中也是一样。it就是迭代iterator吗。至于flatMap函数原型为：<br>
<strong>public inline fun <T, R> Array<out T>.flatMap(transform: (T) -> Iterable<R>): List<R>{}</strong><br>
他是通过遍历每个元素创建一个新集合，最后，把所有集合整合到包含所有元素的唯一列表中。<br>
相同操作Java样例：<br>
public static void main(String... args) {<br>
　　for (String arg : args) {<br>
　　　　String[] arrays = arg.split("_");<br>
　　　　for (String array : arrays) {<br>
　　　　　　System.out.print(array + " ");<br>
　　　　}<br>
　　}<br>
}<br>
相比于java的同样操作是不是简单了很多。<br>
\*/<br>
　　for (array in arrays) {<br>
　　　　print("$array ")  //类似于foreach的遍历，$是字符串插入的一种形式，更简单<br>
　　}<br>
　　println()<br>
　　for (i in arrays.indices) {<br>
　　　print(arrays[i] + " ") //Kotlin中Collection<*>.indices返回的是IntRange,他表示一个范围，如0..8表示0到8<br>
　　}<br>
　　println()<br>
　　for (i in arrays.indices) {<br>
　　　　print("${arrays[i]} ") //$的用法可以跟表达式，但要在{}里写，比如${arrays.length}<br>
　　}<br>
　　println()<br>
　　for (it in arrays.iterator()) {<br>
　　　　print("$it ") //迭代<br>
　　}<br>
　　println()<br>
　　var i = 0<br>
　　while (i <= arrays.indices.endInclusive) {<br>
　　　　print(arrays[i++] + " ") //endInclusive是集合末尾<br>
　　}<br>
　　println()<br>
　　arrays.map {<br>
　　　　print(it + " ") //map1<br>
　　}<br>
　　println()<br>
　　arrays.map(::print) //map2<br>
/\*<br>
map是Kotlin的简单遍历方法，函数原型：<br>
<strong>public inline fun <T, R> Iterable<T>.map(transform: (T) -> R): List<R>{}</strong><br>
他可以接受Lambda表达式如map2（不清楚Lambda表达式的可以去Google一下哈，这里就不介绍了）<br>
到这里是不是感觉Kotlin很好用呢，哈哈，强大的还在后面呢>_<!!!<br>
\*/<br>
}<br>
