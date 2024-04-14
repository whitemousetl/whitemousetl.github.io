每一台联网的电脑都有一个地址，用于和其他计算机进行通讯
IP地址主要有两个版本IPv4和IPv6
IPv4的地址格式是：a.b.c.d，其中abcd表示0~255的数字，如192.168.88.101就是一个标准的IPv4地址
Linux系统可以通过命令ifconfig查看本机IP地址，如无法使用ifconfig命令，
可以安装yum -y install net-tools

127.0.0.1,用于指代本机
0.0.0.0，有三种用法，分别是：
可以用于指代本机
可以在端口绑定中用来确定绑定关系(后续讲解)
在一些IP地址限制中,表示所有IP的意思,如放行规则设置为0.0.0.0,表示允许任意IP访问

每一台电脑除了对外联络的地址（IP地址）以外，也可以有也给名字，称之为主机名
无论是Windows还是Linux系统都可设置

查看Linux系统主机名的命令：hostname
修改主机名：hostnamectl set-hostname 主机名 ，修改后的主机名（需root）

域名解析：IP地址不好记住，然后做一个映射（域名解析）把IP地址与网站名做对应，然后记住网站名就可以访问该网站了

![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/88be0dfe-3322-41b5-96a7-ed61fc54b043)

先查看本机的记录(私人地址本)
Windows看:C:\Windows\System32\drivers\etc\hosts
Linux看:/etc/hosts
再联网去DNS服务器（如114.114.114.114，8.8.8.8等）询问
可以再windows系统中的私人地址本配置Linux的域名解析（地址映射），从而使得FinalShell链接Linux系统时不需要IP地址，使用主机名即可