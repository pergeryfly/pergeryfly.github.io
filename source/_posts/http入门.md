---
title: http入门
date: 2018-12-13 11:33:33
tags:
---

# 关于http的请求与响应
## http请求
**请求示例**
`` curl -s -v -H "Frank: xxx" -- "https://www.baidu.com" ``
请求的内容为
```
GET / HTTP/1.1
Host: www.baidu.com
User-Agent: curl/7.54.0
Accept: */*
Frank: xxx
```
**请求的格式**
1 动词 路径 协议/版本
2 Key1: value1
2 Key2: value2
2 Key3: value3
2 Content-Type: application/x-www-form-urlencoded
2 Host: www.baidu.com
2 User-Agent: curl/7.54.0
3 
4 要上传的数据
**用 Chrome 发请求**
1.打开 Network
2.地址栏输入网址
3.在 Network 点击，查看 request，点击「view source」
4.点击「view source」，可以看到请求的前三部分了
## http响应 ##
**响应示例**
前面的请求对应的响应：
```
HTTP/1.1 200 OK
Accept-Ranges: bytes
Cache-Control: private, no-cache, no-store, proxy-revalidate, no-transform
Connection: Keep-Alive
Content-Length: 2443
Content-Type: text/html
Date: Tue, 10 Oct 2017 09:14:05 GMT
Etag: "5886041d-98b"
Last-Modified: Mon, 23 Jan 2017 13:24:45 GMT
Pragma: no-cache
Server: bfe/1.0.8.18
Set-Cookie: BDORZ=27315; max-age=86400; domain=.baidu.com; path=/

<!DOCTYPE html>
<!--STATUS OK--><html> <head> 后面太长，省略了……
```
**响应的格式**
1 协议/版本号 状态码 状态解释
2 Key1: value1
2 Key2: value2
2 Content-Length: 17931
2 Content-Type: text/html
3
4 要下载的内容
**用 Chrome 查看响应**
1.打开 Network
2.输入网址
3.选中第一个响应
4.查看 Response Headers，点击「view source,会看到响应的前两部分
5.查看 Response 或者 Preview，你会看到响应的第 4 部分