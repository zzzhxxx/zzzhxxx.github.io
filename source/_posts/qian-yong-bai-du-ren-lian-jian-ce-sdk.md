---
title: 浅用百度人脸检测SDK
tags:
  - AI
  - 人脸检测
  - 技术
id: '359'
categories:
  - - 技术
date: 2022-04-13 16:40:56
<<<<<<< HEAD
cover: https://pic.zzzhxxx.top/2022/05/30/a08ad96e3b70b.png
=======
>>>>>>> a597a24e1f7e6d8057e941b01dfcd91c2ba0c5b7
---

# 前言

上信息课的时候提到了百度的人脸检测的SDK并且有个附加作业是要识别图像的性别并用不同颜色的框表示，本来上课一直摸鱼一个字都不听的我当场就不困了，直接开搞

# 准备

## 安装依赖

因为要用百度的SDK所以先安装一下百度的包

```python
pip intsall baidu-aip
```

为了画框还要安装pillow

```python
pip intsall pillow
```

## 申请API\_KEY

进入百度智能云的[控制台](https://console.bce.baidu.com/),在左侧菜单产品服务里找到人脸识别，进入板块后创建应用即可，注意要个人实名认证领取免费额度，不然没额度也没法检测

# 代码编写

## 库

首先需要`import`一下需要用到的库

```python
from turtle import width
from aip import AipFace
import base64
from PIL import Image,ImageDraw
```

## 图像预处理

百度要求以base64传入图片，所以需要对图片进行预处理变为base64编码

```
filepath = "01.webp" 
#图片打开方式
fp=open(filepath, "rb") 
#对图片进行base64编码
base64_data = base64.b64encode(fp.read())
image = base64_data.decode()
#定义图像类型
imageType = "BASE64"
```

## 设置密钥

注意保存刚刚申请的密钥，调用会方便一点

```python
APP_ID = '*****'
API_KEY = '*****'
SECRET_KEY = '*****'
```

## 初始化

引入刚才保存的密钥

```python
aipFace = AipFace(APP_ID, API_KEY, SECRET_KEY)
```

然后需要设定一下可选的参数,详细的接口文档在[这里](https://cloud.baidu.com/doc/FACE/s/ek37c1qiz#%E4%BA%BA%E8%84%B8%E6%A3%80%E6%B5%8B)

我这里选用了需要的设定，一个是`face_field`里的`gender`选项用来取得所识别出来的性别，同时要设定`max_face_num`来确定识别的最大人数

```python
options = {}
options["face_field"] = 'gender'
options["max_face_num"] = 2
```

## 调用

非常简单，一行代码

```python
result = aipFace.detect(image, imageType, options)
```

## 数据读取

返回的数据是以是一串多维数组,里面的数据类似于这样

```

{
  "face_num": 1,
  "face_list": [
        {
            "face_token": "35235asfas21421fakghktyfdgh68bio",
            "location": {
                "left": 117,
                "top": 131,
                "width": 172,
                "height": 170,
                "rotation": 4
            },
            "face_probability": 1,
            "angle" :{
                 "yaw" : -0.34859421849251
                 "pitch" 1.9135693311691
                 "roll" :2.3033397197723
            }
            "landmark": [
                {
                    "x": 161.74819946289,
                    "y": 163.30244445801
                },
                ...
            ],
            "landmark72": [
                {
                    "x": 115.86531066895,
                    "y": 170.0546875
                }，
                ...
            ],
            "age": 29.298097610474,
            "beauty": 55.128883361816,
            "expression": {
                "type": "smile",
                "probability" : 0.5543018579483
            },
            "gender": {
                "type": "male",
                "probability": 0.99979132413864
            },
            "glasses": {
          "type": "sun",
                "probability": 0.99999964237213
            },
            "face_shape": {
                "type": "triangle",
                "probability": 0.5543018579483
            }
            "quality": {
                "occlusion": {
                    "left_eye": 0,
                    "right_eye": 0,
                    "nose": 0,
                    "mouth": 0,
                    "left_cheek": 0.0064102564938366,
                    "right_cheek": 0.0057411273010075,
                    "chin": 0
                },
                "blur": 1.1886881756684e-10,
                "illumination": 141,
                "completeness": 1
            }
        }
    ]
}
```

我们建几个空数组来存这些数据

```python
genders={}
left={}
top={}
width={}
height={}
```

接下来就是存数据了，写一个循环，循环里主要就是把`result`里的数据向不同的数组里存，所以用`result['result']['face_list']['人脸编号']`来读取不同人脸对应的数据，在后面继续加上`['location']['方向']`可以获得人脸的边界，加上`['gender']['type']`获取性别

# 画图

常规操作，把图片打开

```python
im=Image.open("01.webp")
draw=ImageDraw.Draw(im)
```

后面再接一个循环，因为要求不同性别用不同的颜色的框，所以循环里要加上性别的判断

```python
for i in range(2):
    if genders[i]=='male':
        draw.rectangle((left[i], top[i], left[i]+width[i], top[i]+height[i]), outline = (255,0,0))
    if genders[i]=='female':
        draw.rectangle((left[i], top[i], left[i]+width[i], top[i]+height[i]), outline = (0,255,0))
```

最后保存图片

```python
im.save("output.png","PNG")
```

大功告成

# 效果

找不到啥可以用的图，所以用松冈和爱衣的合照试一下 运行前

![before](https://pic.zzzhxxx.top/2022/04/13/f00198adf3cbc.png)

运行后:

![after](https://pic.zzzhxxx.top/2022/04/13/992a901ac8070.png)

# 问题

第一次运行的时候报错`ModuleNotFoundError: No module named 'chardet'`我才发现没装`chardet`库，`pip install`一下即可