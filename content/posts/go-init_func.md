---
title: "Go的Init方法"
date: 2022-01-10T01:38:24+08:00
---

### Go中的init方法

go中有两个特殊的函数：

1. main包中的main函数，是go可执行程序的入口函数
2. `包级别`的init函数



init 函数是一个无参数，无返回值的函数

```go
func init() {
  
}
```

Init 函数有以下逻辑：

1. 如果一个包定义了init函数，go运行时会负责在该包`初始化`时调用它的init函数

2. init不能被显式调用，否则在编译期间会报错

3. 多个包的情况下，在初始化该包时，Go运行时会按照一定次序逐一顺序的调用该包的init函数

4. 每个包内的init函数，在整个Go程序的生命周期内仅会被执行一次

5. 一般来说，先被传递给Go编译器的go源文件中的init函数先被执行， main.go作为起点

6. 同一个源文件中的多个init函数按声明顺序依次执行

7. init的加载顺序如下

   > ![img](https://cdn.learnku.com/uploads/images/202007/13/1/hVMYyqi6EU.png!large)
   >
   > 来源：[https://learnku.com/courses/go-api/1.17/config-package/11880](https://learnku.com/courses/go-api/1.17/config-package/11880)
   >
   > 解读：
   >
   > 1. 如果一个包导入了其他包，则首先初始化导入的包
   > 2. 然后初始化当前包的常量
   > 3. 接下来初始化当前包的变量
   > 4. 最后，调用当前包的init函数
   >
   > 

   
