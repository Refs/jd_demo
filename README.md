# jd_demo

> 复习笔记最正确的姿势，即为将笔记的内容，重新再整理一遍；将全部的内容整合一遍，即自己走了一轮；这句话可以作为自己后期学习的指导； 后期可参照**git_book**的排版整合，将evernote整合成git_book的效果；

> 写代码就是抄，天下代码一大抄，看你会抄不会抄，这也是一种领悟，所以要放下，看着老师的代码，写自己代码的心理障碍,抄也是一种复习，抄的过程中，遇到自己不能理解的点，自己就会自动的去翻看笔记，去解惑；在解惑的同时，将笔记上的知识点捋顺了，然后笔记也复习了；

> 直接去整理笔记，效果应该不如直接抄代码，效果来得快；

## 预备知识__html的viewport属性详解

### viewport的概念

* 移动设备上,用来显示网页的区域，`该属性只在移动端浏览器上有意义，pc端怎么设置都是没有用的`
    - 如果把移动设备的浏览器(也有可能是app中的webview) ,当做相框的话
    - viewport就相当于相框中的画,可能会比相框小,可能会比相框大,如果刚好一样大,那就皆大欢喜.

### 修改viewport的值

 我们可以通过meta标签去修改viewport的值，防止滚动条的出现，提升用户的体验；

* 移动web常用的设置

```html
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
    
```

>  emmet语法 已经帮我们封装了viewport的快捷写法:meta:vp

> name='viewport' 用来告诉浏览器：meta标签配置的是viewport对象，配置的方式是content='key=value,key=value'的形式；属性与值呈键值对，键值对利用`，`分隔开来；

> width:视口宽度，不需要给单位；如果设备的屏幕大小，与预设的视口大小一致，既可以保证页面的正常显示；一般取值：width=device-width;

> initial-scale:视口默认的缩放比例 一般默认设置的是1.0

> user-scalable:设置是否支持缩放(默认情况下，用户两根手指同时按压屏幕即可缩放)；一般设置设置的是no禁用缩放，允许设为rtue;

> maximum-scale/minimum-scale:允许最大缩放值，与最小缩放值；

### 移动端的最小宽度和最大的宽度

> 考虑到移动设备在大尺寸的的屏幕不会过度缩放 失去清晰度,在小尺寸的屏幕中不会出现布局错乱的问题

* demo(常用设置)

```css
max-width: 640px;  
/*在行业当中的移动端的设计图一般使用的是640px*/
min-width: 300px;  
/*在移动设备当中现在最小的尺寸320px*/
```


## 预备知识——移动设备样式注意

### 点击高亮效果

>在移动端浏览器会遇见点击出现高亮的效果，在某项项目是不需要这个默认的效果的。那么我们通常会把这个点击的颜色设置成透明

```css
-webkit-tap-highlight-color:transparent
/*清除点击高亮效果；tap:点击*/
```
### 盒子模型

> 通过css3的新属性box-sizing能够让盒子顾及自己的尺寸而不是内容,避免出现多余的滚动条

```css
/* 保证 内容的大小不变 盒子会被撑大 */
box-sizing: content-box;
/* 保证盒子大小不变 内容可能会变（内减） */
box-sizing: border-box;
```

> 常用设置
```css
/*移动端一般是设置 盒子大小不变，内容内减*/
-webkit-box-sizing: border-box;
/*webkit内核兼容性写法*/
box-sizing: border-box;
```

### input默认样式的清除
>在移动设备的浏览器中input标签一般会有默认的样式,通过border=none,outline=none无法去除,比如立体效果,3d效果等等,我们需要添加下列样式

```css
-webkit-appearence:none;
```
* demo 

```css
input{
    /* input标签在手机的默认样式中，一般都有一种类似3d的效果样式； 但移动端 现在 扁平化 大行其道 除了锤子手机  都是扁平化，所以需要清楚input的默认样式 */
    border: 0;
    /*
    width: 100px;
    height: 100px;
    background-color: skyblue;
    */
    /* 移动端 有一些 浏览器 会默认给 input标签 添加一些 特有的样式 比如 3d 高光效果  */
    -webkit-appearance: none; 
}
<input type="button" name="" value="我是一个按钮">
```

### 移动端的默认字体
> 'sans-serif' 西方国家字母体系分为两类：serif以及sans serif。

* serif，意思是在字的笔画开始、结束的地方有额外的装饰，而且笔画的粗细会有所不同。

* sans serif是无衬线字体，没有这些额外的装饰，而且笔画的粗细差不多。

### 清除浮动css3

> 利用clear:both来清楚浮动；

> visibility: hidden----将元素隐藏，但是在网页中该占的位置还是占着。display: none----将元素的显示设为无，即在网页中不占任何的位置。

```css
    .clearfix::before,
    .clearfic::after{
        content:'';
        display:block;
        height:0;
        line-height:0;
        visibility:hidden;
        clear:both;
    }
```



comimt1 : 


## 项目分析

### 结构伪类选择器

nth-child()如果有多个不同兄弟节点获取的时候,索引需要特殊计算,我们可以限定在某一个类型上,语法如下

* E:first-of-type匹配同类型中的第一个元素E。
* E:last-of-type匹配同类型中的最后一个元素E。
* E:nth-of-type(n) 匹配同类型中的第n个元素E。

### 适配

> 移动端为了在宽度方向上进行适配;会使用百分比宽度, 高度使用固定高度，不需要进行适配；；

> 讲解精灵图时
### 视网膜屏幕与非视网膜屏幕

> 布局 
### uc不支持弹性布局