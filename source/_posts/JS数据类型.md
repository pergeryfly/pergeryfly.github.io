---
title: JS数据类型
date: 2019-04-14 16:11:22
categories: JS
tags: JS
---

JS共有七种数据类型：number、string、boolean、symbol、underfined、null，以及object。这其中boolean类型不常用，不做赘述，这次对其他6种数据类型总结一波。
# 1.分类
从不同角度对6种数据类型进行分类：
![img](./1.png)
# 2.判断
## 1.typeof
typeof返回一个表示数据类型的字符串。返回结果包括number、string、boolean、underfined、null，以及object。typeof可以对基本类型number、string  、boolean、undefined做出准确的判断（null除外，typeof null===“object”，这是由于历史的原因，我就不巴拉巴拉了，其实我也说不清楚😢）；而对于引用类型，除了function之外返回的都是object。但当我们需要知道某个对象的具体类型时，typeof就显得有些力不从心了
## 2.instanceof
当我们需要知道某个对象的具体类型时,可以用运算符 `instanceof，instanceof`操作符判断左操作数对象的原型链上是否有右边这个构造函数的`prototype`属性，也就是说指定对象是否是某个构造函数的实例，最后返回布尔值。 检测的我们用一段伪代码来模拟instanceof内部执行过程：
```
instanceof (A,B) = {
    var L = A.__proto__;
    var R = B.prototype;
    if(L === R) {
        //A的内部属性__proto__指向B的原型对象
        return true;
    }
    return false;
}
```
## 3.delete
我们可以使用`delete`操作符删除对象里的key，使用如下：
```
var obj ={name："xxx"；}
delete obj.name
"name" in obj //false
```
## 4.forin
`for...in`循环用来遍历一个对象的全部属性。
```
var obj = {a: 1, b: 2, c: 3};

for (var i in obj) {
  console.log(obj[i]);
}
// 1
// 2
// 3
```
下面是一个使用`for...in`循环，提取对象属性名的例子。
```
var obj = {
  x: 1,
  y: 2
};
var props = [];
var i = 0;

for (var p in obj) {
  props[i++] = p
}

props // ['x', 'y']
```
`for..in`循环有两个使用注意点。
> 它遍历的是对象所有可遍历（enumerable）的属性，会跳过不可遍历的属性。
> 它不仅遍历对象自身的属性，还遍历继承的属性。
# 3.类型转换
## 1.任意类型转字符串
1.String（x）
```
String(1)
"1"
String(true)
"true"
String(null)
"null"
String(undefined)
"underfined"
String({})
"[object object]"
```
2.x.toString()
3.x + ""
## 2.任意类型转数字
1.Number（X）
2.parseInt(x, 10) MDN
3.parseFloat(x) MDN
4.x - 0
5.+x
## 3.任意类型转布尔
1.Boolean（x）
2.！！x
五个falsy值0、NaN、“”、null、underfined。
对象转布尔永远是true。
# 4.内存图
JS引擎将内存分为代码区和数据区，其中数据区区分为Stack（栈内存）和Heap（堆内存），简单类型的数据直接存在Stack里，复杂类型的数是把Heap地址存在Stack里。
# 5.深拷贝与浅拷贝
## 1.对于简单类型来说，复制就是深拷贝。
## 2.对于复杂类型的数据（对象）来说。才要区分浅拷贝和深拷贝。
这是一个浅拷贝的例子
```
var a = {name: 'frank'}
var b = a
b.name = 'b'
a.name === 'b' // true
```
这里对b进行更改后，a也随之变化，这就是典型的浅拷贝。
对于深拷贝而言，对b进行更改，a不会产生变化，
```
var a = {name: 'frank'}
var b = deepClone(a) // deepClone 还不知道怎么实现
b.name = 'b'
a.name === 'frank' // true
```
这就是典型的深拷贝了。



