### 1. jQuery中，$(document).reday()是什么意思？
意思是等DOM结构加载完毕后再执行函数，与原生JavaScript的window.onload不同的是，window.onload必须要等到页面内包括图片的所有元素加载完毕后才能执行。而$(document).reday()仅需DOM加载完毕。

另外$(document).reday()可以简写为：
```
1. $().ready(function)
2. $(function)
```

### 2. $node.html()和$node.text()的区别?
- $node.html(): 返回节点下的html内容（包括html标签）
- $node.text()：返回节点下的文本内容（不包括html标签）

### 3. $.extend 的作用和用法? 
将两个或多个对象的内容合并到第一个对象。

用法：
```
jQuery.extend(target[,object1] [,objectN])
```
同时$.extend还支持深浅拷贝，如:
```
jQuery.extend([deep], target, object1 [, objectN])
//其中boolean值[deep]为true为深拷贝，为false时浅拷贝
```

### 4. jQuery 的链式调用是什么？
jQuery对象调用jQuery方法后可以直接继续调用其他方法。如：
```
$node.css("width","100px").css("height","100px").css("background","red");
```

### 5. jQuery 中 data 函数的作用
data()函数用于在当前jQuery对象所匹配的元素上存取数据。

通过data()函数存取的数据都是临时数据，一旦页面刷新，之前存放的数据都将不复存在。

该函数属于jQuery对象(实例)。如果需要移除通过data()函数存放的数据，可用removeData()函数。

用法：
```
//用法一：
$.data( [key [, value] ] )
//用法二:
$.data( object )
```

### 6. 写出以下功能对应的 jQuery 方法：
- 给元素 $node 添加 class active，给元素 $noed 删除 class active
```
$node.addClass('active')  //添加
$node.removeClass('active')  //删除
```
- 展示元素$node, 隐藏元素$node
```
$node.show()  //展示
$node.hide()  //隐藏
```
- 获取元素$node 的 属性: id、src、title， 修改以上属性
```
$node.attr('id')  //获取
$node.attr('id','value')  //修改
$node.attr('src')  //获取
$node.attr('src','value')  //修改
$node.attr('title')  //获取
$node.attr('title','value')  //修改
```
- 给$node 添加自定义属性data-src
```
$node.attr('data-src','value')
```
- 在$ct 内部最开头添加元素$node
```
$ct.prepend($node)
```
- 在$ct 内部最末尾添加元素$node
```
$ct.append($node)
```
- 删除$node
```
$node.remove()
```
- 把$ct里内容清空
```
$ct.empty()
```
- 在$ct 里设置 html <div class="btn"></div>
```
$ct.html(<div class="btn"></div>)
```
- 获取、设置$node 的宽度、高度(分别不包括内边距、包括内边距、包括边框、包括外边距)
```
$node.width()  //仅包括内容
$node.height()  //仅包括内容
$node.width(100)  //设置仅包括内容的宽度为100px

$node.innerWidth()  //包括内容和内边距
$node.innerHeight()  //包括内容和内边距
$node.innerWidth(100)  //设置

$node.outerWidth()  //包括内容，内边距，边框宽度
$node.outerHeight()  //包括内容，内边距和边框高度
$node.outerWidth()  //设置

$node.outerHeight(true)  //包括内容，内边距，边框，外边距宽度
$node.outerWidth(true)
```
- 获取窗口滚动条垂直滚动距离
```
$(window).scrollTop()
```
- 获取$node 到根节点水平、垂直偏移距离
```
$node.offset()
```
- 修改$node 的样式，字体颜色设置红色，字体大小设置14px
```
$node.css('color','red').css('font-size','14px')
```
- 遍历节点，把每个节点里面的文本内容重复一遍
```
$node.each(function(){
  console.log($(this).text());
})
```
- 从$ct 里查找 class 为 .item的子元素
```
$ct.find('.item')
```
- 获取$ct 里面的所有孩子
```
$ct.children()
```
- 对于$node，向上找到 class 为'.ct'的父亲，在从该父亲找到'.panel'的孩子
```
$node.parents('.ct').find('.panel')
```
- 获取选择元素的数量
```
$node.length
```
- 获取当前元素在兄弟中的排行
```
$node.index()
```
### 7. 实现效果
[预览](http://js.jirengu.com/xeratorese)

[代码](http://js.jirengu.com/xeratorese/edit?html,output)

### 8. 用 jQuery ajax 实现如下效果。`当点击加载更多会加载数据展示到页面
前端部分
```
<!doctype html>
<html>

<head>
  <meta charset="utf-8">
  <title>加载更多</title>
  <script src="http://apps.bdimg.com/libs/jquery/2.1.4/jquery.js"></script>
  <style>
    ul,
    li {
      margin: 0;
      padding: 0;
    }

    #ct li {
      width: 100%;
      list-style: none;
      padding: 10px;
      margin-top: 10px;
      cursor: pointer;
      border: 1px solid #ccc;
    }

    #ct li:hover {
      background-color: green;
      color: #fff;
    }

    #btn {
      border-radius: 5px;
      text-align: center;
      width: 80px;
      padding: 10px;
      margin: 10px auto;
      border: 1px solid palevioletred;
      color: palevioletred;
      cursor: pointer;
    }
  </style>
</head>

<body>
  <ul id="ct">
    <li>内容1</li>
    <li>内容2</li>
  </ul>
  <div id="btn">
    加载更多
  </div>
  <script>
    var $btn = $("#btn")
    var $ct = $("#ct")
    var pageIdx = 3
    var isDataArrive = true
    $btn.on('click', function () {
      if (isDataArrive === false) {
        return
      }
      isDataArrive = false
      $.ajax({
        url: '/loadMore',
        method: 'GET',
        data: {
          index: pageIdx,
          length: 6
        }
      }).done(function (ret) {
        renderPage(ret)
        isDataArrive = true
      }).fail(function () {
        console.log("error")
        isDataArrive = true
      })
    })

    function renderPage(ret) {
      var html = ''
      pageIdx += 6
      $.each(ret, function (index, value) {
        html += '<li>' + value + '</li>'
      })
      $ct.append(html)
    }
  </script>

</body>

</html>
```

后端部分 router.js
```
//加载更多
router.get('/loadMore', function (req, res) {
  var curIdx = req.query.index
  var len = req.query.length
  var data = []
  for (var i = 0; i < len; i++) {
    data.push('内容' + (parseInt(curIdx) + i))
  }
  res.send(data)
})
```
