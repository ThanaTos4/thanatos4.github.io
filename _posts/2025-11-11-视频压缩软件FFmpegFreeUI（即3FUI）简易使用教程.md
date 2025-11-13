---
layout:     post   				    # 使用的布局（不需要改）
title:      视频压缩软件FFmpegFreeUI（即3FUI）简易使用教程			 
subtitle:   FFmpegFreeUI #副标题
date:       2025-11-11				# 时间
author:     wuxia						# 作者
header-img: img/post-bg-2015.jpg	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签

  - FFmpegFreeUI
  - 知乎
---

# 视频压缩软件FFmpegFreeUI（即3FUI）简易使用教程

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-f43c2dbc5935eec2a83709552d03ea06_r.jpg)

Q群：1050613952

B站教学：[你也许该换一款转码软件了！来试试新的 GUI：FFmpegFreeUI (3FUI)_哔哩哔哩_bilibili](https://link.zhihu.com/?target=https%3A//www.bilibili.com/video/BV1eeH9zLED5/)

**如果您是从知乎推荐来到这篇文章，没有看过B站视频或其他文章介绍，不认识FFmpegFreeUI，这里作简要介绍：**

> 3FUI集齐了格式工厂**（保留源文件日期）**+ShanaEncoder**（软件主体功能五五开）**+[命令行脚本](https://zhida.zhihu.com/search?content_id=262194792&content_type=Article&match_order=1&q=命令行脚本&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3NjMwMjczODYsInEiOiLlkb3ku6TooYzohJrmnKwiLCJ6aGlkYV9zb3VyY2UiOiJlbnRpdHkiLCJjb250ZW50X2lkIjoyNjIxOTQ3OTIsImNvbnRlbnRfdHlwZSI6IkFydGljbGUiLCJtYXRjaF9vcmRlciI6MSwiemRfdG9rZW4iOm51bGx9.dZcczUB3lUBqGCnjp4ORZjFGQ4ZSsloTnQCEDgfwDI4&zhida_source=entity)**（可完全自定义参数 可自己替换FFmpeg.exe文件）**的优点。
> 3FUI界面中的参数选项比ShanaEncoder更多，是更偏专业向的软件。但也意味着小白更难入门，所以我写了这篇教程文章。
> ShanaEncoder也能自定义参数（按F8打开参数面板），但是用过的都知道，和直接敲命令行不太一样。比如shana并不把烧录字幕的选项显示在参数面板中；还默认保留第1条音频轨道(-map 0:a:0)，没法移除，用户自己加“-map 0:a”就会多复制一条0号音轨，很麻烦。
> 3FUI则原原本本显示命令行参数，你可以直接将自己的脚本参数复制过来用。

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-fe993c6cb46bbb631c8ed1f806ef4e5c_r.jpg)

> **请用电脑或者手机浏览器桌面模式观看本文，为保证GIF动图足够清晰，我把GIF全换成了webp格式，在网页上观看没问题，但是手机知乎APP上看，GIF就不动了……**

本篇文章尽量少讲参数理论，只讲 FFmpegFreeUI 如何安装，小白要“点哪里”、“设置什么”。

视频压缩软件的参数是共通的，无论小丸、格式工厂、ShanaEncoder、HandBrake还是3FUI，都是一样用，“知一即百”，因为他们内部都使用FFmpeg，可选参数共通。（除了HandBrake自己特制的AMF编码器用的秘制小参数，跟别人不共通）

所以，假如您有时间请看：

1、 [小刻也能看懂的视频压缩入门四万字超大型科普：CRF、显卡加速、VMAF测视频画质、小丸工具箱、格式工厂、ShanaEncoder、HandBrake、命令行bat脚本、安卓手机压缩视频](https://zhuanlan.zhihu.com/p/1913258114746122747)

2、 [维什戴尔也能看懂的视频压缩5000字入门：CRF、FFmpeg、显卡加速、VMAF测画质得分](https://zhuanlan.zhihu.com/p/1943027518480294814)

看完上述基础知识文章，今后使用压缩软件都不再需要教程，可以直接上手。

**文章中出现的图片都可以双击放大观看，如果仍不够清晰可以右键并“在新标签页打开图像”。**

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-d1fb424ddfbb97dcdcf2e1cc2d1c70f4_r.jpg)

## 本文一览

关键标题摘要：

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-0814cc0a96647fd2e5801c1091a1be71_r.jpg)

电脑端可点击左侧目录跳转，手机app可点击上方目录。

或者在手机浏览器登陆网页知乎，并切换浏览器页面为“桌面模式”。

## 一、下载FFmpegFreeUI

### 1、Github下载

Github主页：[https://github.com/Lake1059/FFm](https://link.zhihu.com/?target=https%3A//github.com/Lake1059/FFmpegFreeUI/releases)

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-5b8efd82fa1621eb865ac7bbde2d57bb_1440w.jpg)

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-bed9f6758870079941fee65dff2ed7f8_r.jpg)

大部分人登陆Github需要使用梯子。如果您没有......

可以用**steam++**（2022年后改名为Watt Toolkit）的免费梯子：[Watt Toolkit](https://link.zhihu.com/?target=https%3A//steampp.net/)

如果steam++速度很慢，可尝试右键复制文件链接，粘贴到该网站下载： [Github Proxy 文件代理加速](https://link.zhihu.com/?target=https%3A//github.akams.cn/)

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-07aa4805c2422a7771e1d0de20a35de2_r.jpg)

### 2、国内官网下载

如果还是很慢，可以到**3FUI的官网**选择“第三方镜像源”下载：[FFmpegFreeUI - 免费开源的FFmpeg图形界面](https://link.zhihu.com/?target=https%3A//ffmpegfreeui.top/index.html)

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-d3b30519f1f3a281afc478b622c4a63f_r.jpg)

“第三方镜像源”是热心群友提供的下载服务器，如果有条件请尽可能从Github下载，能增加Github的“总下载量”数据。

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-8be0e811221bc5a40db1437a580850b7_r.jpg)

### **重要排错：如果下载后无法打开软件，没有任何软件窗口弹出：**

**很可能需要重装系统。**

请放心，这不是你的电脑问题，而是使用.net编写的软件偶尔会出现的奇怪通病，当前无解。

请先按下图步骤走一遍，至少尝试把系统更到最新（不是说要win10升到win11，而是把更新补丁打了）

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-27deefe9c37a918b39be83bf947d3193_r.jpg)

如果都尝试过了，还是无法启动软件，并且除了3FUI，还无法打开ScreenToGif（大家都知道的GIF编辑软件）的 2.41.3 版本，：[https://github.com/NickeManarin/ScreenToGif/releases/tag/2.41.3](https://link.zhihu.com/?target=https%3A//github.com/NickeManarin/ScreenToGif/releases/tag/2.41.3)

但却能打开 ScreenToGif 2.41.2 版本，那么便说明这是“神秘的.net”问题。目前只能重装系统。

> 但放心，你的电脑系统仍是正常的。可以试试把系统硬盘拔下来，插到其他电脑上，可能会发现“突然能运行 3FUI 和 ScreenToGif 2.41.3 了！”，非常奇怪。把硬盘再插回原来的电脑，又没法运行这俩软件了。
> 明明系统软件环境一样，连硬件也一样，为什么A电脑可以运行，B电脑无法运行？
> 为什么系统重装之后，A电脑才可以运行？
> 为什么会有这种奇案？天晓得。
> 不要怀疑自己，.net全背锅罢。

## 二、下载FFmpeg

FFmpeg windows版本下载： [CODEX FFMPEG @ gyan.dev](https://link.zhihu.com/?target=https%3A//www.gyan.dev/ffmpeg/builds/)

> 使用mac和Linux的同学应该不用教罢。

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-b53a89aca74f424a6605f3cc9d0a4005_r.jpg)

**第一种使用方式**：将FFmpeg主体文件与3FUI应用程序放置于相同文件夹

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-27ed15da230dc6e742d09c4ca3bf6124_r.jpg)

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-3eb0d0e0dec3882b381a5deb46fd594b_r.jpg)

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-8b90cce1fa0dce819102190154b4d6ac_r.jpg)

**第二种使用方式**：将FFmpeg的文件路径添加入“windows环境变量”中。

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-0f22ef5ae7132455b0d336679169c8d6_r.jpg)

> 注意：环境变量路径不要填到具体文件名，填到文件夹这一级便可
> 【路径\路径\bin\FFmpeg.exe】 ✘
> 【路径\路径\bin】 ✔

**这两种使用方式的原理都是相同的：都是让3FUI知道FFmpeg在哪，从而调用FFmpeg压缩视频。**

第一种，将FFmpeg.exe与3FUI.exe放在相同的文件夹，自然知道FFmpeg在哪儿。

第二种，环境变量，等于是把 FFmpeg.exe 的文件路径“挂出来”，以便任何软件都能找到并使用FFmpeg。

**不恰当的比喻，相当于“浏览器收藏夹”**。3FUI：“我知道了，你在这里！”

这是一个全局通用的快捷路径，压缩软件调动FFmpeg的时候，要么从软件的文件夹里调动，要么从环境变量的众多文件路径里挑第一个识别到的FFmpeg路径来用。

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-5646be717b79d0da14a449c829ce1074_r.jpg)

试想，如果没有“环境变量”这个功能，FFmpeg放在D盘，压缩软件放在E盘，软件不可能把你的C盘、D盘、E盘全扫一遍来找“FFmpeg.exe”在哪个文件夹对吧。



### 为什么不将FFmpeg集成进软件里？为什么要用户自行下载，而不像格式工厂和ShanaEncoder等众多软件一样内置？

换个问法：可让用户自行下载更新FFmpeg的压缩软件，具有哪些优势？

讲个故事：[视频压缩入门四万字科普](https://zhuanlan.zhihu.com/p/1913258114746122747)

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-9577581cedd669fee6c58f7973a7170f_r.jpg)

> 学会下载FFmpeg是新人必须经历的第一道门槛，如果这都放弃学习，往后使用3FUI会更加困难。
> 学会了，便具备365天随时下载最新版本FFmpeg的能力。
> 可以四个月、半年、一年更新一次FFmpeg，编码器的性能是日新月异的。

## 三、软件设置

请下载好软件后，打开软件，跟着文章来使用。

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-3160043f91571fa3107f7ecaa82bffa7_r.jpg)

### 解码设置

> 别选

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-8c86e02aec106eb807da2005b2163fc7_r.jpg)

### 编码器设置

重点，简单解释：

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-91cbd91cb4a701610429947e2ff15ef9_r.jpg)

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-eccf21d24a62a82386a90186cdf7b446_r.jpg)

> **注意！内存相关需求：**
> 使用CPU压制视频对内存容量有一定要求，当内存不足时，软件会红字报错，无法压缩视频。
> **libsvtav1，动用32线程，压4K视频，经常占用10多GB内存，电脑只有16G内存的同学需要注意。**
> 可以选择“libx264”和“[libx265](https://zhida.zhihu.com/search?content_id=262194792&content_type=Article&match_order=1&q=libx265&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3NjMwMjczODYsInEiOiJsaWJ4MjY1IiwiemhpZGFfc291cmNlIjoiZW50aXR5IiwiY29udGVudF9pZCI6MjYyMTk0NzkyLCJjb250ZW50X3R5cGUiOiJBcnRpY2xlIiwibWF0Y2hfb3JkZXIiOjEsInpkX3Rva2VuIjpudWxsfQ.6cMORmwKTUIt_JxZUvLZyQRn6NxhJPwoq9jy-PQDS3A&zhida_source=entity)”，用32线程压4k视频是5GB左右内存占用。
> 这里只是举个例子，具体内存占用视具体情况而定。
> 动用的cpu线程数越多、压制的视频分辨率越大、视频的画面越复杂，占用内存越多。

**且慢：如果您是从目录跳到此处的，略过了下载FFmpeg的章节，记得回去下，否则就会：**

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-3d95e9e5c959ece8325d5ed57e21d444_r.jpg)

复杂解释：

**1、【必定设置】编码格式与编码器**

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-c05afdc59986144f9e9499802b21f583_r.jpg)

**2、【必定设置】速度预设**

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-48e4558297ba305b173c6d156c895900_r.jpg)

**为何这样选择“速度预设”？**

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-d346f32dee6865d985bccf5c9ebc37e1_r.jpg)

请看测试：[视频压缩大测试结果报告：CPU编码、显卡编码、H264、H265、AV1 - 知乎](https://zhuanlan.zhihu.com/p/1919229481572340130)

### 画面帧设置

> 没事不用选，有事不用教。

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-ba14e7f6bb16203a4733bed2bcff1850_r.jpg)

### 质量设置

**3、【必定设置】质量参数**

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-bb25a6898fc5035143bb864520529f6f_r.jpg)

这就是上方给过的编码路线图

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-29b91f42191422bf4a553d867520ab26_r.jpg)

**为什么这样选“质量参数”？**

还是请看：[视频压缩大测试结果报告：CPU编码、显卡编码、H264、H265、AV1 - 知乎](https://zhuanlan.zhihu.com/p/1919229481572340130)

### 音频参数设置

> opus什么的，有在用吗

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-9d722e5fb5f5f87eb760e7b734f7df36_r.jpg)

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-499430df2045df8216b04027e8f41b69_r.jpg)

几十块钱的“音频信号放大器”

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-248fead5e80d69a28954c7ee5208b777_r.jpg)

3FUI在Github的issue（提问区）里的问题。

### 保留多个字幕轨道和音频轨道

下图讲的是如何把**源视频自身的音频轨道和字幕轨道**保留下来。

如果你想将 A视频.mp4 和 B音频.mp3 合并到一起，这种操作叫**“混流”**，可以点左侧目录跳到最下面的**“其他功能：混流与合并”**的章节。

如果你想将外部的 ass、srt 格式字幕文件合进视频里，可以跳到更下面的**“其他功能：内封字幕和烧录(内嵌/硬嵌)字幕”**的章节。

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-6bcc0891200ae1478d0a2268574ee730_r.jpg)

想保留字幕的时候，一定要记得选MKV，好吗。

**下图科普含量较多，如果暂时不想深入研究，可以跳过。**

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-ddab77a6f4fff2e09fdf1f8711f6e2b6_r.jpg)

只要涉及“视频文件轨道”的压缩操作，必定要知晓“-map”参数。

### 保留源文件日期（自己写参数注意事项）

> 不需要的话便不用设置

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-fa56c1414423ed9d94578b7e5f512dfe_r.jpg)

图中参数： <KeepCreationTime> <KeepWriteTime> <KeepAccessTime>

**3FUI可以让你像使用命令行脚本一样，完全自己写参数。**这里比较专业，小白可以跳着看。

> 知乎回答经常有“向AI问个参数自己跑命令行，比GUI软件好得多”还有几百赞的评论。

**这里用GIF演示用法，并说明两个注意事项：**

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-c128688f251ea8579ced6314e095faf2_r.jpg)

演示：通过“自己写参数”的功能将视频转为RMVB格式

GIF中的参数：-i "<InputFile>" -c:v rv20 -b:v 3000k -g 25 -vf "scale=1280:720" -c:a ra_144 -ar 8000 -ac 1 -f rm -y "<OutputFile>"

GIF中的网址：[全网唯一可用的MP4转RMVB、RM格式视频的方法和探究过程-CSDN博客](https://link.zhihu.com/?target=https%3A//blog.csdn.net/donglxd/article/details/146343084)

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-8edaa5d61f30a375e24b880dbb6b0124_r.jpg)

该功能注意事项

### “最终防线”

> “完了”

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-3b5e54ca1025b3dcc1476fdf54ebd9e4_r.jpg)

### 添加文件与转换视频格式

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-f8ba7ee60fa86cd5778f22120f9c181b_r.jpg)

> **PS：视频文件格式（mp4、mkv）并不是视频轨道的编码格式（h264、h265）**，“复制流”就是不改动后者，直接改变前者，没有繁重的重新编码过程，所以一瞬间就可以完成这个“转封装”的操作。

什么叫“给每个文件单独设置不同的参数”？

举例，让每个视频文件输出到不同文件夹：

拖入文件——“加入编码队列”——更改目录——再拖入文件——再点“加入编码队列”，这样就行了。

**多任务设置**

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-14374465fceb9917f13c09204d870dcb_r.jpg)

即使设定同时压缩99个视频，总的速度也不会变99倍的。

> **在压单个视频时，没办法让 FFmpeg 压所有视频都一定动用全部 cpu 线程。**
> 一般是压高复杂度的 4k 视频才能占满任务管理器里的 CPU 线程框框。
> 压低复杂度的 1080p 视频，如果 FFmpeg 大人懒得出力可能就占不满你的32线程 CPU。
> 这时可以同时运行多个任务，**同时压4个视频基本就能保证什么情况都能吃满cpu了**，总速度能达到最大。
> 如果你在用8线程cpu，那就不用太担心不能吃满的问题（
> 不要说加“-threads 32“ 参数，这真没用罢。

### 设置完成与压缩演示

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-3160043f91571fa3107f7ecaa82bffa7_r3.jpg)

这是本节开头放过的同一个GIF图。

### 压缩报错排查

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-f43c2dbc5935eec2a83709552d03ea06_r8.jpg)

### 其他功能：混流与合并

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-2d1bc8fb9debb5c74bb7c601ee4a2e5e_r.jpg)

> 我这里的**“合并”**用词不是那么严谨，咱平时交流也会有人说“如何合并A视频和B音频？”，他表达的是混流的意思。所以用**“拼接”**更好，更对应“截取”或“分段”。
> 只是3FUI菜单栏写的“合并”，所以我说“合并”(

老祖宗：**[MKVToolNix](https://zhida.zhihu.com/search?content_id=262194792&content_type=Article&match_order=1&q=MKVToolNix&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3NjMwMjczODYsInEiOiJNS1ZUb29sTml4IiwiemhpZGFfc291cmNlIjoiZW50aXR5IiwiY29udGVudF9pZCI6MjYyMTk0NzkyLCJjb250ZW50X3R5cGUiOiJBcnRpY2xlIiwibWF0Y2hfb3JkZXIiOjEsInpkX3Rva2VuIjpudWxsfQ.cc6CTFnXsNYGsEek8LAFVxhmJ3UGhyfq6BzioX2yCsU&zhida_source=entity) 和 [gMKVExtractGUI](https://zhida.zhihu.com/search?content_id=262194792&content_type=Article&match_order=1&q=gMKVExtractGUI&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3NjMwMjczODYsInEiOiJnTUtWRXh0cmFjdEdVSSIsInpoaWRhX3NvdXJjZSI6ImVudGl0eSIsImNvbnRlbnRfaWQiOjI2MjE5NDc5MiwiY29udGVudF90eXBlIjoiQXJ0aWNsZSIsIm1hdGNoX29yZGVyIjoxLCJ6ZF90b2tlbiI6bnVsbH0.ZpOHCbTkevUZstFJskarq4zc4fxnkszGFzzUvenT9eU&zhida_source=entity)** [神一样的工具们 | VCB-Studio 公开教程](https://link.zhihu.com/?target=https%3A//guides.vcb-s.com/basic-guide-03/%234-mkv%E7%9A%84%E6%8A%BD%E6%B5%81)

年轻人：**LosslessCut** [https://github.com/mifi/lossles](https://link.zhihu.com/?target=https%3A//github.com/mifi/lossless-cut)

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-c44b53566346622d2f5e565946ce79fb_r.jpg)

**如果你只是要合B站视频.......建议以后用 bilibili唧唧 下载，自动转为MP4，再也不需要你手动合视频文件和音频文件了**：[唧唧-哔哩哔哩唧唧-bilibili视频|弹幕在线下载](https://link.zhihu.com/?target=https%3A//www.jijidown.com/)

也可以用哔哩下载姬等等，各显手段。

### 其他功能：截取视频片段

> 如果您从目录跳转而来，不知道“截取”、“混流”、“裁剪”的区别，请看上上张图的说明。

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-cd07d19d872f8a6bd8720ea1c5e263c4_r.jpg)

剪辑区间可视化配套小软件 **3FUI Video Helper**： [https://github.com/Lake1059/3fu](https://link.zhihu.com/?target=https%3A//github.com/Lake1059/3fuiVideoHelper)

### 其他功能：内封字幕和烧录(内嵌/硬嵌)字幕

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-e29d94b778743822aa3de9ecabfc4434_r.jpg)

图有点大，双击后请等三秒加载

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-ab7d6643a0368c8e46181f24b2506743_r.jpg)

**SubRenamer字幕文件批量改名工具**： [https://github.com/qwqcode/SubR](https://link.zhihu.com/?target=https%3A//github.com/qwqcode/SubRenamer)

**全文完结！......**

**拓展：这里可能有你需要的软件：**[2025.6.24 有关视频压缩的各种软件/文章网页目录 - 知乎](https://zhuanlan.zhihu.com/p/1919356233766401366)

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/v2-88aa33d0ed5905324fddd1e0c6b03b02_r.jpg)