# 1. class和id的使用场景？
```
class 用于选择页面上带相同类属性的元素，可以有多个
id    它是唯一的，选择页面上唯一带有相同id属性的元素
```
# 2. CSS选择器常见的有几种？
    1. 元素选择器 如：p, h1, span
    2. 类选择器 .class-name
    3. id选择器 #id-name
    4. 通配选择器 *
    5. 属性选择器 E[attr], E[attr=value]等
    6. 组合选择器  E,F 多元素选择器
                  E F 后代选择器
                  E>F 子元素选择器
                  E+F 相邻兄弟选择器
                  E~F 普通相邻选择器
    7. 伪类选择器 E:first-child, E:hover, E:nth-child(n)等
    8. 伪元素选择器 E::before, E::after
# 3. 选择器的优先级是怎样的?对于复杂场景如何计算优先级？
要了解选择器的优先级，必须先知道CSS的特殊性，特殊性即CSS的优先级，而特殊性值的决定了CSS的优先级。
如下：
```
选择器的特殊性值表述为4个部分，用0,0,0,0表示。
1. ID选择器的特殊性值，加0,1,0,0。
2. 类选择器，属性选择器的特殊性值，加0,0,1,0。
3. 元素和伪元素的特殊性值, 加0,0,0,1。
4. 通配选择器*对特殊性没有贡献，即0,0,0,0。
5. 最后一个比较特殊一个标志!important（权重），它没有特殊性值，但它的优先级是最高的，可以用1,0,0,0表示。
```
复杂场景下，如：
```
<body>
  <div class="demo">
    <a href="#">demo</a>
  </div>
</body>
<style>
  div a {
    color: blue; /*这里的优先级为0,0,0,2*/
  }
  .demo a {
    color: red; /*这里的优先级为0,0,1,1 故这个优先级较高*/
  }
</style>
```
再者，1,0,0,0是要比0,99,99,99优先级要高的，因此我们可以得出常见的选择器的优先级为：
  1. !important: 在属性后面使用 !important 会覆盖页面内任何位置定义的元素样式
  2. 内联样式
  3. ID选择器
  4. 类选择器，属性选择器
  5. 元素和伪元素选择器
  6. 通配选择器
# 4.a:link, a:hover, a:active, a:visited 的顺序是怎样的？ 为什么？
>css会先查看规则的权重（!important），加了权重的优先级最高，当权重相同的时候，会比较规则的特殊性，根据（3）的优先级计算规则决定哪条规则起作用，当特殊性值也一样的时候，css规则会按顺序排序，后声明的规则优先级高

一个链接只有访问和未访问的状态，因此 :link 与 :visited 谁前谁后都可以。要保证点击后即active有样式变化，:active必须要覆盖:hover，因此:active要在:hover之后。要保证鼠标滑过有效果，:hover必须要在:link和:visited后。因此一般的顺序为：
  1. a:link
  2. a:visited
  3. a:hover
  4. a:active

有人将这个**LVHT**(LoVe HAte)称为“爱恨原则”。

# 5. 以下选择器分别是什么意思?
```
#header{             id为header的元素
}               
.header{             class为header的元素    
}
.header .logo{       class为header的所有class为logo的后代元素
}
.header.mobile{       class同时包含header和mobile的元素
}
.header p, .header h3{   class为header的后代元素中所有的p和h3元素
}
#header .nav>li{    id为header后代元素中class为.nav的子元素li
}
#header a:hover{  id为header后代元素中a的伪类:hover
}
#header .logo~p{  id为header的后代元素中与class为logo同级的p元素
}
#header input[type="text"]{ 
}  id为header后代中type="text"的input的元素
```
- 列出你知道的伪类选择器
   1. :hover
   2. :link
   3. :visited
   4. :active
   5. :focus
   6. :checked
   7. :enabled
   8. :first-of-type
   9. :first-child
   10.:nth-child(n)
- div:first-child和div:first-of-type的作用和区别

  - div:first-child 指的是当前元素父元素下的第一个子元素
  - div:first-of-type指的是当前元素父元素下拥有相同标签的第一个子元素
- 运行如下代码，解析下输出样式的原因。
```
<style>
.item1:first-child{
  color: red;
}
.item1:first-of-type{
  background: blue;
}
</style>
 <div class="ct">
   <p class="item1">aa</p>
   <h3 class="item1">bb</h3>
   <h3 class="item1">ccc</h3>
 </div>
```
原因是: .item1:first-child匹配了类为.item1的父元素的第一个子元素;.item:first-of-type匹配了类为.item1的父元素下各种相同标签的第一个子元素，即<p>和<h3>的第一个。