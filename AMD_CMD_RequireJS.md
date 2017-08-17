### 1. 为什么要使用模块化？

在多人合作完成的大型项目中，如果每个人都定义全局变量，这会导致命名冲突，同时不利于项目的维护。当项目庞大起来，众多文件之间互相依赖的关系让人眼花缭乱。而模块化编程可以很好的解决这些问题。

模块化的目的：
- 解决命名冲突
- 依赖管理    

其他价值
- 提高代码的可读性
- 代码解耦，提高复用性

### 2. CMD、AMD、CommonJS 规范分别指什么？有哪些应用

CMD(Common Module Definition)是SeaJS推广过程中产生的。和AMD不同的是，它并不是异步加载，而是松散加载，只有当需要加载模块的时候，再用require方法引用模块。在CMD规范中一个模块就是一个文件。代码书写格式如下：
```
define(factory)
/*
    全局函数define，用来定义模块。
    参数factory可以是一个函数，也可以为对象或者字符串。
    当factory为对象、字符串时，表示模块的接口就是该对象、字符串。
*/

/*
factory为函数时，表示是模块的构造方法。执行该构造方法，可以得到模块向外提供的接口。
factory方法在执行时，默认会传如三个参数：require、exports和module:
*/
define(function(require, exports, module){
    // 模块代码
})
```

用法示例：

```
//math.js
define(function (require, exports, module) {
  exports.add = function () {
    var sum = 0;
    i = 0, args = arguments, l = args.length
    while (i < l) {
      sum += args[i++]
    }
    return sum
  }
})

//increment.js
define(function (require, exports, module) {
  var add = require('math').add
  exports.increment = function (val) {
    return add(val, 1)
  }
})

//program.js
define(function (require, exports, module) {
  var inc = require('increment').increment
  var a = 1
  inc(a) // 2

  module.id == 'program'
})
```

CommonJS:

CommonJS是服务器端模块的规范，Node.js采用了这个规范。Node.js首先采用了js模块化的概念。
1. 在一个模块中，存在一个自由的变量"require"，它是一个函数。
- 这个"require"函数接收一个模块标识符。
- "require"返回外部模块所输出的API。
- 如果出现依赖闭环(dependency cycle)，那么外部模块在被它的传递依赖(transitive dependencies)所require的时候可以并没有执行完成；在这种情况下，"require"返回的对象必须至少包含此外部模块在调用require函数(会进入当前模块执行环境)之前就已经准备完毕的输出。
- 如果请求的模块不能返回，那么"require"必须抛出一个错误。
2. 在一个模块中，会存在一个名为"exports"的自由变量，它是一个对象，模块可以在执行的时候把自身的API加入到其中。
3. 模块必须使用"exports"对象来作为输出的唯一表示。

使用示例： 

```
// math.js
exports.add = function () {
  var sum = 0,
    i = 0,
    args = arguments,
    l = args.length
  while (i < 1) {
    sum += args[i++]
  }
  return sum
}
//increment.js
var add = require('math').add
exports.increment = function (val) {
  return add(val, 1)
}
//program.js
var inc = require('increment').increment
var a = 1
inc(a) // 2
```

AMD规范：

AMD(Asynchronous Module Definition，异步模块定义)指定一种机制，在该机制下模块和依赖可以异步加载。这对浏览器的异步加载尤其适用。
实现AMD规范的库有require.js和curl.js等。

语法：

```
define(id?, dependencies?, factory)
```

### 3. 使用 requirejs 完善入门任务15，包括如下功能：

```
1. 首屏大图为全屏轮播
2. 有回到顶部功能
3. 图片区使用瀑布流布局（图片高度不一），下部有加载更多按钮，点击加载更多会加载更多数据(数据在后端 mock)
4.  使用 r.js 打包应用
```

```
[项目预览](https://kmac007.github.io/demos/requirejs/index.html)

[代码](https://github.com/kmac007/demos/tree/master/requirejs)
```