能够被systemctl管理的软件一般成为服务
语法：**systemctl start | stop | enable | disable | status服务名**
启动、停止、开机自启，开机不自启、查看服务状态
需要root权限
系统内置的服务比较多，比如：
NetworkManager，主网络服务
network，副网络服务
firewalld，防火墙服务
sshd，ssh服务（FinalShell远程登录Linux就是使用这个服务）

apache服务软件是：httpd

部分软件安装后没有自动集成到systemctl中，我们可以手动添加