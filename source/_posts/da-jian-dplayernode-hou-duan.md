---
title: 搭建Dplayer-node后端
tags:
  - dplayer
  - node
  - 技术
id: '400'
categories:
  - - 技术
date: 2022-05-27 13:34:56
---

# 前言

dplayer的后端之前其实早就搭好了，只是最近服务器重启了一下服务掉了再次启动的时候发现启动不起来，所以重新搭建了一下

# 踩雷

由于第一次搭建的时间距离现在比较久远，以至于我都忘记了用的是docker还是node直接启动，照着github上的README用docker部署死活不成功，搞了一个上午，发现很多设置已经过时了，所以用node会更简单

# 依赖

## 安装redis

```bash
curl -fsSL https://packages.redis.io/gpg  sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main"  sudo tee /etc/apt/sources.list.d/redis.list

sudo apt-get update
sudo apt-get install redis
```

## 安装mongodb

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc  sudo apt-key add -

echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse"  sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list

sudo apt-get update

sudo apt-get install -y mongodb-org
```

## 启动服务

```bash
sudo systemctl start mongod
```

### redis后台启动

```bash
cp redis.conf /usr/local/redis/bin/
```

找到daemonize，改为yes

```bash
redis-server /usr/local/redis/bin/redis.conf
```

# 启动服务

```
cd Dplayer-node
npm install
node index.js
```

可以挂一个screen在后台运行

# 反向代理

用宝塔做一个反向代理

![](https://pic.zzzhxxx.top/2022/05/27/4c356a8fc0f28.png)

EOF