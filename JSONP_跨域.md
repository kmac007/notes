### 1. 什么是同源策略？
浏览器出于安全方面的考虑，只允许与本域下的接口交互。不同源的客户端脚本在没有明确授权的情况下，不能读写对方的资源。
所谓的同源策略指的是三个相同：
- 协议相同
- 域名相同
- 端口相同

例如:

https://jscode.me/t/jsonp-/216 这个网址，协议是https，域名是jscode.me，端口是80（默认端口可以省略）
对于如下网址：
- http://jscode.me/t/jsonp-/216 不同源(协议不同)
- https://jscode.me/t/jsonp-/215 同源
- https://www.jscode.me/t/jsonp-/216 不同源（域名不同）
- https://jscode.me:8080/t/jsonp-/216 不同源（端口不同）

同源策略的目的，是为了保证用户信息的安全，防止恶意的网站窃取数据。

### 2. 什么是跨域？跨域有几种实现形式?
跨域指的是，突破同源策略，不同源之间进行数据传输或通信。

跨域有如下几种实现形式：
1. JSONP
2. CORS：跨域资源共享（Cross-origin resource sharing）
3. document.domain
4. window.postMessage
等

### 3. JSONP 的原理是什么?
在js中我们直接用XMLHttpRequest请求不同域上的数据时，是不可以的。但是在页面上引入不同域上的js文件却是可以的，JSONP正是利用这个特性来实现的。

JSONP的原理是，在网页中添加一个<script>元素，向服务器请求JSON数据，这种做法不受同源政策限制；服务器收到请求后，将数据包裹在一个指定名字的回调函数里传回来。

如：
```
//前端部分:
  function addScriptTag(src) {
    var script = document.createElement('script');
    script.src = src;
    document.body.appendChild(script);
  }

  window.onload = function () {
    addScriptTag('http://jscode.me/getData?callback=showMes');
  }

  function showMes(data) {
    console.log(data.name)
  }
```
服务器收到这个请求后，会将数据放在回调函数的参数位置返回：
```
//后端部分：
app.get('/getData', function (req, res) {
  var data = {
    "name": "dk",
    "age": "23"
  }
  var cb = req.query.callback
  if (cb) {
    res.send(cb + '(' + JSON.stringify(data) + ')')
  } else {
    res.send(data)
  }
})
/*
  返回：showMes({"name":"dk","age":"23"})
*/
```
### 4. CORS是什么?
CORS是一个W3C标准，全称是“跨域资源共享”(Cross-origin resource sharing)。

它允许浏览器向跨源服务器，发出XMLHttpRequest请求，从而克服了AJAX只能同源使用的限制。  

CORS需要浏览器和服务器同时支持。目前所有浏览器都支持该功能，IE浏览器不能低于IE10。

实现功能非常简单，只需要由服务器发送一个响应标头即可。它是通过客户端+服务端协作声明的方式来确保请求安全的。服务端会在HTTP请求头增加一系列HTTP请求参数（例如Acess-Control-Allow-Origin等），来限制哪些域的请求和哪些类型可以接受，而客户端在发起请求时必须声明自己的源(Origin)，否则服务器将不予处理，如果客户端不作声明，请求甚至会被浏览器直接拦截到不了服务端。服务端收到HTTP请求后会进行域的比较，只有同域的请求才会处理。

浏览器将CORS请求分为两类：简单请求（simple request）和非简单请求（not-so-simple request）。

只要满足以下两大条件，就属于简单请求：
```
（1）请求方法是以下三种方法之一：
- HEAD
- GET
- POST
（2）HTTP的头信息不超过以下几种字段：
- Accept
- Accept-Language
- Content-Language
- Last-Event-ID
- Content-Type：只限于三个值application/x-www-form-urlencoded、multipart/form-data、text/plain
```
凡是不同时满足上面两个条件，就属于非简单请求。

浏览器对这两种请求的处理方式是不一样的。
1. 简单请求  
对于简单请求，浏览器直接发出CORS请求。具体来说就是在头信息中，增加一个Origin字段。而Origin字段说明本次请求来自哪个源（协议+域名+端口）。服务器根据这个值，决定是否同意这次请求。如果Origin指定的源，不在许可范围内，浏览器会返回一个正常的HTTP回应。如果Origin指定的域名在许可范围内，服务器返回的响应，会多出几个头信息 。如：
```
Access-Control-Allow-Origin: http://api.jirengu.com
Access-Control-Allow-Credentials: true
Access-Control-Expose-Headers: showMes
Content-Type: text/html; charset=utf-8
```

2. 非简单请求  
非简单请求是那种对服务器有特殊要求的请求，比如请求方法是PUT或DELETE，或Content-Type字段的类型是application/json。

    非简单请求的CORS请求，会在正式通信之前，增加一次HTTP查询请求。浏览器先询问服务器，当前网页所在的域名是否在服务器的虚空名单之中，一次可以使用哪些HTTP动词和头信息字段。只有得到肯定答复，浏览器才会发出正式的XMLHttpRequest请求，否则就会报错。

### 5.  根据视频里的讲解演示三种以上跨域的解决方式
1. JSONP 
```
//前端部分
<body>
  <button id="btn">点我</button>
  <script>
    var btn = document.getElementById("btn")
    btn.addEventListener('click', function () {
      var script = document.createElement('script')
      script.src = "http://b.kmac007.com:8080/getData?callback=showMes"
      document.body.appendChild(script)
      document.body.removeChild(script)
    })

    function showMes(data) {
      var newLi = document.createElement('li')
      newLi.innerText = data
      document.body.appendChild(newLi)
    }
  </script>
</body>
```
```
//后端部分
app.get('/getData', function (req, res) {
  var data = 'are u ok'
  var cd = req.query.callback
  if (cd) {
    res.send(cd + '(' + JSON.stringify(data) + ')')
  } else {
    res.send(data)
  }
})
```

2. CORS
```
//前端部分
<body>
  <button id="btn">点我</button>
  <script>
    var btn = document.getElementById("btn")
    btn.addEventListener('click', function () {
      var xhr = new XMLHttpRequest()
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
          var newLi = document.createElement('li')
          newLi.innerText = xhr.responseText
          document.body.appendChild(newLi)
        }
      }
      xhr.open('get', 'http://b.kmac007.com:8080/getData', true)
      xhr.send()
    })
  </script>
</body>
```
```
//后端部分
app.get('/getData',function(req,res){
  var data = "are u ok"
  res.header("Access-Control-Allow-Origin","*")  
  // 加入响应头Access-Control-Allow-Origin
  res.send(data)
})
```
3. 降域  
这个方法有局限性，只能用于具有相同主域名的子域名之间的跨域。   

主页面a.html
```
 document.domain = 降域后的域名
```
在主页面中通过iframe引入的b.html
```
 document.domain = 降域后的域名
```
4. postMessage  

由HTML5引入的API,postMEssage()方法允许来自不同源的脚本采用异步方式进行有限通信。这个API为 window对象新增了一个window.postMessage方法，允许跨窗口通信，不论这两个窗口是否同源。

postMessage方法的第一个参数是具体的信息内容，第二个参数是接收信息的窗口源（origin）,即“协议+域名+端口”。也可以设为*，表示不限制域名，向所有窗口发送。

即父窗口与子窗口互相发送消息，通过message事件，监听对方的消息，实现跨域。  

父窗口：
```
  $('.main input').addEventListener('input', function () {
    console.log(this.value);
    window.frames[0].postMessage(this.value, '*');
    //向子窗口发送信息
  })

  window.addEventListener('message', function (e) {
    $('.main input').value = e.data
    console.log(e.data);
    //监听子窗口发送信息的变化
  });

  function $(id) {
    return document.querySelector(id);
  }

```
子窗口：
```
$('#input').addEventListener('input', function(){
	window.parent.postMessage(this.value, '*');
  //向父窗口发送信息
})

window.addEventListener('message',function(e) {
		$('#input').value = e.data
    console.log(e.data);
    //监听父窗口的发送的信息变化
});

function $(id){
	return document.querySelector(id);
}
```