在 WPF (Windows Presentation Foundation) 中，控件属性是定义用户界面元素的各个方面的属性，例如其外观、行为或内容。属性允许您自定义和配置应用程序中控件的行为和外观。

样式是一种定义一组可应用于控件的多个实例的属性值的机制。

它允许您为整个应用程序中的控件定义一致的外观和行为。

**简而言之：控件属性用来定义控件的外观、行为或内容，而样式用来批量定义同一种控件的外观、行为或内容。**

控件都有各种属性，如button，通过改变button的属性值来改变其外观、行为或内容。
下面这段代码定义了6个按钮：
```
<Grid>
    <StackPanel>
        <Button Background="LightBlue"     Content="按钮1" Height="40" Width="100" Foreground="White" FontSize="20" FontWeight="Bold"/>
        <Button Background="DarkRed"       Content="按钮2" Height="40" Width="100" Foreground="White" FontSize="20" FontWeight="Bold"/>
        <Button Background="DarkGoldenrod" Content="按钮3" Height="40" Width="100" Foreground="White" FontSize="20" FontWeight="Bold"/>
        <Button Background="Black"         Content="按钮4" Height="40" Width="100" Foreground="White" FontSize="20" FontWeight="Bold"/>
        <Button Background="DarkSlateGray" Content="按钮5" Height="40" Width="100" Foreground="White" FontSize="20" FontWeight="Bold"/>
        <Button Background="Thistle"       Content="按钮6" Height="40" Width="100" Foreground="White" FontSize="20" FontWeight="Bold"/>
    </StackPanel>
</Grid>
```
界面UI如下图：
<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/6529b0c5-d072-4094-9c8d-b4fffc738c89" alt="style" width="400">


可以看见除了Background和Content属性不同外，其余的Height、Width、Foreground、FontSize、FontWeight的值是相同的，这样会造成代码冗余，并且当其他项目想使用这种风格的控件时不好复用。

所有产生了style，用来定义一组控件的外观、行为或内容。

style常见的有两种定义方式：
**1、直接在Window标签的Window.Resources标签内使用style标签定义**
<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/acdb5a88-4969-48c4-8823-2b0168ac6a90" alt="style1" width="400">

还可以个style命名，这时候如果具体控件没有指定style的名字，那么style将不生效，如下图所示：
<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/0edce4aa-8cfc-4959-b8a8-c3a51f9b6e9b" alt="style2" width="400">

当指定style的名字时：

<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/116c71ef-b658-40ec-b449-aca32563235e" alt="style3" width="400">




**2、使用资源字典来配置sytle，并且配置到xaml的全局文件app.xaml中**
这是没有使用资源字典配置style的情况
<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/116c71ef-b658-40ec-b449-aca32563235e" alt="style3" width="400">

如何使用资源字典并配置到xmal的全局文件app.xaml中？
(1)、在项目右击添加一个文件夹DicRes，然后右击DicRes文件夹添加新建项，选择资源字典（ResourceDictionary）
<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/ab3c2d86-d435-4e42-a0bd-9842cc36c030" alt="添加资源字典" width="200">

<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/28e8f5fb-a8e1-4605-9cb9-298d40a80dbc" alt="资源字典代码" width="400">


(2)、把style标签的所有代码style标签剪切到btnDicRes.xaml中

<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/19b1ab75-6af3-408e-90a4-dd9928c7741b" alt="复制到btnDicRes" width="400">
把style复制后的btnDicRes.xmal的代码
<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/5eea7a0d-8787-4cfe-92b9-c4b90f3e7fbd" alt="复制后的资源字典" width="400">


(3)、在app.xaml中配置资源字典
<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/1e1557ad-9e9b-4360-b02f-7537f1d93c8b" alt="配置app xaml" width="400">

(4)、删除MainWindow的style代码，也能直接使用myBtn

<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/26ca6919-7849-40e1-aa94-da545ea3234b" alt="stylelast" width="400">

效果完全一样。






