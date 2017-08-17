# 1. text-align: center的作用是什么，作用在什么元素上？能让什么元素水平居中
作用是使得元素中的文本水平居中。作用在块级元素上，能让块级元素中display为inline和inline-block元素居中。
# 2. IE 盒模型和W3C盒模型有什么区别?
- IE盒模型的宽度和高度包含border,padding和content
- W3C盒模型只包含content部分的宽高
# 3. *{ box-sizing: border-box;}的作用是什么？
为元素设定的宽度和高度决定了元素的边框盒。
就是说，为元素指定的任何内边距和边框都将在已设定的宽度和高度内进行绘制。通过从已设定的宽度和高度分别减去边框和内边距才能得到内容的宽度和高度。
# 4. line-height: 2和linde-height: 200%有什么区别？
line-height: 2 表示根据子元素自己字体的大小乘以2来计算行高，而line-height: 200% 表示根据父元素的字体大小计算行高，并且子元素会继承父元素的行高。
# 5. inline-block有什么特性？如何去除缝隙？高度不一样的inline-block元素如何顶端对齐?
inline-block使元素具有内联的特性时， 内容又具有块级元素的特性，可以设置宽高等；去除缝隙有两种方法：1.去除两元素间的空白字符，2.将父元素的字体大小设置为0，再分别设置它们的字体大小；高度不一样时，对具有inline-block属性的元素使用    vertical-align: top使其对其。
# 6. CSS sprite 是什么?
CSS精灵，指的是将多张图片拼接在一起，通过改变background-position来改变显示出来的图片，达到减少HTTP请求，提高页面性能的效果。
# 7. 让一个元素"看不见"有几种方式？有什么区别?
```
opacity: 0;  使元素变得透明，仍处在页面上
display: none; 使元素在页面上消失,不占用空间
visibility: hidden; 使元素不可见，但仍在页面上占据空间
background-color: rgba(0, 0, 0, 0.2) 只是背景色透明
```

---
- [CSSsprite](https://kmac007.github.io/demos/test/sprite.html)

- [字体图标实现](https://kmac007.github.io/demos/test/iconfont.html)