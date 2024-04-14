可以通过top命令查看CPU、内存的运行情况，类似windows系统的任务管理器
默认每5秒运行一次，语法：直接输入top即可，按q或者ctrl + c 退出

![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/005339ad-481d-43d6-ac1c-19342f7e24e6)
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/42d5f283-a8b9-4fe8-8e85-1bba6dfbdfd1)
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/cbcff1c3-5efe-40d6-b1b8-3c7a89212502)
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/6e53666f-82ec-41fd-a5f4-574dcd232bc4)

**使用df命令，可以查看磁盘的使用情况**
语法：df [-h]
选项[-h],以更加人性化的单位显示

可以使用iostat查看CPU、磁盘的相关信息
语法：**iostat [-x] [num1] [num2]**
选项[-x],显示更多信息
num1数字，刷新间隔，num2数字，刷新几次
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/1c5999e1-3294-4b94-858c-d9dca4e369d2)

可以使用sar命令查看网络的相关统计（sar命令非常复杂，这里仅用于统计网络）
语法：**sar -n DEV num1 num2**
选项 -n ，查看网络
DEV表示查看网络接口
num1，刷新间隔
num2，刷新次数
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/e60d4e66-799f-4a51-bc3f-c1db9aa96b79)
