## this 相关问题

### 1. apply、call 、bind有什么作用，什么区别
call()和apply()的作用是改变函数的执行上下文，改变this的指向，第一部分参数是要指定的执行上下文，第二部分则是传入的参数。二者的区别在于传入参数的形式的不同，如：
```
func.apply(Obj, [argArray])
func.call(Obj, arg1, arg2, arg3)
```

bind()是ES5的方法，它是用来实现上下文的绑定，与call相似，可接受的参数部分分为两部分，第一个参数都是作为执行时函数上下文中的this的对象，但是bind的返回值是函数，call是改变上下文并执行函数。

### 2. 以下代码输出什么?

```
var john = { 
  firstName: "John" 
}
function func() { 
  alert(this.firstName + ": hi!")
}
john.sayHi = func
john.sayHi()

//输出: John: hi!
```

### 3. 下面代码输出什么，为什么

```
func() 
function func() { 
  alert(this)
}

//输出: [object Window], 这是因为this指向的是全局作用域下的window对象
```

### 4. 下面代码输出什么

```
document.addEventListener('click', function(e){
    console.log(this);
    setTimeout(function(){
        console.log(this);
    }, 200);
}, false);

// 输出: #document Window
// 第一个this指向的是document，而setTimeout中的this指向全局的window对象，超时调用的代码都是在全局作用域中执行的
```

### 5. 下面代码输出什么，why

```
var john = { 
  firstName: "John" 
}

function func() { 
  alert( this.firstName )
}
func.call(john)

// 输出: John
// 原因是func.call()改变了其执行上下文，将func的this指向john
```

###  6. 以下代码有什么问题，如何修改

修改如下

```
var module= {
  bind: function(){
    var _this = this
    $btn.on('click', function(){
      console.log(this) //this指什么
      //这里的this指的是$btn对象
      _this.showMsg();
    })
  },
  
  showMsg: function(){
    console.log('饥人谷');
  }
}
```

## 原型链相关问题

7. 有如下代码，解释Person、 prototype、__proto__、p、constructor之间的关联。

```
function Person(name){
    this.name = name;
}
Person.prototype.sayName = function(){
    console.log('My name is :' + this.name);
}
var p = new Person("若愚")
p.sayName();

// Person.prototype.constuctor === Person
// p.__proto__ === Person.prototype
// p instanceof Person === true
```

### 8. 上例中，对象 p可以这样调用 p.toString()。toString是哪里来的? 画出原型图?并解释什么是原型链。

toString()继承自Object.prootype，对象p执行toString()方法时，首先从它的自由属性开始查找，若不存在，则向p.__proto__中查找（其中p. __proto__  === Person.prototype）, 若仍没有，则继续向Person.prototyp.__proto__中查找，最终在其中找到Object.prototype.toString()方法，过程如图所示：

==原型链：==  原型链作为实现继承的主要方法，其基本思想是利用原型让一个引用类型继续继承另一个引用类型的属性和方法。每个对象都有一个指向它原型对象的内部链接（__proto__）。这个原型对象又有自己的原型，直到某个对象的原型为null为止，组成这条链的最后一环，这种一级一级的链结构就称为原型链。

### 9. 对String做扩展，实现如下方式获取字符串中频率最高的字符

```
var str = 'ahbbccdeddddfg';
var ch = str.getMostOften();
console.log(ch); //d , 因为d 出现了5次
```

代码如下：

```
String.prototype.getMostOften = function(){
  var obj = {};
  for (var i = 0;i<this.length;i++){
    var char = this.charAt(i);
    if(obj[char]){
      obj[char]++;
    }else{
      obj[char] = 1;
    }
  }
  var max = 0;
  var word = "";
  for(var key in obj){
    if(max<obj[key]){
      max = obj[key];
      word = key;
    }
  }
  console.log(word + ', ' + '因为'+word+'出现了'+max+'次');
};

```

### 10.  instanceof有什么作用？内部逻辑是如何实现的？

```
instanceof运算符用来测试一个对象在其原型链中是否存在一个构造函数的prototype属性。可以检测某个对象是不是另一个对象的实例。
```

内部逻辑： 

```
 A instanceof B,
判断规则是: 
先查找A的__proto__链，
同时查找B的prototype链，
一旦二者相等，
则返回true，否则返回false。
```

## 继承相关问题

### 11. 继承有什么作用?

继承的作用是子类共享父类的属性和方法，可以覆盖和扩展父类的属性和方法。继承可以减少内存的使用，提高代码的重用性。

### 12. 下面两种写法有什么区别?

```
//方法1
function People(name, sex){
    this.name = name;
    this.sex = sex;
    this.printName = function(){
        console.log(this.name);
    }
}
var p1 = new People('饥人谷', 2)

//方法2
function Person(name, sex){
    this.name = name;
    this.sex = sex;
}

Person.prototype.printName = function(){
    console.log(this.name);
}
var p1 = new Person('若愚', 27);

// 方法1的printName写在构造函数的内部。方法二则写在构造函数的prototype对象上。
// 前者在每生成一个实例后实例中的printName都会占用内存
// 后者生成的一个实例对象后会共享构造函数prototype对象上的printName方法，达到节省内存的效果 
```

### 13. 