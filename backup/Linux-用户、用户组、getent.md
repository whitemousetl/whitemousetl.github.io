Linux可以配置多个用户、配置多个用户组、用户可以加入多个用户组中

Linux系统中关于权限管控级别有2个级别，分别是：
针对用户的权限控制
针对用户组的权限控制

以下命令需要root用户执行
**创建用户组 groupadd 用户组名**
**删除用户组 groupdel 用户组名**

以下命令需要root用户执行
添加用户
**创建用户 useradd [-g -d] 用户名**
选项[-g] 指定用户的组，不指定[-g] ，会创建同名组并自动加入，指定[-g]需要组已经存在，如已经存在同名组，必须使用[-g]
选项[-d] [-d]指定用户Home路径，不指定，Home目录默认在/home/用户名

以下命令需要root用户执行
删除用户
**userdel [-r] 用户名**
选项 [-r] 删除用户的Home目录，删除用户时不使用[-r]，Home目录保留

以下命令需要root用户执行
查看用户组
**id [用户名]**
参数用户名，被查看的用户，不提供则查看自身

以下命令需要root用户执行
修改用户所属组
**usermod -aG 用户组 用户名，指定用户加入指定用户组**

使用getent passwd命令可以查看当前系统中有哪些用户
**语法：getent passwd**passwd是Linux密码
共有7份信息：
用户名：whitemousetl:
密码（x）：x:
用户ID：1000:
组ID：1000:
描述信息（无用）：whitemousetl:
Home目录：/home/whitemousetl:
执行终端（默认bash）/bin/bash

使用getent group命令可以查看当前系统中有哪些用户组
**语法：getent group**
有3份信息：
组名称：test4:
组认证（显示为x）：x:
组ID 1003:


