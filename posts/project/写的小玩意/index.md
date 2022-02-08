# 写的小玩意


## go

- ### 打麻将投骰子模拟器1.0

  main.go

```go
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func main()  {
	fmt.Println("欢迎使用麻将投骰子模拟器，第一次投色子的人为1号，逆时针依次编号。")
	GenerateNumber(2,12,4)
}

// 最小值，最大值，麻将人数
func GenerateNumber(min int, max int,population int){
	rand.Seed(time.Now().Unix())
	// 第一次投骰子
	tNum0 := rand.Intn(max + 1 - min) + min
	// 选出第二家
	tPeo := tNum0 % population
	if tPeo == 0 {
		fmt.Printf("第一次骰子结果是：第%d号投 \n",population - 1)
	}else {
		fmt.Printf("第一次骰子结果是：第%d号投 \n",tPeo)
	}

	// 再投，出结果
	tNum1 := rand.Intn(max + 1 - min) + min
	sumD := tNum0 + tNum1
	fmt.Printf("两次总和是%d\n",sumD)
}

```



​	
