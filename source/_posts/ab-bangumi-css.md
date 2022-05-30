---
title: 修改AB_Bangumi的css使其与Argon主题风格大致保持一致
tags:
  - css
  - 技术
id: '108'
categories:
  - - 技术
date: 2021-08-06 11:24:52
cover: https://pic.zzzhxxx.top/2022/05/30/9e7a7097e9564.png
---


# 题外话

挺久没摸了，博客的系统从Wordpress到Typecho反复横跳，最终还是用回了Wordpress，趁着最近有时间把博客重新整修了一番

# 前言

由于Argon不自带追番功能，在Argon底层新写一个function又太麻烦，主题更新了还要重新写，于是在网上深度调研锁定了[梓喵](https://www.azimiao.com/ "梓喵")大佬写的wordpress追番插件

# 准备

加了大佬的qq群后拿到了插件，但是插件的风格是这样子的

![](https://pic.zzzhxxx.top/2021/08/06/3f081a763631e.png)

与Argon的圆角风实属违和，我用Argon就是为了他的圆角设计，所以开始修改插件的css文件

# 开始

## 修改导航栏样式

插件原生的导航栏带圆角，基本符合我的需求，但是文字始终是黑色而且鼠标悬停是也没有阴影的淡入，所以这是针对导航栏着重修改的点

打开css文件夹，修改里面的css文件  
![](https://pic.zzzhxxx.top/2021/08/06/c05101df22bed.png)

找到第226行中

```
#zm_ab_bangumi_nav li {
    display: inline-block;
    color: #666;
    padding: 10px;
    border-radius: 3px;
    border:1px solid rgba(160, 160, 160,0.3);
    text-decoration: none;
    margin: 0 1px;
    min-width: 10px;
    transition: background .2s linear;
    font-size: 12px;
    line-height: 12px;
    -o-user-select: none; 
    -moz-user-select: none; 
    /*firefox*/
    -webkit-user-select: none; 
    /*webkit浏*/
    -ms-user-select: none; 
    /*IE10+*/
    -khtml-user-select :none;
     /*早期的浏览器*/
    user-select: none; 
}
```

将 `border:1px solid rgba(160, 160, 160,0.3);`中的rgb的颜色改为自己主题的颜色，以我的为例

```
border:1px solid rgb(51, 143, 255);
```

再将`transition: background .2s linear;`更改为`transition-duration: 0.4s;`

接着修改下面的内容

在第大约250行

```
#zm_ab_bangumi_nav li.current{
 background: var(--zm_bangumi_color);
}

#zm_ab_bangumi_nav li:hover:not(.none){
    background: var(--zm_bangumi_color);
}
#zm_ab_bangumi_nav li.none{
    border:none;
}
```

更改为

```
#zm_ab_bangumi_nav li.current{
 background: var(--zm_bangumi_color);
 color: white;/*这个白色是鼠标悬停或点击后导航文字的颜色，可按自己的需求更改，下一个color同理*/

}

#zm_ab_bangumi_nav li:hover:not(.none){
    background: var(--zm_bangumi_color);
    box-shadow: 0 6px 8px 0 rgba(0,0,0,0.24), 0 8px 25px 0 rgba(0,0,0,0.19);/*悬停阴影*/
    color: white;

}
#zm_ab_bangumi_nav li.none{
    border:none;
}
```

## 为番剧介绍加上圆角

在第282行左右

```
.ab_bangumiItem{
    position: relative;
    width: 100%;
    max-width: 240px;
    height: 320px;
    overflow: hidden;
    margin: 0px;
    background-color: aliceblue;
    box-shadow:0 1px 3px rgba(0,0,0,0.5);
    font-family: 'Noto Serif SC','Source Han Serif SC','Source Han Serif','source-han-serif-sc','PT Serif','SongTi SC','MicroSoft Yahei',Georgia,serif;

}
```

为了使字体统一我删去了font-family，这个可以看个人喜好而定，接着删去box-shadow，加上`border-radius: 6px;`变为圆角，为了做到鼠标悬停阴影还需加上`transition-duration: 0.4s;`,换行再加一个hover

```
.ab_bangumiItem:hover{
    box-shadow: 0 6px 8px 0 rgba(0,0,0,0.24), 0 8px 25px 0 rgba(0,0,0,0.19);
}
```

## 介绍弹出速度

在鼠标悬停在番剧封面上时，会弹出番剧介绍，但是速度有点过快，打算调慢一点

在第372行，找到最后一个transition，把0.3s调成你想要的时间即可

```
.ab_bangumiDestription{
    position: absolute;
    left: 0;
    top:50%;
    width: 100%;
    display: flex;
    transform: translateY(50%);
    height: 100%;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    background-color: rgba(255, 255, 255, 0.9);
    font-weight: bold;
    color: #353535;
    visibility: hidden;
    opacity:0;
    transition:all 0.3s ease;
}
```

## 信息滚动条

在封面的底部存在一个信息滚动条，跟上面一样我也觉得过快了，也需调慢

在第354行,将最后的-100%调为-25%左右即可

```
@keyframes marquee{
    /* from {
        transform:translate(0,0);
       }
       to {
        transform:translate(-100%,0);
       } */
       0%{
        transform:translate(0,0);
       }
       15%{
        transform:translate(0,0);
       }
       100%{
        transform:translate(-100%,0);

       }
}
```

# 成品

导航条  
![](https://pic.zzzhxxx.top/2021/08/06/73e17d9a0421c.png)

圆角封面  
![](https://pic.zzzhxxx.top/2021/08/06/7dfaae757e1ab.png)

悬停阴影  
![](https://pic.zzzhxxx.top/2021/08/06/0fa34468fc06b.png)

具体效果可在本站追番页面查看

全css代码在[Github](https://github.com/zzzhxxx/Argon-css-for-AB_Bangumi "Github")

如有问题请在github提issue或者在本文后留言

# 感想

yysy虽然看上去就这么点步骤，真正要改到自己满意还是挺烦的