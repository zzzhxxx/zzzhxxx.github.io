---
title: 美化uptime-status
tags:
  - css
  - js
  - 美化
  - 魔改
id: '198'
categories:
  - - 技术
date: 2021-08-23 22:21:06
<<<<<<< HEAD
cover: https://pic.zzzhxxx.top/2022/05/30/b660b61c7f9e8.png
=======
>>>>>>> a597a24e1f7e6d8057e941b01dfcd91c2ba0c5b7
---


# 起因

最近云盘总是崩溃所以打算加个uptimerobot监视一下

# 魔改

正好solstice23大佬也用uptimerobot监控，所以照着他的页面样式写了一个，js代码太长不好贴，只贴几个css主要修改的地方

```
#header {
    background-image:url(https://pic.zzzhxxx.top/2021/07/06/bf1a8b8dbcc9e.JPG!compress);
    background-size:100% 100%;
    background-size:cover;
    background-repeat:no-repeat;
    background-attachment:fixed;
    height:60vh
}
#uptime .loading {
    background:url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA1MCA1MCI+PHBhdGggZmlsbD0iI0Q2RDhEOCIgZD0iTTE5LjUyIDQyLjcxMmM5Ljg5NyAyLjkxNiAyMC4yODUtMi43NDMgMjMuMjAxLTEyLjY0bC0zLjkwMi0xLjE1Yy0yLjI4MSA3Ljc0Mi0xMC40MDcgMTIuMTctMTguMTUgOS44ODhsLTEuMTUgMy45MDJ6Ij48YW5pbWF0ZVRyYW5zZm9ybSBhdHRyaWJ1dGVUeXBlPSJ4bWwiIGF0dHJpYnV0ZU5hbWU9InRyYW5zZm9ybSIgdHlwZT0icm90YXRlIiBmcm9tPSIwIDI1IDI1IiB0bz0iMzYwIDI1IDI1IiBkdXI9IjAuNnMiIHJlcGVhdENvdW50PSJpbmRlZmluaXRlIi8+PC9wYXRoPjwvc3ZnPg==) 50%/40px 40px no-repeat;
    height:100px
}
#uptime .meta {
    justify-content:space-between;
    margin-bottom:20px
}
#uptime .meta,#uptime .meta .info {
    display:flex;
    align-items:center
}
#uptime .meta .name {
    font-size:16px;
    line-height:20px;
    color:#525f7f
}
#uptime .meta .link {
    background:url(data:image/svg+xml;base64,PHN2ZyBjbGFzcz0iaWNvbiIgdmlld0JveD0iMCAwIDEwMzYgMTAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48cGF0aCBkPSJNNjAwLjgxOCA2OTcuNmMtNzAuNCAwLTEzNC40LTI1LjYtMTkyLTc2LjgtMjUuNi0yNS42LTI1LjYtNjQtNi40LTg5LjYgMjUuNi0yNS42IDY0LTI1LjYgODkuNi02LjQgNTcuNiA1MS4yIDE0Ny4yIDUxLjIgMTk4LjQgMGwxNjYuNC0xNjYuNGMyNS42LTI1LjYgMzguNC02NCAzOC40LTEwMi40IDAtMjUuNi02LjQtNjQtMzguNC05Ni01Ny42LTUxLjItMTQ3LjItNTEuMi0xOTguNCAwbC02NCA3Ni44Yy0yNS42IDI1LjYtNjQgMjUuNi04OS42IDAtMjUuNi0yNS42LTI1LjYtNjQgMC04OS42bDcwLjQtNzAuNGMxMDIuNC0xMDIuNCAyNjguOC0xMDIuNCAzNzcuNiAwIDUxLjIgNTEuMiA4My4yIDExNS4yIDgzLjIgMTkyIDAgNzAuNC0yNS42IDEzNC40LTc2LjggMTkybC0xNjYuNCAxNjYuNGMtNTcuNiA0NC44LTEyMS42IDcwLjQtMTkyIDcwLjR6IiBmaWxsPSIjODQ5MkE2Ii8+PHBhdGggZD0iTTI3NC40MTggMTAyNGMtNzAuNCAwLTEzNC40LTI1LjYtMTkyLTc2LjgtMTA4LjgtOTYtMTA4LjgtMjYyLjQtNi40LTM3Ny42bDE2Ni40LTE2Ni40YzEwOC44LTEwMi40IDI3NS4yLTEwMi40IDM3Ny42IDAgMjUuNiAyNS42IDI1LjYgNjQgMCA4OS42cy02NCAyNS42LTg5LjYgMGMtNTEuMi01MS4yLTE0MC44LTUxLjItMTk4LjQgMGwtMTY2LjQgMTY2LjRjLTQ0LjggNTEuMi02NCAxNDAuOCAwIDE5OC40IDU3LjYgNTEuMiAxNDcuMiA1MS4yIDE5OC40IDBsNzAuNC03MC40YzI1LjYtMjUuNiA2NC0yNS42IDg5LjYgMHMyNS42IDY0IDAgODkuNmwtNzAuNCA3MC40Yy00NC44IDUxLjItMTA4LjggNzYuOC0xNzkuMiA3Ni44eiIgZmlsbD0iIzg0OTJBNiIvPjwvc3ZnPg==) 50%/100% 100% no-repeat;
    width:13px;
    height:13px;
    margin-left:6px;
    opacity:.6;
    text-indent:-99999px;
    transition:opacity .3s ease-out
}
#uptime .meta .link:hover {
    opacity:1
}
#uptime .meta .status {
    background:0/14px auto no-repeat;
    font-size:14px;
    position:relative
}
#uptime .meta .status.ok {
    color:#4fd69c
}
#uptime .meta .status.down {
    color:#f75676
}
#uptime .meta .status.unknow {
    color:#eee
}
#uptime .meta .status.ok:after,#uptime .meta .status.ok:before {
    content:"";
    display:inline-block;
    width:12px;
    height:12px;
    background:#4fd69c;
    margin-right:8px;
    border-radius:10px;
    position:absolute;
    left:-20px;
    top:1px
}
#uptime .meta .status.down:after,#uptime .meta .status.down:before {
    content:"";
    display:inline-block;
    width:12px;
    height:12px;
    background:#f75676;
    margin-right:8px;
    border-radius:10px;
    position:absolute;
    left:-20px;
    top:1px
}
```

# 使用

1.  将git上的仓库clone至您的服务器
2.  修改config.js
3.  在`/static/js/main.4a0f818c.js`中搜索`zzzhxxx`并将其替换成您自己的名字
4.  在`/static/css/`中的css文件搜索`https://pic.zzzhxxx.top/2021/07/06/bf1a8b8dbcc9e.JPG!compress`并将链接替换成您想要的背景图片

# 鸣谢

原项目作者 yb

[仓库地址](https://github.com/yb/uptime-status)

[solstice23](https://solstice23.top/)的页面原型

背景图来自[香风智乃官方认证老公](https://t.bilibili.com/525357646573634221?tab=2)修的22/7计算中season2 BD全卷购买特典box插图