### 1. Ajax 是什么？有什么作用？
> AJax为“Asynchronous JavaScript and XML”（异步的JavaScript与XML技术）。

作用是：无需重新加载页面即可与服务器交换数据。

AJAX 是一种用于创建快速动态网页的技术。
通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。这种技术带来了不错的用户体验。

而传统的网页（不使用 AJAX）如果需要更新内容，必须重载整个网页页面。

### 2. 前后端开发联调需要注意哪些事情？后端接口完成前如何 mock 数据？
前后端开发联调需要注意的事情：
- 约定数据：需要传输的数据及其数据类型
- 约定接口：确定接口名称及请求响应的格式，请求的参数名称、响应的数据格式
- 根据这些约定整理成接口文档

如何mock数据：参照接口文档，使用假数据来验证接口和页面响应的正确性。
- 可以使用mock工具，如sever-mock来mock数据。
- 也可以通过搭建php本地服务器，php写脚本提供临时数据。
- 也可以直接将mock数据写入代码中，但缺点是联调需要做的改动较多，接口文档变化需要手动刷新。
### 3. 点击按钮，使用 ajax 获取数据，如何在数据到来之前防止重复点击?
可以使用状态锁，判断数据是否到来。状态锁初始值为true，当发起一次请求后状态锁值变为false，等到状态码变为4即数据接收完毕，状态锁值变为true。
```
var isDataArrive = true //默认为true
var btn = document.getElementById("getData")
btn.addEventListener('click', function () {
  if (!isDataArrive) { //如果数据没有到来
    return
  }
  var xhr = new XMLHttpRequest()
  xhr.onreadystatechange = function () {
    if (xhr.readyState === 4) {
      if (xhr.status === 200 || xhr.status === 304) {
        console.log(JSON.parse(xhr.responseText))
      }
      isDataArrive = true // 收到响应
    }
  }
  xhr.open()
  xhr.send()
  isDataArrive = false //停止再次发送请求
})
```
### 4. 封装一个 ajax 函数，能通过如下方式调用。后端在本地使用server-mock来 mock 数据
```
    function ajax(opts) {
      var xhr = new XMLHttpRequest()
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4) {
          if (xhr.status === 200 || xhr.status === 304) {
            var results = JSON.parse(xhr.responseText)
            opts.success(results)
          } 
          if(xhr.status === 404){
            opts.error()
          }
        }
      }
      var dataString = ''
      for (var key in opts.data) {
        dataString += key + "=" + opts.data[key] + "&"
      }
      dataString = dataString.substr(0, dataString.length - 1)
      if (opts.type.toLowerCase() === "get") {
        xhr.open("get", opts.url + "?" + dataString, true)
        xhr.send()
      }
      if (opts.type.toLowerCase() === "post") {
        xhr.open("post", opts.url, true)
        xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded")
        xhr.send(dataString)
      }
    }
```
### 5. 实现加载更多的功能，后端在本地使用server-mock来模拟数据
前端部分
```
<!doctype html>
<html>

<head>
  <meta charset="utf-8">
  <title>加载更多</title>
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
    var btn = document.getElementById("btn")
    var ct = document.getElementById("ct")
    var pageIdx = 2
    var isDataArrive = true
    btn.addEventListener('click', function (e) {
      e.preventDefault()
      if (!isDataArrive) {
        return
      }
      isDataArrive = false
      ajax({
        url: '/loadMore', //接口地址
        type: 'get',
        data: {
          index: pageIdx,
          length: 6
        },
        success: function (results) {
          renderPage(results)
        },
        error: function () {
          console.log("error")
        }
      })
    })

    function renderPage(news) {
      var fragment = document.createDocumentFragment()
      for (var i = 0; i < news.length; i++) {
        var node = document.createElement("li")
        node.innerText = news[i]
        fragment.appendChild(node)
      }
      ct.appendChild(fragment)
    }

    function ajax(opts) {
      var xhr = new XMLHttpRequest()
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4) {
          if (xhr.status === 200 || xhr.status === 304) {
            var results = JSON.parse(xhr.responseText)
            opts.success(results)
            pageIdx += 6
          } else {
            opts.error()
          }
          isDataArrive = true
        }
      }
      var dataStr = ''
      for (var key in opts.data) {
        dataStr += key + "=" + opts.data[key] + "&"
      }
      dataStr = dataStr.substr(0, dataStr.length - 1)
      if (opts.type.toLowerCase() === "get") {
        xhr.open("get", opts.url + "?" + dataStr, true)
        xhr.send()
      }
      if (opts.type.toLowerCase() === "post") {
        xhr.open("post", opts.url, true)
        xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded")
        xhr.send(dataStr)
      }
    }
  </script>

</body>

</html>
```
后端部分，采用server-mock
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