为何无论当前工作目录在哪里，都能执行/usr/bin/cd这个程序呢？
因为环境变量的作用。

环境变量是操作系统（Windows、Mac、Linux）在运行的时候，记录的一些关键信息，用以辅助系统运行。

在Linux系统中执行env命令即可查看当前系统中记录的环境变量

环境变量是一种keyValue型结构

为什么无论当前目录是什么，都能执行/usr/bin/cd这个程序，是因为借助了环境变量中的PATH这个项目的值来做到的。

![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/3160f98a-6304-4d02-baa9-ba0fffb92a66)

在Linux系统中，$符号被用于取“变量”的值
环境变量记录的信息，除了给操作系统自己使用外，如果我们要取用，也可以使用
取得环境变量的值可以通过语法：$环境变量名 
比如：echo $PATH
又或者：echo ${PATH}ABC，当和其他内容混合在一起的时候，可以通过{}来标注取的变量是谁

Linux系统环境变量可以用户自行设置，其中分为：
临时设置，语法：export 变量名 = 变量值
永久生效：
1、针对当前用户生效，配置在当前用户中的：~/.bashrc文件中
2、针对所有用户生效，配置在系统中的：/etc/profile文件中
以后都要通过语法：source 配置文件，进行立刻生效，或者重新登录FinalSHell生效
 如：
vim ~/.bashrc
source ~/.bashrc
echo $MYNAME

