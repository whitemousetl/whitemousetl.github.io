除了通过FinalShell的图形化进行上传下载外，还可以通过rz、sz命令进行文件传输
rz、sa命令需要安装：yum -y install lrzsz


rz命令，上传，语法直接输入rz（rz命令上传很慢，一般用拖拽的方式上传）

sz命令，下载，语法：sz 要下载的文件

压缩、解压（tar、zip、unzip）

.tar，称为tarball，归档文件，即简单地将文件组装到一个.tar文件中内，并没有太多文件体积的减少，仅仅是简单的封装

.gz，也常见为tar.gz，gzip格式压缩文件，即使用gzip压缩算法将文件压缩到一个文件内，可以极大地减少压缩后的体积

语法：tar [-c -v -x -f -z -C] 参数1 参数2 ... 参数N
-c，创建压缩文件，用于压缩模式
-v，显示压缩、解压过程，用于查看进度
-x，解压模式
-f，要创建的文件，或要解压的文件，-f选项必须在所有选项位置中处于最后一个
-z，gzip模式，不适用-z就是普通的tarball模式
-C，选择解压的目的地，用于解压模式

tra两种格式均可使用
-z使用一般在第一位，-f使用必须在最后一位

tar压缩常用的组合有：

tar -cvf test.tar 1.txt 2.txt 3.txt
将1.txt、2.txt、3.txt压缩到test.tar文件内

tar -zcvf test.tar.gz 1.txt 2.txt 3.txt 
将1.txt、2.txt、3.txt压缩到test.tar.gz文件内，使用gzip模式

tar解压常用的组合有：

tar -xvf test.tar
解压test.tar文件，解压后的文件放到当前目录

tar -xvf test.tar -C /home/whitemousetl
解压test.tar，解压后的文件放到指定目录（/home/whitemousetl）

tar -zxvf test.tar.gz -C /home/whitemousetl
以gzip模式解压test.tar.gz，解压后的文件放在指定目录（/home/whitemousetl）