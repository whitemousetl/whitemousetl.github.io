## **Linux目录结构**
Windows系统的目录结构可以有多个**盘符**，如C盘、D盘、E盘等。
Linux的目录结构是树形结构，没有盘符这个概念，只有一个**根目录**，所有文件都在它下面。

路径的层级关系，Linux用左斜杠 / 表示，而Windows使用右斜杠 \表示，**Linux在左，Windows在右**。
Windows的一个盘：
![Windows盘符目录](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/311a8470-2010-4558-910c-579bbe0d63c9)

**Linux的目录结构**：
![Linux树状结构](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/6f438302-cbb5-4f46-8489-8d92ba80c61d)

## Linux命令格式
格式：**command [options] [parameter]**
command **命令本身，必填**，如ls，展示文件夹目录
[options] **可选项，非必填**，可以通过选项来控制命令的细节
[parameter] **参数，非必填**，命令的参数，多数用于指向命令的目标
以展示文件夹目录命令ls为例，因为命令本身必填，所以有三种情况，命令、命令 + 可选项、命令 + 参数、命令+可选项+参数

**命令本身**，ls
![ls](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/671513ac-f8e1-4184-b63a-111937e9d576)

**命令 + 可选项**

- -a 表示All，即列出所有的文件（包含所有的文件/文件夹），以 **.** 开头的就是Linux系统中隐藏的文件/文件夹
- -l 表示以列表（竖向排列）的形式展示内容，并展示更多信息
- -h 表示易于阅读的形式，列出文件大小，如K、M、G，-h 必须搭配 -l 一起使用

语法中可选项可以组合使用，如下面四种写法的功能完全一样

- ls -a -l
- ls -l -a
- ls -al
- ls -la

![ls-a](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/de0fff88-341f-4e1f-8670-87a77cc6e6d3)

**命令 + 参数**，可以指定目标
![ls-para](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/4e70b5c0-9bfa-4565-9f33-ed9e2ef30e2a)

**命令+可选项+参数**，既指定目标，也指定细节
![ls-a-para](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/cb066d91-564c-48e5-b1d0-0199f1989f52)

