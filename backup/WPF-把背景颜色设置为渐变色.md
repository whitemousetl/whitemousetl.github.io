把背景色设置为渐变色的效果有两种。
先来介绍第一中：由左上角到右下角，效果如下图：

<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/b96cc027-2647-4dd4-97c1-0f8a936f40a8" alt="渐变色效果2" width="400">


代码如下：
```
 <Grid>
     <Grid.Background>
         <!--背景渐变颜色 画刷-->
         <!--LinearGradientBrush 由左上角到右下角-->
         <LinearGradientBrush>
             <GradientStop Color="Blue" Offset="0"/>
             <GradientStop Color="Crimson"  Offset="0.5"/>
             <GradientStop Color="SkyBlue" Offset="1"/>
         </LinearGradientBrush>
     </Grid.Background>
 </Grid>
```

接着介绍第二中，由里（中心）向外，效果如下图
<img src="https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/00b69315-f3d3-408a-a1b5-ff4dcce0a262" alt="渐变色效果1" width="400">


代码如下：
```
<Grid>
    <Grid.Background>
        <!--背景渐变颜色 画刷-->
        <!--RadialGradientBrush 由里向外-->
        <RadialGradientBrush>
            <GradientStop Color="Blue" Offset="0"/>
            <GradientStop Color="Crimson"  Offset="0.5"/>
            <GradientStop Color="SkyBlue" Offset="1"/>
        </RadialGradientBrush>
    </Grid.Background>
</Grid>
```
Grid网格标签内写入Grid.Background标签，Grid.Background有两种画刷，一种是由左上角到右下角的LinearGradientBrush标签，另一种是由里（中心）到外的RadialGradientBrush标签，然后两种画刷都有GradientStop 标签可以设置颜色值Color和渐变点Offset，颜色不说，渐变点从0开始，该颜色到第二个渐变点结束，然后下一个颜色也是如此。

如何使用？
1、写Grid标签
```
<Grid>

</Grid>
```
2、在Grid标签内写Grid.Background标签
```
<Grid>
    <Grid.Background>
        
    </Grid.Background>
</Grid>
```
3、确定渐变方式：由里（中心）向外使用RadialGradientBrush标签，由左上角到由右下角用LinearGradientBrush标签
由里向外：
```
<Grid>
    <Grid.Background>
        <RadialGradientBrush>
            
        </RadialGradientBrush>
    </Grid.Background>
</Grid>
```
由左上角到右下角：
```
<Grid>
    <Grid.Background>
        <LinearGradientBrush>
            
        </LinearGradientBrush>
    </Grid.Background>
</Grid>
```
4、确定渐变颜色， 和渐变点，这些参数自己调一调就会知道怎么用了，这里以左上角到右下角的渐变为例子
```
<Grid>
    <Grid.Background>
        <!--背景渐变颜色 画刷-->
        <!--LinearGradientBrush 由左上角到右下角-->
        <LinearGradientBrush>
            <GradientStop Color="Blue" Offset="0"/>
            <GradientStop Color="Crimson"  Offset="0.5"/>
            <GradientStop Color="SkyBlue" Offset="1"/>
        </LinearGradientBrush>
    </Grid.Background>
</Grid>
```