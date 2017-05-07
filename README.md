# R-Style-Guide
## 1. 目的
该文档记录深圳电网项目组R语言编码风格约定。这份R 语言编码风格指南旨在让我们team的R代码更容易阅读、分享和检查。
## 2. 参考文档
- R Style Guide by Hadley Wickham
- Google R Style Guide
- R Coding Conventions by Henrik Bengtsson 
## 3. R编码风格约定
### 3.1 摘要
> 1. 文件命名: 以.R (大写) 结尾  
> 2. 标识符命名：variable.name(or variableName),FunctionName, kConstantName  
> 3. 单行长度: 不超过80 个字符  
> 4. 缩进: 两个空格, 不使用制表符
> 5. 空白
> 6. 花括号: 前括号不折行写, 后括号独占一行
> 7. else: else两侧加括号
> 8. 赋值符号: 使用 <- , 而非 =
> 9. 分号: 不要用
> 10. 总体布局和顺序
> 11. 注释准则: 所有注释以# 开始, 后接一个空格; 行内注释需要在# 前加两个空格
> 12. 函数的定义和调用
> 13. 函数文档
> 14. 示例函数
> 15. TODO 书写风格: TODO(您的用户名)
### 3.2 表示和命名
#### 1) 文件命名
文件名应以.R (大写) 结尾, 文件名本身要有意义。
```
# 正例
predict_ad_revenue.R
 
# 反例
foo.R
```
#### 2)	标识符命名
- 在标识符中不要使用下划线( _ ) 或连字符( - )。标识符应根据如下惯例命名。
> 变量名首选形式为：所有的字母或单词小写，并用点分隔(variable.name)，但也接受variableName;  
> 函数名首字母大写, 不用点分隔(FunctionName);  
> 常数命名规则与函数类似, 但需要以k开头。  
- 首选variable.name，但variableName也行
```
# 正例
avg.clicks

# 还行
avgClicks

# 反例
avg_Clicks
```
- FunctionName
```
# 正例
CalculateAvgClicks

# 反例
calculate_avg_clicks , calculateAvgClicks
```
- 函数命名应为动词或动词性短语。
> 例外：当创建一个含类(class) 属性的对象时, 函数名(也是constructor)和类名(class) 应当匹配(例如, lm)。
- kConstantName
### 3.3 语法
#### 3)	单行长度
- 最大单行长度为80 个字符。
#### 4)	缩进
- 使用两个空格来缩进代码。永远不要使用制表符或混合使用二者。
> 例外：当括号内发生折行时, 所折行与括号内的第一个字符对齐。
#### 5)	空白
- 在所有二元操作符(=, +, -, <-, 等等) 的两侧加上空格。
> 例外：在函数调用中传递参数时 = 两边的空格可加可不加。
- 不可在逗号前加空格, 逗号后总须加空格。
```
# 正例
tab.prior <- table(df[df$days.from.opt < 0, "campaign.id"])
total <- sum(x[, 1])
total <- sum(x[1, ])

# 反例
tab.prior <- table(df[df$days.from.opt<0, "campaign.id"])  # 在'<' 两侧需增加空格
tab.prior <- table(df[df$days.from.opt < 0,"campaign.id"])  # 逗号后需要一个空格
tab.prior<- table(df[df$days.from.opt < 0, "campaign.id"])  # 在<- 前需要一个空格
tab.prior<-table(df[df$days.from.opt < 0, "campaign.id"])  # 在<- 两侧需要增加空格
total <- sum(x[,1])  # 逗号后需要一个空格
total <- sum(x[ ,1])  # 逗号后需要一个空格, 而非逗号之前
```
- 在前括号前加一个空格, 函数调用时除外。
```
# 正例
if (debug)

# 反例
if(debug)
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
#### 6)	花括号
- 前括号永远不应该独占一行；后括号应当总是独占一行。您可以在代码块只含单个语句时省略花括号；但在处理这类单个语句时, 您必须前后一致地要么全部使用花括号, 或者全部不用花括号。
```
# 正例
if (is.null(ylim)) {
ylim <- c(0, 0.06)
}

# 或者（但不同时）
if (is.null(ylim))
ylim <- c(0, 0.06)
```
- 总在新起的一行开始书写代码块的主体。
```
# 反例
if (is.null(ylim)) ylim <- c(0, 0.06)
if (is.null(ylim)) {ylim <- c(0, 0.06)}
```
#### 7)	else 
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
} else {
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
-不要以分号结束一行, 也不要利用分号在同一行放多于一个命令。
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
-	行内短注释应在代码后接两个空格, #, 再接一个空格。
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
(1) 此函数的一句话描述；
(2) 此函数的参数列表, 用Args: 表示, 对每个参数的描述(包括数据类型)；
(3) 此函数的返回值的描述, 以Returns:表示. 
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
- 编码时通篇使用一种一致的风格来书写TODO.
- TODO(您的用户名): 所要采取行动的明确描述

