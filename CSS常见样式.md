# 1. 块级元素和行内元素分别有哪些？动手测试并列出4条以上的特性区别
- 块级元素：div, p, h1-h6, table, form, ul, li, ol, address, article, aside, audio, blockquote, canvas,header,footer等
- 行内元素: span, a, input, button, lable, select, textarea, em, br, img, strong

区别：
1. 行内元素只能容纳行内元素和文本。而块级可以容纳块级元素和行内元素。
2. 块级元素可以设定宽高，而行内元素不可以。
3. 块级元素独占一行，而行内元素可以与其它行内元素共同处在一行。
4. 行内元素的宽度为内容的宽度，块级元素与浏览器窗口宽度一致
# 2. 什么是 CSS 继承? 哪些属性能继承，哪些不能？
> CSS继承: 子元素继承了父元素的CSS属性。
- 不可继承属性：display, margin, border, padding, background, width, height, overflow, z-index, float, position, vertical-align
- 所有元素可继承：visibility和cursor
- 所有元素可继承：visibility和cursor。
- 内联元素可继承：letter-spacing、word-spacing、white-space、line-height、color、font、 font-family、font-size、font-style、font-variant、font-weight、text- decoration、text-transform、direction。
- 块状元素可继承：text-indent和text-align。
- 列表元素可继承：list-style、list-style-type、list-style-position、list-style-image。
- 表格元素可继承：border-collapse。
# 3. 如何让块级元素水平居中？如何让行内元素水平居中?
- 块级元素水平居中：给块级元素设定宽高,margin: 0 auto;
- 行内元素: text-align: center;
# 4. 用 CSS 实现一个三角形
[一个CSS三角形](http://js.jirengu.com/romekefagu/2/edit)
# 5. 单行文本溢出加 ...如何实现?
```
.box {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```
# 6. px, em, rem 有什么区别
- px: 相对长度单位。像素px是相对于显示器屏幕分辨率而言的
- em: 指的是相对于其父级元素的大小，即倍数。
- rem: 相对于根html元素的大小，即倍数。
# 7. 解释下面代码的作用?为什么要加引号?字体里\5b8b\4f53代表什么?
```
body{
  font: 12px/1.5 tahoma,arial,'Hiragino Sans GB','\5b8b\4f53',sans-serif;
}
```
- 字体大小：12px
- 字体行距：1.5倍
- 字体选择的优先级从高到低：tahoma -> ... -> sans-serif
- 字体描述需要加引号的情况，常见有下面几种：
  1. 字体描述使用的中文
  2. 字体描述使用英文，中间有空格
  3. 字体描述使用unicode编码
\5b8b\4f53 是unicode编码模式，表示“宋体”

控制台中输入：escape("字体")将字体中文转换为unicode编码格式

# 代码
[实现如下效果](http://js.jirengu.com/kiqarubose/1/edit?output)

[实现按钮](http://js.jirengu.com/najelasado/1/edit?html,css,output)

[表格](http://js.jirengu.com/xiqilixuzo/4/edit?output)

[三角形](http://js.jirengu.com/goxigeyami/1/edit?html,css,output)

[实现Card](http://js.jirengu.com/lejuyevohi/2/edit?html,css,output)