cp命令可以用来复制文件/文件夹，来自copy

**cp [-r] 文件/文件夹 文件夹**

- cp **命令本身，必填**，表示复制
- [-r] **可选项，非必填**，用于复制目录及其所有的子目录和文件，如果要复制目录，需要使用该选项。
- 文件/文件夹 **参数，必填**
- 文件夹 **参数，必填**

![cp1](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/7cf5323e-b009-491e-9a14-ef48181f3889)

![cp2](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/7851e11f-894f-4a01-b5e9-fd90997c5935)

mv表示移动文件/文件夹,来自move

**mv 文件/文件夹 文件夹**

**mv **命令本身，必填**，表示移动
文件/文件夹 **参数1，必填**，Linux路径，表示要移动的文件或文件夹
文件夹 **参数2，必填**，Linux路径，表示接收的Linux路径，如果路径不存在，则添加新目录，确保路径存在**

![mv](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/838a0908-f53b-4b3e-9c05-94838537cf4b)

rm表示删除文件/文件夹，来自remove

**rm [-r -f] 文件1/文件夹1 文件2/文件夹3 ... 文件n/文件夹n**
**rm 命令本身，必填**，表示删除
[-r] 表示删除文件夹,[-f]表示force，强制删除（不会弹出提示确认信息）普通用户删除内容不会弹出提示，只有root用户删除时有提示，一般用户不会使用到[-f] ,可选项，非必填
**文件1/文件夹1 文件2/文件夹3 ... 文件n/文件夹n 参数，必填**，表示要删除的文件或文件夹的路径，以空格隔开

rm命令支持通配符 * ，用来做模糊匹配
符号 * 表示通配符，即匹配任意内容（包括空），示例：
`*test` 表示以test结尾的内容
`test*`表示以test开头的内容
`*test*`表示含有test的内同

rm是一个危险的命令，特别是在处于root（超级管理员）用户的时候。请谨慎使用。
如下命令，千万不要在root管理员用户下执行：
rm -rf /
rm -rf /*

![rm](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/5697e07c-db0d-47f3-8a4e-ebeda29d9415)
