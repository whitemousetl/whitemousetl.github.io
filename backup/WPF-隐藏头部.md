WPF可以把默认自带的头部给隐藏掉，不隐藏的时候是这样的
<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/de4eafac-62a7-45b2-8cf3-6a791c7fb329" alt="wpf自带头部" width="200">

隐藏使用代码：
```
<WindowChrome.WindowChrome>
    <WindowChrome GlassFrameThickness="0"/>
</WindowChrome.WindowChrome>
```
<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/b6ca1027-06bf-49db-9c24-e0a016b2c57a" alt="隐藏头部的代码" width="400" >

隐藏后的效果：

<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/6f29af14-37cc-49bb-877f-488501c7fdf3" alt="wpf隐藏头部后" width="400">

为什么要隐藏头部？
因为wpf自带的头部样式不好看，需要改动的时候不如直接把这个头部隐藏掉，就可以像写UI一样直接自定义头部。



