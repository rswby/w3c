## jQuery获得内容和属性

### 获得设置内容text(),html(),和val()
三个简单实用的用于DOM操作的jQuery方法

* text()-设置或返回所选元素的文本内容
* html()-设置或返回所选元素的内容(标记之间的所有内容)
* val()-设置或返回表单字段的值

三个函数都可以使用回调函数作为参数.回调函数有两个参数:

* 被选元素列表中当前元素的下标(从0开始)
* 当前元素内容的原始值(html()中的内容是元素内部的HTML文档,text()中的内容是元素内部的文本文档)
* 函数返回希望使用的字符串

### 获取设置属性attr(),prop()
attr用于设置获取元素起始标签中的属性,包括自定义属性
>attr依赖的是element对象的getAttribute和setAttribute方法,设置获取的属性只能是string类型

prop用于设置获取元素的固有属性
>像element[style],element[tagName],这种,而且属性值不一定是字符串类型

用prop()函数来设置获取checked,selected,disabled等属性,会返回布尔类型的值,而attr()函数会返回相应字符串(如果没设置的话会返回undefined)
>attr,prop方法的所有设置属性的操作针对的是当前jQuery对象所匹配的**每一个**元素;所有读取属性的操作只针对第一个匹配的元素

>都可以使用对象作为参数,来设置多个属性值

#### 心得:在对于HTML元素本身就带有的固定属性,在处理时,使用prop方法.对于自定义的DOM属性,在处理时使用attr方法

attr/prop在设置属性时,第二个参数也可以使用回调函数
>同获取设置元素内容的回调函数相同(内容是HTML文档)

### jQuery添加元素

#### 添加新的HTML内容
添加新内容的四个jQuery方法

* append()-在被选元素的结尾插入内容
* prepend()-在被选元素的开头插入内容
* after()-在被选元素之后插入内容
* before()-在被选元素之前插入内容
>参数可以是:HTML字符串,DOM元素(或数组),jQuery对象,函数(返回值)

>append(content1[,content2 [,contentN]])

>添加元素方法可以使用函数作为参数,第一个参数就是当前元素在匹配元素中的索引,第二个参数就是该元素当前的内部HTML内容(innerHTML),函数的返回值就是需要为该元素追加的内容(可以使HTML字符串,DOM元素,jQuery对象)

>只有**第一个参数**可以是回调函数

>如果追加的内容是当前页面中的某些元素,南无这些元素将**从原位置上消失**.简而言之,这是一个移动操作,而不是复制操作

#### 以上添加方法的返回值都是被选元素本身,便于链式操作,与之相对的是返回追加内容的方法

* appendTo()-用于将当前所有匹配的元素追加到指定元素内部的末尾位置
* prependTo()-用于将当前所有匹配的元素追加到指定元素内部的起始位置
* insertAfter()-用于将当前所有匹配元素插入到指定元素之后
* insertbefore()-用于将当前所有匹配的元素插入到指定元素之前
> jQueryObject.appendTo(target);

>target 指定的目标元素,可以是字符串(视为jQuery选择器或HTML内容字符串,jQuery自行判断),DOM元素,jQuery对象


#### 创建元素的三种方法
```js
1. var ele1 = '<p>Text.</p>';
2. var ele2 = $('<p>Text.</p>')//(或者)$('<p></p>').text('Text.')
3. var ele3 = document.createElement("p"); ele3.innerHTML = 'Text.';
```
>三种方式创建的元素都可以通过jQuery方法添加到HTML文档中

### jQuery删除元素
如果需要删除元素和内容,一般可以使用以下两个jQuery方法:

* remove()-从文档中移除匹配的元素(包括所有的子元素,与元素关联绑定的附加数据和事件处理器)
>jqueryObject.remove([selector]),删除被选元素中符合该选择器的元素,返回值当前jQuery元素本身

* detach()-从文档中移除匹配的元素,参数同上,不同之处在于不会移除于元素关联绑定的附加数据和事件处理器

* empty()-用于清空每个匹配元素内的所有内容,返回值为jQuery对象本身

>会删除HTML文档中的内容,但不会把匹配的元素怒从jQuery对象中删除,将来还可以再用这些元素

### jQuery操作css
* addClass()-向所有被选元素添加一个或多个类
* removeClass()-从所有被选元素删除一个或多个类
* toggleClass()-对所有被选元素进行添加/删除类的切换操作
* css()-设置或返回样式属性
>css()方法的所有**设置**操作针对的是当前jQuery对象所匹配的**每一个**元素,所有**读取**操作只针对**第一个**匹配的元素

#### jQueryObject.addClass(classNames)

* classNames String/Function类型 指定css类名,字符串可以通过空格分隔的方式来添加多个css类名.或者为返回css类名的函数
* 函数中的this指向执行元素对应的DOM元素
* addClass()还会为函数传入两个参数:第一个参数就是该元素在匹配元素中的索引,第二个参数就是该元素节点当前的'class'属性值.返回值就是为该元素添加的css类名(也可以使通过多个空格分隔表示多个css类名).
* addClass()方法只会在原有css类名的基础上,添加新的css类名,并不会覆盖掉之前已存在的

>removeClass参数同上

#### toggleClass(classNames[,switch])
* classNames参数同上
* switch Boolean类型,用于指定添加还是移除css类名.
>true相当于addClass() false相当于removeClass()

>toggleClass的classNames参数也可以是由空格分隔的多个css类名,特别的就是:**如果元素没有的类就会被添加,有的会被移除**

>removeClass()方法如果省略参数,就会移除所有类

#### css()函数由两种用法
jqueryObject.css(propertyName[,value]) 设置或返回css属性propertyName的值

jqueryObject.css(object) 以对象的形式同时设置多个属性的值
* propertyName String/Array类型,指定的css属性名称(用于设置或返回),或者css属性名称数组(仅用于返回,以对象的形式)
* value 可选/String/Number/Function类型 指定的属性值,或返回属性值的函数
* Object Object类型,封装多个键值对

>如果value是函数,css()会对匹配的每一个元素遍历执行该函数,函数中的this指向对应的DOM元素.

#### css中value为函数时函数的参数:
* 第一个参数就是该元素在匹配元素中的索引
* 第二个参数就是该元素css属性propertyName的当前值.
* 函数的返回值就是propertyName的设置值
* 在Object参数的键值对中的值value也可以是函数

### jQuery尺寸
jQuery提供多个处理尺寸的重要方法
* width()-设置或返回元素的宽度(不过扩内边距,边框,外边距).
* height()-设置或返回元素的高度(不过扩内边距,边框,外边距).
* innerWidth()-方法返回元素的宽度(包括内边距)
* innerHeight()-方法返回元素的高度(包括内边距)
* outerWidth()-返回元素的宽度(包括内边距和边框)
* outerHeight()-返回元素的高窟(包括内边距和边框)

>$(document).width/height()返回HTML文档的宽度和高度

>$(window).width/height()返回浏览器窗口的宽度和高度

