### 实现函数调用自己的两种方法
```js
function (){
  argument.callee();
}//第一种 使用argument.callee指向当前执行的函数
function aa(){
  aa();
}//直接使用命名函数
//两种方式都可以在回调函数中使用
```

### css 百分比值的属性
可以使用百分比的样式属性:
* 定位:top left bottom right
* 盒模型:height width margin padding
* 背景:background-position background-size(css3)
* 文本:text-indent
* 字体:font-size

>其中定位和背景定位原点都在左上方 其中left向左移动第一个块级父类元素width的相对距离,top向下移动第一个块级父元素高度的相对距离,right/bottom与之相反

>盒模型和text-indent中都是与第一个块级父元素的内容宽高相关,其中只有height属性与第一个块级父元素的height相关,其它都与它的width属性相关

>font-size第一个父级元素的font-size的相对值

#### $ele.focus() 相应的jQuery元素获得焦点

### css visibility属性

* visible 默认值 元素可见
* hidden 元素不可见(仍会占据空间)
* collapse === hidden 在表格元素中使用 隐藏表格的一部分 但不会影响表格布局 
