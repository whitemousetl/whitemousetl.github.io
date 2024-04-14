**which 要查找的命令**

- **whicht 命令本身必填**
- **要查找的命令 参数 必填**

![which](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/0505bdb4-d834-48db-b88a-941ad20f817e)

**find命令用来搜索指定文件**
1、**按文件吗搜索**
语法：**find 起始路径 -name "被检查的文件名"**
可以使用通配符 * ，使用通配符时会把文件和文件夹都搜索出来

![find](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/7b9bfbdf-b0df-4e49-825a-b504098937d9)

**按照文件大小搜索**
语法：**find 起始路径 -size + | -n [kMG]**
+、- 表示大于和小于
kMG表示大小单位，k（小写字母）表示kb，M表示Mb，G表示Gb
如：find / -size -10k
        find / -size +100M
        find / -size +1G

![find1](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/88985daf-4a5b-4420-8461-61981efcf4a0)


