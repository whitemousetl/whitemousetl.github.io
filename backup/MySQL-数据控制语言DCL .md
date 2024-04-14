**DCL （Data Control Language）
数据控制语言：用来创建数据库用户、控制数据库的访问权限**

1、DCL-管理用户
- 查询用户
```
use mysql；
select * from user；
```
- 创建用户
`create user '用户名'@'主机名' identified by '密码';`
- 修改用户密码
`alter user '用户名'@'主机名' identified with mysql_native_password by '新密码';`
- 删除用户
`drop user '用户名'@'主机名';`
注意：
主机名可以与通配符%使用。
这类SQL开发人员用得少，主要是DBA数据库管理员使用。

2、DCL-权限控制
MySQL有很多种权限，但常用的有：
```
ALL，ALL PRIVILEGES 所有权限
SELECT 查询数据
INSERT 插入数据
UPDATE 修改数据
DELETE 删除数据
ALTER 修改表
DROP 删除数据库/表/视图
CREATE 创建数据库/表
```
- 查询权限
`show grants for '用户名'@'主机名';`
- 授予权限
`grant 权限列表 on 数据库名.表名 to '用户名'@'主机名';`
- 撤销权限
`revoke 权限列表 on 数据库名.表名 from '用户名'@'主机名'；`