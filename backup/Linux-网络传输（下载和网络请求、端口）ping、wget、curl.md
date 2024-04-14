通过ping命令，检查指定的网络服务器是否可以联通状态
语法：**ping [-c num] ip或主机名**
选项[-c num] 检查次数，不使用[-c num] 选项，将无限次数持续检查
参数ip或主机名，被检查的服务器的ip地址或主机名地址
如：ping -c 3 baidu.com

wget是非交互式的文件下载器，可以在命令行内下载网络文件
语法：**wget [-b] url**
选项[-b] ，后台下载，会将日志写入到当前工作目录的wget-log文件中
参数url，下载链接

curl可以发送http请求，可用于：下载文件、获取信息等
语法：**curl [-O] url**
选项[-O] ，用于下载文件，当url是下载链接时，可以使用此选项保存文件
参数url，要发起请求的网络地址
curl cip.cc 获取主机的公网ip地址
curl whitemousetl.github.io 获取该网页的HTML代码

端口是设备与外界通讯交流的出入口。端口可以分为：物理端口和虚拟端口两类。
物理端口，可以称之为接口，是可见的端口，如USB接口，RJ45网口，HDMI端口等。
虚拟端口，是指计算机内部的端口，是不可见的，用于操作系统与外部进行交互使用。
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/3d0621cb-34c1-4cdd-9281-ec7041498054)
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/571d2219-545c-4e88-93d2-acc8e6532540)
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/cde9fb66-64d5-4856-bbdf-831e51813f21)
计算机程序之间的通讯，通过IP只能锁定计算机，但是无法锁定具体的程序
通过端口可以锁定计算机上具体的程序，确保程序之间进行沟通
IP地址相当于小区，端口可以看作是门牌号

Linux系统是一个超大号小区，可以支持65535个端口，这6万多个端口分为3类进行使用
公认端口`1~1023`，通常用于系统内置或知名程序的预留使用，如SSH服务的22端口，HTTPS服务的443端口，非特殊需要，不要占用这个范围的的端口
注册端口`1024~49151`，通常可以随意使用，用于松散地绑定一些程序/服务
动态端口`49152~65535`，通常不会固定绑定程序，而是当程序对外进行网络连接时，用于临时使用。

可以通过nmap命令查看有哪些端口被占用了，如果没有nmap命令，通过yum -y install namp来下载
语法：nmap 被查看的IP地址

可以通过netstat命令，查看指定端口的占用情况
语法：netstat -anp | grep 端口号，安装netstat：yum -y install net-tools