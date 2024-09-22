
菜鸟教程：[Go 语言教程 | 菜鸟教程 (runoob.com)](https://www.runoob.com/go/go-tutorial.html)
**MarkDown大纲**
### Go语言的基础组成
包声明
引入包
函数
变量
语句&表达式
注释

Go标记

行分隔符
	Go编译器自动分行，单行多语句需要加 “；” 但是不提倡

注释 
~~~go
//单行注释
/*这是
多行注释
*/
~~~

标识符
	python类似

字符串连接
	用“+”连接

关键字/保留字/标识符
![[截屏2024-08-13 21.57.01.png]]

格式化字符串
	**Sprintf**根据格式化参数生成字符串-返回字符串
	**Printf**根据格式化参数生成字符串-写入标准输出



### Go语言数据类型
bool
数字：int/uint，float32/64，byte
字符串：UTF-8
派生：指针、数组、结构化、函数等


### Go语言变量
变量声明
~~~go
var identifier type
or
var identifier type = value
or
var identifier1, identifier2 type
or
var identifier = true
or 
identifier := 1 //初始化声明，不可用于全局变量
1. 如果定义时未赋值则为系统默认值：0，false等
2. 支持一次声明多个变量
3. 可以根据赋值自行判断变量类型
4. 不能重复声明变量
5. intVal := 1 等同于 var intVal int ； intVal = 1 
~~~
多变量声明
~~~go
var vname1, vname2, vname3 type
vname1, vname2, vname3 = v1, v2, v3
or
var vname1, vname2, vname3 = v1, v2, v3 //类python
or
vname1, vname2, vname3 := v1, v2, v3
a, b, c := 5, 7, "abc"
or
var ( //一般用于全局变量
	vname1 v_type1
	vname2 v_type2
)
~~~
值类型和引用类型 **？**
使用“j = i”赋值实际上为在内存中对i的值进行拷贝
对于引用类型的变量，修改=后变量的值会对=前的变量产生影响

交换变量值
~~~go
a, b = b, a
~~~


### Go语言常量
~~~go
const identifier type = value
or
const identifier = value

//用作枚举
const （
	a = 0
	b = 1
	c = 2
）

//常量表达式中可包含内置函数
const （
	a = "abc"
	b = len(a)
	c = unsafe.Sizeof(a)
）

//特殊 iota
//iota在const关键字出现的时候被重制为0，const中每新增一行常量声明将使iota计数一次
//iota可以理解为const语句块中的行索引
//iota可被用作枚举值
const （
	a = iota //iota = 0
	b = iota //iota = 1
	c = iota //iota = 2
	d = 'ha' //iota = 3
	e = iota //iota = 4
）

~~~


### Go语言运算符
1. 算术运算符
	+, -, \*, /, %, ++(自增), --（自减）
2. 关系运算符
	\==，!=, >, <, >=, <=
3. 逻辑运算符
	&&(and), ||(or), !(not)
4. 位运算符
	&, |, ^, <<, >>
	![[截屏2024-08-14 18.54.59.png]]
5. 赋值运算符
	=, +=, -=, \*=, /=, %=, <<=, >>=, &=(按位与后赋值), ^=, !=
6. 其他运算符
	&(返回变量储存地址), \*(指针变量)
运算符优先级：类python ，可通过加（）临时提升优先级


### Go语言条件语句
 1. if
 2. if----else
 3. if嵌套
 4. switch
 5. select
 **Go不支持三目运算符，无法使用a?b:c的形式进行条件判断**


### Go语言循环语句
for/循环嵌套
Go支持的循环控制：
1. break
2. continue
3. goto


### Go语言函数
函数定义格式：
~~~go
func function_name([parameter list])[return_types] {
	函数体
}
//不需要返回值的函数不需要[return_types]这部分
~~~
默认情况下，Go语言在函数体内使用的是值传递，即在调用函数传入参数时不会影响到外部的实际参数。
函数用法：==？
1. 函数作为另一个函数的实参数
2. 闭包 // 匿名函数，可在动态编程中使用
3. 方法 // 包含了接受者的函数


### Go语言变量作用域
- 函数内定义——局部变量
- 函数外定义——全局变量
- 函数定义中——形式参数


### Go语言数组
~~~go
//声明数组
var arrayName [size]daatType

//初始化数组
var numbers [5]int
or
var numbers = [5]int{1, 2, 3, 4, 5}
or
numbers := [5]int{1, 2, 3, 4, 5}
or
numbers := [...]int{1, 2, 3, 4, 5} //数组长度不固定
or
numbers := [5]int{1:2, 3:7} //在固定数组长度时可通过指定下标赋值

//访问数组元素
var salary float32 = balance[9]
~~~


### Go指针
~~~go
//指针声明格式：
var var_name *var_type //var_type为指针类型
as
var ip *int     /* 指向整形 */
var fp *float32 /* 指向浮点型 */
~~~
#### 指针使用流程
~~~go
package main

import "fmt"

func main(){
	var a int = 20
	var ip *int

	ip = &a

	fmt.Printf("a变量的地址是：%x\n", &a)
	fmt.Printf("ip变量储存的指针地址：%x\n", ip)
	fmt.Printf("*ip变量的值：%d\n", *ip)
}
~~~
返回结果
![[截屏2024-08-14 20.26.08.png]]

#### Go空指针
当一个指针被定义后没有分配到任何变量时，它的值为nil
nil指针被称为空指针
*一个指针变量通常缩写为**ptr***
~~~go
package main
import "fmt"
func main(){
	var ptr *int
	fmt.Printf("ptr的值为：%x\n", ptr)
}

//输出结果
ptr的值为：0

//空指针判断
if(ptr != nil)
if(ptr == nil)
~~~

#### Go语言指针数组
实例：
~~~go
package main
import "fmt"
const Max int = 3
func main() {
	a := []int{10, 100, 200}
	var i int
	var ptr [MAX]*int;
	for i=0; i<MAX; i++ {
		ptr[i] = &a[i] /*整数地址赋值给指针数组*/
	}
	for i=0; i<MAX; i++ {
		fmt.Printf("a[%d] = %d\n", i, *ptr[i])
	}
}

// 输出结果
a[0] = 10
a[1] = 100
a[2] = 200
~~~

#### Go语言指向指针的指针
当定义一个指向指针的指针变量时，第一个指针存放第二个指针的地址，第二个指针存放变量的地址：
![[Pasted image 20240821154128.png]]
~~~go
// 指向指针的指针变量声明格式：
var ptr **int

// 访问实例
var a int
var ptr *int
var pptr **int

a = 3000

ptr = &a

pptr = &ptr

// a == *ptr == **pptr
~~~

#### Go语言指针作为函数参数
实例：
~~~go
package main
import "fmt"
func main(){
	var a int = 100
	b := 200

	// 调用函数用于交换值
	swap(&a, &b);
}

func swap(x *int, y *int){
	var tamp int
	temp = *x
	*x = *y
	*y = temp
}
~~~



### Go语言结构体
#### 定义结构体
结构体的定义格式如下：
~~~go
type struct_variable_type struct {
	member definition
	member definition
	...
	member definition
}
~~~
定义了结构体类型后，可用于变量的声明：
~~~go
variable_name := structure_variable_type {value1, value2, ..., valuen}
or
vairable_name := structure_variable_type {key1: value1, key2: value2, ...  keyn: valuen}. //忽略的字段为0或nil
or
variable_name := structure_variable_type {key1 => value1, ...}
~~~
#### 访问结构体成员
~~~go
//访问格式：
structure_variable.key1

//实例
type Books struct {
	title string
	author string
	subject string
	book_id int
}

func main() {
	var Book1 Books

	Book1.title = "Go语言"
	Book1.author = "菜鸟教程"
	Book1.subject = "Go语言教程"
	Book1.book_id = 123456
}
~~~

#### 结构体作为函数参数
实例：
~~~go
package main

import "fmt"

type Books struct {
	title string
	author string
	subject string
	book_id int
}

func main() {
	var Book1 Books

	Book1.title = "Go语言"
	Book1.author = "菜鸟教程"
	Book1.subject = "Go语言教程"
	Book1.book_id = 123456

	printBook(Book1)
}

func printBook(book Books) {
	fmt.Printf("Book title : %s\n", book.title)
	fmt.Printf("Book author : %s\n", book.author)
	fmt.Printf("Book subject : %s\n", book.subject)
	fmt.Printf("Book book_id : %d\n", book.book_id)
}
~~~
#### 结构体指针
指向结构体的指针类似于其他指针变量：
~~~go
var struct_pointer *Books
~~~
查看结构体变量地址：
~~~go
struct_pointer = &Book1
~~~
使用结构体指针访问结构体成员：
~~~go
s
truct_pointer.title
~~~


### Go语言切片
Go语言切片是对数组的抽象
Go数组的长度不可变，在特定场景中不太适用，对此，Go中提供了一种灵活，功能强悍的内置类型切片（“动态数组”），与数组相比切片的长度是不固定的，可以追加元素，在追加时可以使得切片的容量增大
#### 定义切片
切片的定义说明：
~~~go
// 通过声明一个未指定大小的数组来定义切片
var identifier []type

// 使用make()函数来创建切片
var slice1 []type = make([]type, len)
or
slice1 := make([]type, len)
// 可以在make()函数中通过capacity参数指定容量
make([]T, lenght, capcity)
//上述len为切片的初始长度
~~~
切片初始化
~~~go
//直接初始化切片
s := [] int{1, 2, 3}

//通过引用数组初始化切片
s := arr[:]
or
s := arr[startIndex: endIndex]
or
s := arr[startIndex:]
or
s := arr[:endIndex]

//通过切片s初始化切片
s1 := s[startIndex: endIndex]

//通过内置函数make()初始化切片s，[]int标识为其元素类型为int的切片
s := make([]int, len, cap)
~~~
#### len()和cap()函数
切片可索引，可通过len()函数获取长度，可通过cap()函数测量切片容量。
~~~go
package main
import "fmt"

func main() {
	var numbers = make([]int, 3, 5)
	printSlice(numbers)
}

func printSlice(x []int) {
	fmt.Printf("len=%d cap=%d slice=%v\n", len(x), cap(x), x)
}

//输出结果
len=3 cap=5 slice=[0 0 0]
~~~
#### 空(nil)切片
一个切片在未初始化之前默认为nil，长度为0
~~~go
package main
import "fmt"

func main() {
	var numbers []int
	printSlice(numbers)
	if (numbers == nil){
		fmt.Printf("切片为空")
	}
}

func printSlice(x []int) {
	fmt.Printf("len=%d cap=%d slice=%v\n", len(x), cap(x), x)
}

//输出：
len=0 cap=0 slice=[]
切片是空的
~~~
#### 切片截取
可以通过设置上下限来设置截取切片
_[lower-bound:upper-bound]_
类似python数组切片操作
#### append()和copy()函数
如果想增加切片的容量，必须创建一个新的更大的切片并把原分片的内容都拷贝过来
可以使用拷贝切片的copy方法以及向切片追加新元素的append方法。
~~~go
var numbers []int

//append()
numbers = append(numbers, 0)
or
numbers = append(numbers, 1, 2, 3) //添加多个元素

//copy()
numbers1 := make([]int, len(numbers), (cap(numbers))*2)
copy(numbers1, numbers)
~~~

### Go语言范围(Range)
Go语言中range关键字可用于for循环中迭代数组、切片、通道或集合的元素
**映射/集合(Map)**
for循环的range格式可以省略key和value，如下：
~~~go
//创建空map
oldMap := make(map[int]float32)

//添加key-value对
oldMap[1] = 1.0
oldMap[2] = 2.0
oldMap[3] = 3.0
oldMap[4] = 4.0

for key, value := range oldMap {
	newMap[key] = value
}

//只读取key
for key := range oldMap
or 
for key, _ := range oldMap

//只读取value
for _, value := range oldMap
~~~
**字符串**
range迭代字符串时，返回每个字符的索引和Unicode代码点（rune）。
~~~go
package main
import "fmt"

func main() {
	for i, c := range "hello" {
		fmt.Printf("index: %d, char: %c\n", i, c)
	}
}

//输出
index: 0, char: h
index: 1, char: e
index: 2, char: l
index: 3, char: l
index: 4, char: o
~~~
**通道(Channel)**
range遍历从通道接收的值，直到通道关闭
~~~go
package main
import "fmt"

func main() {
	ch := make(chan int, 2)
	ch <- 1
	ch <- 2
	close(ch)

	for v := range ch {
		fmt.Println(v)
	}
}

//输出
1
2
~~~


### Go语言Map（集合）
#### Map定义
可以使用内建函数make或者使用map关键字来定义Map：
~~~go
// 使用make函数
map_variable := make(map[KeyType]ValueType, initialCapcity)
as
m := make(map[string]int)
or
m := make(map[string]int, 10)

// 使用字面量创建Map
m := map[string]int{
	"apple": 1,
	"banana": 2,
	"orange": 3,
}

// 获取键值对
v1 := m["apple"]
v2, ok := m["pear"] //如果键不存在，则ok返回false，v2的值为该类型的零值

// 修改键值对
m["apple"] = 5

// 获取Map的长度
len := len(m)

// 遍历Map
for k, v := range m {
	fmt.Printf(key=%s, value=%d\n, k, v)
}

//删除元素：
delete(m, "banana")
~~~

### Go语言递归函数
语法格式：
~~~go
func recursion() {
	recursion() 
}
func main() {
	recursion()
}
~~~
几个经典的递归应用
**阶乘**
~~~go
package main
import "fmt"

func Factorial(n uint64)(result uint64) {
	if(n>0) {
		result = n * Factorial(n-1)
		return result
	}
	return 1
}

func main() {
	var i int = 15
	fmt.Printf("%d 的阶乘是 %d\n", i, Factorial(uint64(i)))
}
~~~
**斐波那契数列**
~~~go
package main
import "fmt"

func fibonacci(n int) int {
	if n < 2 {
		return n
	}
	return fibonacci(n-2) + fibonacci(n-1)
}

func main() {
	var i int
	for i = 0; i < 10; i++ {
		fmt.Printf("%d\t", fibonacci(i))
	}
}
~~~
**求平方根**
~~~go
package main
import "fmt"

func sqrtRecursive(x, guess, prevGuess, epsilon float64) float64 {
	if diff := guess*guess - x; diff < epsilon && -diff < epsilon {
		return guess
	}
	newGuess := (guess + x/guess) / 2
	if newGuess == preGuess {
		return guess
	}

	return sqrtRecursive(x, newGuess, guess, epsilon)
}

func sqrt(x float64) float64 {
	return sqrtRecursive(x, 1.0, 0.0, 1e-9)
}

func main() {
	x := 25.0
	result := sqrt(x)
	fmt.Printf("%.2f 的平方根为 %.6f\n", x, result)
}
~~~

### Go语言转换
#### 基本格式：
~~~go
type_name(expression)

// 整形转换为浮点型
var a int = 10
var b float64 = float64(a)

// 字符串类型转换
// 将str转换为整形变量num
var str string = "10"
var num int
num, _ = strconv.Atoi(str) 
// 整数转字符串
num := 123  
str := strconv.Itoa(num)
// 字符串转浮点
str := "3.14"  
num, err := strconv.ParseFloat(str, 64)
//浮点转字符串
num := 3.14  
str := strconv.FormatFloat(num, 'f', 2, 64)
~~~
#### 接口类型转换

- [ ] 可以加上点Go中接口的定义及使用 or 这一小节放在接口后面
Go的接口转换有两种情况：类型断言和类型转换。
**类型断言**
类型断言用于将接口类型转换为指定类型，其语法为：
~~~go
value.(type)
or
value.(T)
~~~
实例：
~~~go
package main
import "fmt"

func main() {
	var i interface{} = "Hello, World"
	str, ok := i.(string)
	if ok {
		fmt.Printf("'%s' is a string\n", str)
	} else {
		fmt.Println("conversion failed")
	}
}
~~~
**类型转换**
类型转换用于将一个接口类型的值转换为另一个接口类型，其语法为：
~~~go
T(value)
~~~
实例：
~~~go
package
import "fmt"

// 定义一个接口Writer
type Writer interface {
	Write([]byte) (int, error)
}

// 实现Writer接口的结构体StringWriter
type StringWriter struct {
	str string
}

// 实现Write方法
func (sw * StringWriter) Write(data []byte) (int, error) {
	sw.str += string(data)
	return len(data), nil
}

func main() {
	// 创建一个StringWriter实例并赋值给Writer接口变量
	var w Writer = &StringWriter{}

	// 将Writer接口类型转换为StringWriter类型
	sw := w.(*StringWriter)
	
	// 修改StringWriter的字段
	sw.str = "Hello, World"
	
	// 打印StringWriter的字段值
	fmt.Println(sw.str)

}
~~~
**空接口类型**
空接口interface{}可以持有任何类型的值。在实际应用中，空接口经常被用来处理多种类型的值。
~~~go
package main
import "fmt"

func printValue(v interface{}) {
	switch v := v.(type) {
	case int:
		fmt.Println("Integer:", v)
	case string:
		fmt.Println("String:", v)
	default:
		fmt.Println("Unknown type")
	}
}

func main() {
	printValue(42)
	printValue("hello")
	printValue(3.14)
}
~~~


---
### Go语言接口
Go的接口类型把所有的具有共性的方法定义在一起，任何其他类型只要实现了这些方法就是实现了这个接口。
接口可以将不同的类型绑定到一组公共的方法上，从而实现多态和灵活的设计。
Go语言中的接口是隐式实现的，即如果一个类型实现了一个接口定义的所有方法，那么它就自动地实现了该接口。因此，我们可以通过将接口作为参数来实现对不同类型的调用，从而实现多态。
**实例**
```go
/* 定义接口 */
type interface_name interface {
   method_name1 [return_type]
   method_name2 [return_type]
   method_name3 [return_type]
   ...
   method_namen [return_type]
}

/* 定义结构体 */
type struct_name struct {
   /* variables */
}

/* 实现接口方法 */
func (struct_name_variable struct_name) method_name1() [return_type] {
   /* 方法实现 */
}
...
func (struct_name_variable struct_name) method_namen() [return_type] {
   /* 方法实现*/
}
```
- 应用实例1
```go
package main
import  "fmt"

type Phone interface {
    call()
}

type NokiaPhone struct {
}

func (nokiaPhone NokiaPhone) call() {
    fmt.Println("I am Nokia, I can call you!")
}

type IPhone struct {
}

func (iPhone IPhone) call() {
    fmt.Println("I am iPhone, I can call you!")
}

func main() {
    var phone Phone

    phone = new(NokiaPhone)
    phone.call()

    phone = new(IPhone)
    phone.call()
}
```
- 应用实例2

```go
package main

import "fmt"

type Shape interface {
    area() float64
}

type Rectangle struct {
    width  float64
    height float64
}

func (r Rectangle) area() float64 {
    return r.width * r.height
}

type Circle struct {
    radius float64
}

func (c Circle) area() float64 {
    return 3.14 * c.radius * c.radius
}

func main() {
    var s Shape

    s = Rectangle{width: 10, height: 5}
    fmt.Printf("矩形面积: %f\n", s.area())

    s = Circle{radius: 3}
    fmt.Printf("圆形面积: %f\n", s.area())
}
```

---

### Go错误处理
Go语言通过内置的错误接口提供了非常简单的错误处理机制。
error类型是一个接口类型，其定义为：

```go
type error interface {
	Error() string
}
```
可以在编码中通过实现error接口类型来生成错误信息。
函数通常在最后的返回值中返回错误信息。使用error.New可返回一个错误信息：

```go
package main
import "fmt"

func Sqrt(f float64) (floatt64, error) {
	if f < 0 {
		return 0, errors.New("math: square root of negative number")
	}
}

func main() {
	result, err := Sqrt(-1)

	if err != nil {
		fmt.Println(err)
	}
}
```
**实例**

```go
package main

import (
    "fmt"
)

// 定义一个 DivideError 结构
type DivideError struct {
    dividee int
    divider int
}

// 实现 `error` 接口
func (de *DivideError) Error() string {
    strFormat := `
    Cannot proceed, the divider is zero.
    dividee: %d
    divider: 0
`
    return fmt.Sprintf(strFormat, de.dividee)
}

// 定义 `int` 类型除法运算的函数
func Divide(varDividee int, varDivider int) (result int, errorMsg string) {
    if varDivider == 0 {
            dData := DivideError{
                    dividee: varDividee,
                    divider: varDivider,
            }
            errorMsg = dData.Error()
            return
    } else {
            return varDividee / varDivider, ""
    }

}

func main() {

    // 正常情况
    if result, errorMsg := Divide(100, 10); errorMsg == "" {
            fmt.Println("100/10 = ", result)
    }
    // 当除数为零的时候会返回错误信息
    if _, errorMsg := Divide(100, 0); errorMsg != "" {
            fmt.Println("errorMsg is: ", errorMsg)
    }

}
```
---

### Go并发
并发是指程序同时执行多个任务的能力
Go语言支持并发，通过goroutines和channels提供了一种简洁高效的方式来实现并发。
**goroutine**
goroutine是轻量级线程，goroutine的调度是由Golang运行时进行管理的。
goroutine语法格式：

```go
go 函数名(参数列表)
as
go f(x, y, z)
//开启一个新的goroutine
f(x, y, z)
```
Go允许使用go语句开启一个新的运行期线程，即goroutine，以一个不同的、新创建的goroutine来执行一个函数。同一个程序中的所有goroutine共享同一个地址空间。
**实例**
```go
package main

import (
        "fmt"
        "time"
)

func say(s string) {
        for i := 0; i < 5; i++ {
                time.Sleep(100 * time.Millisecond)
                fmt.Println(s)
        }
}

func main() {
        go say("world")
        say("hello")
}
```
#### 通道（channel）
通道（channel）是用来传递数据的一个数据结构。
通道可用于两个goroutine之间通过传递一个指定类型的值来同步运行和通讯。
使用make函数创建一个channel，使用<-操作符发送和接收数据。如果未指定方向，则为双向通道。

```go
ch <- v //把v发送到通道ch
v := <- ch //从ch接收数据并把值赋给v
```
通道的声明使用chan关键字，通道在使用前必须先创建：

```go
ch := make(chan int)
```
**实例**
```go
package main
import "fmt"

func sum(s []int, c chan int) {
	sum := 0
	for _, v := range s {
		sum += v
	}
	c <- sum //把sum发送到通道c
}
func main(){
	s := []int{7, 2, 8, -9, 4, 0}
	c := make(chan int)
	go sum(s[:len(s)/2], c)
	go sum(s[len(s)/2], c)
	x, y := <-c, <-c //从通道c中接收
	fmt.Println(x, y, x+y)
}
```
##### 通道缓冲区
通道可以设置缓冲区，通过make的第二个参数指定缓冲区大小：
```go
ch := make(chan int, 100)
```
带缓冲区的通道允许发送端的数据发送和接收端的数据获取处于异步状态，即发送端发送的数据可以放在缓冲区里面，可以等待接收端去获取数据，而不是立刻需要接收端去获取数据。
由于缓冲区的大小有限，因此还是必须有接收端来接收数据，否则缓冲区一满，数据发送端就无法再发送数据。
**注** ：
- 如果通道不带缓冲，发送方会阻塞直到接收方从通道中接收了值。如果通道带缓冲，发送方则会阻塞直到发送的值被拷贝到缓冲区内；
- 如果缓冲区已满，则意味着需要等待直到某个接收方获取到一个值。接收方在有值可以接受之前会一直阻塞。
**实例**
```go
package main

import "fmt"

func main() {
    // 这里我们定义了一个可以存储整数类型的带缓冲通道
        // 缓冲区大小为2
        ch := make(chan int, 2)

        // 因为 ch 是带缓冲的通道，我们可以同时发送两个数据
        // 而不用立刻需要去同步读取数据
        ch <- 1
        ch <- 2

        // 获取这两个数据
        fmt.Println(<-ch)
        fmt.Println(<-ch)
}
```
##### Go遍历通道与关闭通道
Go通过range关键字来实现遍历读取到的数据，类似于与数组或切片。格式如下：
```go
v, ok := <-ch
```
如果通道接收不到数据后ok就为false，此时通道可以使用close()函数来关闭。
**实例**
```go
package main

import (
        "fmt"
)

func fibonacci(n int, c chan int) {
        x, y := 0, 1
        for i := 0; i < n; i++ {
                c <- x
                x, y = y, x+y
        }
        close(c)
}

func main() {
        c := make(chan int, 10)
        go fibonacci(cap(c), c)
        // range 函数遍历每个从通道接收到的数据，因为 c 在发送完 10 个
        // 数据之后就关闭了通道，所以这里我们 range 函数在接收到 10 个数据
        // 之后就结束了。如果上面的 c 通道不关闭，那么 range 函数就不
        // 会结束，从而在接收第 11 个数据的时候就阻塞了。
        for i := range c {
                fmt.Println(i)
        }
}
```
##### Select语句
Select语句使得一个goroutine可以等待多个通信操作。select会阻塞，直到其中的某个case可以继续执行：
```go
package main

import "fmt"

func fibonacci(c, quit chan int) {
    x, y := 0, 1
    for {
        select {
        case c <- x:
            x, y = y, x+y
        case <-quit:
            fmt.Println("quit")
            return
        }
    }
}

func main() {
    c := make(chan int)
    quit := make(chan int)

    go func() {
        for i := 0; i < 10; i++ {
            fmt.Println(<-c)
        }
        quit <- 0
    }()
    fibonacci(c, quit)
}
```
##### 并发编程小结：
- **Goroutines**是轻量级线程，使用go关键字自动
- **Channels**用于goroutines之间的通信。
- **Select**语句用于等待多个channel操作。

---

### 其他
**语法补充**
1. 代码中 **{** 不能单独放在一行，例如：
	~~~go
	func main()    
	{  // 错误，{ 不能在单独的行上  
	    fmt.Println("Hello, World!")  
	}
	~~~
2.  不支持三目运算符
3. Go中数组的大小是类型的一部分，不同大小的数组是不兼容的，即[5]int和[10]int是两个不同的类型
4. ==fmt.Printf函数的通用占位符：%v ，go语言会自动识别

