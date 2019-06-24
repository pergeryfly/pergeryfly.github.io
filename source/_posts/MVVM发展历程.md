---
title: MVVM发展历程
date: 2019-06-19 23:56:39
categories: MVVM
tags: MVVM
---

# 1. 三层架构
三层架构就是将整个业务应用划分为：
UI层：界面层（User Interface layer）
BLL层：业务逻辑层（Business Logic Layer）
DAL层：数据访问层（Data access layer）

区分层次的目的是为了“高内聚低耦合”
在软件体系架构设计中，分层式结构是最常见，也是最重要的一种结构。微软推荐的分层式结构一般分为三层，从下至上分别为：数据访问层、业务逻辑层（又或称为领域层）、表示层。

# 2.MVC
如下图所示
![](1.png)
代码如下：
```
// 一个关于数据操作，页面展示的 js 文件的mvc的代码组织形式
! function (){
var view = document.querySelector('section.message')

var model ={
//初始化数据
init: function(){
var APP_ID = 'XXX';
var APP_KEY = 'xxx';
AV.init({ appId: APP_ID, appKey: APP_KEY });
},
// 获取数据
fetch: function(){
var query = new AV.Query('Message')
return query.find() // Promise 对象
},
// 新建数据
save: function(name, content){
var Message = AV.Object.extend('Message');
var message = new Message();
return message.save({ // Promise 对象
'name': name ,
'content': content
})
}
}

var controller = {
view: null,
model: null,
messageList: null,
init: function(view,model){
this.view = view
this.model = model

this.messageList = view.querySelector('#messageList')
this.form = myForm = view.querySelector('form')
this.model.init()
this.loadMessages()
this.bindEvents()
},
loadMessages: function(){
this.model.fetch().then( (messages) => {
let array = messages.map((item) => item.attributes)
array.forEach((item) => {
let li = document.createElement('li')
li.innerText = `${item.name}: ${item.content}`
let messageList = document.querySelector('#messageList')
messageList.appendChild(li)
})
}, function (error) {
console.log('提交失败, 请改天再留言')
});
},
bindEvents: function(){
this.form.addEventListener('submit', function (e){
e.preventDefault()
this.saveMessage()
}.bind(this)) // 用bind将this绑定到 funtion 里面
},
saveMessage: function(){
let myForm = this.form
let content = myForm.querySelector('input[name=content]').value
let name = myForm.querySelector('input[name=name]').value
this.model.save(name, content).then(function(object) {
let li = document.createElement('li')
if(object.attributes.name !== '' && object.attributes.content !== '') {
li.innerText = `${object.attributes.name}: ${object.attributes.content}`
let messageList = document.querySelector('#messageList')
messageList.appendChild(li)
myForm.querySelector('input[name=content]').value = ''
myForm.querySelector('input[name=name]').value = ''
}
})
}
}
controller.init(view, model)

}.call()
```
缺点：
视图与控制器间的过于紧密的连接，不利于View的组件化，即可复用性低
视图对模型数据的低效率访问
没有UI环境，Controller的单元测试变得困难
# 3. MVP（MVC 的改良）

MVP与MVC最大的区别就用Presenter将Model和View隔开了，不允许其互相直接通信，所有的消息都是通过Presenter这个中间人来传递。
如下图所示：
![](2.png)

缺点：
View层和Presenter层是通过接口连接，在复杂的界面中，维护过多接口的成本很大
View和Presenter层的交互会过于频繁，二者联系太过紧密
# 4. MVVM（MVP 的改良）

MVVM代表的是Model-View-ViewModel，将MVP中的P换成VM（视图模型），它的依赖关系和MVP是一样的
MVVM把View和Model的同步逻辑通过binder自动化了。MVP的Presenter负责的View和Model同步不再需要手动操作，而是交由框架所提供的Binder进行负责
Vue.js就是MVVM框架的一种典型实现，它的核心思想为数据驱动和组件化
缺点：
数据绑定使得 Bug 很难被调试