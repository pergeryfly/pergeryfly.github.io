---
title: 关于this、call、apply和bind
date: 2019-06-25 02:21:06
categories:
tags:
---
# 1.this
## 1.1 this 到底是什么？
this 就是 call 方法传递的 第一个参数，接下来给出转换公式：
`fn(x) <=> fn.call( undefined , x)`
在 严格模式(‘use strict’) 下this 就是的 undefined，非严格模式下，浏览器会默认把undefined 变成 window
`a.b.c. fn(x) <=> a.b.c. fn.call(a.b.c, x)`
this 就是 a.b.c1.2 this 题目分析1.2.1 严格模式与非严格模式下的 this

```
var f1 = function (){
    'use strict' // 使用严格模式
    console.log(this)
}
f1() // undefined，不是对象; f1()等价于f1.call(undefinded)
f1.call(null) // null，不是对象
f1.call(5201314) // 5201314, 不是对象
f1.call(true) // true, 不是对象
f1.call(x) // 报错，x 未定义
```
---------------------------------------------------------------
```
var f1 = function (){
    console.log(this)
}
f1() // window，对象; f1()等价于f1.call(undefinded)
f1.call(null) // window，对象
f1.call(5201314) // 5201314, number对象
f1.call(true) // true, boolean对象
f1.call(x) // 报错，x 未定义
```

## 1.2.2 青铜段位的this

```
var a = 1
var obj1 = {
a:2,
fn:function(){
console.log(this.a)
}
}
obj1.fn() //2 obj1.fn.call(obj1)，this就是obj1
```
## 1.2.3 白银段位的this

```
var obj = {
foo: function(){
console.log(this)
}
}
var bar = obj.foo
obj.foo() // 转换为 obj.foo.call(obj)，this 就是 obj
bar() // bar.call() => bar.call(undefined), 结果是 window 对象

function fn2(){}
function fn (){ console.log(this) }
var arr = [fn, fn2]
arr[0]() // [ƒ, ƒ], this 就是 arr, 相当于arr.0.call(arr)
```
## 1.2.4 黄金段位的this

```
button.onclick = function f1(){
    console.log(this)
} // 看文档，搜索 MDN onclick，文档说给处理器的 this 是触发事件的元素，这里是button

button.addEventListener('click', function(){
    console.log(this)
}) // 看文档，搜索 MDN addEventListener，this是该元素的引用，这里是button

$('ul').on('click', 'li', function(){
    console.log(this)
}) // 看文档，搜索jQuery on，当jQuery的调用处理程序时,
//this关键字指向的是当前正在执行事件的元素,这里就是 'li'
```
## 1.2.5 铂金段位的this

```
button.onclick = function(){
　　function fn(){
　　　　console.log(this); // 竟然是 window, 蛋疼
　　}
　　fn(); // 其实就是这个函数的执行，等价于 fn.call(undefined)，this 就是undefined
};
button.onclick = function(){
　　var _this = this; // this 是 button
　　function fn(){
　　　　console.log(_this); // _this 是botton ，将失去的 this 找回了
　　}
　　fn();
};
```
// 也可以用下面的写法
```
button.onclick = function(){
　　var fn = function(){
　　　　console.log(this); //call 传递的this 值
　　}.call(this); // button
};

var obj={}
obj.fn=function(){
    console.log(this) // obj {fn: function}
    ! function(){
        console.log(this) // window
    }() // 记住一个结论，匿名函数的执行具有全局性，所以传入的是undefined, 所以this是window

}
obj.fn()
```
## 1.2.6 钻石段位的this

```
var obj={
    fn:function(){
        setTimeout(function(){
            console.log(this);
        }，100);
    }
}
obj.fn();//window
// 记住一个结论:
// this出现在全局函数setTimeout()中，在setTimeout的延迟函数(非箭头函数)内，this指向 window

var obj={
    fn:function(){
        console.log(this) // obj
        setTimeout(() => {
            console.log(this); // 就是外面的 this: obj
        });
    }
}
obj.fn(); // 箭头函数中的 this 就是外面的this，这句话很重要
```
## 1.2.7 最强王者的this
```

function X(){
return object = {
name: 'object',
options: null,
f1(x){
this.options = x // 第2步：这个x是第一步传递的options，this是第一步的call的
this.f2() //第一个参数 x(外面的x),它是由x = X()决定, 就是X()的返回值，object
},
f2(){
this.options.f2.call(this) // 第3步：第一个this 是object, 第二个this 也是object
}
}
}

var options = {
name: 'options',
f1(){},
f2(){
console.log(this) // 第4步：这个this是第3步传进来的this, object
}
}

var x = X()
x.f1(options) // object，第1步：改写 x.f1.call(x, options)
```
再也不想看到this了。。。
# 2. call、apply 、bind
## 2.1 三者异同
它们都是用来改变 this 的指向的
call()和apply()功能相同，唯一不同的是传参的时候call第二个参数只能传递参数列表，而apply可以是列表也可以是arguments或数组
使用call和apply会直接执行这个函数，而bind并不直接执行，而是将绑定好的this重新返回一个新函数，什么时候调用由你自己决定，bind的传参方式和call相同

```
function f(a, b) {
console.log(this)
console.log(a)
console.log(b)
}

f() //window, undefined, undefined

/*call*/
f.call('a', 2, 3) //'a', 2, 3
f.call('a', 2) //'a', 2, undefined
f.call() //window, undefined, undefined

/*apply*/
f.apply('a', [2, 3]) //'a', 2, 3
f.apply('a', [2]) //'a', 2
f.apply() //window, undefined, undefined

/*bind*/
nf = f.bind('a', 2, 3) //bind方法返回一个新函数
nf() // 'a', 2, 3
nf = f.bind('a', 2)
nf() // 'a', 2，undefined
nf = f.bind('a')
nf() // 'a', undefined, undefined
nf = f.bind()
nf() // window, undefined, undefined
```
## 2.2 对于箭头函数

箭头函数会捕获其所在上下文的 this 值，作为自己的 this 值
扩展： 箭头函数和普通函数的区别
箭头函数不能使用 new 命令，它作为匿名函数是不能成为构造函数的
箭头函数没有 arguments 对象，但是可以用 Rest 参数代替

```
var fn = (...x)=>{ // ...x 即为rest参数
console.log(x);
}
fn(1, true, function(){}) // [1, true, ƒ]
```
不可以使用 yield 命令, 因此箭头函数不能用作 Generator 函数
通过 call() 或 apply() 方法调用时，只是传入了参数而已，对 this并没有什么影响
箭头函数没有原型属性