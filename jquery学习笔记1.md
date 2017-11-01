### jQuery库特性


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

### 向页面添加jQuery库


```html
<head>
<script type='text/JavaScript' src='jquery/jquery.js'></script>
</head>
```
### jQuery语法


jQuery语法是为HTML元素的选取编制的,可以对元素执行某些操作
基础语法是:**$('selector').action()**

* 美元符号定义jQuery
* 选择符selector查询和查找HTML元素
* jQuery的action()执行对元素的操作

### 文档就绪函数


```js
$(document).ready(function(){
//jQuery functions go here

});
```
>$(document).ready()中回调函数中有一个参数,就是jQuery本身
为了防止文档完全加载之前运行jQuery代码
在文档没完全加载之前就运行函数,操作可能失败,下面是具体的两个例子
* 试图隐藏一个不存在的元素
* 获得未完全加载的图像的大小

### jQuery选择器


#### jQuery元素选择器


jQuery使用CSS选择器来选取HTML元素
```js
$('p')//选取所有的<p>元素
$('p.intro')//选取所有class='intro'的<p>元素
$('p#demo')//选取所有id='demo'的<p>元素 test1
$('#demo")//选取第一个id='demo'的元素
```
css选择器 | example         |selected         |
:-----|:----------------|----------------:|
\*     |$('*')           |所有元素
\#id   |$('#lastname')   |id='lastname'的元素
\.class|$('.intro')      |所有class='intro'的元素
elememt|$('p')|所有的p元素
\.class.class|$('.intro.demo')|所有class='intro'且class='demo'的元素
---|---|------|
:first|$('p:first')|第一个p元素
:last|$('p:last')|最后一个p元素
:even|$('tr:even')|所有的偶数tr元素
:odd|$('tr:odd')|所有的奇数tr元素
---|---|------
:eq(index)|$('ul li:eq(3)')|列表中的第四个元素(index从0开始
:gt(index)|$('ul li:gt(3)')|列出index大于3的元素
:lt(index)|$('ul li:lt(3)')|列出index小于3的元素
:not(selector)|$('input:not(:empty)')|所有不为空的input元素
---|---|------
:header|$(':header')|所有的标题元素h1--h6
:animated| |所有动画元素
---|---|------
:contains(text)|$('contains("w3school")')|包含指定字符串的所有元素
:empty|$(':empty')|无子(元素)节点的所有元素
:hidden|$('p:hidden')|所有隐藏的p元素
:visible|$('table:visible')|所有可见的表格
---|---|-------
s1,s2,s3|$('th,td,.intro')|所有带有匹配选择的元素
---|---|-------
\[attribute]|$('\[href]')|所有带有href属性的元素
\[attribute=value]|$('\[href="#"]')|所有href属性值等于'#'的元素
\[attribute!=value]|$('\[href!="#"]')|所有href属性值不等于'#'的元素
\[attribute$=value]|$('\[href$=".pdf"]')|所有href属性值以'.pdf'结尾的元素
\[attribute*=value]|$('\[href*="www"]')|所有的href属性值包含'www'的元素
\[attribute^=value]|$('[href^="http"]')|所有的href属性值以'http'开头的元素
表单选择器|---|------
:input|$(':input')|所有的input元素
:text|$('text')|所有type='text'的input元素
:password|$(':password')|所有type='password'的input元素
:radio|$(':radio')|所有type='radio'的input元素
:checkbox|$(':checkbox')|所有的type='checkbox'的input元素
:submit|$(':submit')|所有type='submit'的input元素
:reset|$(':reset')|所有type='reset'的input元素
:button|$(':button')|所有type='button'的input元素
:image|$(':image')|所有type='image'的input元素
:file|$(':file')|所有type='file'的input元素
---|---|------
:enable|$(':enable')|所有激活的input元素
:disable|$(':disable')|所有禁用的input元素
:selected|$(':selected')|所有被选取的input元素
:checked|$(':checked')|所有被选中的input元素

#### jQuery选择器补充
>一些选择器作为jQuery扩展,使用这些扩展去查询元素不能利用本机DOM的querySelectorAll()方法提供的性能提升,需要使用一些特殊的方式来达到选择元素时的最佳性能
#### 属性选择器
* \[name|='value'] 选择具有指定属性的元素，其值**等于给定字符串，或以该字符串开头，后跟连字符（ - )**.
* \[name~='value'] 选择具有指定属性的元素,其中包含**由空格分隔的**给定单词的值
* \[attributeFilter1]\[attributeFilter2] 属性选择器可以连用 选择所有匹配指定属性过滤器的元素
#### 基本选择器
* 伪类选择器(以':'开头),前面要先使用其他选择器$(':focus')相当于('*:focus')效率很低
* :animated jQuery扩展 
>最佳性能方式:使用纯css选择器选择元素,然后用.filter(':animated').
* $('\*') 全选通用选择器非常慢
* :eq(index) jQuery扩展 其中index可以使负数表示倒数第几个元素(-1最后一个元素) 
>最佳性能方式:$('your-pure-css-selector').eq(index)
* :even jQuery扩展 
>最佳性能方式:使用纯css选择器选择元素,然后用.filter(':even')
* :first jQuery扩展 选择匹配元素的第一个 只会选择一个元素(:first-child可以匹配多个:每个父项一个)
>最佳性能方式:使用纯css选择器选择元素,然后用.filter(':first') 
* :gt(index) jQuery扩展 index可以接受负值 
>最佳性能方式:$('your-pure-css-selector').slice(index)
* :header jQuery扩展
>最佳性能方式:使用纯css选择器选择元素,然后用.filter(':header')
* :last jQuery扩展
>最佳性能方式:使用纯css选择器选择元素,然后用.filter(':last')
* :lt(index) jQuery扩展 
>最佳性能方式:$('your-pure-css-selector').slice(0,index)
* :not(selector) 所有的选择器都被接受
* :odd jQuery扩展
>最佳性能方式:使用纯css选择器选择元素,然后用.filter(':odd')
* :root $(':root')选择的始终是html元素
* :target 选择由文档URL的片段标识符指定的目标元素
>如果文档的URI包含片段标识符或散列，则:target选择器将使该元素与标识符匹配的ID匹配。例如，给定一个URI为'http://example.com/#foo'的文档，$( "p:target" )将选择该\<p id="foo">元素。

#### 子类选择器
* :first-child 选择器可以匹配多个,相当于:nth-child(1),是父代元素第一个子代的所有元素
* :first-of-type 位于同类型第一位的所有元素
* :last-child 是父代元素最后一个子代的所有元素 :last只匹配一个元素
* :last-of-type 位于同类型最后一位的所有元素
* :nth-child(index/even/odd/equation)选择位于父代的第n个子代的所有元素
* :nth-last-child(index/even/odd/equation)选择位于父代的倒数第n个子代的所有元素
* :nth-last-of-type(index/even/odd/equation)选择位于同类型元素倒数第n位的所有有元素
* :nth-of-type(index/even/odd/equation)选择位于同类型元素第n位的所有元素
* :only-child 选择所有的元素,他们是父代的唯一子代
* :only-of-type 选择同类型元素中,在所有子代元素中是唯一的所有元素
>child的选择器 看所有子代元素  type选择器看所有同名称元素

#### 内容选择器
* :contains(text) 其中text可以不被引号包围,大小写敏感,文本匹配方式*=
* :empty 所有没有子元素的元素(包括不能有文本节点)
>'input','img','br','hr'本来就是空的
* :has(selector) jQuery扩展 选择至少包含一个与指定选择器匹配元素的元素
>$("your-pure-css-selector").has(selector/DOMElement)
* :parent jQuery扩展 选择所有至少有一个子节点(文本或元素)的元素 同empty相反
>最佳性能方式:使用纯css选择器选择元素,然后用.filter(':parent')


#### 表格选择器

* :button jQuery扩展 css等效选择器$('button,input\[type="button"]')
>最佳性能方式:使用纯css选择器选择元素,然后用.filter(':button')
* :checkbox jQuery扩展 css等效选择器$('\[type="checkbox"]')
>最佳性能方式:上面那种或者$('input:checkbox')
* :checked 选择适用于复选框,单选按钮,和选项select元素
>如果要仅检索所选择的select元素选项,使用:selected选择器
* :disabled 匹配所有**实际禁用的元素**,同\[disabled]不同
>实际支持disabled属性的元素有button,input,optgroup,option,select,textarea,menuitem和fieldset.
* :enabled 选择所有不匹配:disabled的元素
>只应该适用于button,input,optgroup,option,select,textarea.
* :file jQuery扩展 
>最佳性能方式:$('\[type="file"]')
* :focus 在前面最后先使用其他选择器
>如果寻找当前的焦点元素,使用$(document.activeElement)
* :image jQuery扩展 等同于\[type='image'],为获得更好的性能,使用后者
* :input jQuery扩展 选择所有的input,button,textarea,button,select元素
>最佳性能方式:首先使用纯CSS选择器选择元素，然后使用.filter(":input")。
* :password jQuery扩展 
>最佳性能方式:\[type='password']
* :radio jQuery扩展
>最佳性能方式:\[type='radio']
* :reset jQuery扩展
>最佳性能方式:\[type='reset']
* :submit jQuery扩展
>最佳性能方式:input\[type='submit']或者button[type='submit']
* :text jQuery扩展
>最佳性能方式:\[type='text']
* :selectd jQuery扩展 只适用于option元素
>最佳性能方式:首先使用纯CSS选择器选择元素，然后使用.filter(":selected")

##### 表格选择其中只有:focus :checked :enabled :disabled选择器不是扩展的

##### 在扩展选择器中只有filter(":selected")使用的是过滤器,其他都是用的属性选择器来提高效率
#### 层级选择器
* 'parent > child' parent任何有效的选择器 child 筛选子元素的选择器
* "祖先 后代 后代" 选择作为给定祖先的后代的所有元素
* "prev + next" 选择位于prev下一个兄弟元素中符合next的所有元素
* "prev ~ sublings" 选择位于prev之后兄弟元素中符合sublings的所有元素

#### 可见性选择器
元素被认为是隐藏的,原因有以下几个:

* display:none
* 他们是形式元素type='hidden'
* 他们的宽高显示设置为0
* 他的祖先元素是隐藏的
具有visibility:hidden或opacity:0认为是课件元素

都是jQuery扩展 获得最佳性能方式:首先使用纯CSS选择器选择元素，然后使用.filter(":hidden")/(":visible")
### jQuery事件

>jQuery是为事件处理特别设计的

#### 什么是事件
页面对不同访问者的响应叫做时事件.
事件处理程序指的是当HTML中发生某些事件时所调用的方法.
#### 常见的DOM事件
鼠标事件|键盘事件|表单事件|文档/窗口事件|
:------|:-----:|:--------:|--------:|
click|keypress|submit|load
dbclick|keydown|change|resize
mouseenter|keyup|focus|scroll
mouseleave| |blur|unload

### 添加事件的api

on是live,bind,delegate的代替,功能最全

live已经被移除

$(selector).bind(event,data,function)

* event 必需.规定添加到元素的一个或多个事件(由空格分隔的多个事件).必须是有效事件
* data 可选.规定传递到函数的额外数据
* function 必需.规定当事件发生时运行的函数
$(selector).delegate(childSelector,event,data,function)
* childSelector 必需.规定要附加事件处理程序的一个多个子元素
* 
>事件委托功能

$(selector).on(event,childSelector,data,function) 推荐使用
>没有childSelector是为selector元素添加事件处理程序,有的话是事件委托

### 实例
#### 使用map参数向被选元素添加多个事件处理程序
```html
<!DOCTYPE html>
<html>
<head>
<script src="jquery.js">
</script>
<script>
$(document).ready(function(){
  $("p").on({
    mouseover:function(){$("body").css("background-color","lightgray");},  
    mouseout:function(){$("body").css("background-color","lightblue");}, 
    click:function(){$("body").css("background-color","yellow");}  
  });
});
</script>
</head>
<body>

<p>Click or move the mouse pointer over this paragraph.</p>

</body>
</html>
```
#### 在元素上添加自定义事件
```js
$("p").on("myOwnEvent", function(event, showName){
   $(this).text(showName + "! What a beautiful name!").show();
 });
$("button").click(function(){
  $("p").trigger("myOwnEvent",["Anja"]);
});
```
$(selector).trigger(event,\[parameter1,parameter2,...])

* 规定被选元素要触发的事件
* event 必需.规定指定元素要触发的事件,可以是自定义事件,或者任何标准事件
* \[parameter1,parameter2,...] 可选.传递给事件处理程序的额外参数.额外参数对自定义事件特别有用

#### 移除事件处理程序
$(selector).off(event,childSelector,function,map)

* 同on相对,map对应on的map写法
* 是unbind,die,undelegate方法的代替
* 移除通过on添加的指定事件函数,方法有两种
    1. 通过命名函数off('click',changeSize).
    2. 通过添加事件命名空间 off('click.changeSize').

##### 如何在事件触发某一确定次数后移除事件处理程序
移除使用 event 对象的事件处理程序
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8"> 
<title>菜鸟教程(runoob.com)</title>
<script src="http://cdn.static.runoob.com/libs/jquery/1.10.2/jquery.min.js">
</script>
<script>
$(document).ready(function(){
	var x=0;
	$("p").click(function(event){
		$("p").animate({fontSize:"+=5px"});
		x++;
		if (x>=2)
		{
			$(this).off(event);
		}
	});
});
</script>
</head>
<body>

<p>点击这个段落放大字体，只会放大两次。</p>

</body>
</html>
```

#### hover
$(selector).hover(inFunction,outFunction)

等同于

$(selector).mouseover(inFunction).mouseout(outFunction)

如果只规定了一个函数,等同于

$(selector).on('mouseover mouseout',function)

