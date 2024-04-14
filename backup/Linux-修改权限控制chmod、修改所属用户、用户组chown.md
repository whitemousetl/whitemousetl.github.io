可以使用chmod命令，修改文件、文件夹的权限信息
注意：只有文件、文件夹的所属用户或root用户可以修改
语法：**chmod [-R] 权限 文件或文件夹**
选项 [-R] ，对文件夹内的全部内容应用同样的操作
chmod u=rwx,g=rx,o=x hello.txt 
chmod -R u=rwx，g=rx，o=x test

u=rwx,g=rx,o=x 这部分可以用751代替
也就是chmod 751 hello.txt
---是0，rwx是7，其他可推导出来