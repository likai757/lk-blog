---
title: CentOS 6.5 Shadowsocks Server配置
date: 2016-07-14 14:10:00
categories:
- Tools
tags:
- vpn
- server
---

## 安装Shadowsocks
	yum install python-setuptools && easy_install pip
	pip install shadowsocks

## 创建并修改JSON配置文件
	touch /etc/shadowsocks.json
	vi /etc/shadowsocks.json

```
{
	"server":"0.0.0.0",
	"server_port":8388,
	"local_address": "127.0.0.1",
	"local_port":1080,
	"password":"your_pwd",
	"timeout":600,
	"method":"aes-256-cfb"
}

server: 服务器外网服务IP
server_port : 服务器外网服务端口
local_address : 本地服务IP
local_port : 本地服务端口
password : 登录密码
timeout : 超时时间
method : 加密方式

```

详细配置参数请参考：[Shadowsocks-ArchWiki](https://wiki.archlinux.org/index.php/Shadowsocks_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))

##启动服务
	ssserver -c /etc/shadowsocks.json -d start  //启动
	ssserver -c /etc/shadowsocks.json -d stop   //停止
