#jQuery库特性
jQuery是个JavaScript函数库
jQuery库包含以下特性:
* HTML元素选取
* HTML元素操作
* css操作
* HTML事件函数
* JavaScript特效和动画
* HTML DOM遍历和修改
* AJAX
* Utilities

#向页面添加jQuery库
```html
<head>
<script type='text/JavaScript' src='jquery/jquery.js'></script>
</head>
```
#jQuery语法
jQuery语法是为HTML元素的选取编制的,可以对元素执行某些操作
基础语法是:**$('selector').action()**
>美元符号定义jQuery,选择符selector查询和查找HTML元素,jQuery的action()执行对元素的操作
#文档就绪函数
```js
$(document).ready(function(){
//jQuery functions go here

});
```
为了防止文档完全加载之前运行jQuery代码
在文档没完全加载之前就运行函数,操作可能失败,下面是具体的两个例子
* 试图隐藏一个不存在的元素
* 获得未完全加载的图像的大小
#jQuery选择器
#jQuery元素选择器
jQuery使用CSS选择器来选取HTML元素
```js
$('p')//选取所有的<p>元素
$('p.intro')//选取所有class='intro'的<p>元素
$('p#demo')//选取所有id='demo'的<p>元素 test1
$('#demo")//选取第一个id='demo'的元素
```
css选择器 | example         |selected         |
:-----|:----------------|----------------:|
*     |$('*')           |所有元素
#id   |$('#lastname')   |id='lastname'的元素
.class|$('.intro')      |所有class='intro'的元素
elememt|$('p')|所有的p元素
.class.class|$('.intro.demo')|所有class='intro'且class='demo'的元素
---|---|------|
:first|$('p:first')|第一个p元素
:last|$('p:last')|最后一个p元素
:even|$('tr:even')|所有的偶数tr元素
:odd|$('tr:odd')|所有的奇数tr元素
---|---|------
