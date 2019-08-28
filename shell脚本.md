**1.第一个shell脚本**

```shell
#!/bin/bash
echo "hello world!"
```

#!是一个约定的标记，告诉系统这个脚本用什么解释器执行

echo命令用于向窗口输出文本

**2.运行脚本的方法**

chmod -x 文件名 把文件改成可执行文件

/bin/sh 文件名 直接通过解释器运行脚本

**3.shell变量**

定义变量时，变量名不加美元符号

命名规范和java差不多，不能使用bash里面的关键字

```shell
name="runoob.com"
#通过语句赋值
for file in `ls /etc`
for file in $(ls /etc)
#使用变量
echo $name
echo${name}
```

数组或者列表的形式

```shell
#!/bin/bash
for skill in Ada Coffe Action Java; do
    echo "I am good at ${skill}Script"
done
```

只读变量

```shell
#!/bin/bash
name="zfc"
readonly name
#删除变量
unset name
```

变量类型

局部变量，脚本或命令中定义，只在当前shell实例中有效

环境变量：所有程序，包括shell启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行，必要的时候shell脚本也可以定义环境变量

shell变量：shell变量是由shell程序设置的特殊变量，shell变量中有一部分是环境变量， 有一部分是局部变量，保证shell的正常运行

**4.shell字符串**

字符串可以用单引号，双引号，也可以不用引号

单引号：

- 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的
- 单引号字符串中不能出现单独一个单引号，可成对出现，用于字符串的拼接

双引号：

- 双引号中可以有变量
- 双引号中可以出现转义字符

获取字符串的长度：

```shell
string='sssssss'
echo ${#string}#输出7
```

提取子字符串

```shell
string='ssaassbb'
echo ${string:1:4}#输出saas
```

查找子字符串

这里的`是反引号，不是单引号

```shell
string='abcd'
echo `expr index $string b`#输出1
```

**5.shell数组**

定义数组

数组名=(值1 值2 ...值n)

读取数组

$(数组名[下标])

使用@符号取出所有元素

echo $(array_name[@])

获取数组的长度

```shell
# 取得数组元素的个数
length=${#array_name[@]}
# 或者
length=${#array_name[*]}
# 取得数组单个元素的长度
lengthn=${#array_name[n]}
```

**6.shell注释**

以#开头的行就是注释行

多行注释:

EOF可以换成其他符号，首位对应

```shell
:<<EOF
注释内容...
注释内容...
注释内容...
EOF
```

**7.shell传递参数**

![1566886100165](C:\Users\konata\AppData\Roaming\Typora\typora-user-images\1566886100165.png)

```shell
#!/bin/bash
# author:菜鸟教程
# url:www.runoob.com

echo "Shell 传递参数实例！";
echo "执行的文件名：$0";
echo "第一个参数为：$1";
echo "第二个参数为：$2";
echo "第三个参数为：$3";
```

$0会接收文件名作为参数

$*和$@的区别

- 相同点：都是引用所有参数
- 不同点： 只有在双引号中体现出来，假设有三个参数，1,2,3， 则*相当于“123”一个参数，@等价于"1","2","3"三个参数

**8.shell运算符**

- 表达式和运算符之间要有**空格**，例如 2+2 是不对的，必须写成 2 + 2，这与我们熟悉的大多数编程语言不一样。
- 完整的表达式要被 `` 包含，注意这个字符不是常用的单引号，在 Esc 键下边。

```shell
#!/bin/bash
# author:菜鸟教程
# url:www.runoob.com

a=10
b=20

val=`expr $a + $b`
echo "a + b : $val"

val=`expr $a - $b`
echo "a - b : $val"

val=`expr $a \* $b`
echo "a * b : $val"

val=`expr $b / $a`
echo "b / a : $val"

val=`expr $b % $a`
echo "b % a : $val"

if [ $a == $b ]
then
   echo "a 等于 b"
fi
if [ $a != $b ]
then
   echo "a 不等于 b"
fi
```

![1566892730373](C:\Users\konata\AppData\Roaming\Typora\typora-user-images\1566892730373.png)

![1566892740971](C:\Users\konata\AppData\Roaming\Typora\typora-user-images\1566892740971.png)![1566892748665](C:\Users\konata\AppData\Roaming\Typora\typora-user-images\1566892748665.png)

![1566892758326](C:\Users\konata\AppData\Roaming\Typora\typora-user-images\1566892758326.png)

![1566892766358](C:\Users\konata\AppData\Roaming\Typora\typora-user-images\1566892766358.png)

- **-S**: 判断某文件是否 socket。
- **-L**: 检测文件是否存在并且是一个符号链接。