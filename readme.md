1. 输出字符串所有排列
 * str.go

 ```
 package main

import (
	"fmt"
)

// Perm() 对 a 形成的每⼀排列调⽤ f().
func Perm(a []rune, f func([]rune)) {
	// fmt.Println(a)
	perm(a, f, 0)
	// fmt.Println(a)
}

// 对索引 i 从 0 到 len(a) - 1，实现递归函数 perm().
func perm(a []rune, f func([]rune), i int) {
	length := len(a)
	if length > 20 {
		panic("This slice is too long to print")
	}
	if i != length {
		strMap := make(map[string]int)
		for j := i; j < length; j++ {
			_, ok := strMap[string(a[j])]
			if !ok {
				strMap[string(a[j])] = 1
				if j != i {
					a[i], a[j] = a[j], a[i]
				}
				perm(a, f, i+1)
				
				// recover slice
				if j != i {
					a[i], a[j] = a[j], a[i]
				}
			}
		}
	} else {
		f(a)
	}
}

func main() {
	Perm([]rune("abc"), func(a []rune) {
		fmt.Println(string(a))
	})
}
 ```

 * str_test.go
 ```
 package main

import (
	"fmt"
	"testing"
)

func TestPerm(t *testing.T) {
	Perm([]rune("abc"), func(a []rune) {
		fmt.Println(string(a))
	})
}
 ```

 * go test -cover -v str.go str_test.go

2. 排⾏榜系统
 * 基于Redis有序集合实现
 * 内存占用：100W条数据，member为16位随机字符串，score为0~10000随机值，占用内存120M左右
 * score格式：实际分值.(9999999999 - 当前时间戳)，保证分值相同时玩家排名靠前
 * 根据当前玩家member可获取到当前排名`ZRANK key member`，前后取10位排名即可，`ZRANGE key start stop [withscores]`
 
3. rand5()和rand13()
 * 根据rand13()构造rand5()
 * 根据rand5()构造rand13()

4. 拼图游戏
 * 定义拼图小格子结构体
 * 定义拼图矩形结构体
 * 维护一个已拼图的map结果，每次放置或取下则更新此map

 

