---
layout: post
title: "dukto port"
description: ""
category: 
tags: [dukto, port, iptable]
---
{% include JB/setup %}

Dukto是一个非常方便的局域网消息和文件传输软件，能够自动发现其他使用Dukto的用户，通过拖拽可以快速发送文件给其他用户。


>安装Dukto后，如果有防火墙，则需要打开TCP和UDP端口 "4644"

Linux平台上，iptables的命令是：

	$sudo iptables -I INPUT -p TCP --dport 4644 -j ACCEPT
	$sudo iptables -I INPUT -p UDP --dport 4644 -j ACCEPT

