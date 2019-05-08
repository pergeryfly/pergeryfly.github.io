---
title: 简单实现一个jQuery的API
date: 2019-05-03 18:10:25
categories: jQuery
tags: jQuery
---
`DOM`的`API`应该可以算是反人类了，所以JQuery应运而生。在我的理解里，jQuery应该就是把`DOM`的`API`封装成函数 ，配合事件绑定实现功能，举例来说就是这样：
```
var $div = $('div')    //输入div
$div.addClass('red')  // 可将所有 div 的 class 添加一个 red
$div.setText('hi')  // 可将所有 div 的 textContent 变为 hi
```
这里哟们可以用`DOM`来试着实现同样的效果。
# DOM代码
```
window.jQuery = function(_x){
  let e;
  if(typeof _x === "string"){
    e = document.querySelectorAll(_x);
  }else{
    e = _x;
  }
  return {
    addClass: function(_classStr){
      for(let i=0; i<e.length;i++){
        e[i].classList.add(_classStr);
      }
    },
    setText: function(_textStr){
      for(let i=0; i<e.length;i++){
        e[i].textContent = _textStr;
      }
    }
  }
}
window.$ = jQuery

var $div = $('div')

$div.addClass('red') // 可将所有 div 的 class 添加一个 red
$div.setText('hi') // 可将所有 div 的 textContent 变为 hi
```
# 细节描述
## 1.传递参数
`var $div =$('div')`
要实现上面这个功能，我的理解是首先设置window对象jQuery为函数返回的结果，然后把参数'div'传递到函数内的DOM，作为变量进行下一步的操作。
```
window.jQuery=function（selector）{  
let alldiv=document.querySelectorAll(selector)  
}

window.$ = jQuery
```
## 2.返回对象
```
$div.addClass('red')  // 可将所有 div 的 class 添加一个 red
$div.setText('hi')  // 可将所有 div 的 textContent 变为 hi
```
可以观察得到$div是一个对象，它的key有addClass和setText。

那我也返回一个含有addClass和setClass的对象。
```
window.jQuery=function (selector){
let alldiv=document.querySelectorAll(selector)  
  return{
       addClass:function (){},
       setClass：function(){}
  }
}
window.$ = jQuery
```
## 3.补全对象的key
我们得到了alldiv，它是一个伪数组。如果每个div都要添加class的话，需要一个for循环，然后每一次用DOM的方法里的classList.add功能对div添加class。
```
addClass: function(){
               for(var i=0;i<alldiv.length;i++){
                   alldiv[i].classList.add("red")
               }
```
同理
```
setText: function(){
               for(var i=0;i<alldiv.length;i++){
                  alldiv[i].textContent = "hi"
              }
```
把addClass和setText的内容结合到函数内，得到：
```
window.jQuery=function (selector){
  let alldiv=document.querySelectorAll(selector)
  return{
       addClass: function(){
               for(var i=0;i<alldiv.length;i++){
                   alldiv[i].classList.add("red")
               }
       },
       setText: function(){
               for(var i=0;i<alldiv.length;i++){
                  alldiv[i].textContent = "hi"
              }
      }
   }
}
window.$ = jQuery
```
# 总结
这样就简单实现了一个jQuery的API,原理大致相同，但jQuery的细节应该更加充实了。