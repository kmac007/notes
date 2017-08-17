## 1. dom对象的innerText和innerHTML有什么区别？
- innerText返回元素内所包含的文本内容，在多层次的时候会按照元素的深浅顺序拼接其内容

- innerHTML返回的是元素的HTML结构

## 2. elem.children和elem.childNodes的区别？
elem.children与elem.childNodes 两者都是返回子节点； 前者返回的是节点集合 后者返回指定节点的子节点的节点集合 包括 元素 、文本 、注释 等

## 3. 查询元素有几种常见的方法？ES5的元素选择方法是什么?
```
常见的方法有： 

1、getElementById()
2、getElementsByTagName()
3、getElementsByClassName()
4、getElementsByName()

ES5的元素选择方法是：

1. querySelector()
2. querySelectorAll()
```

## 4. 如何创建一个元素？如何给元素设置属性？如何删除属性
```
var s = document.createElement("span") //创建元素
s.setAttribute("name","DK") // 设置属性
s.removeAttribute("name") //删除属性
```

## 5. 如何给页面元素添加子元素？如何删除页面元素下的子元素?
```
element.appendChild() 给element添加子元素
element.removeChild(child)删除element元素下的子元素child
```

## 6.  element.classList有哪些方法？如何判断一个元素的 class 列表中是包含某个 class？如何添加一个class？如何删除一个class?

```
add(class1, class2, ...) //在元素中添加一个或多个类名，如指定的类名已存在，则不会添加
contains(class) //返回布尔值，判断指定的类名是否存在
item(index) //返回类名在元素中的索引
remove(class1, class2, ...) //移除元素中的一个或多个类名，移除不存在的类名不会报错
toggle(class, true|false) //在元素中切换类名，第一个参数为要在元素中移除的类名，并返回false。如果类名不存在则会在元素中添加类名，并返回true。第二个是可选参数，是个布尔值用于设置元素是否强制添加或移除类，不管类名是否存在。
```
利用contains()判断是否包含某个class,用add()和remove()添加和删除class

## 7.  如何选中如下代码所有的li元素？ 如何选中btn元素？
```
<div class="mod-tabs">
   <ul>
       <li>list1<li>
       <li>list2<li>
       <li>list3<li>
   </ul>
   <button class="btn">点我</button>
</div>
```

选中所有的li:
```
document.getElementsByTagName('li')
document.querySelectorAll('li')
```
选中btn元素:
```
document.getElementsByTagName("button")[0]
document.getElementsByClassName("btn")[0]
document.querySelector(".btn")
doucument.querySelectorAll(".btn")[0]
```