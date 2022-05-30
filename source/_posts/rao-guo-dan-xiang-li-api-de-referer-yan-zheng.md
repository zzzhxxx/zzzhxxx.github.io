---
title: 绕过单向历api的referer验证
tags:
  - php
  - 技术
id: '217'
categories:
  - - 技术
date: 2021-08-24 21:00:59
---


# 前言

一直想在web上放个单向历，但是单向历的api有referer验证，所以想了个办法绕过

本方法理论上可以绕过各种基本Referer验证

# 开始

单向历的api地址是`http://img.owspace.com/Public/uploads/Download/YYYY/MMDD.jpg`

首先要解决的问题是日期的变换

考虑到需要日期变换和在服务器上运行，这次选用php

## 日期变换

这个问题在php下很好解决，只需要调用一个date函数就行，并且定义一个变量来存date

```
$a = date("Y/md");
```

## 合成链接

得到了日期的参数就很好解决了

只需要合成一个正确的链接地址即可

同样用php解决

```
$txt = "http://img.owspace.com/Public/uploads/Download/$a.jpg";
```

本来想着到这里把链接传给服务器就足够了，但是尝试后发现api有referer验证，查了几种常用的绕referer方法后还是觉得直接用服务器访问读取信息最简单

## 抓取信息

既然选择了这种方法就需要用php显示图片了

```
header('Content-type: image/jpeg');
```

然后用最简单粗暴的方法用`` `file_get_contents` ``直接读取图像信息

```
    echo file_get_contents($txt);
```

大功告成

全代码

```
<?php
    $a = date("Y/md");
    $txt = "http://img.owspace.com/Public/uploads/Download/$a.jpg";
    header('Content-type: image/jpeg');
    echo file_get_contents($txt);
?>
```

这里再提供一个通用的的代码

```
echo file_get_contents(isset($_GET["url"])?$_GET["url"]:'');
```

需要在文件后传入参数

如`https://xxxx.com/xxx.php?url=imgurl`