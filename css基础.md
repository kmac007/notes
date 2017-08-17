# 1. CSS的全称是什么?
层叠样式表(英文全称：Cascading Style Sheets)是一种用来表现HTML（标准通用标记语言的一个应用）或XML（标准通用标记语言的一个子集）等文件样式的计算机语言。
# 2. CSS有几种引入方式? link 和@import 有什么区别?
 ### 三种：
 1. 内联样式
```
<p style="background-color: red"></p>
```
 2. 内部样式
```
<style>
    .demo {
        margin: 0 auto;
        background-color: #ccc;
    }
</style>
```
 3. 外部样式
 ```
 通过link引入外部css文件
<head>
    <link rel="stylesheet" type="text/css" href="index.css">
</head>
 ```
 4. @import引入
```
<style>
   @import url(style.css);
</style>
```
 ### link和@import的区别：
1. 引入的语法不同
link的语法为：
```
<link rel="stylesheet" type="text/css" href="index.css">
```
@import语法为:
```
<style type="text/css">
    @import url(style.css);
</style>
```
2. <link>是html标签，<link>标签除了可以加载CSS外，还可以做很多事情，比如定义RSS，定义rel连接属性等；而@import看作是CSS的样式，只能加载CSS。
3. link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载。
4. link支持使用JavaScript控制DOM去改变样式；而@import不支持。
5. link是html标签，无兼容性问题；@import是在CSS2.1提出的，低版本浏览器不支持。
# 3. 以下这几种文件路径分别用在什么地方，代表什么意思?
- css/a.css
  - 相对路径，当前文件夹内css文件夹内的a.css
- ./css/a.css
  - 相对路径，同上
- b.css
  - 相对路径，当前文件夹下的b.css
- ../imgs/a.png
  - 相对路径，上级目录下img文件夹下的a.png
- /Users/hunger/project/css/a.css
  - 绝对路径，本地文件夹内的a.css
- /static/css/a.css
  - 相对路径，在网站根目录的static文件夹下css文件夹下的a.css
- http://cdn.jirengu.com/kejian1/8-1.png
  - 绝对路径，指向网站上的图片
# 4. 如果我想在js.jirengu.com上展示一个图片，需要怎么操作?
  1. 获取图片URL
  2. 打开js.jirengu.com
  3. 在body中加入<img>标签，URL为图片URL
  4. 修改URL为相对路径
### [例如点我](http://js.jirengu.com/gidopesiso/1/edit)
# 5. 列出5条以上html和 css 的书写规范
    1. CSS 文件使用无 BOM 的 UTF-8 编码。
    2. 选择器 与 { 之间必须包含空格。
    3. 属性名 与之后的 : 之间不允许包含空格， : 与 属性值 之间必须包含空格。
    4. 列表型属性值 书写在单行时，, 后必须跟一个空格。
    5. 属性定义后必须以分号结尾。
    6. 在可以使用缩写的情况下，尽量使用属性缩写。
    7. 长度为 0 时须省略单位。
# 6. 截图介绍 chrome 开发者工具的功能区
## 快速编辑HTML元素
