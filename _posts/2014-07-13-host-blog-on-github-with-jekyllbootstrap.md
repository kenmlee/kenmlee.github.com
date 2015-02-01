---
layout: post
title: "Hosting blog on github with jekyllbootstrap"
description: ""
category: blog
tags: []
---
{% include JB/setup %}

将BLOG放在github上是个不错的选择，首先这是免费的，其次所有内容都是版本化的（当然也就不能用数据库了，全是文件方式），然后还是跨平台的。前提是你得会git，当然你知道github，肯定是会git的。


github上有两种模式，一种是用户或者组织页面，一种是项目页面。顾名思义，用户或者组织页面可以用于用户或者组织的BLOG，而项目页面最好用于某个项目的BLOG。


两者URL格式不同，用户页面是:

    <username>.github.io

项目页面是:

    <username>.github.io/<repositoryname>


如果要用jekyllbootstrap，就只能用用户页面，好处是安装简单方便。如果想自己折腾，当然可以用项目页面，加上jekyll，然后再配置bootstrap。


步骤如下：

1. 注册github账号
2. 创建一个用户仓库
3. 设置GitHub Pages
4. 在本机上克隆jekyll-bootstrap仓库
5. 将本机仓库的远程设置为新创建的github仓库
6. 将本机仓库推到远程
7. 本机安装jekyll和rake等
8. 修改初始页面并推送到远端
9. 用rake创建新的blog条目或者页面
