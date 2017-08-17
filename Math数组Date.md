# Math任务
## 1. 一个函数，返回从min到max之间的 随机整数，包括min不包括max 
```
function getRandom(min, max) {
  return Math.floor(min + Math.random() * (max - min))
}
```
## 2. 写一个函数，返回从min都max之间的 随机整数，包括min包括max 
```
function getRandom(min, max) {
  return Math.floor(min + Math.random() * (max - min + 1))
}
```
## 3. 写一个函数，生成一个长度为 n 的随机字符串，字符串字符的取值范围包括0到9，a到 z，A到Z。

```
var oldStr = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ"

function getRandStr(len) {
  //补全函数
  var strArr = oldStr.split('')
  var randStr = ''
  for (var i = 0; i < len; i++) {
    var strKey = Math.floor(Math.random() * oldStr.length)
    randStr += strArr[strKey]
  }
  return randStr
}
var str = getRandStr(10); // 0a3iJiRZap
```
## 4. 写一个函数，生成一个随机 IP 地址，一个合法的 IP 地址为 0.0.0.0~255.255.255.255
```
function getRandIp() {
  var ipArr = []
  var len = 4
  for (var i = 0; i < len; i++) {
    ipArr[i] = Math.floor(Math.random() * (255 + 1))
    }
    return ipArr.join('.')
  }
  getRandIp()
```

## 5. 写一个函数，生成一个随机颜色字符串，合法的颜色为#000000~ #ffffff
```
function getRandColor() {
  var str = "ABCDEF0123456789"
  var colorArr = str.split('')
  var len = 6
  var colorStr = ''
  for (var i = 0; i < len; i++) {
    colorStr += colorArr[Math.floor(Math.random() * (colorArr.length))]
  }
  return '#' + colorStr
}
getRandColor()
```

# 数组任务

## 1. 数组方法里push、pop、shift、unshift、join、splice分别是什么作用？用 splice函数分别实现push、pop、shift、unshift方法

push: 向数组的末尾添加一个或更多元素，并返回新的数组长度。

pop: 删除并返回数组的最后一个元素

shift: 删除并返回数组的第一个元素

unshift: 向数组的开头添加一个或更多元素，并返回新的长度。

join: 把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔。

splice: 删除元素，并向数组添加新元素。

用splice实现push:
```
arr.splice(arr.length,0,item)
```
用splice实现pop:
```
arr.splice(arr.length-1,1)
```
用slice实现unshift:
```
arr.splice(0,0,item)
```
用slice实现shift:
```
arr.splice(0,1)
```

## 2. 写一个函数，操作数组，数组中的每一项变为原来的平方，在原数组上操作
```
function squareArr(arr) {
  for (var i = 0; i < arr.length; i++) {
    arr[i] = arr[i] * arr[i]
  }
  return arr
}
var arr = [2, 4, 6]
squareArr(arr)
console.log(arr) // [4, 16, 36]
```
## 3. 写一个函数，操作数组，返回一个新数组，新数组中只包含正数，原数组不变
```
function filterPositive(arr) {
  var newArr = []
  for (var i = 0; i < arr.length; i++) {
    if (typeof arr[i] === "number" && arr[i] > 0) {
      newArr.push(arr[i])
    }
  }
  return newArr
}
var arr = [3, -1, 2, '饥人谷', true]
var newArr = filterPositive(arr)
console.log(newArr) //[3, 2]
console.log(arr) //[3, -1,  2,  '饥人谷', true]
```
# Date 任务

## 1. 写一个函数getChIntv，获取从当前时间到指定日期的间隔时间
```
var timeStr = getChIntv("2017-05-01");

function getChIntv(timeStr) {
  var targetTime = new Date(timeStr).getTime() - 1000 * 60 * 60 * 8
  var currentTime = Date.now()
  var offsetTime = targetTime - currentTime
  var days = parseInt(offsetTime / (1000 * 60 * 60 * 24))
  var hours = parseInt(offsetTime % (1000 * 60 * 60 * 24) / (1000 * 60 * 60))
  var mins = parseInt(offsetTime % (1000 * 60 * 60 * 24) % (1000 * 60 * 60) / (1000 * 60))
  var seconds = parseInt(offsetTime % (1000 * 60 * 60 * 24) % (1000 * 60 * 60) % (1000 * 60) / 1000)

  return "距五一还有:" + days + "天" + hours + "小时" + mins + "分" + seconds + "秒"
}
console.log(timeStr); // 距五一还有:11天7小时26分28秒
```

## 2. 把hh-mm-dd格式数字日期改成中文日期
```
var str = getChsDate('2015-01-08');

function getChsDate(timeStr) {
  var dist = ["零", "一", "二", "三", "四", "五", "六", "七", "八", "九", "十", "十一", "十二", "十三", "十四", "十五", "十六", "十七", "十八", "十九", "二十", "二十一", "二十二", "二十三", "二十四", "二十五", "二十六", "二十七", "二十八", "二十九", "三十", "三十一"];
  var arr = timeStr.split('-')
  var year = arr[0]
  var month = arr[1]
  var day = arr[2]
  var chYear = dist[parseInt(year[0])] + dist[parseInt(year[1])] + dist[parseInt(year[2])] + dist[parseInt(year[3])]
  var chMonth = dist[parseInt(month)]
  var chDay = dist[parseInt(day)]
  return chYear + "年" + chMonth + "月" + chDay + "日"
}
console.log(str); // 二零一五年一月八日
```

## 3. 写一个函数，参数为时间对象毫秒数的字符串格式，返回值为字符串。假设参数为时间对象毫秒数t，根据t的时间分别返回如下字符串:

```
function friendlyDate(time) {
  var now = Date.now()
  var offsetTime = (now - time) / 1000 / 60
  if (offsetTime < 1) {
    return parseInt(offsetTime * 60) + "刚刚"
  } else if (offsetTime >= 1 && offsetTime < 60) {
    return parseInt(offsetTime) + "分钟前"
  } else if (offsetTime >= 60 && offsetTime < 60 * 24) {
    return parseInt(offsetTime / 60) + "小时前"
  } else if (offsetTime >= 60 * 24 && offsetTime < 60 * 24 * 30) {
    return parseInt(offsetTime / 60 / 24) + "天前"
  } else if (offsetTime >= 60 * 24 * 30 && offsetTime < 60 * 24 * 39 * 12) {
    return parseInt(offsetTime / 60 / 24 / 30) + "月前"
  } else if (offsetTime >= 60 * 24 * 39 * 12) {
    return parseInt(offsetTime / 60 / 24 / 30 / 12) + "年前"
  }
}
var str = friendlyDate('1492593606284') //  1分钟前
var str2 = friendlyDate('1422583606284') //2年前
```