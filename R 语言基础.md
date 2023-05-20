# R 语言基础

### 变量赋值

最新版本的 R 语言的赋值可以使用左箭头 **<-**、等号 **=** 、右箭头 **->** 赋值:

```R
# 使用等号 = 号赋值
> var.1 = c(0,1,2,3)          
> print(var.1)
[1] 0 1 2 3

# 使用左箭头 <-赋值
> var.2 <- c("learn","R")  
> print(var.2)
[1] "learn" "R"
   
# 使用右箭头 -> 赋值
> c(TRUE,1) -> var.3
> print(var.3)
[1] 1 1         
```

查看已定义的变量可以使用 **ls()** 函数：

```R
> print(ls())
[1] "var.1" "var.2" "var.3"
```

删除变量可以使用 **rm()** 函数：

```R
> rm(var.3)
> print(ls())
[1] "var.1" "var.2"
```

## 输入输出

### print() 输出

**print()** 是 R 语言的输出函数。

和其他编程语言一样，R 语言支持数字、字符等输出。

输出的语句十分简单：

```R
print("RUNOOB")
print(123)
print(3e2)
```

R 语言与 node.js 和 Python 一样，是解释型的语言，所以我们往往可以像使用命令行一样使用 R 语言。

如果我们在一行上进输入一个值，那么 R 也会把它直接标准化输出：

```R
> 5e-2
[1] 0.05
```

### cat() 函数

如果需要输出结果的拼接，我们可以使用 **cat()** 函数：

```R
> cat(1, "加", 1, "等于", 2, '\n')
1 加 1 等于 2
```

<font color='red'>**cat()** 函数会在每两个拼接元素之间自动加上空格。</font>

### 输出内容到文件

R 语言输出到文件的方法十分多样，而且很方便。

**cat()** 函数支持直接输出结果到文件：

`cat("RUNOOB", file="/Users/runoob/runoob-test/r_test.txt")`

这个语句不会在控制台产生结果，而是把 "RUNOOB" 输出到 "/Users/runoob/runoob-test/r_test.txt" 文件中去。

file 参数可以是<font color='red'>绝对路径或相对路径，建议使用绝对路径</font>，Windows 路径格式为 **D:\\r_test.txt**。

```R
cat("RUNOOB", file="D:\\r_test.txt")
```

注意：<font color='red'>这个操作是"覆盖写入"操作，请谨慎使用，因为它会将输出文件的原有数据清除</font>。

如果想"追加写入"，请不要忘记设置 append 参数：

```R
cat("GOOGLE", file="/Users/runoob/runoob-test/r_test.txt", append=TRUE)
```

### sink()

sink() 函数可以<font color='red'>把控制台输出的文字直接输出到文件中去</font>：

```
sink("/Users/runoob/runoob-test/r_test.txt")
```

这条语句执行以后，<font color='red'>任何控制台上的输出</font>都会被写入到 "/Users/runoob/runoob-test/r_test.txt" 文件中去，控制台将不会显示输出。

注意：这个操作也是"覆盖写入"操作，会直接清除原有的文件内容。

<font color='red'>如果我们依然像保留控制台的输出，可以设置 split 属性：</font>font>

`sink("/Users/runoob/runoob-test/r_test.txt", split=TRUE)`

如果想取消输出到文件，可以调用无参数的 sink ：

`sink()`

```R
sink("r_test.txt", split=TRUE)  # 控制台同样输出
for (i in 1:5)
    print(i)
sink()   # 取消输出到文件

sink("r_test.txt", append=TRUE) # 控制台不输出，追加写入文件
print("RUNOOB")
```

执行以上代码，<font color='red'>当前目录下会生存一个 r_test.txt 文件</font>

### 文字输入

可能我们会联想到 C 语言中的 scanf 、Java 中的 java.util.Scanner，如果你学习过 Python 可能对 input() 函数更熟悉。但是 R 语言本身作为一种解释型的语言，更类似于一些终端脚本语言（比如 bash 或者 PowerShell），这些语言是基于命令系统的，本身就需要输入和输出且不适合开发面向用户的应用程序（因为他们本身就是给最终用户使用的）。因此 R 语言没有专门再从控制台读取的函数，文字输入在 R 的使用中一直在进行。

### 从文件读入文字

R 语言中有丰富的文件读取函数，但是如果纯粹的想将某个文件中的内容读取为字符串，可以使用 `readLines` 函数：

```R
readLines("/Users/runoob/runoob-test/r_test.txt")
```

读取结果是两个字符串，分别是所读取的文件包含的两行内容。

**注意：** *所读取的文本文件每一行 (包括最后一行) 的结束必须有换行符，否则会报错。*

### 其他方式

除了文字的简单输入输出以外，R 还提供了很多输入数据和输出数据的方法，R 语言最方便的地方就是可以将数据结构直接保存到文件中去，而且支持保存为 CSV、Excel 表格等形式，并且支持直接地读取。这对于数学研究者来说无疑是非常方便的。但是这些功能对于 R 语言的学习影响不大，我们将在之后的章节提到。

### 工作目录

对于文件操作，我们需要设置文件的路径，R 语言可以通过以下两个行数来获取和设置当前的工作目录：

- **getwd()** : 获取当前工作目录

- **setwd()** : 设置当前工作目录

- ```R
  # 当前工作目录
  print(getwd())
  
  # 设置当前工作目录
  setwd("/Users/runoob/runoob-test2")
  
  # 查看当前工作目录
  print(getwd())
  
  [1] "/Users/runoob/runoob-test"
  [1] "/Users/tianqixin/runoob-test2"
  ```

# R 包

包是 R 函数、实例数据、预编译代码的集合，包括 R 程序，注释文档、实例、测试数据等。

R 语言相关的包一般存储安装目录下对 "library" 目录，默认情况在 R 语言安装完成已经自带来一些常用对包，当然我们也可以在后期自定义添加一些要使用的包。

### 查看 R 包的安装目录 .libPaths()

```R
> .libPaths()
[1] "/Library/Frameworks/R.framework/Versions/4.0/Resources/library"
```

### 查看已安装的包 library()

### 查看已载入的包 **search**()

## 安装新包 **install.packages()** 

`install.packages("要安装的包名")`

我们国内一般建议大家使用国内镜像，以下实例使用清华源进行安装：

```
# 安装 XML 包
install.packages("XML", repos = "https://mirrors.ustc.edu.cn/CRAN/")
```

### 使用包

`library("包名")`

# R 基础运算

本章介绍 R 语言的简单运算。

## 赋值

一般语言的赋值是 **=** 号，但是 R 语言是数学语言，所以赋值符号与我们数学书上的伪代码很相似，是一个<font color='red'>左箭头 **<-**</font> ：

### 实例

```R
a <- 123
b <- 456
print(a + b)
```

## 数学运算符

| 优先级 | 符号 | 含义     |
| ------ | ---- | -------- |
| 1      | ()   | 括号     |
| 2      | ^    | 乘方运算 |
| 3      | %%   | 整除求余 |
|        | %/%  | 整除     |
| 4      | *    | 乘法     |
|        | /    | 除法     |
| 5      | +    | 加法     |
|        | -    | 减法     |

## 关系运算符

关系运算符比较两个向量，将第一向量与第二向量的每个元素进行比较，结果返回一个布尔值。

| 运算符 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| >      | 判断第一个向量的每个元素是否大于第二个向量的相对应元素。     |
| <      | 判断第一个向量的每个元素是否小于第二个向量的相对应元素。     |
| ==     | 判断第一个向量的每个元素是否等于第二个向量的相对应元素。     |
| !=     | 判断第一个向量的每个元素是否不等于第二个向量的相对应元素。   |
| >=     | 判断第一个向量的每个元素是否大于等于第二个向量的相对应元素。 |
| <=     | 判断第一个向量的每个元素是否小于等于第二个向量的相对应元素。 |

```R
v <- c(2,4,6,9)
t <- c(1,4,7,9)
print(v>t)
print(v < t)
print(v == t)
print(v!=t)
print(v>=t)
print(v<=t)

[1]  TRUE FALSE FALSE FALSE
[1] FALSE FALSE  TRUE FALSE
[1] FALSE  TRUE FALSE  TRUE
[1]  TRUE FALSE  TRUE FALSE
[1]  TRUE  TRUE FALSE  TRUE
[1] FALSE  TRUE  TRUE  TRUE
```

## 逻辑运算符

下表列出了 R 语言支持的逻辑运算符，可用于数字、逻辑和复数类型的向量。

<font color='red'>非 0 的数字（正数或负数）都为 TRUE。</font>

逻辑运算符比较两个向量，<font color='red'>将第一向量与第二向量的每个元素进行比较，结果返回一个布尔值</font>。

| 运算符 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| &      | 元素逻辑与运算符，将第一个向量的每个元素与第二个向量的相对应元素进行组合，如果两个元素都为 TRUE，则结果为 TRUE，否则为 FALSE。 |
| ｜     | 元素逻辑或运算符，将第一个向量的每个元素与第二个向量的相对应元素进行组合，如果两个元素中有一个为 TRUE，则结果为 TRUE，如果都为 FALSE，则返回 FALSE。 |
| !      | 逻辑非运算符，返回向量每个元素相反的逻辑值，如果元素为 TRUE 则返回 FALSE，如果元素为 FALSE 则返回 TRUE。 |
| &&     | 逻辑与运算符，只对两个向量对第一个元素进行判断，如果两个元素都为 TRUE，则结果为 TRUE，否则为 FALSE。 |
| \|\|   | 逻辑或运算符，只对两个向量对第一个元素进行判断，如果两个元素中有一个为 TRUE，则结果为 TRUE，如果都为 FALSE，则返回 FALSE。 |

```R
v <- c(3,1,TRUE,2+3i)
t <- c(4,1,FALSE,2+3i)
print(v&t)
print(v|t)
print(!v)

# &&、||只对第一个元素进行比较
v <- c(3,0,TRUE,2+2i)
t <- c(1,3,TRUE,2+3i)
print(v&&t)

v <- c(0,0,TRUE,2+2i)
t <- c(0,3,TRUE,2+3i)
print(v||t)

[1]  TRUE  TRUE FALSE  TRUE
[1] TRUE TRUE TRUE TRUE
[1] FALSE FALSE FALSE FALSE
[1] TRUE
[1] FALSE
```

## 赋值运算符

R 语言变量可以使用向左，向右或等于操作符来赋值。

| 运算符         | 描述       |
| -------------- | ---------- |
| <−    =    <<− | 向左赋值。 |
| −>        −>>  | 向右赋值。 |

```R
# 向左赋值
v1 <- c(3,1,TRUE,"runoob")
v2 <<- c(3,1,TRUE,"runoob")
v3 = c(3,1,TRUE,"runoob")
print(v1)
print(v2)
print(v3)


# 向右赋值
c(3,1,TRUE,"runoob") -> v1
c(3,1,TRUE,"runoob") ->> v2
print(v1)
print(v2)

[1] "3"      "1"      "TRUE"   "runoob"
[1] "3"      "1"      "TRUE"   "runoob"
[1] "3"      "1"      "TRUE"   "runoob"
[1] "3"      "1"      "TRUE"   "runoob"
[1] "3"      "1"      "TRUE"   "runoob"
```

## 其他运算符

| 运算符 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| :      | <font color='red'>冒号运算符，用于创建一系列数字的向量。</font> |
| %in%   | <font color='red'>用于判断元素是否在向量里，返回布尔值，有的话返回 TRUE，没有返回 FALSE。</font> |
| %*%    | <font color='red'>用于矩阵与它转置的矩阵相乘。</font>        |
| %>%    | 本质上而言就是编程中常用的管道符,将上一个函数运行的结果作为下一个函数的第一个参数输入进去 |

```R
# 1 到 10 的向量
v <- 1:10
print(v)

# 判断数字是否在向量 v 中
v1 <- 3
v2 <- 15
print(v1 %in% v)
print(v2 %in% v)

# 矩阵与它转置的矩阵相乘
M = matrix( c(2,6,5,1,10,4), nrow = 2,ncol = 3,byrow = TRUE)
t = M %*% t(M)
print(t)

[1]  1  2  3  4  5  6  7  8  9 10
[1] TRUE
[1] FALSE
     [,1] [,2]
[1,]   65   82
[2,]   82  117
```

## 数学函数

| 函数     | 说明                            |
| -------- | ------------------------------- |
| sqrt(n)  | n的平方根                       |
| exp(n)   | 自然常数e的n次方，              |
| log(m,n) | m的对数函数，返回n的几次方等于m |
| log10(m) | 相当于log(m,10)                 |

```R
> sqrt(4)
[1] 2
> exp(1)
[1] 2.718282
> exp(2)
[1] 7.389056
> log(2,4)
[1] 0.5
> log10(10000)
[1] 4
```

### 取整函数：

| 名称名称 | 参数模型 | 含义                       |
| -------- | -------- | -------------------------- |
| round    | (n)      | 对 n 四舍五入取整          |
|          | (n, m)   | 对 n 保留 m 位小数四舍五入 |
| ceiling  | (n)      | 对 n 向上取整              |
| floor    | (n)      | 对 n 向下取整              |

```R
> round(1.5)
[1] 2
> round(2.5)
[1] 2
> round(3.5)
[1] 4
> round(4.5)
[1] 4
```

**注意**：R 中的 round 函数有些情况下可能会"舍掉五"。

<font color='red'>当取整位是偶数的时候，五也会被舍去</font>，这一点与 C 语言有所不同。

<font color='red'>R 的三角函数是弧度制</font>：

```R
> sin(pi/6)
[1] 0.5
> cos(pi/4)
[1] 0.7071068
> tan(pi/3)
[1] 1.732051
```

### 反三角函数：

```R
> asin(0.5)
[1] 0.5235988
> acos(0.7071068)
[1] 0.7853981
> atan(1.732051)
[1] 1.047198
```

```R
> dnorm(0)
[1] 0.3989423
> pnorm(0)
[1] 0.5
> qnorm(0.95)
[1] 1.644854
> rnorm(3, 5, 2) # 产生 3 个平均值为 5，标准差为 2 的正态随机数
[1] 4.177589 6.413927 4.206032
```

这四个<font color='red'>都是用来计算正态分布的函数。它们的名字都以 norm 结尾，代表"正态分布"</font>

分布函数名字的前缀有四种：

- **d** - 概率密度函数
- **p** - 概率密度积分函数（从无限小到 x 的积分）
- **q** - 分位数函数
- **r** - 随机数函数（常用于概率仿真）

# R 数据类型

R 语言中的最基本数据类型主要有三种：

- 数字
- 逻辑
- 文本

数字常量主要有两种：

| 一般型     | 123 -0.125      |
| ---------- | --------------- |
| 科学计数法 | 1.23e2 -1.25E-1 |

逻辑类型在许多其他编程语言中常称为布尔型（Boolean），常量值只有 **TRUE** 和 **FALSE**。

<font color='red'>**注意：**R 语言区分大小写，true 或 True 不能代表 TRUE。</font>

最直观的数据类型就是文本类型。文本就是其它语言中常出现的字符串（String），<font color='red'>常量用双引号包含。在 R 语言中，文本常量既可以用单引号包含，也可以用双引号包含</font>

## 逻辑型

逻辑向量主要用于向量的逻辑运算，例如：

```R
> c(11, 12, 13) > 12
[1] FALSE FALSE  TRUE
```

which 函数是十分常见的逻辑型向量处理函数，可以用于筛选我们需要的数据的下标:

```R
> a = c(11, 12, 13)
> b = a > 12
> print(b)
[1] FALSE FALSE  TRUE
> which(b)
[1] 3
```

例如我们需要从一个线性表中筛选大于等于 60 且小于 70 的数据：

```R
> vector = c(10, 40, 78, 64, 53, 62, 69, 70)
> print(vector[which(vector >= 60 & vector < 70)])
[1] 64 62 69
```

类似的函数还有 all 和 any：

<font color='red'>all() 用于检查逻辑向量是否全部为 TRUE，any() 用于检查逻辑向量是否含有 TRUE。</font>

```R
> all(c(TRUE, TRUE, TRUE))
[1] TRUE
> all(c(TRUE, TRUE, FALSE))
[1] FALSE
> any(c(TRUE, FALSE, FALSE))
[1] TRUE
> any(c(FALSE, FALSE, FALSE))
[1] FALSE
```

## 字符串

字符串数据类型本身并不复杂，这里注重介绍字符串的操作函数：

```R
> toupper("Runoob") # 转换为大写
[1] "RUNOOB"
> tolower("Runoob") # 转换为小写
[1] "runoob"
> nchar("中文", type="bytes") # 统计字节长度
[1] 4
> nchar("中文", type="char") # 总计字符数量
[1] 2
> substr("123456789", 1, 5) # 截取字符串，从 1 到 5
[1] "12345"
> substring("1234567890", 5) # 截取字符串，从 5 到结束
[1] "567890"
> as.numeric("12") # 将字符串转换为数字
[1] 12
> as.character(12.34) # 将数字转换为字符串
[1] "12.34"
> strsplit("2019;10;1", ";") # 分隔符拆分字符串
[[1]]
[1] "2019" "10"   "1"
> gsub("/", "-", "2019/10/1") # 替换字符串
[1] "2019-10-1"
```

R 支持 perl 语言格式的正则表达式：

```R
> gsub("[[:alpha:]]+", "$", "Two words")
[1] "$ $"
```

按对象类型来分是以下 6 种（后面会详细介绍这几种类型）：

- 向量（vector）
- [列表（list）](https://www.runoob.com/r/r-list.html)
- [矩阵（matrix）](https://www.runoob.com/r/r-matrix.html)
- [数组（array）](https://www.runoob.com/r/r-array.html)
- [因子（factor)](https://www.runoob.com/r/r-factor.html)
- [数据框（data.frame)](https://www.runoob.com/r/r-data-frame.html)

![img](https://www.runoob.com/wp-content/uploads/2020/07/52988954-D570-42FD-9CFC-90CD78D361C3.jpg)

# 向量

**c()** 是一个创造向量的函数。

这里把两个二维向量相加，得到一个新的二维向量 (8, 4)。如果将一个二维向量和三维向量做运算，将失去数学意义，<font color='red'>虽然不会停止运行，但会被警告</font>。

```R
> a = c(3, 4)
> b = c(5, 0)
> a + b
[1] 8 4
```

向量中的每一个元素可以<font color='red'>通过下标单独取出</font>：

```R
> a = c(10, 20, 30, 40, 50)
> a[2]
[1] 20
```

**注意：**<font color='red'>R 语言中的"下标"不代表偏移量，而代表第几个，也就是说是从 1 开始的！</font>

R 也可以方便的取出向量的一部分：

```R
> a[1:4] # 取出第 1 到 4 项，包含第 1 和第 4 项
[1] 10 20 30 40
> a[c(1, 3, 5)] # 取出第 1, 3, 5 项
[1] 10 30 50
> a[c(-1, -5)] # 去掉第 1 和第 5 项
[1] 20 30 40
```

```R
> a = c(1, 3, 5, 2, 4, 6)
> sort(a)
[1] 1 2 3 4 5 6
> rev(a)
[1] 6 4 2 5 3 1
> order(a)
[1] 1 4 2 5 3 6
> a[order(a)]
[1] 1 2 3 4 5 6
```

向量排序 order() 函数返回的是一个向量排序之后的下标向量。

## **向量统计**

| **函数名** | **含义**                             |
| ---------- | ------------------------------------ |
| sum        | 求和                                 |
| mean       | 求平均值                             |
| var        | 方差                                 |
| sd         | 标准差                               |
| min        | 最小值                               |
| max        | 最大值                               |
| range      | 取值范围（二维向量，最大值和最小值） |

```R
> sum(1:5)
[1] 15
> sd(1:5)
[1] 1.581139
> range(1:5)
[1] 1 5
```

## **向量生成**

向量的生成可以用 **c()** 函数生成，也可以用 min:max 运算符生成连续的序列。

如果想生成<font color='red'>有间隙的等差数列</font>，可以用 seq 函数：

```R
> seq(1, 9, 2)
[1] 1 3 5 7 9
```

seq 还可以生成从 m 到 n 的等差数列，只需要指定 m, n 以及数列的长度：

```R
> seq(0, 1, length.out=3)
[1] 0.0 0.5 1.0
```

rep 是 repeat（重复）的意思，可以用于产生重复出现的数字序列：

```R
> rep(0, 5)
[1] 0 0 0 0 0
```

## NA和NULL的区别

向量中常会用到 NA 和 NULL ，这里介绍一下这两个词语与区别：

- NA 代表的是"缺失"，NULL 代表的是"不存在"。
- NA 缺失就像占位符，代表这里没有一个值，但位置存在。
- NULL 代表的就是数据不存在。

```R\> **length**(**c**(NA, NA, NULL))
> length(c(NA, NA, NULL))
[1] 2
> c(NA, NA, NULL, NA)
[1] NA NA NA
```

很显然， NULL 在向量中没有任何意义。

# R 判断语句

![img](https://www.runoob.com/wp-content/uploads/2015/12/if.png)

R 语言提供了以下类型的判断语句：

- if 语句
- if...else 语句
- switch 语句

## if 语句

一个 if 语句 由一个布尔表达式后跟一个或多个语句组成。

```R
if(boolean_expression) {
    // 布尔表达式为真将执行的语句
}
```

```R
x <- 50L
if(is.integer(x)) {
   print("X 是一个整数")
}
```

## if...else 语句

```R
if(boolean_expression) {
    // 如果布尔表达式为真将执行的语句
} else {
    // 如果布尔表达式为假将执行的语句
}
```

```R
x <- c("google","runoob","taobao")

if("runoob" %in% x) {
   print("包含 runoob")
} else {
   print("不包含 runoob")
}
```

如果有多个条件判断，可以使用 if...else if...else：

```R
if(boolean_expression 1) {
    // 如果布尔表达式 boolean_expression 1 为真将执行的语句
} else if( boolean_expression 2) {
    // 如果布尔表达式 boolean_expression 2 为真将执行的语句
} else if( boolean_expression 3) {
    // 如果布尔表达式 boolean_expression 3 为真将执行的语句
} else {
    // 以上所有的布尔表达式都为 false 时执行
}
```

## switch 语句

语法格式如下：

`switch(expression, case1, case2, case3....)`

**switch** 语句必须遵循下面的规则：

- **switch** 语句中的 **expression** 是一个常量表达式，可以是整数或字符串，如果是整数则返回对应的 case 位置值，如果整数不在位置的范围内则返回 NULL。
- 如果匹配到多个值则返回第一个。
- **expression**如果是字符串，则对应的是 case 中的变量名对应的值，没有匹配则没有返回值。
- switch 没有默认参数可用。

```R
x <- switch(
   3,
   "google",
   "runoob",
   "taobao",
   "weibo"
)
print(x)
[1] "taobao"
```

如果是字符串返回字符串变量对应的值

```R
you.like<-"runoob"
switch(you.like, google="www.google.com", runoob = "www.runoob.com", taobao = "www.taobao.com")
"www.runoob.com"
```

如果整数不在范围内的则返回 NULL

```R
> x <- switch(4,"google","runoob","taobao")
> x
NULL
> x <- switch(4,"google","runoob","taobao")
> x
NULL
```

# R 循环

有的时候，我们可能需要多次执行同一块代码。一般情况下，语句是按顺序执行的：函数中的第一个语句先执行，接着是第二个语句，依此类推。

编程语言提供了更为复杂执行路径的多种控制结构。

循环语句允许我们多次执行一个语句或语句组，下面是大多数编程语言中循环语句的流程图：

![循环结构](https://www.runoob.com/wp-content/uploads/2015/12/loop.png)

R 语言提供的循环类型有:

- repeat 循环
- while 循环
- for 循环

R 语言提供的循环控制语句有：

- break 语句
- Next 语句

循环控制语句改变你代码的执行顺序，通过它你可以实现代码的跳转。

## 循环类型

### repeat

repeat 循环会一直执行代码，直到条件语句为 true 时才退出循环，退出要使用到 break 语句。

语法格式如下：

```R
repeat { 
    // 相关代码 
    if(condition) {
       break
    }
}
```

以下实例在变量 cnt 为 5 时退出循环，cnt 为计数变量：

```R
v <- c("Google","Runoob")
cnt <- 2

repeat {
   print(v)
   cnt <- cnt+1
   
   if(cnt > 5) {
      break
   }
}
[1] "Google" "Runoob"
[1] "Google" "Runoob"
[1] "Google" "Runoob"
[1] "Google" "Runoob"
```

### while

只要给定的条件为 true，R 语言中的 while 循环语句会重复执行一个目标语句。

```R
while(condition)
{
   statement(s);
}
```

在这里，statement(s) 可以是一个单独的语句，也可以是几个语句组成的代码块。

condition 可以是任意的表达式，<font color='red'>当为任意非零值时都为 true</font>。当条件为 true 时执行循环。 当条件为 false 时，退出循环，程序流将继续执行紧接着循环的下一条语句。

以下实例在在变量 cnt 小于 7 时输出 while 语句块中的内容，cnt 为计数变量：

```R
v <- c("Google","Runoob")
cnt <- 2

while (cnt < 7) {
   print(v)
   cnt = cnt + 1
}

[1] "Google" "Runoob"
[1] "Google" "Runoob"
[1] "Google" "Runoob"
[1] "Google" "Runoob"
[1] "Google" "Runoob"
```

### for

R 编程语言中 for 循环语句可以重复执行指定语句，重复次数可在 for 语句中控制。

```R
for (value in vector) {
    statements
}
```

```R
v <- LETTERS[1:4]
for ( i in v) {
   print(i)
}
[1] "A"
[1] "B"
[1] "C"
[1] "D"
```

## 循环控制

### break

R 语言的 break 语句插入在循环体中，用于退出当前循环或语句，并开始脚本执行紧接着的语句。

如果你使用循环嵌套，break 语句将停止最内层循环的执行，并开始执行的外层的循环语句。

break 也常用于 switch 语句中。

以下实例在变量 cnt 为 5 时使用 break 退出循环，cnt 为计数变量：

```R
v <- c("Google","Runoob")
cnt <- 2

repeat {
   print(v)
   cnt <- cnt+1
   
   if(cnt > 5) {
      break
   }
}

[1] "Google" "Runoob"
[1] "Google" "Runoob"
[1] "Google" "Runoob"
[1] "Google" "Runoob"
```

### next

next 语句用于跳过当前循环，开始下一次循环（类似其他语言的 continue）。

```R
v <- LETTERS[1:6]
for ( i in v) {
   if (i == "D") {# D 不会输出，跳过这次循环，进入下一次
      next
   }
   print(i)
}

[1] "A"
[1] "B"
[1] "C"
[1] "E"
[1] "F"
```

# R 函数

函数是一组一起执行一个任务的语句。R 语言本身提供了很多的内置函数，当然我们也可以自己创建函数。

您可以把代码划分到不同的函数中。如何划分代码到不同的函数中是由您来决定的，但在逻辑上，划分通常是根据每个函数执行一个特定的任务来进行的。

函数**声明**告诉编译器函数的名称、返回类型和参数。函数**定义**提供了函数的实际主体。

R 语言中函数是一个对象，可以拥有属性。

## 定义函数

R 语言中的函数定义使用 function 关键字，一般形式如下

```R
function_name <- function(arg_1, arg_2, ...) {
    // 函数体
}
```

说明：

- `unction_name `: 为函数名
- `arg_1, arg_2, ... `: 形式参数列表

函数返回值使用 **return()**。

## 内置函数

R 语言提供了很多有用的内置函数，我们无需定义它就可以直接使用。

例如：seq(), mean(), max(), sum(x) 以及 paste(...) 等。

```R
# 输出  32 到 44 到的所有数字
print(seq(32,44))

# 计算两个数的平均数
print(mean(25:82))

# 计算 41 到 68 所有数字之和
print(sum(41:68))

[1] 32 33 34 35 36 37 38 39 40 41 42 43 44
[1] 53.5
[1] 1526
```

## 自定义函数

我们可以自己创建函数，用于特定到功能，定义后可以向内置函数一样使用它们。

```R
# 定义一个函数，用于计数一个系列到平方值
new.function <- function(a) {
   for(i in 1:a) {
      b <- i^2
      print(b)
   }
}

# 调用函数，并传递参数
new.function(6)

[1] 1
[1] 4
[1] 9
[1] 16
[1] 25
[1] 36
```

### 带有参数值的函数

函数参数，<font color='red'>可以按函数创建时的顺序来传递，也可以不按顺序，但需要指定参数名：</font>

```R
# 创建函数
new.function <- function(a,b,c) {
   result <- a * b + c
   print(result)
}

# 不带参数名
new.function(5,3,11)

# 带参数名
new.function(a = 11, b = 5, c = 3)

[1] 26
[1] 58
```

函数创建时也可以为参数指定默认值，如果调用的时候不传递参数就会使用默认值：

```R
# 创建带默认参数的函数
new.function <- function(a = 3, b = 6) {
   result <- a * b
   print(result)
}

# 调用函数，但不传递参数，会使用默认的
new.function()

# 调用函数，传递参数
new.function(9,5)
```

### 懒惰计算的函数

<font color='red'>懒惰计算将推迟计算工作直到系统需要这些计算的结果。如果不需要结果，将不用进行计算。</font>

默认情况下，R 函数对参数的计算是懒惰的，就是只有我们在计算它的时候才会调用：

```R
f <- function(x) {
  10
}
f()
[1] 10
```

以上代码执行，并没有报错，虽然我们没有传入参数，但<font color='red'>函数体内没有使用参数 x，所以不会去调用它，也不会报错。</font>

```R
new.function <- function(a, b) {
   print(a^2)
   print(a)
   print(b)  # 使用到 b，但未传入，所以会报错
}

# 传入一个参数
new.function(6)

[1] 36
[1] 6
Error in print(b) : 缺少参数"b",也没有缺省值
Calls: new.function -> print
停止执行
```

# R 字符串

R 语言字符串可以使用一对单引号 **' '** 或一对双引号 **" "** 来表示。

- 单引号字符串中可以包含双引号。
- 单引号字符串中不可以包含单引号。
- 双引号字符串中可以包含单引号。
- 双引号字符串中不可以包含双引号。

```R
a <- '使用单引号'
print(a)

b <- "使用双引号"
print(b)

c <- "双引号字符串中可以包含单引号（'） "
print(c)

d <- '单引号字符串中可以包含双引号（"） '
print(d)

[1] "使用单引号"
[1] "使用双引号"
[1] "双引号字符串中可以包含单引号（'） "
[1] "单引号字符串中可以包含双引号（\"） "
```

## 字符串操作

### paste() 函数

paste() 函数用于<font color='red'>使用指定对分隔符来对字符串进行连接，默认对分隔符为空格。</font>

`paste(..., sep = " ", collapse = NULL)`

参数说明：

- ... ： 字符串列表
- sep ： 分隔符，默认为空格
- collapse ： 两个或者更多字符串对象根据元素对应关系拼接到一起，在字符串进行连接后，再使用 collapse 指定对连接符进行连接

```R
a <- "Google"
b <- 'Runoob'
c <- "Taobao"

print(paste(a,b,c))

print(paste(a,b,c, sep = "-"))

print(paste(letters[1:6],1:6, sep = "", collapse = "="))
paste(letters[1:6],1:6, collapse = ".")

[1] "Google Runoob Taobao"
[1] "Google-Runoob-Taobao"
[1] "a1=b2=c3=d4=e5=f6"
[1] "a 1.b 2.c 3.d 4.e 5.f 6"
```

### format() 函数

format() 函数用于格式化字符串，format() 可作用于字符串或数字。

`format(x, digits, nsmall, scientific, width, justify = c("left", "right", "centre", "none")) `

参数说明：

- x ： 输入对向量
- digits ： 显示的位数
- nsmall ： 小数点右边显示的最少位数
- scientific ： 设置科学计数法
- width ： 通过开头填充空白来显示最小的宽度
- justify：设置位置，显示可以是左边、右边、中间等。

```R
# 显示 9 位，最后一位四舍五入
result <- format(23.123456789, digits = 9)
print(result)

# 使用科学计数法显示
result <- format(c(6, 13.14521), scientific = TRUE)
print(result)

# 小数点右边最小显示 5 位，没有的以 0 补充
result <- format(23.47, nsmall = 5)
print(result)

# 将数字转为字符串
result <- format(6)
print(result)

# 宽度为 6 位，不够的在开头添加空格
result <- format(13.7, width = 6)
print(result)

# 左对齐字符串
result <- format("Runoob", width = 9, justify = "l")
print(result)

# 居中显示
result <- format("Runoob", width = 10, justify = "c")
print(result)

[1] "23.1234568"
[1] "6.000000e+00" "1.314521e+01"
[1] "23.47000"
[1] "6"
[1] "  13.7"
[1] "Runoob   "
[1] "  Runoob  
```

### nchar() 函数

nchar() 函数用于计数字符串或数字列表的长度。

`nchar(x)`

参数说明：

- x ： 向量或字符串

```R
result <- nchar("Google Runoob Taobao")
print(result)
[1] 20
```

### toupper() & tolower() 函数

toupper() & tolower() 函数用于将字符串的字母转化为大写或者小写。

```R
result <- toupper("Runoob")
print(result)

# 转小写
result <- tolower("Runoob")
print(result)

[1] "RUNOOB"
[1] "runoob"
```

### substring() 函数

substring() 函数用于截取字符串。

`substring(x,first,last)`

参数说明：

- x ： 向量或字符串
- first ： 开始截取的位置
- last： 结束截取的位置

```R
# 从第 2 位截取到第 5 位
result <- substring("Runoob", 2, 5)
print(result)

[1] "unoo"
```

# R 列表

列表是 R 语言的对象集合，可以用来<font color='red'>保存不同类型的数据</font>，可以是数字、字符串、向量、另一个列表等，当然还可以包含矩阵和函数。

R 语言创建列表使用 **list()** 函数。

```R
list_data <- list("runoob", "google", c(11,22,33), 123, 51.23, 119.1)
print(list_data)

[[1]]
[1] "runoob"

[[2]]
[1] "google"

[[3]]
[1] 11 22 33

[[4]]
[1] 123

[[5]]
[1] 51.23

[[6]]
[1] 119.1
```

我们可以使用 **names()** 函数给列表的元素命名：

```R
# 列表包含向量、矩阵、列表
list_data <- list(c("Google","Runoob","Taobao"), matrix(c(1,2,3,4,5,6), nrow = 2),list("runoob",12.3))

# 给列表元素设置名字
names(list_data) <- c("Sites", "Numbers", "Lists")

# 显示列表
print(list_data)

#结果
$Sites
[1] "Google" "Runoob" "Taobao"

$Numbers
     [,1] [,2] [,3]
[1,]    1    3    5
[2,]    2    4    6

$Lists
$Lists[[1]]
[1] "runoob"

$Lists[[2]]
[1] 12.3
```

### 访问列表

列表中的元素可以使用索引来访问，<font color='red'>如果使用来 **names()** 函数命名后，我们还可以使用对应名字来访问</font>

```R
# 列表包含向量、矩阵、列表
list_data <- list(c("Google","Runoob","Taobao"), matrix(c(1,2,3,4,5,6), nrow = 2),list("runoob",12.3))

# 给列表元素设置名字
names(list_data) <- c("Sites", "Numbers", "Lists")

# 显示列表
print(list_data[1])

# 访问列表的第三个元素
print(list_data[3])

# 访问第一个向量元素
print(list_data$Numbers)

$Sites
[1] "Google" "Runoob" "Taobao"

$Lists
$Lists[[1]]
[1] "runoob"

$Lists[[2]]
[1] 12.3


     [,1] [,2] [,3]
[1,]    1    3    5
[2,]    2    4    6
```

### 操作列表元素

我们可以对列表进行添加、删除、更新的操作，如下实例：

```R
# 列表包含向量、矩阵、列表
list_data <- list(c("Google","Runoob","Taobao"), matrix(c(1,2,3,4,5,6), nrow = 2),
   list("runoob",12.3))

# 给列表元素设置名字
names(list_data) <- c("Sites", "Numbers", "Lists")

# 添加元素
list_data[4] <- "新元素"
print(list_data[4])

# 删除元素
list_data[4] <- NULL

# 删除后输出为 NULL
print(list_data[4])

# 更新元素
list_data[3] <- "我替换来第三个元素"
print(list_data[3])

[[1]]
[1] "新元素"

$<NA>
NULL

$Lists
[1] "我替换来第三个元素"
```

### 合并列表

我们可以使用 **c()** 函数将多个列表合并为一个列表：

```R
# 创建两个列表
list1 <- list(1,2,3)
list2 <- list("Google","Runoob","Taobao")

# 合并列表
merged.list <- c(list1,list2)

# 显示合并后的列表
print(merged.list)

[[1]]
[1] 1

[[2]]
[1] 2

[[3]]
[1] 3

[[4]]
[1] "Google"

[[5]]
[1] "Runoob"

[[6]]
[1] "Taobao"
```

### 列表转换为向量

要将列表转换为向量可以使用 **unlist()** 函数，将列表转换为向量，可以方便我们进行算术运算：

```R
# 创建列表
list1 <- list(1:5)
print(list1)

list2 <-list(10:14)
print(list2)

# 转换为向量
v1 <- unlist(list1)
v2 <- unlist(list2)

print(v1)
print(v2)

# 两个向量相加
result <- v1+v2
print(result)

[[1]]
[1] 1 2 3 4 5

[[1]]
[1] 10 11 12 13 14

[1] 1 2 3 4 5
[1] 10 11 12 13 14
[1] 11 13 15 17 19
```

# R 矩阵

R 语言为线性代数的研究提供了矩阵类型，这种<font color='red'>数据结构很类似于其它语言中的二维数组</font>，但 R 提供了语言级的矩阵运算支持。

矩阵里的元素可以是数字、符号或数学式。

一个 **M x N** 的矩阵是一个由 **M（row） 行** 和 **N 列（column）**元素排列成的矩形阵列。

![img](R%20%E8%AF%AD%E8%A8%80%E5%9F%BA%E7%A1%80.assets/Matrix_zh-hans.png)

R 语言的矩阵可以使用 matrix() 函数来创建，语法格式如下：

`matrix(data = NA, nrow = 1, ncol = 1, byrow = FALSE,dimnames = NULL)`

**参数说明：**

- **data** 向量，矩阵的数据
- **nrow** 行数
- **ncol** 列数
- **byrow** 逻辑值，为 FALSE 按列排列，为 TRUE 按行排列
- **dimname** 设置行和列的名称

```R
# byrow 为 TRUE 元素按行排列
M <- matrix(c(3:14), nrow = 4, byrow = TRUE)
print(M)

# Ebyrow 为 FALSE 元素按列排列
N <- matrix(c(3:14), nrow = 4, byrow = FALSE)
print(N)

# 定义行和列的名称
rownames = c("row1", "row2", "row3", "row4")
colnames = c("col1", "col2", "col3")

P <- matrix(c(3:14), nrow = 4, byrow = TRUE, dimnames = list(rownames, colnames))
print(P)
```

### 转置矩阵

R 语言矩阵提供了 **t()** 函数，可以<font color='red'>实现矩阵的行列互换</font>。

```R
# 创建一个 2 行 3 列的矩阵
M = matrix( c(2,6,5,1,10,4), nrow = 2,ncol = 3,byrow = TRUE)
print(M)
     [,1] [,2] [,3]
[1,]    2    6    5
[2,]    1   10    4
# 转换为 3 行 2 列的矩阵
print(t(M))
```

### 访问矩阵元素

如果想获取矩阵元素，可以通过使用元素的列索引和行索引，<font color='red'>类似坐标形式</font>。

```R
# 定义行和列的名称
rownames = c("row1", "row2", "row3", "row4")
colnames = c("col1", "col2", "col3")

# 创建矩阵
P <- matrix(c(3:14), nrow = 4, byrow = TRUE, dimnames = list(rownames, colnames))
print(P)
# 获取第一行第三列的元素
print(P[1,3])

# 获取第四行第二列的元素
print(P[4,2])

# 获取第二行
print(P[2,])

# 获取第三列
print(P[,3])
```

### 矩阵计算

大小相同（行数列数都相同）的矩阵之间可以相互加减，具体是<font color='red'>对每个位置上的元素做加减法</font>。矩阵的乘法则较为复杂。<font color='red'>两个矩阵可以相乘，当且仅当第一个矩阵的列数等于第二个矩阵的行数。</font>

#### 矩阵加减法

```R
# 创建 2 行 3 列的矩阵
matrix1 <- matrix(c(7, 9, -1, 4, 2, 3), nrow = 2)
print(matrix1)

matrix2 <- matrix(c(6, 1, 0, 9, 3, 2), nrow = 2)
print(matrix2)

# 两个矩阵相加
result <- matrix1 + matrix2
cat("相加结果：","\n")
print(result)

# 两个矩阵相减
result <- matrix1 - matrix2
cat("相减结果：","\n")
print(result)
```

#### 矩阵乘除法

```R
# 创建 2 行 3 列的矩阵
matrix1 <- matrix(c(7, 9, -1, 4, 2, 3), nrow = 2)
print(matrix1)

matrix2 <- matrix(c(6, 1, 0, 9, 3, 2), nrow = 2)
print(matrix2)

# 两个矩阵相乘
result <- matrix1 * matrix2
cat("相乘结果：","\n")
print(result)

# 两个矩阵相除
result <- matrix1 / matrix2
cat("相除结果：","\n")
print(result)
```

# R 数组

数组也是 R 语言的对象，R 语言可以创建一维或多维数组。

R 语言数组是一个同一类型的集合，前面我们学的矩阵 matrix 其实就是一个二维数组。

向量、矩阵、数组关系可以看下图：

![img](R%20%E8%AF%AD%E8%A8%80%E5%9F%BA%E7%A1%80.assets/2039-08-06Done.png)

R 语言数组创建使用 array() 函数，该函数使用向量作为输入参数，可以使用 dim 设置数组维度。

array() 函数语法格式如下：

`array(data = NA, dim = length(data), dimnames = NULL)`

**参数说明：**

- data 向量，数组元素。
- dim 数组的维度，默认是一维数组。
- dimnames 维度的名称，必须是个列表，默认情况下是不设置名称的。

```R
# 创建两个不同长度的向量
vector1 <- c(5,9,3)
vector2 <- c(10,11,12,13,14,15)

# 创建数组
result <- array(c(vector1,vector2),dim = c(3,3,2))
print(result)
```

使用 dimnames 参数来设置各个维度的名称：：

```R
# 创建两个不同长度的向量
vector1 <- c(5,9,3)
vector2 <- c(10,11,12,13,14,15)
column.names <- c("COL1","COL2","COL3")
row.names <- c("ROW1","ROW2","ROW3")
matrix.names <- c("Matrix1","Matrix2")

# 创建数组，并设置各个维度的名称
result <- array(c(vector1,vector2),dim = c(3,3,2),dimnames = list(row.names,column.names,matrix.names))
print(result)
```

### 访问数组元素

如果想获取数组元素，可以通过使用元素的列索引和行索引，类似坐标形式。

```R
# 创建两个不同长度的向量
vector1 <- c(5,9,3)
vector2 <- c(10,11,12,13,14,15)
column.names <- c("COL1","COL2","COL3")
row.names <- c("ROW1","ROW2","ROW3")
matrix.names <- c("Matrix1","Matrix2")

# 创建数组
result <- array(c(vector1,vector2),dim = c(3,3,2),dimnames = list(row.names, column.names, matrix.names))

# 显示数组第二个矩阵中第三行的元素
print(result[3,,2])

# 显示数组第一个矩阵中第一行第三列的元素
print(result[1,3,1])

# 输出第二个矩阵
print(result[,,2])
```

### 操作数组元素

由于数组是由多个维度的矩阵组成，所以我们可以通过访问矩阵的元素来访问数组元素。

```R
# 创建两个不同长度的向量
vector1 <- c(5,9,3)
vector2 <- c(10,11,12,13,14,15)

# 创建数组
array1 <- array(c(vector1,vector2),dim = c(3,3,2))

# 创建两个不同长度的向量
vector3 <- c(9,1,0)
vector4 <- c(6,0,11,3,14,1,2,6,9)
array2 <- array(c(vector1,vector2),dim = c(3,3,2))

# 从数组中创建矩阵
matrix1 <- array1[,,2]
matrix2 <- array2[,,2]

# 矩阵相加
result <- matrix1+matrix2
print(result)
```

另外我们可以使用 **apply()** 元素对数组元素进行跨维度计算，语法格式如下：

`apply(x, margin, fun)`

参数说明：

- **x** 数组
- **margin** 数据名称
- **fun** 计算函数

以下我们使用 apply() 函数来计算数组两个矩阵中每一行对数字之和。

```R
# 创建两个不同长度的向量
vector1 <- c(5,9,3)
vector2 <- c(10,11,12,13,14,15)

# 创建数组
new.array <- array(c(vector1,vector2),dim = c(3,3,2))
print(new.array)

# 计算数组中所有矩阵第一行的数字之和
result <- apply(new.array, c(1), sum)
print(result)
```

# R 因子

因子用于存储不同类别的数据类型，例如人的性别有男和女两个类别，年龄来分可以有未成年人和成年人。

R 语言创建因子使用 factor() 函数，向量作为输入参数。

factor() 函数语法格式：

```R
factor(x = character(), levels, labels = levels,
       exclude = NA, ordered = is.ordered(x), nmax = NA)
```

参数说明：

- x：向量。
- levels：指定各水平值, 不指定时由x的不同值来求得。
- labels：水平的标签, 不指定时用各水平值的对应字符串。
- exclude：排除的字符。
- ordered：逻辑值，用于指定水平是否有序。
- nmax：水平的上限数量。

```R
x <- c("男", "女", "男", "男",  "女")
sex <- factor(x)
print(sex)
print(is.factor(sex))

[1] 男 女 男 男 女
Levels: 男 女
[1] TRUE
```

以下实例设置因子水平为 **c('男','女')**：

```R
x <- c("男", "女", "男", "男",  "女",levels=c('男','女'))
sex <- factor(x)
print(sex)
print(is.factor(sex))
```

### 因子水平标签

接下来我们使用 labels 参数为每个因子水平添加标签，labels 参数的字符顺序，要和 levels 参数的字符顺序保持一致

```R
sex=factor(c('f','m','f','f','m'),levels=c('f','m'),labels=c('female','male'),ordered=TRUE)
print(sex)
```

### 生成因子水平

我们可以使用 **gl()** 函数来生成因子水平，语法格式如下

`gl(n, k, length = n*k, labels = seq_len(n), ordered = FALSE)`

参数说明：

- **n**: 设置 level 的个数
- **k**: 设置每个 level 重复的次数
- **length**: 设置长度
- **labels**: 设置 level 的值
- **ordered**: 设置是否 level 是排列好顺序的，布尔值。

```R
v <- gl(3, 4, labels = c("Google", "Runoob","Taobao"))
print(v)
```

# R 数据框

### 基本操作和创建

数据框（Data frame）可以理解成我们常说的"表格"。

数据框是 R 语言的数据结构，是特殊的二维列表。

数据框每一列都有一个唯一的列名，长度都是相等的，同一列的数据类型需要一致，不同列的数据类型可以不一样。

```R
data.frame(…, row.names = NULL, check.rows = FALSE,
           check.names = TRUE, fix.empty.names = TRUE,
           stringsAsFactors = default.stringsAsFactors())
```

- **…**: 列向量，可以是任何类型（字符型、数值型、逻辑型），一般以 tag = value 的形式表示，也可以是 value。
- **row.names**: 行名，默认为 NULL，可以设置为单个数字、字符串或字符串和数字的向量。
- **check.rows**: 检测行的名称和长度是否一致。
- **check.names**: 检测数据框的变量名是否合法。
- **fix.empty.names**: 设置未命名的参数是否自动设置名字。
- **stringsAsFactors**: 布尔值，字符是否转换为因子，factory-fresh 的默认值是 TRUE，可以通过设置选项（stringsAsFactors=FALSE）来修改。

```R
table = data.frame(
    姓名 = c("张三", "李四"),
    工号 = c("001","002"),
    月薪 = c(1000, 2000)
   
)
print(table) # 查看 table 数据
```

数据框的数据结构可以通过 **str()** 函数来展示：

```R
table = data.frame(
    姓名 = c("张三", "李四"),
    工号 = c("001","002"),
    月薪 = c(1000, 2000)
)
# 获取数据结构
str(table)
```

**summary()** 可以显示数据框的概要信息：

```R
table = data.frame(
    姓名 = c("张三", "李四"),
    工号 = c("001","002"),
    月薪 = c(1000, 2000)
   
)
# 显示概要
print(summary(table))  
```

我们也可以提取指定的列：

```R
table = data.frame(
    姓名 = c("张三", "李四"),
    工号 = c("001","002"),
    月薪 = c(1000, 2000)
)
# 提取指定的列
result <- data.frame(table$姓名,table$月薪)
print(result)
```

以下形式显示前面两行：

```R
table = data.frame(
    姓名 = c("张三", "李四","王五"),
    工号 = c("001","002","003"),
    月薪 = c(1000, 2000,3000)
)
print(table)
# 提取前面两行
print("---输出前面两行----")
result <- table[1:2,]
print(result)
```

我们可以通过类似坐标的形式读取指定行的某一列的数据，以下我们读取第 2 、3 行的第 1 、2 列数据：：

```R
table = data.frame(
    姓名 = c("张三", "李四","王五"),
    工号 = c("001","002","003"),
    月薪 = c(1000, 2000,3000)
)
# 读取第 2 、3 行的第 1 、2 列数据：
result <- table[c(2,3),c(1,2)]
print(result)
```

### 删除数据列

```R
## R语言删除某列
library(dplyr)
## 按索引删除
data <- select(data,-3)
## 按列名删除单列
data <- select(data,-lieming)
## 按列名删除多列
data <- select(data,-c(lieming1,lieming2))
```

### 删除数据行

```R
#删除1-10行数据
df[-c(1:10),]
#删除NA数据
mydata <- na.omit(mydata)
```



### 扩展数据框

我们可以<font color='red'>对已有的数据框进行扩展</font>，以下实例我们添加部门列：

```R
table = data.frame(
    姓名 = c("张三", "李四","王五"),
    工号 = c("001","002","003"),
    月薪 = c(1000, 2000,3000)
)
# 添加部门列
table$部门 <- c("运营","技术","编辑")

print(table)
```

我们可以使用 **cbind()** 函数<font color='red'>将多个向量合成一个数据框</font>：

```R
# 创建向量
sites <- c("Google","Runoob","Taobao")
likes <- c(222,111,123)
url <- c("www.google.com","www.runoob.com","www.taobao.com")

# 将向量组合成数据框
addresses <- cbind(sites,likes,url)

# 查看数据框
print(addresses)
```

如果要对<font color='red'>两个数据框进行合并</font>可以使用 **rbind()** 函数：

```R
table = data.frame(
    姓名 = c("张三", "李四","王五"),
    工号 = c("001","002","003"),
    月薪 = c(1000, 2000,3000)
)
newtable = data.frame(
    姓名 = c("小明", "小白"),
    工号 = c("101","102"),
    月薪 = c(5000, 7000)
)
# 合并两个数据框
result <- rbind(table,newtable)
print(result)
```

# R 数据重塑

### 合并数据框

R 语言合并数据框使用 **merge()** 函数。

merge() 函数语法格式如下：

```
# S3 方法
merge(x, y, …)

# data.frame 的 S3 方法 
merge(x, y, by = intersect(names(x), names(y)),
      by.x = by, by.y = by, all = FALSE, all.x = all, all.y = all,
      sort = TRUE, suffixes = c(".x",".y"), no.dups = TRUE,
      incomparables = NULL, …)
```

常用参数说明：

- x, y： 数据框
- by, by.x, by.y：指定两个数据框中匹配列名称，默认情况下使用两个数据框中相同列名称。
- all：逻辑值; all = L 是 all.x = L 和 all.y = L 的简写，L 可以是 TRUE 或 FALSE。
- all.x：逻辑值，默认为 FALSE。如果为 TRUE, 显示 x 中匹配的行，即便 y 中没有对应匹配的行，y 中没有匹配的行用 NA 来表示。
- all.y：逻辑值，默认为 FALSE。如果为 TRUE, 显示 y 中匹配的行，即便 x 中没有对应匹配的行，x 中没有匹配的行用 NA 来表示。
- sort：逻辑值，是否对列进行排序。

merge() 函数和 SQL 的 JOIN 功能很相似：

![img](R%20%E8%AF%AD%E8%A8%80%E5%9F%BA%E7%A1%80.assets/r-merge-join.jpg)

- **Natural join 或 INNER JOIN**：如果表中有至少一个匹配，则返回行
- **Left outer join 或 LEFT JOIN**：即使右表中没有匹配，也从左表返回所有的行
- **Right outer join 或 RIGHT JOIN**：即使左表中没有匹配，也从右表返回所有的行
- **Full outer join 或 FULL JOIN**：只要其中一个表中存在匹配，则返回行

```R
# data frame 1
df1 = data.frame(SiteId = c(1:6), Site = c("Google","Runoob","Taobao","Facebook","Zhihu","Weibo"))


# data frame 2
df2 = data.frame(SiteId = c(2, 4, 6, 7, 8), Country = c("CN","USA","CN","USA","IN"))

# INNER JOIN
df1 = merge(x=df1,y=df2,by="SiteId")
print("----- INNER JOIN -----")
print(df1)

# FULL JOIN
df2 = merge(x=df1,y=df2,by="SiteId",all=TRUE)
print("----- FULL JOIN -----")
print(df2)

# LEFT JOIN
df3 = merge(x=df1,y=df2,by="SiteId",all.x=TRUE)
print("----- LEFT JOIN -----")
print(df3)

# RIGHT JOIN
df4 = merge(x=df1,y=df2,by="SiteId",all.y=TRUE)
print("----- RIGHT JOIN -----")
print(df4)
```

### 数据整合和拆分

R 语言使用 **melt()** 和 **cast()** 函数来对数据进行整合和拆分。

- melt() ：宽格式数据转化成长格式。
- cast() ：长格式数据转化成宽格式。

下图很好展示来 melt() 和 cast() 函数的功能(后面实例会详细说明)：

![img](R%20%E8%AF%AD%E8%A8%80%E5%9F%BA%E7%A1%80.assets/6634703-5e733d531862b668.webp)

melt() 将数据集的每个列堆叠到一个列中，函数语法格式：

`melt(data, ..., na.rm = FALSE, value.name = "value")`

参数说明：

- data：数据集。
- ...：传递给其他方法或来自其他方法的其他参数。
- na.rm：是否删除数据集中的 NA 值。
- value.name 变量名称，用于存储值。

进行以下操作之前，我们先安装依赖包：

```
# 安装库，MASS 包含很多统计相关的函数，工具和数据集
install.packages("MASS", repos = "https://mirrors.ustc.edu.cn/CRAN/") 
  
#  melt() 和 cast() 函数需要对库 
install.packages("reshape2", repos = "https://mirrors.ustc.edu.cn/CRAN/") 
install.packages("reshape", repos = "https://mirrors.ustc.edu.cn/CRAN/") 
```

```R
# 载入库
library(MASS)
library(reshape2)
library(reshape)
 
# 创建数据框
id<- c(1, 1, 2, 2)
time <- c(1, 2, 1, 2)
x1 <- c(5, 3, 6, 2)
x2 <- c(6, 5, 1, 4)
mydata <- data.frame(id, time, x1, x2)
 
# 原始数据框
cat("原始数据框:\n")
print(mydata)
# 整合
md <- melt(mydata, id = c("id","time"))
 
cat("\n整合后:\n")
print(md)
```

cast 函数用于对合并对数据框进行还原，dcast() 返回数据框，acast() 返回一个向量/矩阵/数组。

cast() 函数语法格式：

```
dcast(
  data,
  formula,
  fun.aggregate = NULL,
  ...,
  margins = NULL,
  subset = NULL,
  fill = NULL,
  drop = TRUE,
  value.var = guess_value(data)
)
acast(
  data,
  formula,
  fun.aggregate = NULL,
  ...,
  margins = NULL,
  subset = NULL,
  fill = NULL,
  drop = TRUE,
  value.var = guess_value(data)
)
```

参数说明：

- data：合并的数据框。
- formula：重塑的数据的格式，类似 x ~ y 格式，x 为行标签，y 为列标签 。
- fun.aggregate：聚合函数，用于对 value 值进行处理。
- margins：变量名称的向量（可以包含"grand\_col" 和 "grand\_row"），用于计算边距，设置 TURE 计算所有边距。
- subset：对结果进行条件筛选，格式类似 **subset = .(variable=="length")**。
- drop：是否保留默认值。
- value.var：后面跟要处理的字段。

```R
# 载入库
library(MASS)
library(reshape2)
library(reshape)
 
# 创建数据框
id<- c(1, 1, 2, 2)
time <- c(1, 2, 1, 2)
x1 <- c(5, 3, 6, 2)
x2 <- c(6, 5, 1, 4)
mydata <- data.frame(id, time, x1, x2)
# 整合
md <- melt(mydata, id = c("id","time"))
# Print recasted dataset using cast() function
cast.data <- cast(md, id~variable, mean)
 
print(cast.data)
 
cat("\n")
time.cast <- cast(md, time~variable, mean)
print(time.cast)


cat("\n")
id.time <- cast(md, id~time, mean)
print(id.time)

cat("\n")
id.time.cast <- cast(md, id+time~variable)
print(id.time.cast)

cat("\n")
id.variable.time <- cast(md, id+variable~time)
print(id.variable.time)

cat("\n")
id.variable.time2 <- cast(md, id~variable+time)
print(id.variable.time2)
```

```
id x1  x2
1  1  4 5.5
2  2  4 2.5

  time  x1  x2
1    1 5.5 3.5
2    2 2.5 4.5

  id   1 2
1  1 5.5 4
2  2 3.5 3

  id time x1 x2
1  1    1  5  6
2  1    2  3  5
3  2    1  6  1
4  2    2  2  4

  id variable 1 2
1  1       x1 5 3
2  1       x2 6 5
3  2       x1 6 2
4  2       x2 1 4

  id x1_1 x1_2 x2_1 x2_2
1  1    5    3    6    5
2  2    6    2    1    4
```

# R CSV 文件

### CSV 表格交互

CSV 本质是文本，它的文件格式极度简单：数据一行一行的用文本保存起来而已，每条记录被分隔符分隔为字段，每条记录都有同样的字段序列。

以下是一个简单的 sites.csv 文件（存储在测试程序的相同目录下）：

```
id,name,url,likes
1,Google,www.google.com,111
2,Runoob,www.runoob.com,222
3,Taobao,www.taobao.com,333
```

CSV 用逗号来分割列，如果数据中含有逗号，就要用双引号将整个数据块包括起来。

**注意：**包含非英文字符的文本要注意保存的编码，<font color='red'>由于很多计算机普遍使用 UTF-8 编码，所以我是用 UTF-8 进行保存的。</font>

**注意：**<font color='red'> CSV 文件最后一行需要保留一个空行，不然执行程序会有警告信息。</font>

```
Warning message:
In read.table(file = file, header = header, sep = sep, quote = quote,  :
  incomplete final line found by readTableHeader on 'sites.csv'
```

![img](R%20%E8%AF%AD%E8%A8%80%E5%9F%BA%E7%A1%80.assets/057FE509-4EE4-4A74-9F7D-786AC2C5282E.jpg)

### 读取 CSV 文件

接下来我们就可以使用 read.csv() 函数来读取 CSV 文件的数据：

```R
data <- read.csv("sites.csv", encoding="UTF-8")
print(data)
```

如果不设置 encoding 属性，read.csv 函数将默认以操作系统默认的文字编码进行读取，<font color='red'>如果你使用的是 Windows 中文版系统且没有设置过系统的默认编码，那系统的默认编码应该是 GBK</font>。所以大家请尽可能地统一文字编码以防出错。

<font color='red'>read.csv() 函数返回的是数据框</font>，我们可以很方便的对数据进行统计处理，以下实例我们查看行数和列数：

```R
data <- read.csv("sites.csv", encoding="UTF-8")

print(is.data.frame(data))  # 查看是否是数据框
print(ncol(data))  # 列数
print(nrow(data))  # 行数
```

以下统计数据框中 likes 字段最大对数据：

```R
data <- read.csv("sites.csv", encoding="UTF-8")

# likes 最大的数据
like <- max(data$likes)
print(like)
```

我们也可以指定查找条件，类似 SQL where 子句一样查询数据，需要用到到函数是 **subset()**。

以下实例查找 likes 为 222 到数据：

```R
data <- read.csv("sites.csv", encoding="UTF-8")

# likes 为 222 的数据
retval <- subset(data, likes == 222)
print(retval)
```

**注意**：条件语句等于使用 **==**。

多个条件使用 **&** 分隔符，以下实例查找 likes 大于 1 name 为 Runoob 的数据：

```R
data <- read.csv("sites.csv", encoding="UTF-8")

# likes 大于 1 name 为 Runoob 的数据
retval <- subset(data, likes > 1 & name=="Runoob")
print(retval)
```

### 保存为 CSV 文件

R 语言可以使用 **write.csv()** 函数将数据保存为 CSV 文件。

接着以上实例，我们将 likes 为 222 的数据 保存到 runoob.csv 文件：

```R
data <- read.csv("sites.csv", encoding="UTF-8")

# likes 为 222 的数据
retval <- subset(data, likes == 222)

# 写入新的文件
write.csv(retval,"runoob.csv")
newdata <- read.csv("runoob.csv")
print(newdata)

 X id   name            url likes
1 2  2 Runoob www.runoob.com   222
```

X 来自数据集 newper，可以通过参数 row.names = FALSE 来删除它：

```R
data <- read.csv("sites.csv", encoding="UTF-8")

# likes 为 222 的数据
retval <- subset(data, likes == 222)

# 写入新的文件
write.csv(retval,"runoob.csv", row.names = FALSE)
newdata <- read.csv("runoob.csv")
print(newdata)

  id   name            url likes
1  2 Runoob www.runoob.com   222
```

执行完后，我们就可以看到 runoob.csv 文件生存：

![img](R%20%E8%AF%AD%E8%A8%80%E5%9F%BA%E7%A1%80.assets/BE113FF7-AD00-4D34-8E93-6DDBFDB1F866.jpg)

# R Excel 文件

Excel 格式的文件主要是 xls 或 xlsx，这两种文件可以在 R 语言中导入 xlsx 库来实现直接的读取。

R 语言读写 Excel 文件需要安装扩展包，我们可以在 R 到控制台输入以下命令来安装：

`install.packages("xlsx", repos = "https://mirrors.ustc.edu.cn/CRAN/")`

事实上，几乎所有的 Excel 软件与大多数表格软件一样支持 CSV 格式的数据，所以完全可以通过 CSV 与 R 交互，没必要再使用 Excel。

查看 xlsx 是否安装成功：

```R
# 验证包是否安装
any(grepl("xlsx",installed.packages()))
# 载入包
library("xlsx")
library("xlsx")
```

接下来，我们可以使用 read.xlsx() 函数来读取 Excel 数据：

```R
# 读取 sites.xlsx 第一个工作表数据
data <- read.xlsx("sites.xlsx", sheetIndex = 1)
print(data)
```

# R XML 文件

XML 指的是可扩展标记语言（eXtensible Markup Language），<font color='red'>XML 被设计用来传输和存储数据。</font>

如果你对 XML 还不了解，可以先查阅：[XML 教程](https://www.runoob.com/xml/xml-tutorial.html)

R 语言读写 XML 文件需要安装扩展包，我们可以在 R 到控制台输入以下命令来安装：

`install.packages("XML", repos = "https://mirrors.ustc.edu.cn/CRAN/")`

查看是否安装成功：

```
> any(grepl("XML",installed.packages()))
[1] TRUE
```

# R MySQL 连接

MySQL 是最流行的关系型数据库管理系统，在 WEB 应用方面 MySQL 是最好的 RDBMS(Relational Database Management System：关系数据库管理系统)应用软件之一。

如果你对 MySQL 还不了解，可以先查阅：[MySQL 教程](https://www.runoob.com/mysql/mysql-tutorial.html)

R 语言读写 MySQL 文件需要安装扩展包，我们可以在 R 到控制台输入以下命令来安装：

`install.packages("RMySQL", repos = "https://mirrors.ustc.edu.cn/CRAN/")`

查看是否安装成功：

```R
> any(grepl("RMySQL",installed.packages()))
[1] TRUE
```

MySQL 目前被甲骨文收购，所以很多人使用来它的复制版本 MariaDB，MariaDB 在 GNU GPL下开源，MariaDB 的开发是由 MySQL 的一些原始开发者领导的，所以语法操作都差不多：

`install.packages("RMariaDB", repos = "https://mirrors.ustc.edu.cn/CRAN/")`

在 test 数据库中创建数据表 runoob，表结构及数据代码如下：

```R
--
-- 表的结构 `runoob`
--
 
CREATE TABLE `runoob` (
  `id` int(11) NOT NULL,
  `name` char(20) NOT NULL,
  `url` varchar(255) NOT NULL,
  `likes` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
 
--
-- 转存表中的数据 `runoob`
--
 
INSERT INTO `runoob` (`id`, `name`, `url`, `likes`) VALUES
(1, 'Google', 'www.google.com', 111),
(2, 'Runoob', 'www.runoob.com', 222),
(3, 'Taobao', 'www.taobao.com', 333);
```

接下来我们可以使用 RMySQL 包来读取数据：

```R
library(RMySQL)

# dbname 为数据库名，这边的参数请根据自己实际情况填写
mysqlconnection = dbConnect(MySQL(), user = 'root', password = '', dbname = 'test',host = 'localhost')

# 查看数据
dbListTables(mysqlconnection)
```

接下来我们可以使用 dbSendQuery 来读取数据库的表，结果集通过 fetch() 函数来获取：

```R
library(RMySQL)
# 查询 sites 表，增删改查操作可以通过第二个参数的 SQL 语句来实现
result = dbSendQuery(mysqlconnection, "select * from sites")

# 获取前面两行数据
data.frame = fetch(result, n = 2)
print(data.frame)
```

https://www.math.pku.edu.cn/teachers/lidf/docs/Rbook/html/_Rbook/summary-manip.html
