---
title: html
date: 2018-12-18 10:08:41
tags:
---
# W3C 简介
>   网站	[W3C](www.w3.org W3C)
>   万维网联盟（World Wide Web Consortium，W3C），又称W3C理事会，是万维网的主要国际标准组织。为半自治非政府组织 。为解决网络应用中不同平台、技术和开发者带来的不兼容问题，保障网络   信息的顺利和完整流通，万维网联盟制定了一系列标准并督促网络应用开发者和内容提供者遵循这些标准。标准的内容包括使用语言的   规范，开发中使用的导则和解释引擎的行为等等。W3C也制定了包括XML和CSS等的众多影响深远的标准规范。 但是，W3C制定的网络标   准似乎并非强制，而只是推荐标准。因此部分网站仍然不能完全实现这些标准，特别是使用早期所见即所得网页编辑软件设计的网页往   往会包含大量非标准代码。
# MDN 简介
>   MDN Web Docs
>   MDN Web Docs.svg
>   网站	[MDN](developer.mozilla.org "MDN")
>   MDN Web Docs（旧称Mozilla Developer Network、Mozilla Developer Center，简称MDN）是一个汇集众多Mozilla基金会产品和网络技术开发文档的免费网站。该项目始于2005年，最初由Mozilla公司员工Deb Richardson领导。自2006年以来，文档工作由Eric Shepherd领导。网站最初的内容是由DevEdge提供，但在AOL收购Netscape后，DevEdge网站也宣布关闭。为此Mozilla基金会向AOL获取了DevEdge发布的内容，同时将DevEdge内容搬移到mozilla.org。MDN本身有一个论坛，并在Mozilla IRC网络上有一个IRC频道#mdn。MDN由Mozilla公司提供服务器和员工的资助。2016年10月3日发表的Brave网页浏览器将MDN作为其搜索引擎选项之一。
# HTML 
>  HTML（超文本标记语言）
>  网站 [w3c](www.w3.org/html/ "w3c")
>  超文本标记语言（英语：HyperText Markup Language，简称：HTML）是一种用于创建网页的标准标记语言。HTML是一种基础技术，常与CSS、JavaScript一起被众多网站用于设计令人赏心悦目的网页、网页应用程序以及移动应用程序的用户界面[3]。网页浏览器可以读取HTML文件，并将其渲染成可视化网页。HTML描述了一个网站的结构语义随着线索的呈现，使之成为一种标记语言而非编程语言。
>  HTML元素是构建网站的基石。HTML允许嵌入图像与对象，并且可以用于创建交互式表单，它被用来结构化信息——例如标题、段落和列表等等，也可用来在一定程度上描述文档的外观和语义。HTML的语言形式为尖括号包围的HTML元素（如<html>），浏览器使用HTML标签和脚本来诠释网页内容，但不会将它们显示在页面上。
# 什么是空标签
>   一个空元素（empty element）可能是 HTML，SVG，或者 MathML 里的一个不可能存在子节点（例如内嵌的元素或者元素内的文本）的element。HTML，SVG 和 MathML 的规范都详细定义了每个元素能包含的具体内容（define very precisely what each element can contain）。许多组合是没有任何语义含义的，比如一个 <audio> 元素嵌套在一个 <hr> 元素里。
>   在 HTML 中，通常在一个空元素上使用一个闭标签是无效的。例如，` <input type="text"></input> `的闭标签是无效的 HTML。在 HTML 中有以下这些空元素：
```
- <area>
+ <base>
- <br>
+ <col>
- <colgroup> when the span is present
- <command>
+ <embed>
- <hr>
+ <img>
- <input>
- <keygen>
+ <link>
+ <meta>
+ <param>
- <source>
+ <track>
+ <wbr>
```
# 什么是可替换标签
>   CSS 里，可替换元素`（replaced element）`的展现不是由CSS来控制的。这些元素是一类 外观渲染独立于CSS的 外部对象。 典型的可替换元素有` <img>、 <object>、 <video>` 和 表单元素，如`<textarea>、 <input>` 。 某些元素只在一些特殊情况下表现为可替换元素，例如` <audio> `和 `<canvas>` 。 通过 CSS content 属性来插入的对象 被称作 匿名可替换元素（anonymous replaced elements）。

>   CSS在某些情况下会对可替换元素做特殊处理，比如计算外边距和一些auto值。

>   需要注意的是，一部分（并非全部）可替换元素，本身具有尺寸和基线（baseline），会被像`vertical-align`之类的一些 CSS 属性用到。

