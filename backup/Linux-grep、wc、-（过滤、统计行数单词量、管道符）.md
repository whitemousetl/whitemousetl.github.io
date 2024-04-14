通过grep命令，从文件中根据关键字过滤文件行

**语法：grep [-n] 关键字 文件路径**

[-n] 可选，表示在选项中显示匹配的行的行号
**参数关键字 必填**，表示过滤的关键字，带有空格或其他特殊符号的关键字，建议用""将其包围起来
**参数文件路径 必填**，表示要过滤内容的文件路径，可作为内容输出端口

![grep](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/4fab4f06-078c-4772-8fe2-1ee2d29e8fca)

通过wc命令统计文件的行数、单词量等
**语法：wc [-c -m -l -w] 文件路径**
选项 [-c] ，统计byte的数量
选项[-m] ，统计字符数量
选项[-l] ，统计行数
选项[-w] ，统计单词量
参数文件路径，被统计的文件，可作为内容输入端口

![wc](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/93194f23-2a90-4f8e-9583-0e8e97e74e16)

管道符 | 将管道符左边命令输出的结果，作为右边命令的输入，是对输出结果的过滤
如：cat test.txt | grep "哈"
管道符可以嵌套使用，只要有输出结果，就可使用管道符
![管道符](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/f3217e9c-a909-4a1b-9afb-2f4891306aa6)

