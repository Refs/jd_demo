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



comimt1 : 'base.css/index(base).html'


## 项目分析

### 结构伪类选择器

nth-child()如果有多个不同兄弟节点获取的时候,索引需要特殊计算,我们可以限定在某一个类型上,语法如下

* E:first-of-type匹配同类型中的第一个元素E。
* E:last-of-type匹配同类型中的最后一个元素E。
* E:nth-of-type(n) 匹配同类型中的第n个元素E。

### 适配

> 移动端为了在宽度方向上进行适配;会使用百分比宽度, 高度使用固定高度，不需要进行适配；；
宽度百分比自适应，高度固定；

### 视网膜屏幕与非视网膜屏幕对web开发的影响


> 布局 
### uc不支持弹性布局


## 顶部通栏布局


 
### 学会看别人的网站
> 后期做项目，主要还是依靠参考别人的成品，或经验；

* 遇到一个图片css属性中有：background:url() ;background-position: ;基本上可以确定，采用的是背景精灵图的做法； 遇到移动页面还会遇到background-size属性；用来解决


## 理解ios视网膜屏幕
### 显示器分辨率和图像分辨率的关系



## 布局思路（利用图片进行配合布局）
首页可以使用图片将效果快速的做出来（li>a>img）; 但是当点击进去子页面的时候，子页面就可以做的稍微复杂一点；因为最外层的首页，对于用户而言，仅仅只是一个入口；    通过图片让用户看到最直观的结果，然后用户会点进去；

## 抽取通用的样式
将常用的样式，定义为通用的资源，调用的时候，直接在html上添加class即可；

## 左边定宽，右边自适应的布局；


## less

> less的好处，关键是体现在维护上；

* less变量 （实现 当需要替换变量时，所有使用该变量的位置的值都会被替换；比如页面4大量使用京东红，要换为淘宝黄 ，只需要替换原京东红的值就可以了）

* less混合
混合可以将一个定义好的classA轻松的引入到另外一个classB,从而简单的实现classB继承classA的所有属性，我们也可以带参数引用，使用的过程类似于使用函数；

## js
> 我们在建js时，一般命名为与页面相同的名字，这样做有一个好处就是比较好找；


有两个名字：

一个是自适应页面；（根据设备屏幕进行自适应）
另一个是动态网站；（后台生成与渲染的网站）页面中的数据。图片等等，都是后台生成与渲染出来的；


## 轮播图

> 当将老师的话，在笔记上记录一遍的时候，一路就串了一遍；因为记录的过程也是思考的过程； 只有不停的听不能的记，才是`实`，记录也是一种实践；

### 常见bug 
* 若过渡的时间设置的比定时器的时间长或者相等，会出现一个问题；假如定时器一秒执行一次，切换过渡的时间也是一秒；定时器执行后，图片就会切换，中间过渡的时间是一秒；而由于定时器触发的时间间隔是1秒，即这一轮刚过渡完，又立即开始下一轮的过渡，这样图片就会一直过渡下去，肉眼分辨不开，看到的图片是连续运动的； 更甚之，会连过渡的结束事件，都触发不了，因为有可能过渡还没有结束，就进行了下一轮的过渡；

* 将判断index是否越界的代码，从定时器回调函数中抽出来，放到了过渡结束事件回调函数里面；因为当切到最后一张图片的时候，我们是在动画停止之后，才会去跳到第一张图片； 如果我们是在动画过渡当中，如过渡到一半时将index跳过去，这样就会闪烁一下，用户一看就会露馅；  所以我们必须等到过渡停下来之后，再去进行相应的操作；

* 确定index已经越界后，要先将过渡关闭，然后才将ul跳到初始的位置；如果我们不关闭过渡，用户会看到图片刷的一声就过去了；

```js
    if(index>8){
        index = 1;
        //关闭过渡
        moveUl.style.transition = '';
        //将ul跳到初始的位置；
        moveUl.style.transform = 'translateX('+(index*width*-1)+'px)';
    }
```

* touch事件，touch事件比较特殊，其只支持在移动端；即若使用touch事件，则html的meta标签要设置viewport属性；touch类事件有三个：
    + touchstart事件；用来获取触摸点的位置，该事件的event对象中touches数组对象中包含有clientX与clientY记录有触摸点相对于视口的坐标值；（只要位置相关的事物，肯定是要牵涉到坐标）； **关闭定时器，**定时器若不关闭则自己手在划屏的时候，ul还在动；
    + touchmove事件；计算触摸移动的距离，并将这段距离加到ul的translateX中，即随着手指一动，touchmove事件不断被触发，ul也不断的移动；
    + touchend事件；吸附效果； 如果移动距离比较小（无需在乎向左还是向右划），就直接吸附过去；如果移动距离比较大，就需要判断向左滑动与向右滑动， **开启定时器； 当你用手动，就将自动关掉，当你用自动，就将自动开启** 

    + 没有记录已经移动distance的值，而是利用index记录距离(区别于touch滑块案例);
    + 掌握将思路转化为代码的一个过程；

```js

moveX = event.touches[0].clientX - 
```

### js代码封装 优化代码；

> js经常要对经常出现的变量或代码进行抽取与封装，这样会有利于维护与重用，若需要修改，则只需要改一处就ok了； 将代码封装到一个函数中，如同less混合中，将样式封装到类中；在合适的地方直接调用就可以了；

```js
    //1.开启过渡
    var stratTransition = function(){
        moveUl.style.transition = 'all .3s';  
    }
    //2.关闭过渡
    var endTransition = function(){ 
        moveUl.style.transition = '';
    }
    //3.设置变换回跳原点
    var setTransform = function(){
        moveUl.style.transform = 'translateX('+ndex*width*-1+'px)';
    }

        // 由于移动的距离无法确定，所以提取为参数；
        var setTransform = function(distance){
            moveUl.style.transform = 'translateX('+distance+'px)';
        }
        //回调至原点
        setTransform(index*width*-1)
        //随触摸一起移动
        setTransform(index*width*-1 + moveX)

    
    //在上述代码出现的地方，直接去调用startTranstion与endTransition函数；好处在于维护的之后，直接改上面两个函数体就可以了；
```


## jdm_list项目

> 目的是左面滑动效果，而现在是滑动左面是，整个页面都跟着滚动，而我们的目的当在左面toc上滑动时，只有toc动，而不是整个页面都跟着动；下面代码就是用于解决此bug
> body如果设置height:100%;overflow:hidden是依然可以滑动的，如果需禁止，要再加一层div设置 height:100%加overflow：hidden（html,body加height:100%） ，这样元素超出body的高度也不能滑动了
```css
    /*设置最外层的盒子跟显示的页面一样大（移动端就是与viewport视口一样大）*/
    html,body{
        height:100%;
    }
    body{
        overflow:hidden;
    }
```

### 老师书写代码有一个技巧，先不用关注语言本身而是先去要捋清逻辑，即先先文字代码；而后将文字翻译成代码；这一点自己是可以理解的，因为自己以前做数学题时也是这样； 不管用什么样的代码写得，思路就是这：

![](http://baihua.xicp.cn/17-4-10/59752717-file_1491785968386_10ade.png)

由于ul的父元素的高度是由子元素自然撑开的，无约束的，此处要给其一个约束

```css
    html,body,.jd_container,.main,{
        height:100%;
    }
    .main_left{
        height:100%;
    }
```

```js
    //左边滑动效果
    /*
        1.获取必须知道的一些东西
            移动的dom元素 移动的ul
                获取ul父盒子的高度
                获取ul的高度
                获取移动的范围（移动的最大值与最小值）
        2.通过touch事件进行滑动
        3.手指松开 吸附回去
            touchend事件 
                吸附回去
    */
    function left_scroll(){
        //1.获取移动的dom元素ul
        //2.计算ul移动的范围
            //1）.获取ul的高度
            //2）.获取ul父元素的高度
            //3）.范围的最大值
            //4）.范围的最小值
        //3.通过touch事件控制ul的移动
            //1).定义一些变量记录距离 起始值 移动值 总的移动值 delayDistance
            //2).touchstart事件   
                //1>.初始触摸起始点的值
            //3).touchmove事件
                //1>.计算当前移动值
                //2>.判断ul是否满足移动的条件
                    //(1).移动距离超出最大范围，修正
                    //(2).移动距离超出最小范围，修正
                //3>.移动ul(经过上面过滤，可以保证值有效,**且ul的移动没有越界**)
            //4).touchend事件
                //1>.记录已经移动的总值
                //2>.吸附效果

            //吸附的效果就是，当ul划出移动范围的时候，可以吸附过来；
    }

      function left_scroll(){
        //1.获取移动的dom元素ul
        var moveUl = document.querySelector('.main_left ul');
        //2.计算ul移动的范围
            //1）.获取ul的高度(占位高) offsetHeight/clientHeight前面在书写的时候，都无需添加style;
            var ulHeight = moveUl.offsetHeight;
            //2）.获取ul父元素的高度
            var parentHeight = document.querySelector('.main_left').offsetHeight;
            //3）.范围的最大值
            var maxDistance = 0;
            //4）.范围的最小值
            var minDistance = parentHeight - ulHeight;
         //3.通过touch事件控制ul的移动
            //1).定义一些变量 记录距离
            var startY = 0;
            var moveY = 0;
            var distanceY = 0;
            //2).touchstart事件
            moveUl.addEventListener('touchstart',function(event){
                //1>. 初始触摸起始点的值
                var startY = event.touches[0].clientY;
 
            })
            //3).touchmove事件
            moveUl.addEventListener('touchmove',function(event){
                //1>.计算当前移动距离
                var moveY = event.touches[0].clientY - startY;
                //2>.判断ul是否满足移动的条件
                if(distanceY+moveY > maxDistance){
                    //(1).移动距离超出最大范围，修正
                    moveY = 0;
                    distanceY = maxDistance;
                }else if(distanceY + moveY < minDistance){
                    //(2).移动距离超出最小范围，修正
                    moveY = 0;
                    distanceY = minDistance;
                }
                //3>.移动ul
                moveUl.style.transform = 'translateY('+(moveY + distanceY)+'px)';

            })
            //4).touchend事件
            moveUl.addEventListener('touchend',function(event){
                //1>.记录已经移动的总距离
                distanceY += moveY; 
            })
    }
```

```js
    //添加吸附 吸附的效果就是，当ul划过其移动之后，松开手ul能过吸附回来；

    //1. 是ul能够超出其移动范围；上文中 若distanceY+moveY > maxDistance 则moveY=0, distanceY=maxDistance 即当范围超出去之后，ul就停在哪里，不随自己手指动了；所以首先要做的就是ul能随手指出其所在的移动范围，但这个多出去的范围应该也是可控的，第3步定义一些变量的时候应该多定义一个delayDistance;

    //2. touchmove事件中
        //1).扩大ul的移动范围；使ul能移动到额定范围之外；
    //3. touchend事件中
        //1). 手指松开吸附过去
            //1>. 判断吸附方位 - ul出范围上界 - 向下吸     
                //(1).修改distance的值 
            //2>. 判断吸附方位 - ul出范围上界 - 向上吸      
                //(1).修改distance的值
            //3>. 移动ul并添加过渡 
    //4. 在touchmove事件中清楚过渡 若不清除过渡，则会有0.3s的延迟；
    //5. 优化代码 ,将常用的代码封装到一个函数中，使用的情景类似于less中的mxin;
        //1). 开始过渡
        //2). 结束过渡 
        //3). 设置变换
    //6. bug解决，底部位置吸不回去；向上滑动，当ul移出移动范围后松手，ul会自动吸附，当吸附的位置不是ul的底边而是ul的中间部分； 问题出在minDistanceY的计算方式上，应该考虑.header占位高度的影响；
        //1). 获取.header的占位高度
        //2). 从新计算范围下界 目的是为了让ul的范围下界向上抬一个header高的距离，而y轴的正方向是向下的，所以此处为向上应加一个负值；有时没必要过于纠结正负，随便写一个在浏览器上调试一下就确定了，这是最快的也是最直观的；
    
        function left_scroll(){
        var moveUl = document.querySelector('.main_left ul');
            var ulHeight = moveUl.offsetHeight;
            var parentHeight = document.querySelector('.main_left').offsetHeight;
            //获取.header的占位高度
            var headerHeight = document.querySelector('.header').offsetHeight;
            var maxDistance = 0;
            //从新计算移动范围下界
            //var minDistance = parentHeight - ulHeight;
            var minDistance = parentHeight - ulHeight - headerHeight;
            var startY = 0;
            var moveY = 0;
            var distanceY = 0;
            //定义ul能超出其移动范围的距离
            var delayDistance = 100;
            //4.优化代码 定义函数
            //1). 开始过渡
            function startTransition (){
                moveUl.style.transition = 'all .3s';
            }
            //2). 结束过渡
            function endTransition (){
                moveUl.style.transition = '';
            }
            //3). 设置变换
            function setTransform (distance){
                 moveUl.style.transform = 'translateY('+distance+'px)';
            }

            moveUl.addEventListener('touchstart',function(event){    
                var startY = event.touches[0].clientY;
            })
            moveUl.addEventListener('touchmove',function(event){
                //清除ul的过渡
                //moveUl.style.transtion = '';
                endTransition();
                var moveY = event.touches[0].clientY - startY;

                //限制ul的移动范围，原本是限制在其移动范围最大值与最小值之内，现在在其范围的基础上，加上一个delayDistance这样，ul就能随手指移动至范围之外了，吸附的过程就是先移到移动范围以外，而后再自动吸附回移动范围以内；
                if(distanceY+moveY > maxDistance + delayDistance){
                    moveY = 0;
                    distanceY = maxDistance + delayDistance;
                }else if(distanceY + moveY < minDistance - delayDistance){
                    moveY = 0;
                    distanceY = minDistance - delayDistance;
                }
                //moveUl.style.transform = 'translateY('+(moveY + distanceY)+'px)';
                setTransform(moveY + distanceY);

            })
            moveUl.addEventListener('touchend',function(event){
                distanceY += moveY; 
                //1). 手指松开吸附过去
                //1>. 判断吸附方位 - ul出范围上界 - 向下吸     
                if(distanceY > maxDistance){
                    //(1).修改distance的值 
                    distanceY = maxDistance;
                //2>. 判断吸附方位 - ul出范围上界 - 向上吸      
                }else if(distanceY < minDistance){
                    //(1).修改distance的值
                    distanceY = minDistance;
                }
                //3>. 移动ul并添加过渡 
                //moveUl.style.transition = 'all .3s';
                startTransition();
                //moveUl.style.transform = 'translateY('+distanceY+'px)';
                setTransform(distanceY);
            })
    }

```

> 吸附bug:

![](http://baihua.xicp.cn/17-4-10/1825011-file_1491826732597_14.png )