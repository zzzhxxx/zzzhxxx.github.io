---
title: Python使用FFmpeg进行视频抽帧
tags:
  - ffmpeg
  - python
  - 技术
  - 视频处理
id: '296'
categories:
  - - 技术
date: 2022-01-23 16:48:55
---


# 前言

最近会了很多新东西，到时候会慢慢全部写下来，先把这个写下来

# 开始

首先是文件选择，这次放弃了上次使用的`win32ui`因为这次需要把抽出来的帧放到一个文件夹里，所以用python自带的tkinter

```
import tkinter as tk
from tkinter import filedialog
root=tk.Tk()
root.withdraw()
```

# FFmpeg

因为涉及视频处理，所以要使用`ffmpeg`，目前主要有两种通过python使用的方法，第一种是使用anaconda和pip一起安装库和依赖，另一种是下载ffmpeg的发行版通过shell调用，因为第一种太烦这里使用第二种

```
import subprocess
```

首先引入`subprocess`

`subprocess`其实可以比喻成一个包壳的命令行，原则上可以在命令行中实现的事情都可以使用subprocess在python中实现，固然可以实现ffmpeg

```
subprocess.Popen(ffmpegpath +' -i'+ ' ' + filename+ ' ' +'-qscale:v 1 -qmin 1 -qmax 1 -vsync 0 ' + pathname +'/frame%08d.png', shell=True)
```

这里的`ffmpegpath` `filename` `pathname`会稍后再提

# 路径处理

这里来处理上文提到的路径

`ffmpegpath`代表了ffmpeg的文件位置，因为和代码在一个文件夹下，所以可以直接定义

```
import os
ffmpegpath=os.getcwd()+'/ffmpeg/bin/ffmpeg.exe'
```

`filename`是用来储存视频文件的路径的变量，而`pathname`是用来储存输出文件夹路径的变量，这个时候就需要用到上面引入的tkinter了

```
pathname=filedialog.askdirectory()
filename=filedialog.askopenfilename()
```

这样路径也就处理好了

现在再来看subprocess部分的代码就很好理解，用单引号框住的全是ffmpeg的变量，剩下的则是我们定义的变量

# 最终效果

这里以一段海贼王的视频为例

![视频](https://pic.zzzhxxx.top/2022/01/23/06aaeb7956713.png)

输出文件夹选择新一个叫做tmp\_frames的文件夹

![](https://pic.zzzhxxx.top/2022/01/23/eccaf8c5cb9fa.png)

选择文件

![](https://pic.zzzhxxx.top/2022/01/23/8a1b5c4851737.png)

在终端检查一下运行状况

![](https://pic.zzzhxxx.top/2022/01/23/f7778bed57120.png)

输出文件夹

![](https://pic.zzzhxxx.top/2022/01/23/6f42ef4ecda52.png)

# 总结

至此工作就已经大致结束了，ffmpeg还可以实现很多其他的功能，像转码录屏等等，我这里抽帧是为了输送到realesrgan进行超分，ffmpeg的github参考在这篇文章的顶部，另外一个是这篇文章的代码