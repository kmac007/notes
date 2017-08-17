# 问答
## 1. 浮动元素有什么特征？对父容器、其他浮动元素、普通元素、文字分别有什么影响?

浮动的特征是使元素脱离普通流，按照指定方向发生移动，遇到父级边界或者相邻的浮动元素才停下来；

**对父容器的影响:** 父容器中的元素浮动后，脱离普通流会使得父容器失去高度；

**对其他浮动元素的影响：** 如果是同一方向浮动，相邻的浮动元素会并列在同一行，空间不够，会换到下一行

**对普通元素的影响**： 浮动元素会脱离普通流，普通元素会占据它原有的空间，从而会出现浮动元素覆盖普通元素

**对文字的影响：** 文字可以感知的浮动元素的存在，文字会在浮动元素周围形成环绕效果

## 2. 清除浮动指什么? 如何清除浮动? 两种以上方法
- 清除浮动指的是通过clear属性解决由元素浮动引起的父容器的塌陷问题。
- 清楚浮动的方法：
  1. 方法一：父级元素定义：overflow: hidden;
  2. 方法二：使用伪元素
  ```
  .container::after {
    content: '';
    display: block;
    visibility: hidden;
    clear: both;
  }
  ```
  3. 方法三：在父元素末尾添加一个空div,设置样式clear: both (与方法二类似)
## 3. 有几种定位方式，分别是如何实现定位的，参考点是什么，使用场景是什么？
1. static: 默认值,没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）
2. relative: 生成相对定位元素，相对于元素本身正常位置进行定位。
3. absolute: 脱离普通流，生成绝对定位的元素，相对于static定位以外的第一个祖先元素（offset parent）进行定位,元素的位置通过 left, top, right 以及 bottom 属性进行规定
4. fixed: 绝对定位，脱离普通流，相对于浏览器窗口进行定位。元素的位置通过 left, top, right 以及 bottom 属性进行规定
5. sticky: CSS3新属性，表现类似position: relative和position: fixed的合体，在目标区域在屏幕中可见时，它的行为就像position:relative;而当页面滚动超出目标区域时，它的表现就像position:fixed，它会固定在目标位置

## 4. z-index 有什么作用? 如何使用?
z-index 属性设置元素的堆叠顺序。拥有更高堆叠顺序的元素总是会处于堆叠顺序较低的元素的前面。元素可拥有负的 z-index 属性值。
- 应用 ：元素脱离了普通流，覆盖了普通元素，要修改显示顺序，可以为两者添加z-index属性值，其中属性值越大，显示的越靠前。
## 5. position:relative和负margin都可以使元素位置发生偏移?二者有什么区别
- position: relative: 相对于自身偏移，不脱离普通流，仍占据原有空间，不影响其他元素
- 负margin: 除了让元素自身发生偏移还影响其它普通流中的元素。
## 6. BFC 是什么？如何生成 BFC？BFC 有什么作用？举例说明
- BFC(Block formatting context)直译为“块级格式化上下文 ”。BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。同时BFC任然属于文档中的普通流。
- 如何生成BFC：当一个HTML元素满足下面条件的任何一点，都可以产生Block Formatting Context
    - float: 除了none以外的值
    - overflow除了visible意外的值（hidden, auto, scroll）
    - display(table-cell, table-caption, inline-block)
    - position(absolute, fixed)
- BFC的作用
    1. **阻止边距折叠：** 
        我们知道在一般情况下，两个上下相邻的盒子会折叠它们垂直方向接触到的边距，这种情况只会发生在同一个Block Formatting Context中。换句话说，在同一个布局环境中（Block Formatting Context）是边距折叠的必要条件。这也就是为什么浮动的元素和绝对定位元素不会发生边距折叠的原因（当然还有很多种情况也不会折叠）。
    2. **可以包含浮动元素如:** [BFC实现包含浮动元素](http://js.jirengu.com/puruxexuhe/1/edit?html,css,output)
    3. **阻止元素被浮动覆盖，如:**  [BFC防止元素被浮动覆盖](http://js.jirengu.com/hawapetoxu/1/edit)
## 7. 在什么场景下会出现外边距合并？如何合并？如何不让相邻元素外边距合并？给个父子外边距合并的范例
- 外边距合并指的是，当两个垂直外边距相遇时，它们将形成一个外边距。合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。即：**两个或多个毗邻的普通流中的块元素垂直方向上的 margin 会折叠** 当然负margin的情况下也会出现margin合并的现象。
- 不让相邻元素外边距合并： 
    1. 浮动元素、inline-block元素、绝对定位元素不会和垂直方向上其他元素的margin折叠(这里指的是上下相邻的元素)
    2. 创建了格式化上下文的元素，不和它的子元素发生margin折叠（这里指的是BFC的元素和它的子元素不会发生折叠）
- [父子外边距合并范例](http://js.jirengu.com/lexizumilo/2/edit)
# 代码
1. [代码1,alert效果](http://js.jirengu.com/duruyoketa/1/edit)
2. [代码2,表单效果](http://js.jirengu.com/qapesofalu/1/edit?html,css,output)
3. [代码3,模态框效果](http://js.jirengu.com/baluvomosu/1/edit)
4. [代码4,导航栏效果](http://js.jirengu.com/womefuguxa/1/edit?html,css,output)