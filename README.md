# R-Style-Guide
## 1. 目的
该文档记录深圳电网项目组R语言编码风格约定。这份R 语言编码风格指南旨在让我们team的R代码更容易阅读、分享和检查。
## 2. 参考文档
- Google R Style Guide
- R Style Guide by Hadley Wickham
- R Coding Conventions by Henrik Bengtsson 
## 3. R编码风格约定
### 3.1 摘要
1. 文件命名: 以.R (大写) 结尾  
2. 标识符命名：variable_name(or variableName),functionName, kConstantName
3. 单行长度: 不超过80 个字符  
4. 缩进: 两个空格, 不使用制表符
5. 空白
6. 花括号: 前括号不折行写, 后括号独占一行
7. else: else两侧加括号
8. 赋值符号: 使用 <- , 而非 =
9. 分号: 不要用
10. 总体布局和顺序
11. 注释准则: 所有注释以# 开始, 后接一个空格; 行内注释需要在# 前加两个空格
12. 函数的定义和调用
13. 函数文档
14. 示例函数
15. TODO 书写风格: TODO(您的用户名)
### 3.2 表示和命名
#### 1) 文件命名
文件名应以.R (大写) 结尾, 文件名本身要有意义。
```
# 正例
predict_ad_revenue.R
fit-models.R
utility-functions.R
 
# 反例
foo.R
stuff.r
```
如果文件需要按顺序运行，那么文件名应该加上数字前缀。
```
0-download.R
1-parse.R
2-explore.R
```
#### 2) 标识符命名
- 在标识符中不要使用连字符( - )。标识符应根据如下惯例命名。
> 变量名首选形式为：所有的字母或单词小写，并用下划线分隔(variable_name)，但也接受variableName;  
> 函数名采用小驼峰命名法, 不用点分隔(functionName);  
> 常数命名规则与函数类似, 但需要以k开头。  
- 首选variable_name，但variableName也行
```
# 正例
day_one
day_1

# 还行
dayOne

# 反例
first_day_of_the_month
DayOne
dayone
djm1
```
- functionName
```
# 正例
calculateAvgClicks

# 反例
calculate_avg_clicks
```
- 函数命名应为动词或动词性短语。
> 例外：当创建一个含类(class) 属性的对象时, 函数名(也是constructor)和类名(class) 应当匹配(例如, lm)。
- kConstantName
- 尽可能避免使用已经存在的函数名和变量名，否则可能会使读者困惑。
```
# 反例
T <- FALSE
c <- 10
mean <- function(x) sum(x)
```
Henrik Bengtsson教授的建议
1. 变量命名建议
```
1. 变量命名尽量少用缩写，e.g. fileName而不是flNm，但某些约定俗成的词最好还是保留缩写，但首字母大写外，其余都用小写，Html而不是HTML，也不是HyperTextMarkupLanguage；  
2. 临时变量要尽量短，让读者明确该变量仅在某几行代码内有效，e.g. i或ii而不是iterationNumber；    
3. 变量命名要有可读性，e.g. okButton、mainWindow或leftScrollbar而不是Flag或variable；  
4. 变量命名时要突出某些变量的类型，如矩阵、列表，e.g. 如果matrixElement代表矩阵的某一个元素，需要使用matrixElementList代表矩阵元素列表，而不是使用matrixElements表示；  
5. 变量如果表示物体或者实体数量时，尽量使用nXXXX表示，e.g. nPoints和nLines代表点和线的数量，而不是points；   
6. 变量如果表示实体的编号时，尽量使用xxxNo表示，e.g. tableNo或employeeNo.
```

2. 函数命名建议
```
1. 函数命名要注意减少复杂度，e.g. setTopic(topic)而不是setTopic(value)，getLength(line)而不是getLineLength(line)；  
2. 如果函数返回值为布尔型，最好把is作为前缀，e.g. isSet()、isVisible()或isOpen()而不是isFlag()或whetherOpen()，也可用hascanshould代替is；但不要用逻辑关系词not，e.g. isNotOpen()；  
3. 如果函数需要一定时间遍历或者计算某个变量的值，最好使用find作为前缀，e.g. findNearestVertex(vertex)或findMinElement(matrix)；当不需要计算即可直接获得的可以使用get作为前缀，e.g. getDictionary(Dictionary)或getValue(value)；  
4. 如果函数用于初始化，则使用initialize作为前缀，e.g. initializeFontSet(printer)而不是initFontSet(printer)；  
5. 如果某两个函数有相关性，尽量使用对称的动词作为前缀，减少命名复杂度，e.g. getName(name) v.s. setName(name)，addStudent(student) v.s. removeStudent(student)，或create/destroy，start/stop，begin/end或next/previous；  
6. 函数命名不要使用缩写，不要用cmd代替command，或用cp代替copy等，e.g. computeAverage()而不是compAvg().
```
### 3.3 语法
#### 3) 单行长度
- 最大单行长度为80 个字符。
#### 4) 缩进
- 使用两个空格来缩进代码。永远不要使用制表符或混合使用二者。
> 例外：当括号内发生折行时, 所折行与括号内的第一个字符对齐。
```
# 例如
long_function_name <- function(a = "a long argument", 
                               b = "another argument",
                               c = "another long argument") {
  # As usual code is indented by two spaces.
}
```
#### 5) 空白
- 在所有二元操作符(=, +, -, <-, 等等) 的两侧加上空格。
> 例外：在函数调用中传递参数时 = 两边的空格可加可不加。
- 不可在逗号前加空格, 逗号后总须加空格。
```
# 正例一
average <- mean(feet / 12 + inches, na.rm = TRUE)

# 反例一
average<-mean(feet/12+inches,na.rm=TRUE)

# 正例二
tab.prior <- table(df[df$days.from.opt < 0, "campaign.id"])
total <- sum(x[, 1])
total <- sum(x[1, ])

# 反例二
tab.prior <- table(df[df$days.from.opt<0, "campaign.id"])  # 在'<' 两侧需增加空格
tab.prior <- table(df[df$days.from.opt < 0,"campaign.id"])  # 逗号后需要一个空格
tab.prior<- table(df[df$days.from.opt < 0, "campaign.id"])  # 在<- 前需要一个空格
tab.prior<-table(df[df$days.from.opt < 0, "campaign.id"])  # 在<- 两侧需要增加空格
total <- sum(x[,1])  # 逗号后需要一个空格
total <- sum(x[ ,1])  # 逗号后需要一个空格, 而非逗号之前
```
> 例外：:, :: and :::两边不需要加空格。
```
# 正例
x <- 1:10
base::get

# 反例
x <- 1 : 10
base :: get
```
- 在前括号前加一个空格, 函数调用时除外。
```
# 正例
if (debug)
plot(x, y)

# 反例
if(debug)
plot (x, y)
```
- 多加空格(即, 在行内使用多于一个空格) 也是可以的, 如果这样做能够改善等号或箭头(<-) 的对齐效果。
```
 plot(x    = xCoord,
      y    = dataMat[, makeColName(metric, ptiles[1], "roiOpt")],
      ylim = ylim,
      xlab = "dates",
      ylab = metric,
      main = (paste(metric, " for 3 samples ", sep="")))
```
- 不要向圆括号或方括号中的代码两侧加入空格。
> 例外：逗号后总须加空格。
```
# 正例
if (debug)
x[1, ]

# 反例
if ( debug )  # debug 的两边不要加空格
x[1,]  # 需要在逗号后加一个空格
```
#### 6) 花括号
- 前括号永远不应该独占一行；后括号应当总是独占一行（除非后面跟着else）。总是在括号内缩进代码。
```
# 正例
if (y < 0 && debug) {
  message("Y is negative")
}

# 反例
if (y < 0 && debug)
message("Y is negative")
```
- 可以将非常短的语句放在同一行。
```
# 例如
if (y < 0 && debug) message("Y is negative")
```
#### 7) else 
- else语句应该总被同一行的花括号包围。
```
# 正例
if (condition) {
one or more lines
} else {
one or more lines
}

# 反例一
if (condition) {
one or more lines
} 
else {
one or more lines
}

# 反例二
if (condition)
one line
else
one line
```
#### 8)	赋值符号
- 使用 <- 进行赋值, 不用 = 赋值。
```
# 正例
x <- 5

# 反例
x = 5
```
#### 9)	分号
- 不要以分号结束一行, 也不要利用分号在同一行放多于一个命令。
### 3.4 代码组织
#### 10)	 总体布局和顺序
- 如果所有人都以相同顺序安排代码内容, 我们就可以更加轻松快速地阅读并理解他人的脚本了。
1. 版权声明注释
2. 作者信息注释
3. 文件描述注释, 包括程序的用途, 输入和输出
4. source() 和library() 语句
5. 函数定义
6. 执行语句，如果适用(例如， print, plot)
- 单元测试应该在一个命名为originalfilename_test.R的单独文件中。
#### 11)	 注释准则
- 注释您的代码. 整行注释应以# 后接一个空格开始。
- 行内短注释应在代码后接两个空格, #, 再接一个空格。
- 使用 - 或 = 组成的线将文件分割为不同的块儿。
```
# Load data ---------------------------

# Plot data ---------------------------
```
#### 12)	 函数的定义和调用
-	函数定义应首先列出无默认值的参数, 然后再列出有默认值的参数。
-	函数定义和函数调用中, 允许每行写多个参数; 折行只允许在赋值语句外进行。
```
# 正例
PredictCTR <- function(query, property, num.days,
                            show.plot = TRUE)
# 反例
PredictCTR <- function(query, property, num.days, show.plot =
                            TRUE)
```
- 理想情况下, 单元测试应该充当函数调用的样例(对于包中的程序来说)。
#### 13)	 函数文档
- 函数在定义行下方都应当紧接一个注释区。这些注释应当由如下内容组成：
> (1) 此函数的一句话描述;  
> (2) 此函数的参数列表, 用Args: 表示, 对每个参数的描述(包括数据类型)；  
> (3) 此函数的返回值的描述, 以Returns:表示。  
- 这些注释应当描述得足够充分, 这样调用者无须阅读函数中的任何代码即可使用此函数。
#### 14)	 示例函数
```
CalculateSampleCovariance <- function(x, y, verbose = TRUE) {
# Computes the sample covariance between two vectors.
#
# Args:
# x: One of two vectors whose sample covariance is to be calculated.
# y: The other vector. x and y must have the same length, greater than one,
# with no missing values.
# verbose: If TRUE, prints sample covariance; if not, not. Default is TRUE.
#
# Returns:
# The sample covariance between x and y.
n <- length(x)
# Error handling
if (n <= 1 || n != length(y)) {
stop("Arguments x and y have different lengths: ",
length(x), " and ", length(y), ".")
}
if (TRUE %in% is.na(x) || TRUE %in% is.na(y)) {
stop(" Arguments x and y must not have missing values.")
}
covariance <- var(x, y)
if (verbose)
cat("Covariance = ", round(covariance, 4), ".\n", sep = "")
return(covariance)
}
```
#### 15)	 TODO 书写风格
- 编码时通篇使用一种一致的风格来书写TODO。
- TODO(您的用户名): 所要采取行动的明确描述。
 
