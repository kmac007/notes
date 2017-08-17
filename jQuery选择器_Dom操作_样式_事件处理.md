### 1. 说说库和框架的区别？
- 库：其实就是对原生代码进行了一个完整的封装，通过封装，解决了许多兼容性的问题。用户可以简易的调用API来构建项目，而不需要考虑许多兼容性的问题。
- 框架：会基于自身的特点向用户提供一套完整的模版，用户需要按照框架的规范来构建项目。   
- 类比来说：前端库就像我们家里的工具箱，里面有锯子、锤子等工具，需要时，我们从工具箱中取工具；而框架像是房子的骨架，我们通过给房子添加建材等，使其完整。

### 2. jquery 能做什么？
jQuery是JavaScript的一个类库，仍是js，jQuery主要用来简化原生js的各种操作以及解决各种浏览器之间的兼容性。jQuery能办到的事情原生js都能办到。
通常来说jQuery有以下几个功能：
1. 方便快捷获取DOM元素
2. 动态修改页面样式、动态改变DOM内容
3. 解决跨浏览器兼容
4. 响应用户的交互操作
5. 为页面添加动态效果
6. 统一Ajax操作
7. 简化常见的JavaScript操作

### 3. jquery 对象和 DOM 原生对象有什么区别？如何转化？
- DOM原生对象：
  - 通过原生JavaScript获得的对象
  - 只能使用DOM的属性和方法
- jQuery对象：
  - 是通过jQuery包装DOM对象后产生的对象
  - 只能使用jQuery的属性和方法  

1. DOM对象转jQuery对象：  
```
$(document.getElementById("btn")  //通过$()将DOM对象包裹起来转换成jQuery对象
```

2. jQuery对象转DOM对象
如：
```
<ul class="ct">
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
</ul>
```
- 通过类数组下标方式转换成DOM对象
```
$(".ct>li")[0]  
$(".ct>li").eq(0)[0]
```
- 通过get方法
```
$(".ct>li").get(0)
```

### 4. jquery中如何绑定事件？bind、unbind、delegate、live、on、off都有什么作用？推荐使用哪种？使用on绑定事件使用事件代理的写法？
使用bind,live,delegate,on这些绑定事件的方法来绑定事件，而从jQuery1.7开始，.on()方法是绑定数据的首选方法：
如：
```
$("#btn").on("click",function(){
  //do something  
})
```
#### bind:  
bind()作用就是在选择到的元素上绑定特定事件类型的监听函数。已于jQuery3.0弃用。

语法：$(selector).bind(event,data,function)

参数：  
event: 必需。规定添加到元素的一个或多个事件。由空格分隔多个事件。必须是有效事件。  
data：可选。规定传递到函数的额外数据。  
function：必需。规定当事件发生时执行的函数。

#### unbind:   
bind()的反向操作，从每个匹配的元素中删除绑定的事件。jQuery3.0中已弃用，用off()代替。若没有参数，则删除所有绑定的事件。

#### delegate:   
delegate()方法为指定的元素（属于被选元素的子元素）添加一个或多个事件处理程序，并规定当这些事件发生时运行的函数。
使用 delegate() 方法的事件处理程序适用于当前或未来的元素（比如由脚本创建的新元素）。jQuery 3.0中已弃用此方法，用 on()代替。

语法：$(selector).delegate(childSelector,event,data,function)

参数：  
childSelector：必需。规定要添加事件处理程序的一个或多个子元素。  
event：必需。规定添加到元素的一个或多个事件。由空格分隔多个事件值。必须是有效的事件。  
data:可选。传递到该函数的额外参数  
function:必需。当事件发生时，运行的函数

#### live：

live()，从 jQuery 1.7 开始，不再建议使用 .live() 方法，在版本 1.9 中被移除。请使用 .on() 来添加事件处理。使用旧版本的用户，应该优先使用 .delegate() 来替代 .live()。添加一个或多个事件处理程序到当前或未来的被选元素。

语法：$(selector).live(event,data,function)

参数:  
event：必需。规定添加到元素的一个或多个事件。由空格分隔多个事件值。必须是有效的事件。  
data:可选。传递到该函数的额外参数  
function:必需。当事件发生时，运行的函数

#### on：（首选方法）
on() 方法在被选元素及子元素上添加一个或多个事件处理程序。

自 jQuery 版本 1.7 起，on() 方法是 bind()、live() 和 delegate() 方法的新的替代品。该方法给 API 带来很多便利，我们推荐使用该方法，它简化了 jQuery 代码库。

语法: $(selector).on(event,childSelector,data,function,map)

参数：  
event:必需。规定要从被选元素移除的一个或多个事件或命名空间。由空格分隔多个事件值。必须是有效的事件  
data:可选。规定只能添加到指定的子元素上的事件处理程序（且不是选择器本身，比如已废弃的 delegate() 方法）。  
function:可选。规定当事件发生时运行的函数。  
map:规定事件映射 ({event:function, event:function, ...})，包含要添加到元素的一个或多个事件，以及当事件发生时运行的函数。

#### off：

off() 方法通常用于移除通过 on() 方法添加的事件处理程序。  
自 jQuery 版本 1.7 起，off() 方法是 unbind()、die() 和 undelegate() 方法的新的替代品。该方法给 API 带来很多便利，我们推荐使用该方法，它简化了 jQuery 代码库。

#### 使用on绑定事件使用事件代理的写法：
```
//html 
<ul class="ct">
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
</ul>
//js
    $(".ct").on('click', 'li', function () {
      console.log($(this).text())
    })
```

### 5. jquery 如何展示/隐藏元素？
展示元素：
```
.show( duration [, easing ] [, complete ] )
```
隐藏元素：
```
.hide([duration ] [,easing ] [,complete ])
```
没有参数时直接等同于直接设置选中元素display属性，如：
```
.css('display', 'none')
```

.toggle( [duration ] [, easing ] [, complete ] )  
用来切换元素的隐藏、显示，类似toggleClass

参数：

1. duration：动画持续的时间。一个字符串或数字决定动画运行的时间。（注：默认值为"400毫秒"）
2. easing：表示过渡使用哪种缓冲函数，jQuery自身提供"linear"和"swing",默认为"swing"
3. complete：在动画完成时执行的函数

### 6. jquery 动画如何使用？
```
.animate( properties [, duration ] [, easing ] [, complete ] )
```
properties是一个CSS属性和值的对象,动画将根据这组对象移动。 如：

```
$('#clickme').click(function() {
  $('#book').animate({
    opacity: 0.25,
    left: '+=50',
    height: 'toggle'
  }, 5000, function() {
    // Animation complete.
  });
});
```
**.animate( properties, options )**

options是一组包含动画选项的值的集合。 常用的选项:

1. duration (default: 400)：一个字符串或者数字决定动画将运行多久。默认值: "normal"， 三种预定速度的字符串("slow", "normal", 或 "fast"或表示动画时长的毫秒数值(如：1000) ）
2. easing (default: swing)：一个字符串，表示过渡使用哪种缓动函数。jQuery自身提供"linear" 和 "swing"，其他效果可以使用jQuery Easing Plugin插件
3. step：每个动画元素的每个动画属性将调用的函数。这个函数为修改Tween 对象提供了一个机会来改变设置中得属性值。
4. complete：在动画完成时执行的函数

### 7. 如何设置和获取元素内部 HTML 内容？如何设置和获取元素内部文本？
```
.html([string])
用于获取/修改元素的innerHTML
无参数时，返回元素的innerHTML
有参数时，修改元素的innerHTML

.text([string])
无参数时，获取元素的内部文本
有参数时，将元素内部文本设置为参数值
```

### 8. 如何设置和获取表单用户输入或者选择的内容？如何设置和获取元素属性？

1. 设置和获取表单用户输入和选择内容：使用val()方法
```
$("input").val() //获取input中的内容
$("input").val("name") //设置input中的内容
```
2. 设置和获取元素属性：使用attr()方法
```
$("#img").attr('src') //获取id为img元素的src属性值
$("#img").attr('src','kmac007.com/logo.jpg') //设置id为img元素的src属性值为kmac007.com/logo.jpg
```
### 9. 使用 jquery实现如下效果
[效果9](https://kmac007.github.io/demos/jQuery/side-nav/index.html)

### 10. 使用 jquery 实现如下效果
[效果10](https://kmac007.github.io/demos/jQuery/tab/tab.html)

### 11. 使用 jquery 实现如下效果
[效果11](https://kmac007.github.io/demos/jQuery/add/add.html)