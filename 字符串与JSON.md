# 1. 使用数组拼接出如下字符串
```
var prod = {
  name: '女装',
  styles: ['短款', '冬季', '春装']
}

function getTplStr(data) {
  var arr = []
  arr.push('<dl class="product">')
  arr.push('<dt>' + data.name + '</dt>')
  for (key in data['styles']) {
    arr.push('<dd>' + data['styles'][key] + '</dd>')
  }
  arr.push("</dl>")
  return arr.join('')
}
var result = getTplStr(prod) //result为下面的字符串
```
# 2. 写出两种以上声明多行字符串的方法
```
/*使用\n转义字符回车*/
var str1 = "line1\nline2\nline3\n"
console.log(str1)

/*使用反斜杠转义*/
var str2 = "line1\
            line2\
            line3\
"
console.log(str2)

/*连接运算符(+)*/
var str3 = "line1"
  + "line2"
  + "line3"
console.log(str3)

/*使用多行注释，生成多行字符串*/
var str4 = (function(){/*
  line1
  line2
  line3
*/}).toString().split('\n').slice(1,-1).join('\n')
```
# 3. 补全如下代码,让输出结果为字符串:
>  hello\\\饥人谷

```
var str = "hello\\\\饥人谷"
console.log(str)
```

# 4. 以下代码输出什么?为什么
```
var str = 'jirengu\nruoyu'
console.log(str.length)
/*输出13，因为"\"为转义字符,"\n"只占一个字符*/
```

# 5. 写一个函数，判断一个字符串是回文字符串，如 abcdcba是回文字符串, abcdcbb不是

```
function isPalindrome(str) {
  if (typeof str === "string") {
    var newStr = str.toLowerCase().split('').reverse().join('')
    if(newStr === str.toLowerCase()) {
      console.log("是回文")
    }else {
      console.log("不是回文")
    }
  }
}
```

# 6. 写一个函数，统计字符串里出现出现频率最多的字符

```
function isMost(str) {
  var dict = {}
  for (var i = 0; i < str.length; i++) {
    if(dict[str[i]]) {
      ++dict[str[i]]
    }else{
      dict[str[i]] = 1
    }
  }
  var count = 0
  var maxValue
  for(var key in dict){
    if(dict[key] > count){
      maxValue = key
      count = dict[key]
    }
  }
  return maxValue + ":" + count
}
```
# 7. 写一个camelize函数，把my-short-string形式的字符串转化成myShortString形式的字符串，如
```
camelize("background-color") == 'backgroundColor'
camelize("list-style-image") == 'listStyleImage'
```
代码如下:
```
function camelize(str) {
  var arr = str.toLowerCase().split('-')
  var newStr = arr[0]
  for (var i = 1; i < arr.length; i++) {
    newStr += (arr[i].charAt(0).toUpperCase() + arr[i].substring(1))
  }
  return newStr
}
```

# 8. 写一个 ucFirst函数，返回第一个字母为大写的字符 （***）
```
ucFirst("hunger") == "Hunger"
```
代码如下：
```
function ucFirst(str) {
  return str.charAt(0).toUpperCase() + str.substring(1)
}
```

# 9. 写一个函数truncate(str, maxlength), 如果str的长度大于maxlength，会把str截断到maxlength长，并加上...，如
```
truncate("hello, this is hunger valley,", 10) == "hello, thi...";
truncate("hello world", 20) == "hello world"
```
代码如下:
```
function truncate(str, maxlength) {
  if (str.length > maxlength) {
    return str.substring(0, maxlength) + "..."
  } else {
    return str
  }
}
```

# 10. 什么是 json？什么是 json 语言？JSON 语言如何表示对象？window.JSON 是什么？

> JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。它基于JavaScript（Standard ECMA-262 3rd Edition - December 1999）的一个子集.JSON采用完全独立于语言的文本格式，但是也使用了类似于C语言家族的习惯（包括C, C++, C#, Java, JavaScript, Perl, Python等）。这些特性使JSON成为理想的数据交换语言。 易于人阅读和编写，同时也易于机器解析和生成(网络传输速度)。

> 严格的JavaScript对象表示法表示结构化的数据。具体写法是：数据在名称/值对中；数据由逗号分隔；花括号保存对象；方括号保存数组

> JSON 数据的书写格式是：名称/值对，名称/值对组合中的名称写在前面（在双引号中），值对写在后面(同样在双引号中)，中间用冒号隔开：
值（value）可以是双引号括起来的字符串（string）、数值(number)、boolean、 null、对象（object）或者数组（array）。这些结构可以嵌套。

> window.JSON是浏览器内置对象
其中JSON.parse()表示把字符串解析为JSON对象，而JSON.stringify()表示将JSON对象解析为字符串

# 11. 如何把JSON 格式的字符串转换为 JS 对象？如何把 JS对象转换为 JSON 格式的字符串?

JSON.parse() 把JSON 格式的字符串转换为 JS 对象

JSON.stringify() 如何把 JS对象转换为 JSON 格式的字符串

eval() 可以把字符串转为json 但不推荐使用