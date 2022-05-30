---
title: 搭建Zerotier-Planet服务器
tags:
  - zerotier
  - 服务器
id: '368'
categories:
  - - 技术
date: 2022-04-29 19:06:27
cover: https://pic.zzzhxxx.top/2022/05/30/1b8c998bd7be9.png
---

# 前言

网课在家无聊，和朋友联机玩游戏，SakuraFrp老是拉跨所以直接转战zerotier，因为担心zerotier的国外服务器所以把planet部署在了自己的服务器上

## Zerotier 是啥

> ZeroTier 是一款非常简单易用的内网穿透工具，不需要配置，就能实现虚拟局域网的组建

# 开始

## 依赖

为了部署简单所以开发者使用了docker

\[github author="Jonnyan404" project="zerotier-planet"\]\[/github\]

## 如果啥也不会

```
docker run --restart=on-failure:3 -d --name ztncui -e HTTP_PORT=4000 -e HTTP_ALL_INTERFACES=yes -e ZTNCUI_PASSWD=mrdoc.fun -p 4000:4000 keynetworks/ztncui
```

## 正常步骤

```
git clone https://github.com/Jonnyan404/zerotier-planet
cd zerotier-planet
docker-compose up -d
```

开放4000端口，访问服务器ip:4000就可以访问

# 配置

默认的用户名和密码是admin/mrdoc.fun

打开Add Network添加一个虚拟局域网组

![](https://pic.zzzhxxx.top/2022/04/29/e9696be9c1f92.png)

创建好后点击Easy Setup配置ip地址段

![](https://pic.zzzhxxx.top/2022/04/29/aff0124438c01.png)

如果没啥个性化需求直接点击Generate就行

点击submit提交，返回主页面后将名字旁的id添加到zerotier客户端即可

# 测试

## Ping

拉了个人来测试

![](https://pic.zzzhxxx.top/2022/04/29/9516538c50c45.png)

打开cmd，ping一下，若能成功则说明配置成功

![](https://pic.zzzhxxx.top/2022/04/29/67ed609fb8a2a.png)

大功告成

## 游戏

保险起见将一些局域网游戏也测了一下，主要测了mc、泰拉瑞亚、星露谷物语，结果均成功且延迟低

实现局域网游戏联机自由！