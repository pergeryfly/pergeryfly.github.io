---
title: hexo重装
date: 2019-03-19 21:31:02
categories:
  hexo
tags:
  hexo
  git
  npm
---
最近我的小米笔记本硬盘存储吃紧，加了块硬盘结果出了问题只能重装系统。搞得什麽都要重新配置，今天刚配置完git发现个人博客居然崩了，着实不能忍，Google了一波，决定放弃目录，重新来过。
## 1. 新建`blog`文件，初始化。
```
       mkdir blog
       hexo init blog
       cd blog
       npm install
```

## 2. 改动 `_config.yml`文件。
```
       deploy:
       type: git
       repo: 仓库地址
```

## 3. 文件覆盖
 覆盖`module、source、themes`文件夹，主题居然还可以正常使用，很是nice。
## 4. 登录检测
高兴的我`hexo g`一下，又`hexo s`一下，打开浏览器输入网址`http://localhost:4000`，美滋滋，我的博客全回来了。
## 5.终曲
 ok，是时候去`github`嗨一波了，果断敲出
 `hexo d`
于是bash告诉我
    `ERROR Deployer not found: git`
问题不大，只要继续
    `npm install hexo-deployer-git --save`
Enjoy :)
