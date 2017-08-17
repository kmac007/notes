### 1. 下面的代码输出多少？修改代码让fnArr[i]() 输出 i。使用**两种以上的**方法
```
    var fnArr = [];
    for (var i = 0; i < 10; i ++) {
        fnArr[i] =  function(){
    	    return i;
        };
    }
    console.log( fnArr[3]() );  // 输出10
```
代码的输出结果为10
```
// 方法一
var fnArr = [];
for (var i = 0; i < 10; i++) {
  !function(i){
    fnArr[i]=function(){
      return i;
    }
  }(i)
}
console.log(fnArr[3]()); //
```

```
// 方法二
var fnArr = [];
for (var i = 0; i < 10; i++) {
  fnArr[i] = (function(i){
    return function(){
      return i;
    }
  }(i));
}
console.log(fnArr[3]()); //
```

```
// 方法三
var fnArr = [];
for (let i = 0; i < 10; i++) {  //使用ES6的let语法
  fnArr[i] = function () {
    return i;
  };
}
console.log(fnArr[3]()); //
```
### 2. 封装一个汽车对象，可以通过如下方式获取汽车状态

```
var Car = (function () {
  var speed = 0

  function setSpeed(s) {
    speed = s
  }

  function getSpeed() {
    console.log(speed)
  }

  function accelerate() {
    speed += 10
  }

  function decelerate() {
    speed > 0 ? speed -= 10 : speed
  }

  function getStatus() {
    if (speed <= 0) {
      console.log("stop");
      speed = null
    } else if (speed > 0) {
      console.log("running")
    }
  }
  return {
    setSpeed: setSpeed,
    getSpeed: getSpeed,
    accelerate: accelerate,
    decelerate: decelerate,
    getStatus: getStatus
  }
})()
Car.setSpeed(30);
Car.getSpeed(); //30
Car.accelerate();
Car.getSpeed(); //40;
Car.decelerate();
Car.decelerate();
Car.getSpeed(); //20
Car.getStatus(); // 'running';
Car.decelerate();
Car.decelerate();
Car.getStatus(); //'stop';
//Car.speed;  //error
```

### 3. 下面这段代码输出结果是? 为什么?
```
var a = 1;
var a ;
setTimeout(function(){
    a = 2;
    console.log(a); //2
}, 0);
console.log(a); //1
a = 3;
console.log(a); //3
```
> 输出结果为1,3,2 因为setTimeout()会在程序的最后执行，前面声明a并赋值，重复声明不会改变a的值

### 4. 下面这段代码输出结果是? 为什么?
```
var flag = true;
setTimeout(function(){
    flag = false;
},0) //原本会在程序的末尾执行，但由于while是个死循环，程序不会往下执行，故setTimeout也不会执行
while(flag){} //flag永远是true,死循环
console.log(flag); //不会执行
```

### 5. 下面这段代码输出？如何输出`delayer: 0, delayer:1...`（使用闭包来实现）
```
for (var i = 0; i < 5; i++) {
  setTimeout(function () {
    console.log('delayer:' + i);
  }, 0);
  console.log(i);
}
// 输出 0,1,2,3,4 delayer: 5, delayer: 5...
```
修改：
```
for (var i = 0; i < 5; i++) {
  (function (i) {
    setTimeout(function () {
      console.log('delayer:' + i);
    }, 0);
    console.log(i);
  })(i)
}
// 输出0,1,2,3,4 delayer: 0, delayer: 1, delayer: 2, delayer: 3, delayer: 4,
```

### 6. 如何获取元素的真实宽高
使用window.getComputedStyle()方法
```
var ele = doutment.getElementById("test")
window.getComputedStyle(ele).width //获取id为test元素的宽
window.getComputedStyle(ele).height //获取id为test元素的高
```
### 7. URL如何编码解码？为什么要编码？
JavaScript提供四个URL的编码/解码方法。

1. decodeURI()
2. decodeURIComponent()
3. encodeURI()
4. encodeURIComponent()
区别

- encodeURI方法不会对下列字符编码

  1. ASCII字母
  2. 数字
  3. ~!@#$&*()=:/,;?+'
- encodeURIComponent方法不会对下列字符编码

  1. ASCII字母
  2. 数字
  3. ~!*()'

所以encodeURIComponent比encodeURI编码的范围更大。
之所以要进行编码，是因为URL中有些字符会引起歧义。

### 8. 补全如下函数，判断用户的浏览器类型
```
function isAndroid() {
  return /Android/.test(window.navigator.userAgent)
}

function isIphone() {
  return /iPhone/.test(window.navigator.userAgent)
}

function isIpad() {
  return /iPad/.test(window.navigator.userAgent)
}

function isIOS() {
  return /iOS/i.test(window.navigator.userAgent)
}
```