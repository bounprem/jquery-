#  jQuery概述

### 1.1 javascript 库

JavaScript库：即library，是一个封装好的特定的集合（方法和函数），从封装函数的角度理解，就是在这个库中，封装了很多预先定义好的函数在里面,比如动画animate,hide,show,获取元素。

###  1.2 jQuery的概念

jQuery是一个快速、简洁的javascript库。

jQuery封装了javascript常用的功能代码

优化了DOM操作、事件处理、动画设计和Ajax交互。

学习jQuery本质：就是学习调用函数（方法）。

### 1.3 jQuery的优点

- 轻量级，核心文件才几十kb，不会影响页面加载速度
- 跨浏览器兼容，基本兼容了现在主流浏览器
- 链式编程，隐式迭代
- 对事件、样式、动画支持，大大简化了DOM操作
- 支持插件扩展开发。有看丰富的第三方插件，如：树形单元、日期控件
- 免费、开源



# jQuery的基本使用

###  2.1 jQuery下载网址

[官方网址](https://jquery.com/)

### 2.2 jQuery的入口函数

```
$(function(){
	...//此处是页面DOM加载完成的入口
});
```

### 2.3 jQuery的顶级对象$

1. $是jQuery的别称，在代码可以使用jQuery代替$，通常都直接使用$。
2. ==$==是jQuery的顶级对象，相当于原生JavaScript中的window。把元素利用$包装成jQuery对象，就可以调用jQuery的方法。



###  2.4 jQuery对象和DOM对象

1. 用原生JS获取来的对象就是DOM对象

```
var myDiv = doucment.queryselector('div');//myDiv 是DOM对象
```

2. 用jQuery方式获取过来的对象是jQuery对象，本质通过$把DOM元素进行包装

```
$('div');//$('div')是一个jQuery对象
```

3. jQuery对象只能使用jQuery方法，DOM对象则使用原生的JavaScript属性和方法。



### 2.5 DOM对象和jQuery对象相互转换

1. DOM对象转换为jQuery对象

   

```
<video scr = "mov.mp1"></video>
$('video'); //直接获取视频，得到jQuery对象
已经使用原生js 获取过来的DOM对象
var myVideo = doucment.quertySelector('video');
$(myVideo);
```

2. jQuery对象转换为DOM对象

   ```
   方法一：$('video')[index]
   $('video')[0].play()
   ```

   ```
   方法二：$('video').get(index)
   $('video').get(0).play()
   ```

   

# jQuery常用的API

### 1. jQuery选择器

#### 1.1 jQuery基础选择器

原生的js获取元素方式有很多种，而且兼容性情况不同，因此jQuery做了封装，使获取元素统一标准

```
$("选择器") //选择器直接写css选择器即可
```

| 名称       | 用法            | 描述                     |
| ---------- | --------------- | ------------------------ |
| ID选择器   | $("#id")        | 获取指定ID元素           |
| 全选选择器 | $("*")          | 匹配所有元素             |
| 类选择器   | $(".class")     | 获取同一类class元素      |
| 标签选择器 | $("div")        | 获取同一类标签的所有元素 |
| 并集选择器 | $("div.p.li")   | 选择多个元素             |
| 交集选择器 | $("li.current") | 交集元素                 |

#### 1.2 jQuery层级选择器

| 名称       | 用法       | 描述                                                        |
| ---------- | ---------- | ----------------------------------------------------------- |
| 子代选择器 | $("ul>li") | 使用>号，获取亲儿子层级的元素；注意：并不会获取孙子层级元素 |
| 后代选择器 | $("ul li") | 使用空格，代表后代选择器，获取ul下所有li元素，包括孙子等    |

#### 1.3 jQuery筛选选择器

| 语法       | 用法          | 描述                                                      |
| ---------- | ------------- | --------------------------------------------------------- |
| :first     | $("li:first") | 获取第一个li元素                                          |
| :last      | $("li:last")  | 获取最后一个li元素                                        |
| :eq(index) | $("li:eq(2)") | 获取到的li元素中，选择索引号为2的元素，索引号index从0开始 |
| :odd       | $("li:odd")   | 获取到li元素中，选择索引号为奇数的元素                    |
| :even      | $("li:even")  | 获取到li元素中，选择索引号为偶数的元素                    |

#### 1.4 jQuery筛选方法(重点)

| parent()           | $("li").parent();          | 查找父级                            |
| ------------------ | -------------------------- | ----------------------------------- |
| children(selector) | $("ul").children("li")     | 相当于$("ul>li"),最近一级（亲儿子） |
| find(selector)     | $("ul").find("li")         | 相当于$("ul li"),后代选择器         |
| siblings(selector) | $(".first").siblings("li") | 查找兄弟节点，不包括自己本身        |
| eq(index)          | $("li").eq(2)              | 相当于$("li:eq(2)")                 |



### 2. jQuery隐式迭代



#### 2.1 jQuery设置样式

```
$("div").css('属性','值')
```

#### 2.2 隐式迭代(重点)

遍历内部DOM元素(伪数组形式存储)的过程就叫==隐式迭代==

简单理解：给匹配到所有元素进行循环遍历，执行相应的方法，而不用再进行循环，简化操作，方便调用。

```css
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div>脏脏星</div>
    <div>脏脏星</div>
    <div>脏脏星</div>
    <ul>
        <li>大理寺日志</li>
        <li>大理寺日志</li>
        <li>大理寺日志</li>
        <li>大理寺日志</li>
    </ul>
    <script>
        // 给3个div设置背景颜色为紫色 jQuery对象不用使用style
        $("div").css("background", "purple");
        // 隐式迭代就是把匹配的所有元素内部进行遍历循环，给每个元素添加css这个方法
        $("ul li").css("color", "pink");
    </script>
</body>

</html>
```



### 3.jQuery样式操作

#### 3.1 操作css方法

参数只写属性名，则返回属性值

> $(this).css("color");

参数是==属性名、属性值、逗号分隔==，是设置一组样式，属性必须加引号，值如果是数字可以不用跟定位和引号

> $(this).css("color","purple");

参数可以是==对象形式==，方便设置多组样式。属性名和属性值用冒号隔开，属性可以不用加引号

```css
$(this).css({
	width:100,
	height:100,
	backgroundColor:"red"
})
```

#### 3.2 设置类样式方法

作用等同于以前的classList，可以操作类样式，注意==操作类里面的参数不要加点==

1. 添加类==addClass()==

```css
 <style>
        div {
            width: 100px;
            height: 100px;
            margin: 100px auto;
            background-color: saddlebrown;
            transition: all 0.5s;
        }
        
        .current {
            background-color: slateblue;
            transform: rotate(360deg);
        }
    </style>
    <script src="jquery.js"></script>
</head>

<body>
    <div class="current"></div>
    <script>
        $(function() {
            //1.添加类 addClass()
            $("div").click(function() {
                $(this).addClass("current");
            });
           }
```

2. 移除类==removeClass()==

```jquery
 //2.删除类 removeClass()
            $("div").click(function() {
                $(this).removeClass("current");
            });
```

3. 切换类==toggleClass()==

```jquery
 //3.切换类
            $("div").click(function() {
                $(this).toggleClass("current");
            });
```

#### 3.3 类操作与className的区别

原生js中className会覆盖原先里面的类名

jQuery里面的类操作只是对指定类进行操作，相当于追加类名不影响原先的类名

 

# jQuery效果

### 1. 显示隐藏效果

语法规范

> 显示：==show([speed],[easing],[fn])==

参数

- 参数都可以省略
- speed：三种预定速度的之一的字符串('slow','nomal','fast')或表示动画长度的毫秒数值（如：1000）
- easing：（optional）用来指定切换效果，默认"swing"，可用参数"linear"

>隐藏：==hide([speed],[easing],[fn])==

>切换：==toggle([speed],[easing],[fn])==



### 2. 滑动效果

>下滑动：==slideDown([speed],[easing],[fn])==

>上滑动：==slideUp([speed],[easing],[fn])==

>滑动切换：==slideToggle([speed],[easing],[fn])==

注：里面的参数都可以省略



### 3. 事件切换==hover==

事件切换hover 鼠标经过和离开的复合写法

```jquery
$(".nav>li").hover(function() { //第一个function表示经过，第二个表示离开
             $(this).children("ul").slideDown();
             }, function() {
              $(this).children("ul").slideUp();
           })
```

事件切换 hover 如果只写一个函数，那么鼠标经过和鼠标离开都会触发这个函数

```jquery
$(".nav>li").hover(function() {
                $(this).children("ul").slideToggle();
            })
```



### 4. 动画队列及其停止排队方法

#### 4.1 动画或队列效果

动画或效果一旦触发就会执行，如果多次触发，就会造成多个动画或者效果排队

#### 4.2 停止排队

```
stop()
```

stop()方法用于停止动画或者效果

注意：stop()写到动画或者效果的==前面，相当于停止结束上一次动画==

### 5. 淡入淡出效果

```
淡入：fadeIn([[speed],[easing],[fn]])
淡出：fadeOut([[speed],[easing],[fn]])
淡入淡出切换：fadeToggle([[speed],[easing],[fn]])
```

渐进方式调整到指定==不透明度==

```
fadeTo([[speed],opacity,[easing],[fn]])
```

- ==opacity透明度必须写，取值0~1之间==
- speed：三种预定速度的之一的字符串('slow','nomal','fast')或表示动画长度的毫秒数值（如：1000）==必须写==

### 6.自定义动画 ==animate==

#### 6.1 语法

```
animate(params,[speed],[easing],[fn])
```

- ==params:想要更改的样式属性，以对象形式传递，必须写。属性名可以不用带引号，如果是复合属性则需要采用驼峰命名法==。其余参数可以省略。
- speed：三种预定速度的之一的字符串('slow','nomal','fast')或表示动画长度的毫秒数值（如：1000）
- easing：（optional）用来指定切换效果，默认"swing"，可用参数"linear"
- fn:回调函数，在动画完成时执行的函数，每个元素执行一次。
- 注：==自定义动画要添加绝对定位==

```javascript
 <style>
        div {
            position: absolute;
            width: 100px;
            height: 100px;
            background-color: tomato;
        }
    </style>
    <script src="jquery.js"></script>
</head>

<body>
    <button>动起来</button>
    <div></div>
    <script>
        $(function() {
            $("button").click(function() {
                $("div").animate({
                    left: 500,
                    top: 200,
                    opacity: .4
                }, 500)
            })
        })
    </script>
</body>
```



# jQuery属性操作

### 1.设置或获取元素固有属性值==prop()==

1.1元素固有属性值就是元素本身自带的属性，如<a>元素里面的href

获取属性语法

```
prop("属性")
```

设置属性语法

```
prop("属性"，“属性值)
```

### 2.设置或获取元素自定义属性值==attr()==

用户自己给元素添加的属性，称为自定义属性，如给div添加index="1"

获取属性语法

```
attr("属性")
```

设置属性语法

```
attr("属性","属性值")
```



# jQuery内容文本值

### 1.获取设置元素内容 ==html()==

```
html()  //获取元素的内容
html("内容")  //设置元素的内容
html标签和文字都获取过来
```

###  2. 普通元素==文本==内容==text()==

```
text()  //获取元素的内容
text("内容")  //设置元素的内容
text只把文字获取过来，标签忽略
```

### 3.获取设置表单值==val()==

```
val()  //获取元素的内容
val("内容")  //设置元素的内容
```

==parents ()==返回指定的祖先元素

==toFixed(2)==保留两位小数

==:checked==返回到底有几个复选框被选中

# jQuery元素操作

### 1.遍历元素

jQuery隐式迭代是对同一类元素做了相同的操作。如果要给同一类元素做不同操作，就需要用到遍历。

语法1

```
$("div").each(function(index,domEle){***;})
```

- ==each()==方法遍历匹配每一个元素。主要用DOM处理

- index是每个元素的索引号，domEle是每个==DOM元素的对象，不是jQuery对象==

- ==所有要想使用jQuery方法，需要给DOM元素转换威jQuery对象$(domEle)==



语法2

```
$.each(object,function(index,element){***})
```

- $.each()方法可以用于遍历任何对象，==主要用于数据处理==，比如数组、对象
- index是每个元素的索引号，element遍历内容

### 2.创建元素

 2.1 内部添加

```
element.append("内容")  //放到内容的最后面
element.prepend("内容") //放到内容的最前面
```

```javascript
<ul>
	<li>原先的li</li>
</ul>
<div class="test"原先的div</div>
<script>
	$(function(){
		//1创建元素
		var li = $("<li>后来创建的li</li>");
		//内部添加
		$("ul").append(li);
		$("ul").prepend(li);
	})
```

2.2 外部添加

```
element.after("内容") //放在目标元素的后面
element.before("内容") //放在目标元素的前面
```

==内部元素添加，生成之后，是父子关系==

==外部元素添加，生成之后，是兄弟关系==

2.3删除元素

```
element.remove() //删除匹配的元素（本身）
element.empty() //删除匹配元素里面的子节点（孩子）
element.html("")//删除匹配元素里面的子节点（孩子）
```



# jQuery事件

### 1. jQuery事件注册

1.1 单个事件注册

语法

```
element.事件(function(){})
```

```
$("div").click(function(){事件处理程序})
```

### 2.事件处理==on()==绑定事件

on()方法在匹配元素上==绑定一个或多个事件==的事件处理函数

语法：

```
element.on(events,[selector],fn)
```

events：一个或多个用空格分隔的事件类型，如"click"或"keydown"。

selector：元素的子元素选择器

fn: 回调函数即绑定在元素身上的侦听函数。

```
// on可以绑定1个或者多个事件处理程序
$("div").on({
               mouseenter: function() {
                    $(this).css("background", "skyblue");
                },
               click: function() {
               		$(this).css("background", "purple");
             },
               mouseleave: function() {
                 	$(this).css("background", "blue");
            }
        });
```

```
 .current {
            background-color: purple;
        }
$("div").on("mouseenter mouseleave", function() {
                $(this).toggleClass("current"); 
            });
```

*on()方法优势2*：

==可以事件委派操作==，事件委派的定义就是把原先加给子元素身上的事件绑定在父元素身上，就是把事件委托给父元素。

```
//on可以实现事件委托（委派）
$("ul").on("click", "li", function() {
                alert(11);
            });
            // click 是绑定在ul 身上的，但是 触发的对象是 ul 里面的小li
```

*on()方法优势3：*

==动态创建元素==，click()没有办法绑定事件，on()可以给动态生成的元素绑定事件

```
 $("ol").on("click", "li", function() {
                alert(11);
            })
            var li = $("<li>我是后来创建的</li>");
            $("ol").append(li);
        })
```

### 3.事件处理==off()==解绑事件

off()方法可以移除通过on()方法添加的事件处理程序。

```
$("div").off() //解除div身上的所有事件
$("div").off("click") //解除div身上的点击事件
$("div").off("click","li")//事件委托
```

==one()==只能触发事件一次

```
$("p").one("click",function(){
	alert(11);
})
```

### 4.自动触发事件==trigger()==

有些事件希望自动触发，比如轮播图自动播放功能跟点击右侧按钮一致，可以利用定时器自动自动触发右侧按钮点击事件，不必鼠标点击触发。

```
element.click()//第一种简写形式
element.trigger("事件")//自动触发模式
element.triggerHandler("事件")//自动触发模式，不会触发元素的默认行为
```

事件被触发，就会有事件对象的产生。

```
element.on(events,[selector],function(event){})
```

```
$(function(){
	$(document).on("click",function(){
		console.log("点击document");
	})
	$(document).on("click",function(event){
		console.log("点击div");
		event.atopPropagetion();//阻止冒泡行为
	})	
})
```

阻止默认行为：event.preventDefault()或者return false

阻止冒泡：event.atopPropagetion()

·

# jQuery拷贝对象

如果想要把某个对象拷贝（合并）给另一个对象使用，可以使用==$extend()==方法

语法：

```
$.extend([deep],target,object1,[objectN])
```

deep：如果设为true为深拷贝，默认false为浅拷贝

target：要拷贝的目标对象

object1：待拷贝的第一个对象的对象

浅拷贝把原来对象里面的==复杂数据类型地址==拷贝给目标对象，修改目标对象==会影响==被拷贝对象

深拷贝把里面的数据完全复制一份给目标对象，如果里面有不冲突的属性会合并到一起

# jQuery多库共存

jQuery使用$作为标识符，随着jQuery的流行，其它的js库也会使用$作为标识符，这样一起使用会引起冲突。让jQuery和其它的js库不存在冲突，可以同时存在，叫多库共存

jQuery解决方案：

1. ==把里面的$符号统一改为jQuery，如jQuery("div")==

2. ==jQuery变量规定新的名称：$.noConflict()    var xx = $.noConflict() ;(让jQuery释法对$的控制权，让用户自己决定)==

# jQuery插件

1. jQuery插件

jQuery插件库 :http://www.jq22.com

jQuery之家：http://www.htmleaf.com

使用步骤：

1.引入相关文件（jQuery文件和插件文件）

2.复制相关html、css、js(调用插件）

2. ==图片懒加载==（图片使用延迟加载可提高网页加载速度。它能帮助减轻服务器负载）

jQuery插件库:http://www.jq22.com

当页面滑动到可视区，再显示图片

使用jQuery插件库easylazyload，注意：此时的js引入文件和js调用必需写在DOM元素（图片）最后面

3. ==全屏滚动==

   github ： https://github.com/alvarotrigo/fullpage.js

   中文翻译网站：http://www.dowebok.com/demo/2014/77/

4. bootstrap js插件：

   https://v3.bootcss.com/

   bootstrap 框架也是依赖于jQuery开发，里面的js使用，也必须引入jQuery文件。

# jQuery尺寸、位置操作

### 1.jQuery尺寸

| 语法                               | 用法                                                 |
| ---------------------------------- | ---------------------------------------------------- |
| width()/height()                   | 获取匹配元素的高度和宽度 只算width/height            |
| innerwidth()/innerheight()         | 获取匹配元素的高度和宽度 包含padding                 |
| outerwidth()/outerheight()         | 获取匹配元素的高度和宽度 包含padding，border         |
| outerwidth(true)/outerheight(true) | 获取匹配元素的高度和宽度 包含padding，border，margin |

- 以上参数为空，则是获取相应值，返回的是数字型
- 如果参数为数字，则是修改相应值
- 参数可以不必写单位

### 2.jQuery位置

位置主要有三个：==offset()==、scrollTop()/scrollLeft()

**offset()设置或获取元素偏移**

1. offset()方法设置或返回被选元素相对于==文档==的偏移坐标，跟父级没有关系
2. 该方法有两个属性left、top，offset().top用于获取距离文档顶部的距离，offset().left用于获取距离文档左侧的距离
3. 可以设置元素的偏移：offset({top:10;left:30})

 **获取带有==定位父级位置==（偏移）position() 如果没有带有定位的父级，则以文档为准。这个方法只能获取不能设置偏移**



