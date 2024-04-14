可以使用chmod命令，修改文件、文件夹的权限信息
注意：只有文件、文件夹的所属用户或root用户可以修改
语法：**chmod [-R] 权限 文件或文件夹**
选项 [-R] ，对文件夹内的全部内容应用同样的操作
chmod u=rwx,g=rx,o=x hello.txt 
chmod -R u=rwx，g=rx，o=x test

u=rwx,g=rx,o=x 这部分可以用751代替
也就是chmod 751 hello.txt
---是0，rwx是7，其他可推导出来

使用chown命令，可以修改文件、文件夹的所属用户和用户组，此命令只能root用户使用
语法：**chown [-R] [用户] [ : ] [用户组] 文件或文件夹**
选项[-R] ,同chmod，对文件夹内全部内容应用相同规则
选项用户 ，修改所属用户
选项用户组，修改所属用户组
选项[ : ]用于分隔用户和用户组
chown root hello.txt 将hello.txt所属用户修改为root
chown ：root hello.txt 将hello.txt 用户组修改为root
chown root：whitemousetl 将hello.txt用户改为root，用户组改为whitemousetl
chown -R root test