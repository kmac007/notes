# HTML、XML、XHTML 有什么区别
- HTML：超文本标记语言（HyperText Markup Language）,是一种用于创建网页的标准标记语言，被涉及用来显示数据。
- XML：可扩展标记语言（Extensible Markuo Language）,它被涉及用来传输和存储数据。它是对超文本标记语言的补充，是各种应用程序之间进行数据传输的常用工具。由于标签没有被预定义，使用者可以自行定义标签。
- XHTML：可扩展的超文本标记语言（Extensible HyperText Markup Language）,HTML4 和XML1.0 重组而成。改进了HTML定义不规范，结构不严谨的缺点。它的语法更加严格，相对HTML的兼容性也不差。
# 怎样理解 HTML 语义化
根据内容的结构化（内容语义化），选择合适的标签（代码语义化）便于开发者阅读和写出更优雅的代码的同时让浏览器的爬虫和机器很好地解析。
# 怎样理解内容与样式分离的原则
即：
- HTML 仅处理内容，只考虑 HTML 的结构和语义化，避免出现属性样式。
- 写 JS 的时候，尽量不使用 JS直接操作样式。
- 页面展现的所有样式，都由CSS来负责实现。
# 有哪些常见的meta标签
> <meta> 标签提供关于HTML文档的元数据。元数据不会显示在页面上，但是对于机器是可读的。它可用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他 web 服务。
-  **页面关键字**
```
<meta name="keywords" content="your tags">
```
- **页面描述**
```
<meta name="description" content="150 words">
```
- **声明文件编码**
```
<meta charset="UTF-8">
```
- **viewport**:能优化移动浏览器显示
```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
- **优先使用IE最新版本和Chrome**
```
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
<!-- 关于X-UA-Compatible -->
<meta http-equiv="X-UA-Compatible" content="IE=6" ><!-- 使用IE6 -->
<meta http-equiv="X-UA-Compatible" content="IE=7" ><!-- 使用IE7 -->
<meta http-equiv="X-UA-Compatible" content="IE=8" ><!-- 使用IE8 -->
```
- **浏览器内核控制**
```
<meta name="renderer" content="webkit|ie-comp|ie-stand">
```
# 文档声明的作用?严格模式和混杂模式指什么?<!DOCTYPE html> 的作用?
  **文档声明**声明文档的解析类型(document.compatMode)，避免浏览器的混杂模式。
  - 严格模式：浏览器使用W3C的标准解析渲染页面
  - 混杂模式：浏览器使用自身的方式解析渲染页面
  - <!DOCTYPE html>的作用是声明该页面的HTML版本为HTML5
# 浏览器乱码的原因是什么？如何解决
页面的编码方式与浏览器的解码方式不匹配；解决方法为在<head>中加
```
<meta charset="文档编码方式">
```
# 常见的浏览器有哪些，什么内核
###常见的浏览器如下：

浏览器 | 内核
---|---
IE | Trident
Chrome | WebKit
Safari | WebKit
Firefox | Gecko
Opera | Presto

其中国内的浏览器一般为WebKit/Trident的双内核，如360浏览器，QQ浏览器等

# 列出常见的标签，并简单介绍这些标签用在什么场景
```
<!--...-->：注释
<!DOCTYPE>：定义文档类型
<html>： 定义 HTML 文档
<head>：定义关于文档的信息
<body>： 定义文档的主体
<header>：定义了文档的头部区域
<section>：<section> 标签定义文档中的节（section、区段）。比如章节、页眉、页脚或文档中的其他部分。
<footer>：定义 section 或 body的页脚。
<div>： 定义文档中的节
<meta>：定义关于 HTML 文档的元信息。
<title>：定义文档的标题。
<link>：定义文档与外部资源的关系
<script>：定义客户端脚本。
<nav>：定义导航链接的部分
<aside>：定义页面的侧边栏内容
<a>：定义超文本链接
<br>： 定义换行
<button>： 定义一个点击按钮
<canvas>：定义图形,绘图
<form>：定义了HTML文档的表单
<h1> to <h6>：定义 HTML 标题
<iframe>：定义内联框架
<img>：定义图像
<input>：定义输入控件
<label>：定义 input 元素的标注
<li>：定义列表的项目
<object>：定义内嵌对象
<param>：定义对象的参数。
<ol>： 定义有序列表。
<p>： 定义段落。
<select>：定义选择列表（下拉列表）。
<option>：定义选择列表中的选项。
<style>：定义文档的样式信息。
<table>： 定义表格。
```