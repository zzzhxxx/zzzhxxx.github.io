---
title: 使用Python实现csv图像绘制
tags:
  - python
  - 技术
  - 数据可视化
id: '239'
categories:
  - - 技术
date: 2021-08-25 22:22:22
<<<<<<< HEAD
cover: https://pic.zzzhxxx.top/2022/05/30/e2ed500d5a19a.png
=======
>>>>>>> a597a24e1f7e6d8057e941b01dfcd91c2ba0c5b7
---


# 前言

最近有处理csv的需求，于是摸了个这个出来

众所周知Python对于数据可视化性能不是很高，所以这种方法只能处理少量数据，几百条应该没问题

# 开始

## 文件选择

为了易用性加了个文件选择的功能，用到了`win32ui`库(需要用pip提前安装pypiwin32)

效果像这样

![文件选择](https://pic.zzzhxxx.top/2021/08/25/cb193a27f1c3b.png)

首先import一下这个库

```
import win32ui
```

调用系统窗口

```
dlg = win32ui.CreateFileDialog(1)
dlg.SetOFNInitialDir('E:/Python') 
dlg.DoModal()
```

这时存储文件名，因为后面要用到

```
filename = dlg.GetPathName() 
```

## 读取csv文件

Python自带csv处理库，现在只要调用就行

```
import csv
```

读取文件列信息

```
with open(filename) as f:
        reader = csv.reader(f)
        header_row = next(reader)
```

这时候加一个print来看一下是否能够正常读取

```
for index, column_header in enumerate(header_row):
                print(index, column_header)
```

![](https://pic.zzzhxxx.top/2021/08/25/dc813a8f82755.png)

能够看到正常读取就可以删了

# 存数据

由于我的csv只有两种数据，定义两个数组即可(记得放在循环内)

```
        dates,ch1 = [],[]
```

然后把数据存进数组

```
for row in reader:
            dates.append(row[0])
            ch1.append(row[1])
```

再写一个print检查一下

```
print(dates)
```

![](https://pic.zzzhxxx.top/2021/08/25/99952ed702c9e.png)

# 绘制

绘图用到了`matplotlib`

常规操作

```
from matplotlib import pyplot as plt
```

定义一下窗口大小还有dpi

```
fig = plt.figure(dpi=64, figsize=(20,12))
```

定义一下x轴和y轴的数据

```
x_values=dates
y_values=ch1
```

绘制函数，同时设置折线颜色以及图标标题

```
plt.plot(x_values,y_values,c='red')
plt.title("CSV", fontsize=24)
plt.xlabel('',fontsize=16)//x轴单位
plt.ylabel("", fontsize=16)//y轴单位
plt.tick_params(axis='both', which="major", labelsize=16) 
```

最后让他显示

```
plt.show()
```

# 效果

![](https://pic.zzzhxxx.top/2021/08/25/749730a5da138.png)

# 忠告

切勿用于大量数据处理，否则软件会异常卡顿(亲身经历)，如果你硬要处理大数据，为什么不用Matlab呢？