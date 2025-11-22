---
layout:     post   				    # 使用的布局（不需要改）
title:      VScode去掉复制代码的行号以及删除或缩进多行tab			 
subtitle:   VScode格式化 #副标题
date:       2025-11-22				# 时间
author:     wuxia						# 作者
header-img: img/post-bg-2015.jpg	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签

  - vscode
---

## 去掉多行行号

在vscode中使用正则查找：ctrl+f 选中正则表达式  

带点

```
^\s*([0-9]+)\.
```


不带点

```
^\s*([0-9]+)
```


综合起来

```
^\s*([0-9]+)[\.]*
```


[正则表达式来自此博客](https://blog.csdn.net/youji8/article/details/104926293)  
输入正则表达式之后全部替换即可。

## 删除去掉行号后留下的空格

```
shift+tab
```

## 缩进

```
向左缩进：Ctrl + [  
向右缩进：Ctrl + ]
```

