# Grammar memo

## 基中基

#### uint、unit32、unit64

都是无符号整形，在32位系统中uint和uint32相同，在64位系统中uint和uint64位相同

#### 断言

##### 通过断言实现类型转换

形如A.(T)

其中A只能为interface{}, T可以是string, int, struct等类型.

```go
func echoString(content interface{}) {
    result, err := content.(string)  //通过断言实现类型转换
    if err != nil {  // 断言失败
        fmt.Println(err .Error())  // 输出失败原因
        return
    }
    fmt.Println(result)
}
```

#### 运算符

- ##### "<< "left shift operator

  ```go
  	pow := make([]int, 10)
  	for i := range pow {
  		pow[i] = 1 << uint(i) // == 2**i
  		a := 1 << uint(i)
  		fmt.Printf("%b \n",a)
  // 结果
  // 1 10 100 ...
  ```

  1的二进制数0001，把有效值1向左移unit(i)位，正数左边第一位补0，负数补1，等于2的unit(i)次方

- ##### ">>"right shift operator

  ```go
  	p := make([]int, 6)
  	for i := range p{
  		a := 7 >> uint(i)
  		fmt.Printf("%b \n",a)
  	}
  // result
  // 111 11 1 0 0 ...
  ```

  7的二进制数0111，把有效值111向右移unit(i)位，正数左边第一位补0，负数补1，等于除以2的unit(i)次方

#### 切片

- ##### []string

  ```go
  strs := []string{"123","dsfg"}
  strs[0][0] // =="1"
  strs[0][0:0] // ==""
  ```

  

## 语法糖

### ...
##### 用法：

- 可以接受任意个数但相同类型的参数。
- slice可以被打散进行传递。

```go
func test1(args ...string) { //可以接受任意个string参数
	for _, v:= range args{
		fmt.Println(v)
	}
}

func main(){

	var strss0 = []string{
		"qwr",
		"234",
	}
	var strss1 = []string{
		"q",
	}
	strss := append(strss0,strss1...)// strss2的元素被打散一个个append进strss
	fmt.Println(strss)
	test1(strss...) //切片被打散传入
}
/* 结果：
[qwr 234 q]
qwr
234
q
*/
```

## 标准库

### fmt

- #### int转binary

  ```go
  var a uint
  a = 66
  fmt.Printf("%b \n", a)
  ```

  

### log

- #### log.Fatal

  1. 打印输出内容
  2. 退出应用程序
  3. defer函数不会执行

  ```go
  package main
   
  import (
      "log"
  )
   
  func foo() {
      defer func () { log.Print("3333")} ()
      log.Fatal("4444")
  }
  func main() {
      log.Print("1111")
      defer func () { log.Print("2222")} ()
      foo()
      log.Print("9999")
  }
  ```

  运行结果：

  ```groovy
  2018/08/20 17:48:44 1111
  2018/08/20 17:48:44 4444
  ```

### panic

1. 函数立刻停止执行 (注意是函数本身，不是应用程序停止)
2. defer函数被执行
3. 返回给调用者(caller)
4. 调用者函数假装也收到了一个panic函数，从而
   4.1 立即停止执行当前函数
   4.2 它defer函数被执行
   4.3 返回给它的调用者(caller)
5. ...(递归重复上述步骤，直到最上层函数)
   应用程序停止。
6. panic的行为

```Go
package main
import (
    "log"
)

func foo() {
    defer func () { log.Print("3333")} ()
    panic("4444")
}
func main() {
    log.Print("1111")
    defer func () { log.Print("2222")} ()
    foo()
    log.Print("9999")
}
```

运行结果：

```groovy
2018/08/20 17:49:28 1111
2018/08/20 17:49:28 3333
2018/08/20 17:49:28 2222
panic: 4444

goroutine 1 [running]:
main.foo()
        /home/.../main.go:9 +0x55
main.main()
        /home/.../main.go:15 +0x82
```


