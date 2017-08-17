### 1. HTML5是什么？有哪些新特性？有哪些新增标签？如何让低版本的 IE 支持 HTML5新标签
HTML5 是定义 HTML 标准的最新的版本。 该术语表示两个不同的概念：

- 它是一个新版本的HTML语言，具有新的元素，属性和行为，
- 它有更大的技术集，允许更多样化和强大的网站和应用程序。这个集合有时称为HTML5和朋友，通常缩写为HTML5。

新特性：
- 语义化：HTML5赋予网页更好的意义和结构，语义化标签可以使内容显而易见
- 本地存储特性：IndexedDB是一个为了能够在浏览器中存储大量结构化数据，并且能够在这些数据上使用索引进行高性能检索的 Web 标准。
- 新的通信方式：Web Sockets允许页面和服务器之间建立持久连接并通过这种方法来交换非HTML数据，实现基于页面的实时聊天。
- 多媒体特性：<audio>和<video>元素嵌入并支持新的多媒体内容操作。
- 样式：可以通过CSS3的新属性制作出更绚丽的页面。
- 3D，图像和效果：基于SVG、Canvas、WebGL及CSS3的3D功能，可以绘制出惊人的图像。
- 设备访问：允许使用和操作计算机的摄像头，并从中存取照片、让浏览器使用地理位置服务定位用户的位置、对用户按下触控屏的事件做出反应的处理程序等。
- 性能与集成特性：HTML5会通过XMLHttpRequest2等技术，解决以前的跨域等问题，帮助您的Web应用和网站在多样化的环境中更快速的工作。

新增标签：
- <article>标签定义一个独立完整的内容，比如一篇文章
- <aside>标签定义独立于主内容的区块，比如一个组件
- <footer> 标签定义 section 或页面的尾部内容
- <section> 标签定义文档中的一个章节，比如产品介绍部分
- <nav> 标签定义导航部分
- <header> 标签定义 section 或页面的头部
- <hgroup> 标签一般包括一个H加一个P标签
- <figure>与<figcaption>一般包括一张img及图片介绍
- <audio> 标签定义声音
- <video> 标签定义视频
- <canvas> 标签定义图形，可以绘制矢量图形
- <command> 标签定义命令按钮，比如单选按钮、复选框或按钮
- <datalist> 标签定义可选数据的列表。与 input 元素配合使用。但一般多使用ajax与后端交互实现
- <embed> 标签定义嵌入的内容，比如插件
- <mark>标签主要用来在视觉上向用户呈现那些需要突出的文字，一般用于高亮显示结果
- <source> 标签为媒介元素（比如 <video> 和 <audio>）定义媒介资源
- <time> 标签定义日期或时间，或者两者
等等

让低版本的IE支持HTML5：
html5shiv.js：通过JavaScript 来创建HTML5元素(如 main, header, footer等)。在某种程度上通过JavaScript 创建的元素是 styleable(可样式)的。
使用方法：

```
<!--[if lt IE 9]><script src="http://cdn.bootcss.com/html5shiv/3.7/html5shiv.js"></script><![endif]-->
```

### 2. input 有哪些新增类型？

1. email 检查是否为email地址
2. url 检查是否为url地址
3. number 检查是否为数字
4. range 出现一个滑块拖动条
5. Date pickers (date, month, week, time, datetime, datetime-local) 拥有多个可供选取日期和时间的新输入类型
6. search 搜索输入框
7. color 一个颜色选择器

### 3. 浏览器本地存储中 cookie 和 localStorage 有什么区别？ localStorage 如何存储删除数据。
1. cookie在浏览器和服务器之间来回传递，而localStorage不会把数据发给服务器，仅在本地保存
2. 数据的有效期不同，cookie值在设置的cookie过期时间之前一直有效，即使窗口和浏览器关闭。localStorage始终有效且长期保存。
3. cookie数据还有路径的概念，可以限制cookie只属于某个路径下。
4. 存储大小也不同，cookie数据不能超过4k, localStorage虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。

通过localSorage对象将数据存储在其域对应的本地储存下

```
localStorage.setItem("myname":'dk') //存储
localStorage.removeItem("myname") //删除
```

### 4.  写出如下 CSS3效果的简单事例

[预览](http://js.jirengu.com/wefokotuzi)

### 5. 实现如下全屏图加过渡色的效果（具体效果随意）

[预览](http://js.jirengu.com/vijajajaxe/1/edit?html,css,output)

### 6.  写出如下 loading 动画效果 [DEMO1](http://js.jirengu.com/lomamoyuma/1/edit?html,css,output) [DEMO2](http://js.jirengu.com/ducewebobu/1/edit?html,css,output)