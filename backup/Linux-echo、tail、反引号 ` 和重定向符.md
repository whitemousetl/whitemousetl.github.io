echo命令可以在命令行输出指定内容
语法：**echo 输出内容**
无需选项，只有一个参数，表示要输出的内容，内容用""包围起来

![echo](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/3c1cb60e-6f1d-4fa4-8fcf-93f79e5cd9a8)

**反引号（飘号）`**
被 ` 包围的内容，会被作为命令执行，而非普通字符

**重定向符 > 和 >>**
> ，将左侧命令的输出结果，覆盖写入到符号右侧指定的文件中
>> ，将左侧命令的输出结果，追加写入到符号右侧指定的文件中
![追加覆盖](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/54724248-e25e-49cf-893a-9767d25c27e4)

tail命令，可以查看文件尾部内容，跟踪文件的最新更改
**语法：tail [-f -num] Linux路径**
参数 Linux路径，表示被跟踪的文件路径
选项[-f] 表示持续跟踪
选项[-num] 表示查看尾部多少行，不填默认10行
[-f] 持续追踪表示当尾部更新时，命令行会实时跟新
![tail](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/5a0a41b7-b4cc-4cae-afd7-8db739ab6d28)
