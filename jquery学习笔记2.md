## jQuery效果
### 隐藏和显示
$(selector).hide(speed,callback);

$(selector).show(speed,callback);

* speed 可选.规定显示/隐藏的速度.可以取以下值'slow','fast'或毫秒
* callback 可选.规定显示/隐藏完成后所执行的函数
>hide 透明度和height同时减少到0,然后display:none.
>show display:原来的值,透明度和height同时恢复到原来的值.

$(selector).toggle(speend,callback)

显示被隐藏的元素,并隐藏已显示的元素
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script src="//libs.baidu.com/jquery/1.10.2/jquery.min.js">
</script>
<script>
$(document).ready(function(){
  $("button:eq(0)").click(function(){
    $("p").toggle("slow");
  }).next().click(function(){
  	var p = $('p');
	if(p.is(':hidden')){
		p.show('slow');
	}else{
		p.hide('slow');
	}
  })
});
</script>
</head>
<body>

<button>toggle</button>
<button>hide/show</button>
<p>这是一个文本段落。</p>
<p>这是另外一个文本段落。</p>
</body>
</html>
```

### 淡入淡出
$(selector).fadeIn(speed,callback);

用于淡入已隐藏的元素

$(selector).fadeOut(speed,callback);

用于淡出可见元素

$(selector).fadeToggle(speed,callback);

如果元素已经淡出,则fadeToggle()方法会向元素添加淡入效果

如果元素已经淡入,则fadeToggle()方法会向元素添加淡出效果

$(selector).fadeTo(speed,opacity,callback);

* opacity 必需.规定淡入淡出的最终透明度(值介于0与1之间).
>允许元素渐变为给定的透明度
#### 淡出会渐变减少透明度,当透明度为0时,设置display:none
#### 淡入会先display:原来的值,然后逐渐恢复透明度

### 滑动
$(selector).slideDown(speed,callback);
>用于向下滑动元素

$(selector).slideUp(speed,callback);
>用于向上滑动元素

$(selector).slideToggle(speed,callback);
>用于slideDown()方法和slideUp()方法的切换

### 动画
$(selector).animate({parameters},speed,easing,callback);
* parameters 必需.定义形成动画的css属性
* speed,callback 可选.同上
* easing 可选. 规定动画在不同点中元素的速度.默认值'swing'.可能的值:
    * 'swing'-在开头/结尾移动慢,在中间移动快
    * 'linear'-匀速移动

该方法通过css样式将元素从一个状态改为另一个状态,css属性值是逐渐改变的,这样就可以创建动画效果

只有数字值可创建动画.字符串值无法创建动画,颜色动画不包含在jQuery核心库中
>使用'+='或'-='来创建相对动画

>如果对元素的位置进行操作,首先要设置元素的position属性

>使用animate操作css属性时,所有的属性必须使用驼峰命名法

>animate方法中css属性有预设值'show','hide','toggle'

#### 越过队列
所有的动画效果都可以连缀,就形成了队列

一种情况就是多种动画效果需要同时出现,但是所有的动画效果的动画时间不同

这种情况下需要animate的第二种参数形式

$(selector).animate({parameters},{options})

* parameters 同上.
* options 可选. 规定动画的额外选项
    * duration:设置动画的速度
    * easing:规定要使用的easing函数
    * complete:规定动画完成后要执行的函数
    * step:规定动画的每一帧完成后要执行的函数
    * queue:布尔值.指示是否在效果队列中放置动画,如果为false,则动画立即开始
    * specialEasing:来自parameters参数的一个或多个css属性的映射,以及它们对应的easing值


#### 实例
#### 在元素向右移动过程中,先增大字体,在增大height
>通过queue:false使动画越过队列
```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <script src="jquery.js">
    </script>
    <script>
    $(document).ready(function() {
        const fontsize = $('div').css('fontSize');
        const height = $('div').css('height');
        var div = $('div');
        alert(fontsize);
        $("#start").click(function() {

            $("div").animate({ left: '100px' }, 2000, 'linear');
            //animate({fontSize:'3em'},1000);
            $("div").animate({ fontSize: '3em' }, {
                duration: 1000,
                queue: false,
                easing: 'linear',
                complete: function() {
                    div.animate({ height: '400px' }, {
                        duration: 1000,
                        easing: 'linear',
                        queue: false,
                    });
                }
            });

        });
        $('#reset').click(function() {

            $('div').css({
                left: 0 + 'px',
                fontSize: fontsize,
                height: height
            })
        });

        $("#stop").click(function() {
            $("div").stop();
        });

        $("#stop2").click(function() {
            $("div").stop(true);
        });

        $("#stop3").click(function() {
            $("div").stop(true, true);
        });

    });
    </script>
</head>

<body>
    <button id='reset'>重置</button>
    <button id="start">开始</button>
    <button id="stop">停止</button>
    <button id="stop2">停止所有</button>
    <button id="stop3">停止动画，但完成动作</button>
    <p>点击 "开始" 按钮开始动画。</p>
    <p>点击 "停止" 按钮停止当前激活的动画，但之后我们能再动画队列中再次激活。</p>
    <p>点击 "停止所有" 按钮停止当前动画，并清除动画队列，所以元素的所有动画都会停止。</p>
    <p>点击 "停止动画，但完成动作" 快速完成动作，并停止它。</p>
    <div style="background:#98bf21;height:100px;width:200px;position:absolute;">HELLO</div>
</body>

</html>
```
#### step
参数step:规定每个动画的每一步完成之后要执行的函数
>要特别特别注意的是：在animate方法中，每一步具体是怎么分解的，不是由我们设定的CSS属性值和动画时长来决定的，是由系统来决定的。

step:function(now,fx){};

* now: 是当前动画正在改变的属性的实时值
* fx: jQuery.fx原型对象的一个引用,其中包含了多项属性,比如:
    * 执行动画的元素: fx.elem;
    * 动画正在改变的属性: fx.prop;
    * 正在改变属性的当前值: fx.now;
    * 正在改变属性的结束值: fx.end;
    * 正在改变属性的开始值: fx.start;
    * 正在改变属性的单位: unit;
    * 动画当前状态在整个动画过程中的百分比: fx.pos,是从0到1的一个小数
以上属性都可以改变
#### 属性之间的关系
fx.now = (fx.end - fx.start) * fx.pos + fx.start

倘若修改了fx.end的话，now值有可能会改变，就会造成中途动画突然抽搐一下的情况。所以需要修改fx.start的值。

fx.start = (fx.start - fx.pos * (fx.start - (fx.end - end1)))/(1 - fx.pos)

提供了在动画执行过程中,中途修改动画的机制.

### 停止动画
$(selector).stop(stopAll,goToEnd)

* stopAll 可选. 规定是否应该清除动画队列.默认为false,即仅停止活动的动画,允许任何排入队列的动画向后执行
* goToEnd 可选,规定是否立即完成当前动画.默认为false.

#### 执行完当前动画,删除后续的动画队列
$(selector).clearQueue([queueName])

* queueName 默认为'fx'
>'fx'标准动画队列

与stop(true,false)的不同是不会停止当前动画
#### 跳过执行动画,直接到达动画队列的最终值
$('selector').finish([queueName]);

.stop(false,true) 停止当前动画,到达当前动画的css值,执行后续动画,相当于一步步快进

.stop(true,false) 彻底停止动画 效果等同于 .clearQueue().stop()
>.stop().clearQueue()不行,因为.stop()之后会立即执行队列的下一个动画函数,clearQueue()只能清除下一个队列之后的队列

.finish 直接动画队列的css最终值,一步到结束
 
.stop(true,true) 立即达到当前动画的css值,然后停止 效果等同于.clearQueue().finish()

.stop()/stop(false,false) 停止当前动画,立即执行后续动画 


.clearQueue()执行完当前动画,停止

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>finish demo</title>
  <style>
  .box {
    position: absolute;
    top: 10px;
    left: 10px;
    width: 15px;
    height: 15px;
    background: black;
  }
  #path {
    height: 244px;
    font-size: 70%;
    border-left: 2px dashed red;
    border-bottom: 2px dashed green;
    border-right: 2px dashed blue;
  }
  button {
    width: 12em;
    display: block;
    text-align: left;
    margin: 0 auto;
  }
  </style>
  <script src="https://code.jquery.com/jquery-1.10.2.js"></script>
</head>
<body>
 
<div class="box"></div>
<div id="path">
  <button id="go">Go</button>
  <br>
  <button id="bstt" class="b">.stop( true,true )</button>
  <button id="bcf" class="b">.clearQueue().finish()</button>
  <br>
  <button id="bstf" class="b">.stop( true, false )</button>
  <button id="bcs" class="b">.clearQueue().stop()</button>
  <br>
  <button id="bsff" class="b">.stop( false, false )</button>
  <button id="bs" class="b">.stop()</button>
  <br>
  <button id="bsft" class="b">.stop( false, true )</button>
  <br>
  <button id="bf" class="b">.finish()</button>
</div>
 
<script>
var horiz = $( "#path" ).width() - 20,
  vert = $( "#path" ).height() - 20;
 
var btns = {
  bstt: function() {
    $( "div.box" ).stop( true, true );
  },
  bs: function() {
    $( "div.box" ).stop();
  },
  bsft: function() {
    $( "div.box" ).stop( false, true );
  },
  bf: function() {
    $( "div.box" ).finish();
  },
  bcf: function() {
    $( "div.box" ).clearQueue().finish();
  },
  bsff: function() {
    $( "div.box" ).stop( false, false );
  },
  bstf: function() {
    $( "div.box" ).stop( true, false );
  },
  bcs: function() {
    $( "div.box" ).clearQueue().stop();
  }
};
 
$( "button.b" ).on( "click", function() {
  btns[ this.id ]();
});
 
$( "#go" ).on( "click", function() {
  $( ".box" )
    .clearQueue()
    .stop()
    .css({
      left: 10,
      top: 10
    })
    .animate({
      top: vert
    }, 3000 )
    .animate({
      left: horiz
    }, 3000 )
    .animate({
      top: 10
    }, 3000 );
});
</script>
 
</body>
</html>
```
### $(selector).promise().done(callback)
当集合的所有元素动画执行完毕后,执行回调函数



### 延迟动画
在动画队列中添加delay(speed[,queueName]),队列的后续动画会延迟speed的时间执行

* speed 这里不是动画执行时间,而是延迟时间
* queueName 包含队列名称的字符串,默认为'fx'

### 在队列中添加回调函数
在动画队列中有两种方式使用回调函数
1. 直接在动画函数后面的callback参数中添加回调函数
2. 通过连缀.queue(function(next){/*执行*/ next()})的方法

没什么用,$ele.queue('fx'); 返回元素当时的动画队列长度

### 总结
* 所有的动画默认为400毫秒，指定的速度中'slow'为600毫秒,'fast'为400毫秒
* 动画的回调函数中的this被设置为执行动画的DOM元素
* jQuery.fx.off属性,默认为false属性,如果设置为true,所有动画方法将在调用时立即将元素设置为最终状态,而不是显示动画效果.





