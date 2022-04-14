---
title: Go语言深入浅出
tags:
  - Go
categories:
  - 后端开发
toc: true
date: 2022-04-13 09:15:21
---

## 背景

### Java和Go的语法区别

1. Go语言中函数是一等公民
2. 不支持Overload重载
3. 不支持@Override重写，因此math.Max(float64,float64) 不支持int

### 编译命令

#### go mod tidy

#### go build

#### go install

## 基本语法

在switch或select语句中，break的作用是跳过整个代码块，执行swith或select之后的代码。

### 作用域

1. 花括号标识一个代码块，一般都存在作用域划分的作用（花括号内的局部变量互相屏蔽）
2. 全局变量在代码块内部可以被覆盖声明，因此要避免重名（在开发规范中约定）

### 常量

```golang
const MaxUint = ^uint(0) 
```

### 变量声明

```go
// 声明多个
var maxCount,base,count int
// 短式声明（只能在函数内使用）
v:=999
s:="hello world!"
// 多赋值
base, count,s := 1, 0,"hello world!"
```

### 数据类型

#### 值类型和引用类型

值类型的特点是：变量直接存储值，内存通常在**栈中分配**

引用类型的特点是：变量存储的是一个地址，这个地址对应的空间里才是真正存储的值，内存通常在**堆中分配**

#### 值类型：数组

空接口可以标识任意类型（切片也有相同的特性）

```go
// will print [1,a]
func main() {
   a := make([]interface{},0) // 空接口可以标识任意类型
   a = append(a, 1)
   a = append(a, `a`)
   fmt.Printf("%+v", a)
}
```

#### 引用类型：切片

切片的底层是数组。

添加成员时，容量是2的指数递增的，2，4，8，16，32。而且是在长度要超过容量时，才增加容量。

```go
// 使用make初始化（推荐）
a := make([]int, 5, 10)
// 使用字面量初始化
a = []int{1,2,3,4,5}
var a= new([]int)
// append
// copy
```

#### 引用类型：Interface

#### 引用类型：map

#### 引用类型：管道channel

#### 值类型：函数

```go
var dfs func(*TreeNode) # 声明一个函数类型
```

#### 引用类型：指针

#### 值类型：int系列

```golang
uint8  : 0 to 255 
uint16 : 0 to 65535 
uint32 : 0 to 4294967295 
uint64 : 0 to 18446744073709551615 
int8   : -128 to 127 
int16  : -32768 to 32767 
int32/int  : -2147483648 to 2147483647 
int64  : -9223372036854775808 to 9223372036854775807
```

#### 值类型：float系列

#### 值类型：结构体



### 组合与方法集

golang中没有继承的概念，代码复用是通过组合的方式实现。

### 闭包

### 控制语句

#### defer

后进先出

#### switch

Go语言中的break，fallthrough

####  func

### 异常处理

#### error

#### panic

#### recover

## SDK核心包

### fmt

```go
// 打印数组
fmt.printf("%v",arr)
```

### math

### bytes

### strings

### utf8

### strconv

## 工程结构

### 环境变量与项目目录

- GOROOT 安装目录

- GOPATH 工程目录

> 1. GOPATH在项目管理中非常重要，创建项目必须确保目录在GOPATH中，多个项目用分号分隔
> 2. src 源代码
> 3. pkg 存放编译后生成的文件
> 4. bin 存放编译后生成的可执行文件

### 源代码管理

> 1. Go中使用package来结构化的组织代码
> 2. Init()函数常用于包的初始化，不能被其它函数调用，在main()方法之前自动执行
> 3. Init()函数有多个时，其执行顺序是无法确定的
> 4. import关键字将当前文件与package关联

### 命名规范

go中的变量和类型通过名称的首字母的大小写控制包外的可见性。

```go
// 包外可见
var Value1 int = 1
type DemoType {}
func (x *X) Set(i int) {
    x.a = i
}
// 包外不可见
var value2 int = 3
type fooType{}
```

## 常见问题

### 函数

#### Go语言中，函数的参数传递是值传递还是引用传递？

### 数据类型

#### 切片的扩容规则

#### 鸭子类型

