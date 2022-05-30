# hexo-bilibili-bangumi-butterfly

![](https://fp1.fghrsh.net/2021/02/16/18f1c5a45a473786b01cc39bebc92a44.png!webp)

## 追番

> 想给博客加一个追番列表，但是我在去年（2020年）没找到那些关于hexo的，所以没有QAQ
> 好在，现在有啦~

## 部署

Github：[https://github.com/XiaoLFeng/hexo-bilibili-bangumi-butterfly](https://github.com/XiaoLFeng/hexo-bilibili-bangumi-butterfly)

安装代码：

```powershell
npm install hexo-bilibili-bangumi-butterfly --save
```

升级代码：

```powershell
npm install hexo-bilibili-bangumi-butterfly --update --save
```

将下面的配置写入站点的配置文件 **<font color="red">_config.yml</font>** 里(不是主题的配置文件).

```yml
bangumi:
  enable: true
  path:
  vmid:
  title: '追番列表'
  quote: '不宅也不肥'
  show: 1
  loading:
  metaColor:
  color:
  webp:
  progress:
```

* **enable**: 是否启用
* **path**: 番剧页面路径，默认bangumis/index.html
* **vmid**: 哔哩哔哩番剧页面的 vmid(uid),如何获取？
* **title**: 该页面的标题
* **quote**: 写在页面开头的一段话，支持 html 语法，可留空。
* **show**: 初始显示页面：0: 想看, 1: 在看, 2: 看过，默认为1
* **loading**: 图片加载完成前的 loading 图片
* **metaColor**: meta 部分(简介上方)字体颜色
* **color**: 简介字体颜色
* **webp**: 番剧封面使用webp格式(此格式在safari浏览器下不显示，但是图片大小可以缩小 100 倍左右), 默认true
* **progress**: 获取番剧数据时是否显示进度条，默认true

## 使用方式

在 <font color="#DAA520">hexo generate</font> 或 <font color="#DAA520">hexo deploy</font> 之前使用

```powershell
hexo bangumi -u
```
命令更新番剧数据！

删除数据命令

```powershell
hexo bangumi -d
```

例如（代码）

```powershell
hexo bangumi -u && hexo clean && hexo g -d
```

### 获取 uid

登录哔哩哔哩后前往[https://space.bilibili.com/](https://space.bilibili.com/)页面，网址最后的一串数字就是 **uid**

<font color="red">需要将追番列表设置为公开！</font>

## Lisense

[Apache Licence 2.0](https://github.com/XiaoLFeng/hexo-bilibili-bangumi-butterfly/blob/master/LICENSE)
