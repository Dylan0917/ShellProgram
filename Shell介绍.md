#  Shell介绍

通过编写shell命令发送给Linux内核去执行，操作计算机硬件，所以shell命令时用户操作计算机硬件的桥梁

Shell是命令

shell是一门编程语言

```shell
[root@hecs-x-medium-2-linux-20201105091825 home]# cat /etc/shells 
/bin/sh
/bin/bash
/usr/bin/sh
/usr/bin/bash
```

## Centos默认的解析器

```shell
[root@hecs-x-medium-2-linux-20201105091825 home]# echo $SHELL
/bin/bash
```

> 含义：打印输出当前系统环境使用的shell解析器



## 小结

shell脚本是一个文本文件，里面可以编写shell命令或进行编程，形成一个可重用的脚本文件



## Shell脚本编写格式与执行方式

### 首行格式

```shell
#!/bin/bash
```

> 设置当前shell脚本文件采用bash解析器运行脚本代码

### 注释格式

```shell
#这里是注释内容
```

> 单行注释

```shell
:<<!
注释
注释
!
```

> 多行注释

### 执行方式

```shell
sh 脚本文件
bash 脚本文件
./脚本文件  #必须有可执行权限
```



## Shell脚本的多命令处理

创建目录batchdir，并在目录下创建文件one.txt，并增加Hello Shell

## Shell变量

1. 系统环境变量

2. 自定义变量

3. 特殊符号变量

   

### 查看系统环境变量

```shell
env
```



### 查看所有变量（系统+自定义+函数）

```shell
set
```

### 常用系统环境变量

| 变量名称 | 含义                               |
| -------- | ---------------------------------- |
| PATH     | 设置命令的搜索路径                 |
| HOME     | 当前用户的主目录                   |
| SHELL    | 当前shell解析器内容                |
| HISTFILE | 现实当前用户执行命令的历史列表文件 |
| PWD      | 显示当前所在的路径                 |
| OLDPWD   | 显示之前的路径                     |
| HOSTNAME | 显示主机名                         |
| HOSTTYPE | 显示主机架构                       |
| LANG     | 显示当前系统语言环境               |

```shell
[root@hecs-x-medium-2-linux-20201105091825 ~]# cat ~/.bash_history
```

> ```
> 保存了500条使用过的命令，这样能使你输入使用过的长命令变得容易
> ```

## Shell 自定义变量

1. 自定义局部变量
2. 自定义常量
3. 自定义全局变量

### 自定义局部变量

定义在一个脚本文件中的变量，只能在这个脚本文件中使用的变量

```shell
[root@hecs-x-medium-2-linux-20201105091825 ~]# name=yuu
[root@hecs-x-medium-2-linux-20201105091825 ~]# echo $name
[root@hecs-x-medium-2-linux-20201105091825 ~]# echo my name is ${name} #拼接
my name is yuu
[root@hecs-x-medium-2-linux-20201105091825 ~]# unset name #	变量删除
```

### 自定义常量

```sh
[root@hecs-x-medium-2-linux-20201105091825 ~]# name=yu
[root@hecs-x-medium-2-linux-20201105091825 ~]# readonly name
[root@hecs-x-medium-2-linux-20201105091825 ~]# name=777
-bash: name: 只读变量
```

### 自定义全局变量

两个脚本文件，父脚本文件中执行子脚本文件

在当前脚本文件中定义全局变量，这个全局变量可以在当前Shell环境与子Shell环境中使用

脚本文件`demo2.sh`和`demo3sh`

```shell
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# cat demo2.sh 
#!/bin/bash
var4=ywh
export var4 #设置为全局变量
sh demo3.sh
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# cat demo3.sh 
#!/bin/bash
echo "demo3.sh文件中输出var4的值为：${var4}"
```

## 特殊符号变量

```shell
$n
```

> 用于接收脚本文件执行时传入的参数 $1-$9 第一个到第9个参数 十个之后为${数字} $0获取当前脚本文件的名称

脚本文件`demo4.sh`

```shell
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# cat demo4.sh 
#!/bin/bash
echo 脚本文件名称为:$0
echo 第一个参数:$1
echo 第二个参数:$2
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# sh demo4.sh 23 56
脚本文件名称为:demo4.sh
第一个参数:23
第二个参数:56
```

```shell
$#
```

> 获取所有输入参数的个数

```shell
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# cat demo4.sh 
#!/bin/bash
echo 脚本文件名称为:$0
echo 第一个参数:$1
echo 第二个参数:$2
echo 参数个数为：$#
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# sh demo4.sh 23 56
脚本文件名称为:demo4.sh
第一个参数:23
第二个参数:56
参数个数为：2

```

```shell
$*
$@
```

> 用于输出所有的参数$*是个字符串 `$@`是个数组 使用循环可以输出

```shell
$?
```

> 获取上一个Shell命令的退出状态码，或者函数的返回值

```shell
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo "343"
343
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo $?
0

```

```shell
$$
```

> 用于获取当前Shell环境的进程ID号

```shell
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo $$
26713
```

## 自定义系统环境变量

编辑/etc/profile

## shell工作环境分类

交互式Shell

> 与用户进行交互，输入命令就会得到反馈

非交互式Shell

> 不需要用户参与就能执行多个命令，比如执行一个脚本

### 登陆Shell和非登陆环境

> 需要用户名和密码登录的shell环境
>
> 不需要用户名和密码登录的shell环境为非登陆环境

```shell
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# sh -l helloworld.sh
以登陆环境执行脚本
```

```shell
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# bash
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# sh helloworld.sh 
helloworld
非登陆环境执行脚本
```

### 识别Shell登陆环境

```shell
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo $0
-bash
登陆环境
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# bash
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo $0
bash
非登陆环境
```

```shell
su切换用户时 默认是非登陆环境 su 用户名 + -l登陆环境切换用户
```

## 字符串

var1='11'

var1="33" -----推荐

var1=33

```shell
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# name=88889
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo ${#name} #获取字符串长度
5

```

## 字符串拼接

### 无符号拼接

```shell
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# name=88889
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo ${#name}
5
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# name1=0000
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# var1=${name}${name1}
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo $var1
888890000

```

### 双引号拼接

```shell
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# var1="${name}${name1}"
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo $var1
888890000

```

### 混合拼接

```shell
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo hhhh ${var1}
hhhh 888890000

```

## **字符串截取**

```shell
${string: start :length}
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo $name
88889
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo ${name:0:1}
8
${string: start}
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo ${name:2}
889
${string: 0-start :length} 从 string 字符串的右边第 start 个字符开始，向右截取 length 个字符。
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo ${name:0-2:2}
89
${string: 0-start}从 string 字符串的右边第 start 个字符开始截取，直到最后
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo ${name:0-2}
89
${string#*chars}从 string 字符串第一次出现 *chars 的位置开始，截取 *chars 右边的所有字符。
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# name1=abcdefg
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo ${name1#*e}
fg
${string##*chars} 从 string 字符串最后一次出现 *chars 的位置开始，截取 *chars 右边的所有字符。
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo ${name1##*e}
fg
${string%*chars}从 string 字符串第一次出现 *chars 的位置开始，截取 *chars 左边的所有字符。
${string%%*chars} string 字符串最后一次出现 *chars 的位置开始
```

## 数组

```shell
array_name=(ele1  ele2  ele3 ... elen)
ages=([3]=24 [5]=19 [10]=12)
${array_name[index]} #获取数据
#获取所有
${nums[*]}
${nums[@]}
#删除某个元素
unset array_name[index]
#删除数组
unset array_name
```

### 数组拼接

```shell
array_new=(${array1[@]}  ${array2[@]})
array_new=(${array1[*]}  ${array2[*]})
```

### type命令

```bash
type命令 用来显示指定命令的类型，判断给出的指令是内部指令还是外部指令。
```

```shell
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# type cd
cd 是 shell 内嵌
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# type crontab
crontab 是 /usr/bin/crontab
```

```shell
echo -n 不换行输出
echo -e 处理特殊字符
```

若字符串中出现以下字符，则特别加以处理，而不会将它当成一般文字输出：
\a 发出警告声；
\b 删除前一个字符；
\c 最后不加上换行符号；
\f 换行但光标仍旧停留在原来的位置；
\n 换行且光标移至行首；
\r 光标移至行首，但不换行；
\t 插入tab；
\v 与\f相同；
\ 插入\字符；
\nnn 插入nnn（八进制）所代表的ASCII字符；

read命令

| -p        | 指定要显示的提示                                       |
| --------- | ------------------------------------------------------ |
| -s        | 静默输入，一般用于密码                                 |
| -n #      | 指定输入的字符长度最大值#                              |
| -d ‘字符’ | 输入结束符，当你输入的内容出现这个字符时，立即结束输入 |
| -t N      | 超出N秒没有进行输入，则自动退出。                      |

# 运算符

## expr命令

```shell
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# result=`expr 1 + 2`
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo $result
3
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# result=`expr 1 \* 2`
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo $result
2
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# result=`expr 1 / 2`
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo $result
0
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# result=`expr 1 - 2`
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo $result
-1
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# result=`expr 1 % 2`
[root@hecs-x-medium-2-linux-20201105091825 0211shell]# echo $result
1

```

## 比较运算符

### 整数比较建议使用(())

```shell
-eq 等于,如:if [ $a -eq $b ] 
-ne 不等于,如:if [ $a -ne $b ] 
-gt 大于,如:if [ $a -gt $b ] 
-ge 大于等于,如:if [ "$a" -ge "$b" ] 
-lt 小于,如:if [ $a -lt $b ] 
-le 小于等于,如:if [ $a -le $b ] 
<   小于(需要双括号),如:(($a < $b)) 
<=  小于等于(需要双括号),如:(($a <= $b)) 
>   大于(需要双括号),如:(($a > $b)) 
>=  大于等于(需要双括号),如:(($a >= $b))  
```

### 字符串比较

| -z string          | 如果 string 长度为零，则为真         | [ -z "$myvar" ]                 |
| ------------------ | ------------------------------------ | ------------------------------- |
| -n string          | 如果 string 长度非零，则为真         | [ -n "$myvar" ]                 |
| string1 = string2  | 如果 string1 与 string2 相同，则为真 | [ "$myvar" = "one two three" ]  |
| string1 != string2 | 如果 string1 与 string2 不同，则为真 | [ "$myvar" != "one two three" ] |

### [[]]与[]的区别

`[[]]`不会发生分割

`[]`会发生分割

## 布尔运算符   必须使用[]

```shell
！n非运算，表达式为true则返回false，否则返回true；

[ ! false ]

-o 或运算，有一个表达式为true，则返回true；

[ $1 -lt 20 -o $2 -gt 10 ]

-a 与运算，两个表达式都为true才返回true

[ $1 -lt 20 -a $2 -gt 10 ]


```

## 逻辑运算符

```shell
逻辑与：    &&
第一个条件为假时，第二个条件不用再判断，最终结果已经有；
第一个条件为真时，第二个条件必须得判断。
逻辑或：    ||
逻辑非:       !
```

> || && 必须由[[]]或者(())执行

> ！可以用在[]或者[[]]

## 文件检测运算符 [[]]执行

| **文件运算符** | **描述**                     |
| -------------- | ---------------------------- |
| -b file        | 检测 file 是否为块设备文件   |
| -c file        | 检测 file 是否为字符设备文件 |
| -d file        | 检测 file 是否为目录         |
| -e file        | 检测 file 是否存在           |
| -f file        | 检测 file 是否存在为普通文件 |
| -r file        | 检测 file 是否可读           |
| -s file        | 检测 file 是否为空文件       |
| -w file        | 检测 file 是否可写           |
| -x file        | 检测 file 是否可执行         |
| -L file        | 检测 file 是否符号链接       |

> filename1 ``-nt `` filename2 如果 filename1比 filename2新，则为真 [ /tmp/install/etc/services -nt /etc/services ]
> filename1` -ot`  filename2 如果 filename1比 filename2旧，则为真 [ /boot/bzImage -ot arch/i386/boot/bzImage ]

```shell
char="I am a teacher ."                      ##定义字符串变量

expr length "${char}"

expr index String1 String2  返回 String1 中包含 String2 中任意字符的第一个位置
```

### 正则表达式

```sh
[root@localhost shell]# string="hello,everyone my name is xiaoming"  
[root@localhost shell]# expr match "$string" my  
0  
[root@localhost shell]# expr match "$string" hell.*  
34  
```

## (())计算

## let命令 赋值

```shell l
let a=5+4
let b=9-3 
echo $a $b
```

## bc计算命令

| 选项                | 说明                  |
| ------------------- | --------------------- |
| -h \| --help        | 帮助信息              |
| -v \| --version     | 显示命令版本信息      |
| -l \| --mathlib     | 使用标准数学库        |
| -i \| --interactive | 强制交互              |
| -w \| --warn        | 显示 POSIX 的警告信息 |
| -s \| --standard    | 使用 POSIX 标准来处理 |
| -q \| --quiet       | 不显示欢迎信息        |

# 流程控制

## if

```shell
if [ command ];then
   符合该条件执行的语句
elif [ command ];then
   符合该条件执行的语句
else
   符合该条件执行的语句
fi
```

## Test

整数

| 参数 | 说明           |
| :--- | :------------- |
| -eq  | 等于则为真     |
| -ne  | 不等于则为真   |
| -gt  | 大于则为真     |
| -ge  | 大于等于则为真 |
| -lt  | 小于则为真     |
| -le  | 小于等于则为真 |

| 参数      | 说明                     |
| :-------- | :----------------------- |
| =         | 等于则为真               |
| !=        | 不相等则为真             |
| -z 字符串 | 字符串的长度为零则为真   |
| -n 字符串 | 字符串的长度不为零则为真 |

文件

| 参数      | 说明                                 |
| :-------- | :----------------------------------- |
| -e 文件名 | 如果文件存在则为真                   |
| -r 文件名 | 如果文件存在且可读则为真             |
| -w 文件名 | 如果文件存在且可写则为真             |
| -x 文件名 | 如果文件存在且可执行则为真           |
| -s 文件名 | 如果文件存在且至少有一个字符则为真   |
| -d 文件名 | 如果文件存在且为目录则为真           |
| -f 文件名 | 如果文件存在且为普通文件则为真       |
| -c 文件名 | 如果文件存在且为字符型特殊文件则为真 |
| -b 文件名 | 如果文件存在且为块特殊文件则为真     |

## case语句

```sh
case 变量名 in
 值1) 
  指令1 
 ;; 
 值2) 
  指令2 
 ;; 
 值3) 
  指令3 
 ;;
 *)
  指令4
 ;;
esac
```

## while语句

```shell
while condition
do
    statements;
    #continue;
    #break;
done
```



## untill语句

```shell
until 条件
    command1
    command2
    ...
    commandN
done
```

> ntil循环执行一系列命令直至条件为真时停止

## for 循环

```shell
for 变量 in 值1 值2 值3…
do
程序
done
```

```shell
for ((初始值；循环控制条件；变量变化)）
do
程序
done
```

### 无限循环

```shell
for ((；；))
do
程序
done
```



## select语句

```shell
select var in ... ; do
　break;
done
.... now $var can be used ....


#!/bin/bash
echo "What is your favourite OS?"
select var in "Linux" "Gnu Hurd" "Free BSD" "Other"; do
  break;
done
echo "You have selected $var"
```



# 系统函数

### basename

> basename 是去除目录后剩下的名字

```shell
[deng@localhost ~]$ basename /home/deng/scott_data.sql .sql
scott_data
[deng@localhost ~]$ 

[deng@localhost ~]$ basename /home/deng/scott_data.sql 
scott_data.sql
[deng@localhost ~]$
```

### dirname

> 获取当前路径

```shell
[root@qzt196 ~]# dirname /usr/bin/sort 
/usr/bin
[root@qzt196 ~]# dirname stdio.h 
.
```

## 自定义函数

```shell
[ function ] funname [()]
{
    action;
    [return int;]
}

funname  调用
```

### 有参数函数

| 特殊变量 | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| $#       | 传递给函数的参数个数。                                       |
| $*       | 显示所有传递给函数的参数。                                   |
| $@       | 与$*相同，但是略有区别，请查看[Shell特殊变量](http://c.biancheng.net/cpp/view/2739.html)。 |
| $?       | 函数的返回值。                                               |

```shell
$str="This is a test!"
fun1(){
echo $str;
        echo $1;
        echo $2;
}
#调用fun1
fun1  "aa" "bb"
fun1  "cc" "dd"
结果：
This is a test!
aa
bb
This a test!
cc
dd
```

## Shell重定向

| **>** | **箭头代表重定向**             |
| ----- | ------------------------------ |
| **&** | **代表引用**                   |
| **2** | **表示**STDERR**标准错误输出** |
| 0     | 表示STDIN标准输入              |
| 1     | 表示STDOUT标准输出             |

> **输出重定向**就是指将输出内容写入到一个文件中去，>表示覆盖，>>表示追加

## [wc](http://www.linuxso.com/command/wc.html)[命令]

\- c 统计字节数。 

\- l 统计行数。 

\- w 统计字数。



## cut命令

```shell
cut [options] filename
```

> 按列分割

- -b ：以字节为单位进行分割。这些字节位置将忽略多字节字符边界，除非也指定了 -n 标志。
- -c ：以字符为单位进行分割。
- -d ：自定义分隔符，默认为制表符。
- -f ：与-d一起使用，指定显示哪个区域。
- -n ：取消分割多字节字符。仅和 -b 标志一起使用。如果字符的最后一个字节落在由 -b 标志的 List 参数指示的
  范围之内，该字符将被写出；否则，该字符将被排除

# sed命令

> **sed在处理文本时是逐行读取文件内容，读到匹配的行就根据指令做操作，不匹配就跳过**。

**参数说明**：

- -e<script>或--expression=<script> 以选项中指定的script来处理输入的文本文件。
- -f<script文件>或--file=<script文件> 以选项中指定的script文件来处理输入的文本文件。
- -h或--help 显示帮助。
- -n或--quiet或--silent 仅显示script处理后的结果。
- -V或--version 显示版本信息。

**动作说明**：

- a ：新增， a 的后面可以接字串，而这些字串会在新的一行出现(目前的下一行)～

- c ：取代， c 的后面可以接字串，这些字串可以取代 n1,n2 之间的行！

- d ：删除，因为是删除啊，所以 d 后面通常不接任何咚咚；

- i ：插入， i 的后面可以接字串，而这些字串会在新的一行出现(目前的上一行)；

- p ：打印，亦即将某个选择的数据印出。通常 p 会与参数 sed -n 一起运行～

- s ：取代，可以直接进行取代的工作哩！通常这个 s 的动作可以搭配正规表示法！例如 1,20s/old/new/g 就是啦！

  ## Sort命令

  排序选项：

  -b, --ignore-leading-blanks 忽略前导的空白区域
  -d, --dictionary-order 只考虑空白区域和字母字符
  -f, --ignore-case 忽略字母大小写
  -g, --general-numeric-sort 按照常规数值排序
  -i, --ignore-nonprinting 只排序可打印字符
  -n, --numeric-sort 根据字符串数值比较
  -r, --reverse 逆序输出排序结果

  其他选项：

  -c, --check, --check=diagnose-first 检查输入是否已排序，若已有序则不进行操作
  -k, --key=位置1[,位置2] 在位置1 开始一个key，在位置2 终止(默认为行尾)
  -m, --merge 合并已排序的文件，不再进行排序
  -o, --output=文件 将结果写入到文件而非标准输出
  -t, --field-separator=分隔符 使用指定的分隔符代替非空格到空格的转换
  -u, --unique 配合-c，严格校验排序；不配合-c，则只输出一次排序结果 