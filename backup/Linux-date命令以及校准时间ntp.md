通过date命令可以在命令行中查看系统的时间
语法：**date [-d] [+格式化字符串]**
[-d] 按照给定的字符串显示日期，一般用于日期计算
格式化字符串：通过特定的字符串标记，来控制显示时间的格式
date默认不带参数是输出当前时间
[-d] 选项，可以按照给定的字符串显示日期，一般用于日期计算
date -d "+1 day"  +"%Y-%m-%d"

`%Y 年
%y 年份后两位数组（00~99）
%m月份（01~12）
%d日（01~31）
%H小时（00~23）
%M分钟（00~59）
%S秒（00~60）`
%s自1970-01-01 00：00：00 UTC到现在的秒数

Lunux系统默认时区并非东8区

UTC 代表协调世界时。它是世界调节时钟和时间的主要时间标准。它是全球民用时间和时区的基础。UTC 不随季节变化，全球统一。

PDT 代表太平洋夏令时。这是美国西部的一个时区，特别是在加利福尼亚州、俄勒冈州和华盛顿州等州，在一年中的夏令时期间。比协调世界时 (UTC-7) 晚 7 小时。

使用root权限，执行如下命令，修改时区为东八区时区
rm -f /etc/localtime
ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

通过ntp程序可自动校准时间,需要root权限
安装ntp ：yum -y install ntp
启动并设置开机自启 systemctl start ntpd
                                    systemctl enable ntpd
手动校准：ntpdate -u ntp.aliyun.com