---
title: ajax
date: 2019-06-03 01:45:03
categories: ajax
tags: ajax
---
# ajax如何发请求？

用 form 可以发请求，但是会刷新页面或新开页面
用 a 可以发 get 请求，但是也会刷新页面或新开页面
用 img 可以发 get 请求，但是只能以图片的形式展示
用 link 可以发 get 请求，但是只能以 CSS、favicon 的形式展示
用 script 可以发 get 请求，但是只能以脚本的形式运行
有没有什么方式可以实现
```
	 get、post、put、delete 请求都行
	 想以什么形式展示就以什么形式展示
```

## 微软的突破
```
`IE 5` 率先在 JS 中引入 `ActiveX `对象（`API`），使得 `JS `可以直接发起 `HTTP` 请求。
随后 `Mozilla`、 `Safari`、 `Opera` 也跟进（抄袭）了，取名 `XMLHttpRequest`，并被纳入 `W3C` 规范
```
## AJAX
`Jesse James Garrett `將如下技术取名叫做 `AJAX`：异步的 `JavaScript `和` XML`
```
	 使用 XMLHttpRequest 发请求
	 服务器返回 XML 格式的字符串
	 JS 解析 XML，并更新局部页面
```

## 如何使用 XMLHttpRequest
```
myButton.addEventListener('click', (e)=>{
let request = new XMLHttpRequest()
request.open('get', '/xxx') // 配置request
request.send()
request.onreadystatechange = ()=>{
if(request.readyState === 4){
console.log('请求响应都完毕了')
console.log(request.status)
if(request.status >= 200 && request.status < 300){
console.log('说明请求成功')
console.log(typeof request.responseText)
console.log(request.responseText)
let string = request.responseText
// 把符合 JSON 语法的字符串
// 转换成 JS 对应的值
let object = window.JSON.parse(string)
// JSON.parse 是浏览器提供的
console.log(typeof object)
console.log(object)
console.log('object.note')
console.log(object.note)

}else if(request.status >= 400){
console.log('说明请求失败')
}

}
}
})

// 后端代码
}else if(path==='/xxx'){
response.statusCode = 200
response.setHeader('Content-Type', 'text/json;charset=utf-8')
response.setHeader('Access-Control-Allow-Origin', 'http://frank.com:8001')
response.write(`
{
"note":{
"to": "小谷",
"from": "方方",
"heading": "打招呼",
"content": "hi"
}
}
`)
response.end()
```
## 同源策略
只有 协议+端口+域名 一模一样才允许发 AJAX 请求
一模一样一模一样一模一样一模一样一模一样一模一样一模一样一模一样
浏览器必须保证
只有 协议+端口+域名 一模一样才允许发 AJAX 请求
CORS 可以告诉浏览器，我俩一家的，别阻止他
突破同源策略 === 跨域
Cross-Origin Resource Sharing
C O源 R SCORS 跨域