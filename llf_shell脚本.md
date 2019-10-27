# shell脚本

## 第一阶段：shell编程

shell的定义：

* 在计算机科学中，shell就是一个命令解释器

shell的分类：

* 图形shell
* 命令行shell

echo $SHELL 查看本机的默认shell位置

echo 'i Love' ：

* 手工方式，手工敲击硬盘，在shell的命令输入命令，然后shell返回并显示命令结果
* 重点：**每行输入命令，每行进行确认命令**

#### 脚本开发规范

1、脚本命名要有意义，文件后缀是.sh 

2、脚本文件首行**是而且必须是**脚本解释器 

\#!/bin/bash

3、脚本文件解释器后面要有脚本的基本信息等内容 

脚本文件中尽量不用中文注释; 尽量用英文注释，防止本机或切换系统环境后中文乱码的困扰 

常见的注释信息：脚本名称、脚本功能描述、脚本版本、脚本作者、联系方式等 

4、脚本文件常见执行方式：bash 脚本名 

5、脚本内容执行：从上到下，依次执行 

6、代码书写优秀习惯; 

1）成对内容的一次性写出来,**防止遗漏**。 

如：()、{}、[]、''、``、"" 

2）[]中括号两端要有空格,书写时即可留出空格[ ],然后再退格书写内容。 

3）流程控制语句一次性书写完，再添加内容 

7、通过缩进让代码易读;(即该有空格的地方就要有空格)

##### sehll 脚本示例

```shell
# 创建脚本文件
vim itcast.sh
======================
# 写入脚本
#!/bin/bash
# 这是一个测试脚本
echo 'i love'
echo 'itcast'
=======================
# 用本机shell执行脚本
/bin/bash itcast.sh
```

脚本创建工具：vi和vim

脚本命名：shell的脚本，命名要有意义，一眼就懂里面要执行的命令

脚本内容：各种可以执行的命令

```shell
#！这是指定用哪一个解释器的位置
# 这是单行注释
===========================
echo '下一行是多行注释'
:<<!
echo '1'
echo '2'
echo '3'
！
echo '4'
============================
===========================
echo '下一行是多行注释'
:<<a
echo '1'
echo '2'
echo '3'
a
echo '4'
============================
```

```shell
脚本执行方式：
# 1.绝对执行路径
/bin/bash /home/python/Desktop/itcash.sh

# 2.直接执行
/home/python/Desktop/itcash.sh
# 要给文件加权限
chmod +x itcash.sh

# 3.用source 执行或者前面加个‘.’
source itcash.sh 
. itcash.sh
# 注释尽量不用中文注释
# 脚本内容执行：从上到下，依次执行
# 代码书写优秀习惯
```

本地变量：在当前系统的某个环境下才能生效的变量，作用很小

#### 本地变量的分类： 普通变量，命令变量

```shell
# 普通变量
echo $SHELL
# 方式一,必须完整的变量名
echo $itcast
itcast=nihao666
echo $itcast
# 方式二，单引号看见什么内容，我就输出什么内容
echo $itcast
itcast='dan—$itcast'
echo $itcast
# 方式三，双引号是如果变量值范围内，有可以解析的变量A，那么先解析A，将原来的变量赋值给变量B
echo $itcast
itcast="shuang-$itcast"
echo $itcast
```

```shell
# 命令变量的定义有两种
# 定义的方式一：
变量名=`命令`
注意：``是反引号
python@PC:~$ dir=`pwd`
python@PC:~$ echo $dir
/home/python
#定义的方式二：
变量名=$(命令)
python@PC:~$ dir1=$(pwd)
python@PC:~$ echo $dir1
/home/python
```

### 全局变量 是当前系统的所有环境下都能生效的变量

```shell
$SHELL # 它就是一个全局变量
# 可以通过命令查看环境变量
env # 只显示全局变量
# 定义的方式一
变量=值
export 变量
====================================
python@PC:~/Desktop$ itcast=ls
python@PC:~/Desktop$ export itcast
python@PC:~/Desktop$ $itcast
# 方式二:(最常用)
export 变量=值
=====================================
python@PC:~/Desktop$ export itcast=ls
python@PC:~/Desktop$ $itcast
1.txt	     demo_text	  itcash.sh	     MEIDUO_STOP_APP  storage_python  WHW demo_python  itcash_1.sh # meiduo_mall_admin  Navicat.desktop  text
```

#### 查看&删除

```shell
# 查看变量
# 方式一:  echo $变量名
	# 场景: 私下里,在命令行/脚本中使用图省事
# 方式二:  echo "$变量名"
	# 场景:私下里,在命令行/脚本中使用图省事
# 方式三:  echo ${变量名}
	# 场景:echo "dsa dsafsa dsafsa &{变量名}f"
	# 使用频率较高
# 方式四:  echo "${变量名}"
	# 场景:标准使用
# 取消变量
unset 变量名
```

### 内置变量

```shell
# shell 内置变量
# 脚本文件
$0  # 获取当前执行的shell脚本文件名
$n  # 获取当前执行的shell脚本的第n个参数值,n=1..9,当n为0是表示脚本的文件名,如果n大于9就要用大括号括起来${10}
$#  # 获取当前shell命令行中的参数的总数
$?  # 获取执行上一个指令的返回值(0为成功,非0为失败)
# 演示效果:
# $0:
python@PC:~/Desktop$ vim get_name.sh
python@PC:~/Desktop$ cat get_name.sh 
============================================
#!/bin/bash									
# $0 获取当前脚本的名称						  
echo "我的脚本名称是: get_name.sh"			   
echo "获取当前脚本名称: $0"
============================================
python@PC:~/Desktop$ bash get_name.sh 
我的脚本名称是: get_name.sh
获取当前脚本名称: get_name.sh

# $n:
python@PC:~/Desktop$ vim get_arg.sh
python@PC:~/Desktop$ cat get_arg.sh 
============================================
#!/bin/bash									
# $n 获取位置参数						  
echo "这是第一个参数:$1"			   
echo "这是第一个参数:$2"
============================================
python@PC:~/Desktop$ bash get_arg.sh 1 2 
这是第一个参数:1
这是第一个参数:2

# $#:
python@PC:~/Desktop$ vim get_aum.sh
python@PC:~/Desktop$ cat get_aum.sh 
=============================================
#!/bin/bash
# $# 获取脚本传参的总数
echo "当前获取的参数的总数是: $#"
=============================================
python@PC:~/Desktop$ bash get_aum.sh 1 2 3
当前获取的参数的总数是: 3
$?
python@PC:~/Desktop$ echo $?
0 # 成功,非0失败

# 字符串精确截取: 格式 ${变量名:起始开始:截取长度}
# 示例
python@PC:~/Desktop$ file=dassdasfassdwqdsa
python@PC:~/Desktop$ echo "${file:0:-1}"
dassdasfassdwqds
```

```shell
# 默认值相关:
# 场景一: 
# 变量a如果内容,那么就输出a的变量值
# 变量a如果没有内容,那么就输出默认内容
# 格式: ${变量名:-默认值}
# 示例:
python@PC:~/Desktop$ vim moren1.sh
python@PC:~/Desktop$ cat moren1.sh 
========================================
#!/bin/bash
# 默认值场景1 有条件的默认值

# 定义一个本地变量,接收脚本传参
a="$1"
echo "您选择得到套餐是: ${a:-1}套餐"
========================================
python@PC:~/Desktop$ bash moren1.sh 2
您选择得到套餐是: 2套餐
# 场景二:
python@PC:~/Desktop$ vim moren2.sh 
python@PC:~/Desktop$ cat moren2.sh 
========================================
#!/bin/bash
# 默认值场景二,默认值强制生效
# 定义一个本地变量,接收脚本传入的参数
a="$1"
echo="国家法定结婚年龄(男性)是: ${a+22} 岁"
=========================================
python@PC:~/Desktop$ bash moren2.sh 
国家法定结婚年龄(男性)是: 22 岁
```

### 表达式

**测试语句**

```shell
# 测试表达式
# 第一种
python@PC:~/Desktop$ test 1 = 1 
python@PC:~/Desktop$ echo $?
0
# 第二种: 常用是二
python@PC:~/Desktop$ [ 1 = 1 ]
python@PC:~/Desktop$ echo $?
0
```

条件表达式

```shell
# 逻辑表达式
# 逻辑表达式一般用于判断多个条件之间的依赖关系
# 常见的逻辑表达式有:  && 和 ||
# &&:
# 命令执行成功 && 那么我才执行命令
# 命令执行失败 && 那么我不执行命令
python@PC:~/Desktop$ [ 1 = 1 ] && echo "条件成立"
条件成立
# ||
# 反着
# 命令执行成功 || 那么我不执行命令
# 命令执行失败 || 那么我执行命令
python@PC:~/Desktop$ [ 1 = 2 ] || echo "条件不成立"
条件不成立
```

文件表达式

```shell
# -f 判断是不是一个文件
python@PC:~/Desktop$ [ -f moren1.sh ] || echo "条件成立"
python@PC:~/Desktop$ [ -f moren1.sh ] && echo "条件成立"
条件成立
# -d 判断是不是一个目录
python@PC:~/Desktop$ [ -d moren1.sh ] && echo "条件成立"
python@PC:~/Desktop$ [ -d moren1.sh ] || echo "条件不成立"
条件不成立
# -x 判断输入内容是否可执行
python@PC:~/Desktop$ [ -x moren1.sh ] || echo "它是不执行文件"
它是不执行文件
python@PC:~/Desktop$ [ -x moren1.sh ] && echo "它是可执行文件"
python@PC:~/Desktop$ [ -x itcash.sh ] && echo "它是可执行文件"
它是可执行文件
============================================================
python@PC:~/Desktop$ [ -x itcash.sh ] && ./itcash.sh 
i love
itcash
hello world
4
============================================================
python@PC:~/Desktop$ [ -x itcash_1.sh ] || chmod +x itcash_1.sh 
python@PC:~/Desktop$ ls
```

### 数值操作符

```shell
# 判断两个值的关系,如是否相等、大于、小于、等于第二数
n1 -eq n2   相等
n1 -gt n2	大于
n1 -lt n2	小于
n1 -ne n2	不等于
# 判断字符串是否内容一致
str1 == str2   str1和str2字符串内容一致
str1 != str2   str1和str2字符串内容不一致，!表示相反的意思
```

### 计算表达式

```shell
# 使用场景: 简单来说就是对具体的内容进行算数计算
# 计算格式:
# 方式一: $(())  $((计算表达式))
python@PC:~/Desktop$ echo $((1+1))
2
# 方式二: let     let 计算表达式
python@PC:~/Desktop$ let a=a+1
python@PC:~/Desktop$ echo $a
10
python@PC:~/Desktop$ a=$((a+7))
python@PC:~/Desktop$ echo $a
17
# 注意: $(())中只能用+-*/和()运算符,并且只能做整数运算
# $(())可以有空格,let 必须整体
```

###  linux常见符号

```shell
# 重定向
# 在shell脚本中有两种常见的重定向符号 > 和 >>
# >
python@PC:~/Desktop$ echo 'nihao' > nihao.txt
python@PC:~/Desktop$ cat nihao.txt
nihao
# 作用：> 表示将符号左侧的内容，以覆盖的方式输入到右侧文件中
python@PC:~/Desktop$ echo 'nisdadas' > nihao.txt 
python@PC:~/Desktop$ cat nihao.txt
nisdadas
# >>
python@PC:~/Desktop$ echo 'nisdadas' >> nihao.txt 
python@PC:~/Desktop$ cat nihao.txt
nisdadas
nisdadas

# 管道符
# 定义：| 这个就是管道符，传递信息使用的
# 使用格式: 命令1 | 命令2 
# 管道符左侧命令1 执行后的结果，传递给管道符右侧的命令2使用
# 查看当前系统中的全局变量SHELL
# env 是查看所有全局变量
env | grep SHELL
```

#### 其他符号

```shell
# 后台展示符号: & 
# 定义：
# 		& 就是将一个命令从前台转到后台执行
# 使用格式：
# 		命令 &
# 示例:
python@PC:~/Desktop$ sleep 10 & 
[1] 22972
python@PC:~/Desktop$ ps aux | grep sleep
python    22972  0.0  0.0  14572   736 pts/2    S    17:13   0:00 sleep 10
python    22974  0.0  0.0  21532  1036 pts/2    S+   17:13   0:00 grep --color=auto sleep
```

**信息符号**

```shell
# 符号详解：
# 1 表示正确输出的信息
# 2 表示错误输出的信息
python@PC:~/Desktop$ rm ceshi.sh 
python@PC:~/Desktop$ vim ceshi.sh
python@PC:~/Desktop$ bash ceshi.sh 
下一条是错误信息
ceshi.sh: 行 3: dasdasdsa: 未找到命令
python@PC:~/Desktop$ bash ceshi.sh 1>> ceshi-ok 2>> ceshi-err 
python@PC:~/Desktop$ cat ceshi-ok 
下一条是错误信息
python@PC:~/Desktop$ cat ceshi-err 
ceshi.sh: 行 3: dasdasdsa: 未找到命令

# 2>&1 代表所有输出的信息
python@PC:~/Desktop$ bash ceshi.sh >> cashi-all 2>&1
python@PC:~/Desktop$ cat cashi-all 
下一条是错误信息
ceshi.sh: 行 3: dasdasdsa: 未找到命令
```

#### 特殊设备

/dev/null 是linux下的一个设备文件， 

这个文件类似于一个垃圾桶，特点是：容量无限大

### 常见命令详解

#### grep命令

```shell
# 命令格式
# grep命令是我们常用的一个强大的文本搜索命令。
# grep [参数] [关键字] <文件名>
# 注意：
# 我们在查看某个文件的内容的时候，是需要有<文件名>
# 参数详情:
# -c: 只能输出匹配的计数
python@PC:~/Desktop/脚本$ vim find.txt
python@PC:~/Desktop/脚本$ grep -c aaa find.txt 
2
python@PC:~/Desktop/脚本$ grep -c nihao find.txt 
6
python@PC:~/Desktop/脚本$ grep nihao find.txt
nihao aaa
nihao aaa
nihao AAA
nihao AAA
nihao bbb
nihao ccc
# -n:显示匹配行及行号
python@PC:~/Desktop/脚本$ grep -n nihao find.txt
1:nihao aaa
2:nihao aaa
3:nihao AAA
4:nihao AAA
5:nihao bbb
6:nihao ccc
# -v: 显示不包含匹配文本的所有行
python@PC:~/Desktop/脚本$ grep -v nihao find.txt
aaaaaaaaaaa

# 小技巧：
# 精确定位错误代码
grep -nr [错误关键字] *
```

#### sed命令

```shell
# 格式详解
# sed 行文件编辑工具。因为它编辑文件是以行为单位的。
# 命令格式：
# 		sed [参数] '<匹配条件> [动作]' [文件名]
# 注意：
# 		可以通过 sed --help 查看帮助信息
# 参数详解：
# 		参数为空 表示sed的操作效果，实际上不对文件进行编辑
# 		-n 取消静默输出
# 		-i 表示对文件进行编辑
# 匹配条件：
# 匹配条件分为两种：数字行号或者关键字匹配
# 		'/关键字/'
# 注意：
# 		隔离符号 / 可以更换成 @、#、！等符号
# 		根据情况使用，如果关键字和隔离符号有冲突，就更换成其他的符号即可。
# 动作详解
# a 在匹配到的内容下一行增加内容
# i 在匹配到的内容当前行增加内容
# d 删除匹配到的内容
# s 替换匹配到的内容
# p 查看指定内容
# 注意：
# 上面的动作应该在参数为-i的时候使用，不然的话不会有效果
```

#### 替换命令:

```shell
# 替换实践
# 关于替换，我们从三个方面来学习：
# 		行号、列号、全体
# 命令格式：
# 	sed -i [替换格式] [文件名]
# 注意：替换命令的写法
#  's###' ---> 's#原内容##' ---> 's#原内容#替换后内容#'
# 匹配每行首个之母为大写
python@PC:~/Desktop/脚本$ sed -i 's#sed#SED#' sed.txt
python@PC:~/Desktop/脚本$ cat sed.txt 
nihao SED sed sed
nihao SED sed sed
nihao SED sed sed
# 匹配全部内容:
python@PC:~/Desktop/脚本$ sed -i 's#sed#SED#g' sed.txt
python@PC:~/Desktop/脚本$ cat sed.txt 
nihao SED SED SED
nihao SED SED SED
nihao SED SED SED
```

#### 增加操作

```shell
# 增加实践
# 作用：
# 		在指定行号的下一行增加内容
# 格式：
# 		sed -i '行号a\增加的内容' 文件名
python@PC:~/Desktop/脚本$ sed -i '3a\add-1' sed.txt
python@PC:~/Desktop/脚本$ cat sed.txt 
nihao SED SED SED
add-1
nihao SED SED SED
add-1
nihao sed sed sed
# 如果增加多行，可以在行号位置写个范围值，彼此间使用逗号隔开，例如
# sed -i '1,3a\增加内容'文件名
python@PC:~/Desktop/脚本$ sed -i '1,4a\add-3' sed.txt
python@PC:~/Desktop/脚本$ cat sed.txt 
nihao SED SED SED
add-3
add-1
add-3
nihao SED SED SED
add-3
add-1
add-3
nihao sed sed sed
```

#### 删除实践

```shell
# 作用：
# 		指定行号删除
# 格式：
# 		sed -i '行号d' 文件名
# 注意：
# 如果删除多行，可以在行号位置多写几个行号，彼此间使用逗号隔开，例如
# sed -i '1,3d' 文件名
python@PC:~/Desktop/脚本$ sed -i '2,8d' sed.txt 
python@PC:~/Desktop/脚本$ cat sed.txt 
add-3
```

### awk命令详解

```shell
# 格式详解
# awk是一个功能非常强大的文档编辑工具，它不仅能以行为单位还能以列为单位处理文件。
# 命令格式
# 		awk [参数] '[ 动作]' [文件名]
# 常见参数：
# 	-F 指定列的分隔符
# 	-f 调用脚本
# 	-v 定义变量
# 常见动作：
# 		print 显示内容 		

=================================================
ython@PC:~/Desktop/脚本$ cat awk.txt 
nihao awk awk
nihao awk awk
nihao awk awk
python@PC:~/Desktop/脚本$ awk '{print $1}' awk.txt 
nihao
nihao
nihao
# $n 显示当前行的第n列内容，如果存在多个$n，它们之间使用逗号(,)隔开
python@PC:~/Desktop/脚本$ awk '{print $1,$2}' awk.txt 
nihao awk
nihao awk
nihao awk
# $0 显示当前行所有内容
python@PC:~/Desktop/脚本$ awk '{print $0}' awk.txt 
nihao awk awk
nihao awk awk
nihao awk awk
==================================================
# 动作组成
# BEGIN{ 命令 } 	初始代码块，主要和变量相关
# /pattern/{ 命令 }	 匹配、执行代码块
# END{ 命令 }	 结束代码块，主要和信息输出相关
# 内置变量
# FILENAME	 当前输入文件的文件名，该变量是只读的
# NR 	指定显示行的行号
===================================================
python@PC:~/Desktop/脚本$ awk '{print NR,$0}' awk.txt 
1 nihao awk awk
2 nihao awk awk
3 nihao awk awk
python@PC:~/Desktop/脚本$ awk -F ':' '{print NR,$2,$4}' awk.txt 
1 awk 
2 awk 
3 awk 
====================================================
# NF 	输出 最后一列的内容
# OFS 	输出格式的列分隔符，缺省是空格
====================================================
python@PC:~/Desktop/脚本$ awk -F ':' 'BEGIN{OFS="~"} {print NR,$2,$3}' awk.txt 
1~awk~awk
2~awk~awk
3~awk~awk
# FS 	输入文件的列分融符，缺省是连续的空格和Tab
```

### find命令详解

```shell
# 格式详解 
# 命令格式： 
# find [路径] [参数] [关键字] [动作] 参数详解 
# -name 按照文件名查找文件。 
# -user 按照文件属主来查找文件。 
# -group 按照文件所属的组来查找文件。 
# -type 查找某一类型的文件， 
# 诸如： 
# b - 块设备文件 d - 目录 c - 字符设备文件 
# p - 管道文件 l - 符号链接文件 f - 普通文件。
# 动作详解
# 动作就表示，我们对查找出来的文件做进一步的操作，主要都动作有三个
# -print 默认选项，显示名称，-o -print 表示不仅仅显示目录名，还显示目录里面的文件名
# -ls 显示文件属性
# -exec 命令 {} \; 使用命令对查找结果处理，查找结果使用"{}"来表示
# 简单实践
# 在当前系统中查找一个叫awk的文件
root@centos ~]# sudo find /home/admin-1/ -name "awk.txt"
/home/admin-1/awk.txt
# 在当前系统中查找文件类型为普通文件的文件
root@centos ~]# find /tmp -type f
/tmp/.X0-lock
/tmp/vgauthsvclog.txt.0
/tmp/unity_support_test.0
/tmp/config-err-4igbXW
# 根目录下查找5日以内更改的文件
find / -mtime -5
# 在/tmp/目录下查找3日以前更改的文件，可以用:
find /tmp/ -mtime +3
# 在目录下查找不包含backup子目录
find /data/scripts -path "/data/scripts/backup" -prune -o -print
# 忽略多个文件夹
find . \( -path "./backup" -o -path "./backup2" \) -prune -o -print
# 动作实践
# 以列表方式查看查找到的文件
find /etc -perm -640 -ls
# 对查找到的文件进行改名
find ./ -perm -002 -exec mv {} {}.old \;
# 查找到的文件删除
find . -name .svn | xargs rm -rf
# 查找磁盘中大于3M的文件
find . -size +3000k -exec ls -ld {} ;
```

## 第二阶段：流程控制

### 简单的流程控制语句

#### 单分支if语句和双分支if语句

```shell
if [ 条件 ]
then
	指令
fi
# 场景：
	# 单一条件，只有一个输出
	# 单分支if语句示例
#!/bin/bash
# 单 if 语句的使用场景
=============================
if [ "$1" == "nan" ]
then
	echo "您的性别是 男"
fi
=============================
# 双分支
# 语法格式
=============================
#!/bin/bash
# 单 if 语句的使用场景
if [ "$1" == "nan" ]
then
	echo "您的性别是 男"
elif [ "$1" == "nv" ]
	echo "您的性别是 女"
else 
	echo "您的性别是 人妖"
fi
==============================
# 启动 | 关闭 | 重启
python@PC:~/Desktop/脚本$ bash system.sh start
系统启动中...
python@PC:~/Desktop/脚本$ bash system.sh stop
系统关闭中...
python@PC:~/Desktop/脚本$ bash system.sh restart
系统重启中...
python@PC:~/Desktop/脚本$ bash system.sh aa
system.sh 脚本的使用方式是: system.sh [ start | stop | restart ]
```

#### case语句 

```shell
# 语句格式
# case 变量名 in
#	值 1)
#		指令 1
#			;;
#	... 
#	值 n)
#		指令 n
#			;;
# esac
# 注意：
# 首行关键字是case，末行关键字esac
# 选择项后面都有 )
# 每个选择的执行语句结尾都有两个分号;
# 语句示例
# 场景：在多if语句的基础上对脚本进行升级
# 需求：
# 要求脚本执行需要有参数，通过传入参数来实现不同的功能。
# 参数和功能详情如下：
# 参数 执行效果
# start 服务启动中...
# stop 服务关闭中...
# restart 服务重启中...
# * 脚本 X.sh 使用方式 X.sh [ start|stop|restart ]
python@PC:~/Desktop/脚本$ vim case.sh 
python@PC:~/Desktop/脚本$ cat case.sh 
#!/bin/bash
# case 语句使用场景
a="$1"
case "${a}" in 
  start)
    echo "服务器启动中.."
    ;;
  stop)
    echo "服务器停止中.."
    ;;
  restart)
    echo "服务器重启中.."
    ;;
   *)
    echo "$0 脚本使用方式: $0 [ start|stop|restart ]"
esac
python@PC:~/Desktop/脚本$ bash case.sh start 
服务器启动中..
python@PC:~/Desktop/脚本$ bash case.sh stop
服务器停止中..
python@PC:~/Desktop/脚本$ bash case.sh restart
服务器重启中..
python@PC:~/Desktop/脚本$ bash case.sh dasda
case.sh 脚本使用方式: case.sh [ start|stop|restart ]
```

#### for循环语句

```shell
# 语法格式
# for 值 in 列表
# do
# 	执行语句
# done
# 场景：
# 遍历列表
# 注意：
# ”for” 循环总是接收 “in” 语句之后的某种类型的字列表
# 执行次数和list列表中常数或字符串的个数相同，当循环的数量足够了，就自动退出
python@PC:~/Desktop/脚本$ vim for.sh 
python@PC:~/Desktop/脚本$ cat for.sh 
#!/bin/bash
# for循环语句

for i in $(ls /home/python/Desktop/脚本)
do
    echo "/脚本 目录下有的文件: ${i}"
done	
python@PC:~/Desktop/脚本$ bash for.sh 
/脚本 目录下有的文件: 1.txt
/脚本 目录下有的文件: awk.txt
/脚本 目录下有的文件: case.sh
/脚本 目录下有的文件: ceshi.sh
/脚本 目录下有的文件: danif.sh
/脚本 目录下有的文件: duoif.sh
/脚本 目录下有的文件: find.txt
/脚本 目录下有的文件: for.sh
/脚本 目录下有的文件: get_arg.sh
/脚本 目录下有的文件: get_aum.sh
/脚本 目录下有的文件: get_name.sh
/脚本 目录下有的文件: itcash_1.sh
/脚本 目录下有的文件: itcash.sh
/脚本 目录下有的文件: moren1.sh
/脚本 目录下有的文件: moren2.sh
/脚本 目录下有的文件: nihao.txt
/脚本 目录下有的文件: sed.txt
/脚本 目录下有的文件: system.sh
=================================================
# while语句
# 语法格式
# while 条件
# do
# 	执行语句
# done
# 注意：
# 条件的类型：
# 命令、[[ 字符串表达式 ]]、(( 数字表达式 ))
# 场景：
# 只要条件满足，就一直循环下去
python@PC:~/Desktop/脚本$ vim while.sh 
python@PC:~/Desktop/脚本$ bash while.sh 
1
2
3
4
python@PC:~/Desktop/脚本$ cat while.sh 
#!/bin/bash
# while 语法演示

a=1

while [ "${a}" -lt 5 ]
do 
   echo "${a}"
   a=$((a+1))
done

# until语句
# 语法格式
# until 条件
# do
# 	执行语句
# done
# 注意：
# 条件的类型：
# 		命令、[[ 字符串表达式 ]]、(( 数字表达式 ))
# 场景：
# 		只要条件不满足，就一直循环下去
# until语句示例
python@PC:~/Desktop/脚本$ cat until.sh 
#!/bin/bash
# until 语句
a=1
until [ "${a}" -eq 5 ]
do
    echo "${a}"
    a=$((a+1))
done
python@PC:~/Desktop/脚本$ bash until.sh 
1
2
3
4
```

### 函数

```shell
# 函数定义
# 函数就是将某些命令组合起来实现某一特殊功能的方式，是脚本编写中非常重要的一部分。
# 函数样式
# 简单函数格式： 
# 	定义函数：
# 		函数名(){ 
# 			函数体
# 		} 
# 调用函数：
# 		函数名
# 脚本传参 函数调用：
# 		脚本传参数
# 		/bin/bash 脚本名 参数
# 函数体调用参数：
# 	函数名(){
# 		函数体 $1
# 	}
# 	函数名 $1 
python@PC:~/Desktop/脚本$ cat fun.sh 
#!/bin/bash
# 简单函数定义

dayin(){
   echo "你好"
}

# 调用函数 直接输入函数名字就行
dayin
python@PC:~/Desktop/脚本$ bash fun.sh 
你好
===================================================
# 传参函数格式:
#  	定义格式：
#		函数名(){
# 			函数体 $n
# 		 }
#  调用函数：
# 		 函数名 参数
# 脚本传参 函数调用(生产用)
# 		 脚本传参数
#  			/bin/bash 脚本名 参数
#  函数体调用参数：
# 		本地变量名 = "$1"
#  			函数名(){
# 			函数体 $1
# 			 }
# 			函数名 "${本地变量名}"
# 注意：
# 类似于shell内置变量中的位置参数
# 函数实践
python@PC:~/Desktop/脚本$ cat fun1.sh 
#!/bin/bash
# 函数传参
fun1 (){
  echo "nihao $1"
}

# 调用参数
fun1 "$1"
# fun1 itcast1

python@PC:~/Desktop/脚本$ bash fun1.sh hah
nihao hah
```

